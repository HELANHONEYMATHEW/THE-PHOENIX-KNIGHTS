# THE-PHOENIX-KNIGHTS
This project explores the integration of Digital Twin (GenTwin) technology with AI to create a simulated cybersecurity environment. The system mirrors real or synthetic infrastructure, processes telemetry data, detects anomalous behavior, and assists in proactive threat identification and response.
# backend/data_manager.py

from typing import Dict, List, Tuple
import pandas as pd
import numpy as np
from dataclasses import dataclass
from enum import Enum

class ProcessStage(Enum):
    P1 = "Raw Water Supply"
    P2 = "Chemical Dosing"
    P3 = "Ultrafiltration"
    P4 = "Dechlorination"
    P5 = "Reverse Osmosis"
    P6 = "Backwash"

@dataclass
class SensorGroup:
    stage: ProcessStage
    sensors: List[str]
    actuators: List[str]
    critical_thresholds: Dict[str, Tuple[float, float]]

class SWaTDataManager:
    """
    Handles SWaT dataset loading, validation, and preprocessing.
    Organizes sensors by process stage for targeted analysis.
    """
    
    # SWaT sensor mapping to process stages
    SENSOR_MAPPING = {
        ProcessStage.P1: {
            'sensors': ['FIT101', 'LIT101'],
            'actuators': ['MV101', 'P101', 'P102'],
            'thresholds': {
                'LIT101': (250, 1200),  # mm, tank level
                'FIT101': (0, 2.5)       # m³/h, flow rate
            }
        },
        ProcessStage.P2: {
            'sensors': ['AIT201', 'AIT202', 'AIT203', 'FIT201'],
            'actuators': ['MV201', 'P201', 'P202', 'P203', 'P204', 'P205', 'P206'],
            'thresholds': {
                'AIT201': (200, 400),   # Chemical analyzer
                'FIT201': (0, 2.5)      # Flow rate
            }
        },
        # P3-P6 mappings follow similar pattern...
    }
    
    def __init__(self):
        self.normal_data: pd.DataFrame = None
        self.attack_data: pd.DataFrame = None
        self.metadata: Dict = {}
        
    def load_swat_dataset(self, 
                          normal_path: str, 
                          attack_path: str = None) -> Dict:
        """
        Load and validate SWaT CSV files.
        
        Returns:
            metadata: {
                'total_samples': int,
                'duration_hours': float,
                'sensor_count': int,
                'attack_periods': List[Tuple[str, str]]
            }
        """
        self.normal_data = pd.read_csv(normal_path)
        
        # Parse timestamp
        self.normal_data['Timestamp'] = pd.to_datetime(
            self.normal_data['Timestamp'], 
            format='%d/%m/%Y %I:%M:%S %p'
        )
        
        if attack_path:
            self.attack_data = pd.read_csv(attack_path)
            self.attack_data['Timestamp'] = pd.to_datetime(
                self.attack_data['Timestamp'],
                format='%d/%m/%Y %I:%M:%S %p'
            )
            
            # Identify attack windows
            attack_periods = self._extract_attack_periods()
        else:
            attack_periods = []
        
        # Calculate metadata
        sensor_cols = [col for col in self.normal_data.columns 
                       if col not in ['Timestamp', 'Normal/Attack']]
        
        self.metadata = {
            'total_samples': len(self.normal_data),
            'duration_hours': (
                self.normal_data['Timestamp'].max() - 
                self.normal_data['Timestamp'].min()
            ).total_seconds() / 3600,
            'sensor_count': len(sensor_cols),
            'sensors': sensor_cols,
            'attack_periods': attack_periods,
            'sampling_rate': '1 second'
        }
        
        return self.metadata
    
    def preprocess_for_training(self, 
                                window_size: int = 60,
                                stride: int = 1) -> np.ndarray:
        """
        Create sliding windows for time-series modeling.
        
        Args:
            window_size: Number of timesteps per window (default 60s = 1 min)
            stride: Step size between windows
            
        Returns:
            windows: Array of shape (n_windows, window_size, n_features)
        """
        # Use only normal data for training generative models
        features = self.normal_data.drop(
            columns=['Timestamp', 'Normal/Attack'], 
            errors='ignore'
        )
        
        # Normalize to [0, 1] per sensor
        normalized = (features - features.min()) / (features.max() - features.min())
        
        # Create windows
        windows = []
        for i in range(0, len(normalized) - window_size, stride):
            window = normalized.iloc[i:i+window_size].values
            windows.append(window)
        
        return np.array(windows)
    
    def get_process_stage_data(self, stage: ProcessStage) -> pd.DataFrame:
        """Extract data for specific process stage."""
        mapping = self.SENSOR_MAPPING[stage]
        relevant_cols = mapping['sensors'] + mapping['actuators']
        
        return self.normal_data[relevant_cols]
    
    def _extract_attack_periods(self) -> List[Tuple[str, str]]:
        """Identify continuous attack sequences in labeled data."""
        attacks = self.attack_data[
            self.attack_data['Normal/Attack'] == 'Attack'
        ]['Timestamp']
        
        if len(attacks) == 0:
            return []
        
        # Find continuous sequences
        periods = []
        start = attacks.iloc[0]
        prev = start
        
        for timestamp in attacks.iloc[1:]:
            if (timestamp - prev).total_seconds() > 2:  # Gap > 2s
                periods.append((str(start), str(prev)))
                start = timestamp
            prev = timestamp
        
        periods.append((str(start), str(prev)))
        return periods


        # backend/api/data_routes.py

from fastapi import APIRouter, UploadFile, File
from fastapi.responses import JSONResponse

router = APIRouter(prefix="/api/data", tags=["data"])

@router.post("/upload")
async def upload_dataset(
    normal_file: UploadFile = File(...),
    attack_file: UploadFile = File(None)
):
    """Upload SWaT dataset files."""
    # Save files temporarily
    normal_path = f"/tmp/{normal_file.filename}"
    with open(normal_path, "wb") as f:
        f.write(await normal_file.read())
    
    attack_path = None
    if attack_file:
        attack_path = f"/tmp/{attack_file.filename}"
        with open(attack_path, "wb") as f:
            f.write(await attack_file.read())
    
    # Load into data manager
    from backend.data_manager import SWaTDataManager
    manager = SWaTDataManager()
    metadata = manager.load_swat_dataset(normal_path, attack_path)
    
    return JSONResponse(content={
        "status": "success",
        "metadata": metadata
    })

@router.get("/schema")
async def get_data_schema():
    """Return sensor grouping by process stage."""
    from backend.data_manager import SWaTDataManager
    
    schema = {}
    for stage, mapping in SWaTDataManager.SENSOR_MAPPING.items():
        schema[stage.value] = {
            "sensors": mapping['sensors'],
            "actuators": mapping['actuators'],
            "thresholds": mapping['thresholds']
        }
    
    return schema


    # backend/genai/vae_attack_generator.py

import torch
import torch.nn as nn
import torch.nn.functional as F
from torch.utils.data import DataLoader, TensorDataset

class TimeSeriesVAE(nn.Module):
    """
    Variational Autoencoder for SWaT time-series generation.
    
    Architecture:
    - Encoder: LSTM → μ and log(σ²) vectors
    - Latent: Reparameterization trick
    - Decoder: LSTM → Reconstructed sequence
    
    Why LSTM?
    - Captures temporal dependencies in sensor readings
    - Models autocorrelation in process variables
    """
    
    def __init__(self, 
                 input_dim: int,      # Number of sensors
                 hidden_dim: int = 128,
                 latent_dim: int = 32,
                 window_size: int = 60):
        super().__init__()
        
        self.input_dim = input_dim
        self.latent_dim = latent_dim
        self.window_size = window_size
        
        # Encoder
        self.encoder_lstm = nn.LSTM(
            input_size=input_dim,
            hidden_size=hidden_dim,
            num_layers=2,
            batch_first=True,
            dropout=0.2
        )
        self.fc_mu = nn.Linear(hidden_dim, latent_dim)
        self.fc_logvar = nn.Linear(hidden_dim, latent_dim)
        
        # Decoder
        self.decoder_fc = nn.Linear(latent_dim, hidden_dim)
        self.decoder_lstm = nn.LSTM(
            input_size=hidden_dim,
            hidden_size=hidden_dim,
            num_layers=2,
            batch_first=True,
            dropout=0.2
        )
        self.output_fc = nn.Linear(hidden_dim, input_dim)
        
    def encode(self, x):
        """
        Encode input sequence to latent distribution.
        
        Args:
            x: (batch, window_size, input_dim)
        Returns:
            mu, logvar: (batch, latent_dim)
        """
        _, (h_n, _) = self.encoder_lstm(x)
        h = h_n[-1]  # Last layer hidden state
        
        mu = self.fc_mu(h)
        logvar = self.fc_logvar(h)
        
        return mu, logvar
    
    def reparameterize(self, mu, logvar):
        """Sample from N(mu, sigma) using reparameterization trick."""
        std = torch.exp(0.5 * logvar)
        eps = torch.randn_like(std)
        return mu + eps * std
    
    def decode(self, z):
        """
        Decode latent vector to sequence.
        
        Args:
            z: (batch, latent_dim)
        Returns:
            reconstruction: (batch, window_size, input_dim)
        """
        h = self.decoder_fc(z)
        h = h.unsqueeze(1).repeat(1, self.window_size, 1)
        
        lstm_out, _ = self.decoder_lstm(h)
        reconstruction = self.output_fc(lstm_out)
        
        return reconstruction
    
    def forward(self, x):
        mu, logvar = self.encode(x)
        z = self.reparameterize(mu, logvar)
        reconstruction = self.decode(z)
        
        return reconstruction, mu, logvar
    
    def loss_function(self, reconstruction, x, mu, logvar, beta=1.0):
        """
        ELBO loss = Reconstruction + KL Divergence
        
        Beta parameter controls KL weighting (beta-VAE for disentanglement)
        """
        # Reconstruction loss (MSE for continuous data)
        recon_loss = F.mse_loss(reconstruction, x, reduction='sum')
        
        # KL divergence: -0.5 * sum(1 + log(sigma^2) - mu^2 - sigma^2)
        kl_loss = -0.5 * torch.sum(1 + logvar - mu.pow(2) - logvar.exp())
        
        return recon_loss + beta * kl_loss

class VAEAttackGenerator:
    """
    Attack generation using trained VAE.
    
    Strategy:
    1. Train on normal behavior
    2. Generate attacks by:
       a) Latent space perturbation (shift z vector)
       b) Constrained decoding (violate physical constraints)
       c) Adversarial latent search (maximize digital twin damage)
    """
    
    def __init__(self, model: TimeSeriesVAE):
        self.model = model
        self.model.eval()
        
    def generate_stealthy_drift(self, 
                                 target_sensors: List[str],
                                 drift_magnitude: float = 0.1,
                                 n_samples: int = 10) -> np.ndarray:
        """
        Generate gradual sensor drift attacks.
        
        Method:
        - Sample from latent space
        - Add small perturbation to target sensor dimensions
        - Decode to create slow-moving attack
        
        Why this works:
        - Normal VAE generates typical behavior
        - Small latent shifts create plausible-but-anomalous sequences
        - Hard to detect with threshold-based alarms
        """
        with torch.no_grad():
            # Sample base latent vectors
            z = torch.randn(n_samples, self.model.latent_dim)
            
            # Apply directional drift
            # (In practice, learn which latent dims affect which sensors)
            drift_direction = torch.randn(self.model.latent_dim)
            drift_direction = drift_direction / drift_direction.norm()
            
            z_attacked = z + drift_magnitude * drift_direction
            
            # Decode
            attacks = self.model.decode(z_attacked)
            
        return attacks.cpu().numpy()
    
    def generate_coordinated_attack(self,
                                     process_stage: ProcessStage,
                                     attack_type: str = "sensor_spoof") -> Dict:
        """
        Generate multi-sensor coordinated attacks.
        
        Attack Types:
        - sensor_spoof: Manipulate multiple sensors simultaneously
        - actuator_hijack: Override pump/valve commands
        - timing_attack: Delay sensor readings
        
        Returns:
            {
                'attack_sequence': np.ndarray,
                'affected_sensors': List[str],
                'anomaly_score': float,
                'explanation': str
            }
        """
        if attack_type == "sensor_spoof":
            # Generate attack that keeps P1 sensors in "safe" range
            # while violating physical dependencies (e.g., flow vs level)
            
            z = torch.randn(1, self.model.latent_dim)
            attack_seq = self.model.decode(z).squeeze().cpu().numpy()
            
            # Post-process to violate correlations
            # Example: FIT101 (flow) high but LIT101 (level) low
            # This is physically impossible but sensors appear normal
            
            explanation = (
                "Coordinated sensor spoofing attack on P1: "
                "High inflow (FIT101) reported while tank level (LIT101) "
                "remains low. Physical impossibility suggests MITM attack "
                "on sensor network."
            )
            
            return {
                'attack_sequence': attack_seq,
                'affected_sensors': ['FIT101', 'LIT101'],
                'anomaly_score': self._calculate_physics_violation(attack_seq),
                'explanation': explanation,
                'severity': 'CRITICAL'
            }
    
    def _calculate_physics_violation(self, sequence: np.ndarray) -> float:
        """
        Score how much sequence violates known physical laws.
        
        Examples:
        - Flow continuity: ∑inflows = ∑outflows + Δstorage
        - Level-flow correlation: dL/dt ∝ (Q_in - Q_out)
        - Chemical balance: Dosing rate vs concentration
        
        Returns:
            Score in [0, 1] where 1 = severe violation
        """
        # Simplified example
        violation_score = 0.0
        
        # Check flow-level consistency (would use actual physics model)
        # ...
        
        return violation_score


        # backend/genai/train_vae.py

def train_vae(data_manager: SWaTDataManager, 
              epochs: int = 100,
              batch_size: int = 64) -> TimeSeriesVAE:
    """
    Train VAE on normal SWaT behavior.
    """
    # Prepare data
    windows = data_manager.preprocess_for_training(window_size=60)
    dataset = TensorDataset(torch.FloatTensor(windows))
    dataloader = DataLoader(dataset, batch_size=batch_size, shuffle=True)
    
    # Initialize model
    input_dim = windows.shape[2]
    model = TimeSeriesVAE(input_dim=input_dim, latent_dim=32)
    optimizer = torch.optim.Adam(model.parameters(), lr=1e-3)
    
    # Training loop
    model.train()
    for epoch in range(epochs):
        epoch_loss = 0
        for batch in dataloader:
            x = batch[0]
            
            optimizer.zero_grad()
            reconstruction, mu, logvar = model(x)
            loss = model.loss_function(reconstruction, x, mu, logvar)
            loss.backward()
            optimizer.step()
            
            epoch_loss += loss.item()
        
        if epoch % 10 == 0:
            print(f"Epoch {epoch}: Loss = {epoch_loss/len(dataloader):.4f}")
    
    return model


    # backend/digital_twin/swat_simulator.py

from dataclasses import dataclass
from typing import Dict, List
import numpy as np

@dataclass
class TankState:
    """Physical state of water tank."""
    level: float          # mm
    volume: float         # liters
    temperature: float    # Celsius
    conductivity: float   # μS/cm (water quality indicator)

@dataclass
class ProcessState:
    """Complete SWaT system state."""
    p1_tank: TankState
    p2_chem_concentration: float
    p3_uf_membrane_pressure: float
    p4_chlorine_level: float
    p5_ro_permeate_flow: float
    p6_backwash_active: bool
    
    timestamp: float
    alarms: List[str]

class SWaTDigitalTwin:
    """
    Simplified physics-based simulation of SWaT water treatment.
    
    Modeling Approach:
    - Ordinary Differential Equations for tank levels
    - Empirical relationships for chemical processes
    - Discrete event logic for pump/valve control
    
    Simplifications:
    - Linearized flow dynamics
    - Instantaneous chemical mixing
    - Simplified membrane fouling
    
    (Production version would use rigorous process models)
    """
    
    def __init__(self):
        # P1 Raw Water Storage Tank
        self.p1_tank_area = 1.0  # m²
        self.p1_capacity = 1200  # mm maximum level
        
        # Process parameters
        self.NOMINAL_FLOW = 1.5  # m³/h
        self.CHEM_DOSE_RATE = 0.5  # mg/L per actuator activation
        
        # Initialize state
        self.state = ProcessState(
            p1_tank=TankState(
                level=500,  # mm
                volume=500,  # L
                temperature=25,
                conductivity=500
            ),
            p2_chem_concentration=300,  # mg/L
            p3_uf_membrane_pressure=2.5,  # bar
            p4_chlorine_level=0.5,  # mg/L
            p5_ro_permeate_flow=1.0,  # m³/h
            p6_backwash_active=False,
            timestamp=0,
            alarms=[]
        )
        
        # Safety thresholds
        self.SAFETY_LIMITS = {
            'p1_tank_level_max': 1200,
            'p1_tank_level_min': 250,
            'p2_chem_max': 450,
            'p4_chlorine_max': 2.0,
            'p3_pressure_max': 4.0
        }
    
    def step(self, 
             sensor_inputs: Dict[str, float],
             actuator_commands: Dict[str, bool],
             dt: float = 1.0) -> ProcessState:
        """
        Advance simulation by dt seconds.
        
        Args:
            sensor_inputs: Current sensor readings (may be attacked)
            actuator_commands: Pump/valve states
            dt: Timestep in seconds
            
        Returns:
            Updated process state
        """
        # === P1: Raw Water Tank Dynamics ===
        # dL/dt = (Q_in - Q_out) / Area
        
        q_in = sensor_inputs.get('FIT101', self.NOMINAL_FLOW)  # Inflow
        
        # Outflow controlled by MV101 (motorized valve)
        if actuator_commands.get('MV101', False):
            q_out = self.NOMINAL_FLOW * 0.8
        else:
            q_out = 0.0
        
        # Pump override
        if actuator_commands.get('P101', False):
            q_in *= 1.5  # Pump boost
        
        # Integrate level change
        dL_dt = (q_in - q_out) * 1000 / self.p1_tank_area  # mm/h
        new_level = self.state.p1_tank.level + (dL_dt * dt / 3600)
        
        # Check overflow/underflow
        if new_level > self.SAFETY_LIMITS['p1_tank_level_max']:
            self.state.alarms.append("P1_TANK_OVERFLOW")
            new_level = self.SAFETY_LIMITS['p1_tank_level_max']
        elif new_level < self.SAFETY_LIMITS['p1_tank_level_min']:
            self.state.alarms.append("P1_TANK_UNDERFLOW")
            new_level = self.SAFETY_LIMITS['p1_tank_level_min']
        
        self.state.p1_tank.level = new_level
        self.state.p1_tank.volume = new_level * self.p1_tank_area
        
        # === P2: Chemical Dosing ===
        # Concentration change based on dosing pumps
        active_pumps = sum([
            actuator_commands.get(f'P{200+i}', False) 
            for i in range(1, 7)
        ])
        
        dose_rate = active_pumps * self.CHEM_DOSE_RATE * dt
        self.state.p2_chem_concentration += dose_rate
        
        if self.state.p2_chem_concentration > self.SAFETY_LIMITS['p2_chem_max']:
            self.state.alarms.append("CHEMICAL_OVERDOSE")
        
        # === P3: Ultrafiltration ===
        # Pressure builds with flow, affected by membrane fouling
        target_flow = sensor_inputs.get('FIT301', 1.0)
        self.state.p3_uf_membrane_pressure = 2.0 + 0.5 * target_flow
        
        # === P4-P6: Simplified models ===
        # (Would include RO permeate quality, backwash cycles, etc.)
        
        self.state.timestamp += dt
        
        return self.state
    
    def inject_attack(self, attack_data: np.ndarray) -> List[ProcessState]:
        """
        Simulate process response to attack sequence.
        
        Args:
            attack_data: (timesteps, n_sensors) generated attack
            
        Returns:
            trajectory: List of states showing system evolution
        """
        trajectory = []
        
        # Convert attack data to sensor dictionary
        sensor_names = ['FIT101', 'LIT101', 'AIT201', 'FIT201', ...]  # Full list
        
        for t in range(len(attack_data)):
            sensor_inputs = {
                name: attack_data[t, i] 
                for i, name in enumerate(sensor_names)
            }
            
            # Control logic uses (potentially spoofed) sensor readings
            actuator_commands = self._control_logic(sensor_inputs)
            
            # Simulate physical response
            state = self.step(sensor_inputs, actuator_commands, dt=1.0)
            trajectory.append(state)
            
            # Early termination on critical failure
            if "TANK_OVERFLOW" in state.alarms:
                break
        
        return trajectory
    
    def _control_logic(self, sensors: Dict[str, float]) -> Dict[str, bool]:
        """
        SWaT's control program (Ladder Logic simulation).
        
        Example rules:
        - If LIT101 < 300mm: Activate P101 (refill)
        - If LIT101 > 1000mm: Open MV101 (drain)
        - If AIT201 < 250: Activate dosing pumps
        
        Vulnerability: Control trusts sensor readings blindly
        """
        commands = {}
        
        # P1 Tank level control
        if sensors.get('LIT101', 500) < 300:
            commands['P101'] = True
            commands['MV101'] = False
        elif sensors.get('LIT101', 500) > 1000:
            commands['P101'] = False
            commands['MV101'] = True
        else:
            commands['P101'] = False
            commands['MV101'] = False
        
        # P2 Chemical dosing
        if sensors.get('AIT201', 300) < 250:
            for i in range(1, 4):
                commands[f'P{200+i}'] = True
        
        return commands
    
    def get_vulnerability_report(self) -> Dict:
        """
        Analyze current state for vulnerabilities.
        
        Returns:
            {
                'single_points_of_failure': List[str],
                'unmonitored_variables': List[str],
                'control_weaknesses': List[str],
                'severity_score': float
            }
        """
        vulnerabilities = {
            'single_points_of_failure': [],
            'unmonitored_variables': [],
            'control_weaknesses': []
        }
        
        # Check for SPOF
        if not self._has_redundant_sensor('LIT101'):
            vulnerabilities['single_points_of_failure'].append(
                "LIT101: No backup tank level sensor"
            )
        
        # Check unmonitored
        if not self._has_flow_meter('P1_outlet'):
            vulnerabilities['unmonitored_variables'].append(
                "P1 outlet flow: Cannot detect unauthorized drainage"
            )
        
        # Check control logic weaknesses
        if self._control_lacks_bounds_checking():
            vulnerabilities['control_weaknesses'].append(
                "No rate-of-change validation on sensor inputs"
            )
        
        severity = len(vulnerabilities['single_points_of_failure']) * 0.4 + \\
                   len(vulnerabilities['unmonitored_variables']) * 0.3 + \\
                   len(vulnerabilities['control_weaknesses']) * 0.3
        
        return {
            **vulnerabilities,
            'severity_score': min(severity, 1.0)
        }


        # backend/digital_twin/swat_simulator.py

from dataclasses import dataclass
from typing import Dict, List
import numpy as np

@dataclass
class TankState:
    """Physical state of water tank."""
    level: float          # mm
    volume: float         # liters
    temperature: float    # Celsius
    conductivity: float   # μS/cm (water quality indicator)

@dataclass
class ProcessState:
    """Complete SWaT system state."""
    p1_tank: TankState
    p2_chem_concentration: float
    p3_uf_membrane_pressure: float
    p4_chlorine_level: float
    p5_ro_permeate_flow: float
    p6_backwash_active: bool
    
    timestamp: float
    alarms: List[str]

class SWaTDigitalTwin:
    """
    Simplified physics-based simulation of SWaT water treatment.
    
    Modeling Approach:
    - Ordinary Differential Equations for tank levels
    - Empirical relationships for chemical processes
    - Discrete event logic for pump/valve control
    
    Simplifications:
    - Linearized flow dynamics
    - Instantaneous chemical mixing
    - Simplified membrane fouling
    
    (Production version would use rigorous process models)
    """
    
    def __init__(self):
        # P1 Raw Water Storage Tank
        self.p1_tank_area = 1.0  # m²
        self.p1_capacity = 1200  # mm maximum level
        
        # Process parameters
        self.NOMINAL_FLOW = 1.5  # m³/h
        self.CHEM_DOSE_RATE = 0.5  # mg/L per actuator activation
        
        # Initialize state
        self.state = ProcessState(
            p1_tank=TankState(
                level=500,  # mm
                volume=500,  # L
                temperature=25,
                conductivity=500
            ),
            p2_chem_concentration=300,  # mg/L
            p3_uf_membrane_pressure=2.5,  # bar
            p4_chlorine_level=0.5,  # mg/L
            p5_ro_permeate_flow=1.0,  # m³/h
            p6_backwash_active=False,
            timestamp=0,
            alarms=[]
        )
        
        # Safety thresholds
        self.SAFETY_LIMITS = {
            'p1_tank_level_max': 1200,
            'p1_tank_level_min': 250,
            'p2_chem_max': 450,
            'p4_chlorine_max': 2.0,
            'p3_pressure_max': 4.0
        }
    
    def step(self, 
             sensor_inputs: Dict[str, float],
             actuator_commands: Dict[str, bool],
             dt: float = 1.0) -> ProcessState:
        """
        Advance simulation by dt seconds.
        
        Args:
            sensor_inputs: Current sensor readings (may be attacked)
            actuator_commands: Pump/valve states
            dt: Timestep in seconds
            
        Returns:
            Updated process state
        """
        # === P1: Raw Water Tank Dynamics ===
        # dL/dt = (Q_in - Q_out) / Area
        
        q_in = sensor_inputs.get('FIT101', self.NOMINAL_FLOW)  # Inflow
        
        # Outflow controlled by MV101 (motorized valve)
        if actuator_commands.get('MV101', False):
            q_out = self.NOMINAL_FLOW * 0.8
        else:
            q_out = 0.0
        
        # Pump override
        if actuator_commands.get('P101', False):
            q_in *= 1.5  # Pump boost
        
        # Integrate level change
        dL_dt = (q_in - q_out) * 1000 / self.p1_tank_area  # mm/h
        new_level = self.state.p1_tank.level + (dL_dt * dt / 3600)
        
        # Check overflow/underflow
        if new_level > self.SAFETY_LIMITS['p1_tank_level_max']:
            self.state.alarms.append("P1_TANK_OVERFLOW")
            new_level = self.SAFETY_LIMITS['p1_tank_level_max']
        elif new_level < self.SAFETY_LIMITS['p1_tank_level_min']:
            self.state.alarms.append("P1_TANK_UNDERFLOW")
            new_level = self.SAFETY_LIMITS['p1_tank_level_min']
        
        self.state.p1_tank.level = new_level
        self.state.p1_tank.volume = new_level * self.p1_tank_area
        
        # === P2: Chemical Dosing ===
        # Concentration change based on dosing pumps
        active_pumps = sum([
            actuator_commands.get(f'P{200+i}', False) 
            for i in range(1, 7)
        ])
        
        dose_rate = active_pumps * self.CHEM_DOSE_RATE * dt
        self.state.p2_chem_concentration += dose_rate
        
        if self.state.p2_chem_concentration > self.SAFETY_LIMITS['p2_chem_max']:
            self.state.alarms.append("CHEMICAL_OVERDOSE")
        
        # === P3: Ultrafiltration ===
        # Pressure builds with flow, affected by membrane fouling
        target_flow = sensor_inputs.get('FIT301', 1.0)
        self.state.p3_uf_membrane_pressure = 2.0 + 0.5 * target_flow
        
        # === P4-P6: Simplified models ===
        # (Would include RO permeate quality, backwash cycles, etc.)
        
        self.state.timestamp += dt
        
        return self.state
    
    def inject_attack(self, attack_data: np.ndarray) -> List[ProcessState]:
        """
        Simulate process response to attack sequence.
        
        Args:
            attack_data: (timesteps, n_sensors) generated attack
            
        Returns:
            trajectory: List of states showing system evolution
        """
        trajectory = []
        
        # Convert attack data to sensor dictionary
        sensor_names = ['FIT101', 'LIT101', 'AIT201', 'FIT201', ...]  # Full list
        
        for t in range(len(attack_data)):
            sensor_inputs = {
                name: attack_data[t, i] 
                for i, name in enumerate(sensor_names)
            }
            
            # Control logic uses (potentially spoofed) sensor readings
            actuator_commands = self._control_logic(sensor_inputs)
            
            # Simulate physical response
            state = self.step(sensor_inputs, actuator_commands, dt=1.0)
            trajectory.append(state)
            
            # Early termination on critical failure
            if "TANK_OVERFLOW" in state.alarms:
                break
        
        return trajectory
    
    def _control_logic(self, sensors: Dict[str, float]) -> Dict[str, bool]:
        """
        SWaT's control program (Ladder Logic simulation).
        
        Example rules:
        - If LIT101 < 300mm: Activate P101 (refill)
        - If LIT101 > 1000mm: Open MV101 (drain)
        - If AIT201 < 250: Activate dosing pumps
        
        Vulnerability: Control trusts sensor readings blindly
        """
        commands = {}
        
        # P1 Tank level control
        if sensors.get('LIT101', 500) < 300:
            commands['P101'] = True
            commands['MV101'] = False
        elif sensors.get('LIT101', 500) > 1000:
            commands['P101'] = False
            commands['MV101'] = True
        else:
            commands['P101'] = False
            commands['MV101'] = False
        
        # P2 Chemical dosing
        if sensors.get('AIT201', 300) < 250:
            for i in range(1, 4):
                commands[f'P{200+i}'] = True
        
        return commands
    
    def get_vulnerability_report(self) -> Dict:
        """
        Analyze current state for vulnerabilities.
        
        Returns:
            {
                'single_points_of_failure': List[str],
                'unmonitored_variables': List[str],
                'control_weaknesses': List[str],
                'severity_score': float
            }
        """
        vulnerabilities = {
            'single_points_of_failure': [],
            'unmonitored_variables': [],
            'control_weaknesses': []
        }
        
        # Check for SPOF
        if not self._has_redundant_sensor('LIT101'):
            vulnerabilities['single_points_of_failure'].append(
                "LIT101: No backup tank level sensor"
            )
        
        # Check unmonitored
        if not self._has_flow_meter('P1_outlet'):
            vulnerabilities['unmonitored_variables'].append(
                "P1 outlet flow: Cannot detect unauthorized drainage"
            )
        
        # Check control logic weaknesses
        if self._control_lacks_bounds_checking():
            vulnerabilities['control_weaknesses'].append(
                "No rate-of-change validation on sensor inputs"
            )
        
        severity = len(vulnerabilities['single_points_of_failure']) * 0.4 + \\
                   len(vulnerabilities['unmonitored_variables']) * 0.3 + \\
                   len(vulnerabilities['control_weaknesses']) * 0.3
        
        return {
            **vulnerabilities,
            'severity_score': min(severity, 1.0)
        }


        # backend/api/twin_routes.py

@router.post("/simulate-attack")
async def simulate_attack(
    attack_id: str,
    realtime: bool = False
):
    """
    Run digital twin simulation with generated attack.
    
    Args:
        attack_id: Reference to generated attack scenario
        realtime: If True, stream results via WebSocket
        
    Returns:
        {
            'trajectory': List[ProcessState],
            'safety_violations': List[str],
            'max_impact': {
                'variable': str,
                'deviation': float
            }
        }
    """
    # Load attack from GenAI engine
    attack_data = load_attack(attack_id)
    
    # Run simulation
    twin = SWaTDigitalTwin()
    trajectory = twin.inject_attack(attack_data)
    
    # Analyze impact
    safety_violations = set()
    for state in trajectory:
        safety_violations.update(state.alarms)
    
    return {
        'trajectory': [state.__dict__ for state in trajectory],
        'safety_violations': list(safety_violations),
        'duration': len(trajectory),
        'criticality': 'HIGH' if 'OVERFLOW' in safety_violations else 'MEDIUM'
    }

@router.websocket("/ws/twin-live")
async def twin_live_stream(websocket: WebSocket):
    """Stream digital twin state in real-time during simulation."""
    await websocket.accept()
    # Stream process state updates
    # ...


    @router.get("/vulnerabilities")
async def get_vulnerabilities(
    min_severity: float = 0.5,
    top_n: int = 10
):
    """
    Retrieve discovered vulnerabilities.
    
    Returns:
        {
            'vulnerabilities': List[Vulnerability],
            'heatmap': Array,
            'summary': {
                'total_count': int,
                'critical_count': int,
                'most_affected_stage': str
            }
        }
    """
    pass

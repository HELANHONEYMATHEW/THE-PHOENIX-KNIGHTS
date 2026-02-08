# THE-PHOENIX-KNIGHTS
This project explores the integration of Digital Twin (GenTwin) technology with AI to create a simulated cybersecurity environment. The system mirrors real or synthetic infrastructure, processes telemetry data, detects anomalous behavior, and assists in proactive threat identification and response.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SWaT Guardian Twin - Cybersecurity Intelligence Platform</title>
    <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://cdn.plot.ly/plotly-2.27.0.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Audiowide&family=Rajdhani:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SWaT Guardian AI - Intelligent Cybersecurity Assistant</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.plot.ly/plotly-2.26.0.min.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600;700&family=Inter:wght@400;500;600;700;800&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
        }
        
        h1, h2, h3 {
            font-family: 'Inter', sans-serif;
        }

        .mono {
            font-family: 'JetBrains Mono', monospace;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateX(-20px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        @keyframes slideInRight {
            from {
                opacity: 0;
                transform: translateX(20px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .animate-fadeIn {
            animation: fadeIn 0.5s ease-out;
        }

        .animate-slideIn {
            animation: slideIn 0.4s ease-out;
        }

        .animate-slideInRight {
            animation: slideInRight 0.4s ease-out;
        }

        @keyframes pulse-slow {
            0%, 100% {
                opacity: 1;
            }
            50% {
                opacity: 0.5;
            }
        }

        .pulse-slow {
            animation: pulse-slow 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
        }

        @keyframes typing {
            from { width: 0 }
            to { width: 100% }
        }

        .typing-indicator {
            display: inline-block;
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: #64748b;
            animation: pulse-slow 1.5s infinite;
        }

        .typing-indicator:nth-child(2) {
            animation-delay: 0.2s;
        }

        .typing-indicator:nth-child(3) {
            animation-delay: 0.4s;
        }

        .chat-container {
            height: 600px;
            overflow-y: auto;
            scroll-behavior: smooth;
        }

        .chat-container::-webkit-scrollbar {
            width: 6px;
        }

        .chat-container::-webkit-scrollbar-track {
            background: #f1f5f9;
        }

        .chat-container::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 3px;
        }

        .chat-container::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }

        .danger-badge {
            animation: pulse-slow 2s infinite;
        }

        .tank {
            position: relative;
            width: 120px;
            height: 180px;
            border: 4px solid #1e293b;
            border-radius: 8px;
            overflow: hidden;
            background: linear-gradient(to bottom, #f1f5f9 0%, #e2e8f0 100%);
        }

        .tank-water {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            transition: height 1s ease-out, background-color 0.5s ease;
        }

        .tank-water::before {
            content: '';
            position: absolute;
            inset: 0;
            background: linear-gradient(to top, transparent 0%, rgba(255, 255, 255, 0.3) 100%);
        }

        .tooltip {
            position: relative;
            display: inline-block;
        }

        .tooltip .tooltiptext {
            visibility: hidden;
            width: 200px;
            background-color: #1e293b;
            color: #fff;
            text-align: center;
            border-radius: 6px;
            padding: 8px;
            position: absolute;
            z-index: 1;
            bottom: 125%;
            left: 50%;
            margin-left: -100px;
            opacity: 0;
            transition: opacity 0.3s;
            font-size: 12px;
        }

        .tooltip .tooltiptext::after {
            content: "";
            position: absolute;
            top: 100%;
            left: 50%;
            margin-left: -5px;
            border-width: 5px;
            border-style: solid;
            border-color: #1e293b transparent transparent transparent;
        }

        .tooltip:hover .tooltiptext {
            visibility: visible;
            opacity: 1;
        }

        .gradient-bg {
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 50%, #334155 100%);
        }

        .glass-effect {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .glow {
            box-shadow: 0 0 20px rgba(6, 182, 212, 0.3);
        }

        .chat-bubble-user {
            background: linear-gradient(135deg, #0891b2 0%, #0e7490 100%);
            border-radius: 18px 18px 4px 18px;
        }

        .chat-bubble-ai {
            background: linear-gradient(135deg, #334155 0%, #475569 100%);
            border-radius: 18px 18px 18px 4px;
        }

        .quick-action-btn {
            transition: all 0.2s ease;
        }

        .quick-action-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        }
    </style>
</head>
<body class="gradient-bg min-h-screen text-white">
    <!-- Header -->
    <header class="glass-effect border-b border-white/10">
        <div class="max-w-7xl mx-auto px-6 py-6">
            <div class="flex items-center justify-between">
                <div class="flex items-center gap-4">
                    <div class="p-3 bg-gradient-to-br from-cyan-500 to-blue-600 rounded-xl shadow-lg glow">
                        <i class="fas fa-shield-halved text-white text-3xl"></i>
                    </div>
                    <div>
                        <h1 class="text-4xl font-bold text-white">
                            SWaT Guardian AI
                        </h1>
                        <p class="text-cyan-300 text-sm mt-1 mono">Intelligent Cybersecurity Defense System</p>
                    </div>
                </div>
                <div class="flex items-center gap-4">
                    <div class="text-right">
                        <div class="text-xs text-slate-400">AI Status</div>
                        <div class="text-sm font-semibold text-emerald-400 flex items-center gap-2">
                            <i class="fas fa-circle text-emerald-500 text-xs pulse-slow"></i>
                            Active & Monitoring
                        </div>
                    </div>
                    <div id="current-danger-badge" class="px-4 py-2 rounded-lg bg-emerald-500/20 border border-emerald-500/30">
                        <div class="text-xs text-emerald-300">Danger Level</div>
                        <div class="text-lg font-bold text-emerald-400 mono">LOW</div>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="max-w-7xl mx-auto px-6 py-8">
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <!-- Left Column: System Status -->
            <div class="lg:col-span-1 space-y-6">
                <!-- System Health -->
                <div class="glass-effect rounded-xl p-6 border border-white/10">
                    <h3 class="text-lg font-semibold text-white mb-4 flex items-center gap-2">
                        <i class="fas fa-heartbeat text-cyan-400"></i>
                        System Health
                    </h3>
                    <div class="text-center">
                        <div id="system-health-display" class="text-6xl font-bold text-emerald-400 mono">92%</div>
                        <div class="text-sm text-slate-400 mt-2">Overall Infrastructure Status</div>
                    </div>
                    <div class="mt-6 space-y-3" id="process-stages-mini"></div>
                </div>

                <!-- Real-time Alerts -->
                <div class="glass-effect rounded-xl p-6 border border-white/10">
                    <h3 class="text-lg font-semibold text-white mb-4 flex items-center gap-2">
                        <i class="fas fa-bell text-yellow-400"></i>
                        Real-time Alerts
                    </h3>
                    <div id="alerts-container" class="space-y-2 max-h-64 overflow-y-auto"></div>
                </div>

                <!-- Quick Actions -->
                <div class="glass-effect rounded-xl p-6 border border-white/10">
                    <h3 class="text-lg font-semibold text-white mb-4 flex items-center gap-2">
                        <i class="fas fa-bolt text-purple-400"></i>
                        Quick Actions
                    </h3>
                    <div class="space-y-2">
                        <button onclick="quickAction('scan')" class="quick-action-btn w-full px-4 py-3 bg-cyan-600/20 hover:bg-cyan-600/30 border border-cyan-500/30 rounded-lg text-left text-sm text-white flex items-center gap-3">
                            <i class="fas fa-radar text-cyan-400"></i>
                            <span>Run Full System Scan</span>
                        </button>
                        <button onclick="quickAction('attack')" class="quick-action-btn w-full px-4 py-3 bg-red-600/20 hover:bg-red-600/30 border border-red-500/30 rounded-lg text-left text-sm text-white flex items-center gap-3">
                            <i class="fas fa-exclamation-triangle text-red-400"></i>
                            <span>Simulate Attack</span>
                        </button>
                        <button onclick="quickAction('status')" class="quick-action-btn w-full px-4 py-3 bg-blue-600/20 hover:bg-blue-600/30 border border-blue-500/30 rounded-lg text-left text-sm text-white flex items-center gap-3">
                            <i class="fas fa-chart-line text-blue-400"></i>
                            <span>Detailed Status Report</span>
                        </button>
                        <button onclick="quickAction('vulnerabilities')" class="quick-action-btn w-full px-4 py-3 bg-purple-600/20 hover:bg-purple-600/30 border border-purple-500/30 rounded-lg text-left text-sm text-white flex items-center gap-3">
                            <i class="fas fa-bug text-purple-400"></i>
                            <span>Analyze Vulnerabilities</span>
                        </button>
                    </div>
                </div>
            </div>

            <!-- Center & Right: AI Chat Interface -->
            <div class="lg:col-span-2">
                <div class="glass-effect rounded-xl p-6 border border-white/10 h-full flex flex-col">
                    <!-- Chat Header -->
                    <div class="flex items-center justify-between mb-6 pb-4 border-b border-white/10">
                        <div class="flex items-center gap-3">
                            <div class="w-12 h-12 bg-gradient-to-br from-cyan-500 to-blue-600 rounded-full flex items-center justify-center shadow-lg">
                                <i class="fas fa-robot text-white text-xl"></i>
                            </div>
                            <div>
                                <h2 class="text-xl font-bold text-white">Guardian AI Assistant</h2>
                                <p class="text-sm text-cyan-300 mono">Threat Analysis & Response System</p>
                            </div>
                        </div>
                        <div class="flex items-center gap-2">
                            <div class="px-3 py-1 rounded-full bg-emerald-500/20 border border-emerald-500/30 text-xs text-emerald-400 mono">
                                <i class="fas fa-circle text-emerald-500 text-xs mr-1"></i>
                                Online
                            </div>
                        </div>
                    </div>

                    <!-- Chat Messages -->
                    <div id="chat-container" class="chat-container flex-1 space-y-4 mb-4 pr-2">
                        <!-- Initial greeting -->
                        <div class="flex gap-3 animate-slideIn">
                            <div class="w-8 h-8 bg-gradient-to-br from-cyan-500 to-blue-600 rounded-full flex items-center justify-center flex-shrink-0">
                                <i class="fas fa-robot text-white text-sm"></i>
                            </div>
                            <div class="flex-1">
                                <div class="chat-bubble-ai text-white p-4 shadow-lg">
                                    <p class="text-sm leading-relaxed">
                                        👋 Hello! I'm <strong>SWaT Guardian AI</strong>, your intelligent cybersecurity assistant.
                                    </p>
                                    <p class="text-sm leading-relaxed mt-2">
                                        I continuously monitor all 6 process stages of the water treatment system and can instantly assess danger levels, detect anomalies, and recommend mitigations.
                                    </p>
                                    <p class="text-sm leading-relaxed mt-2">
                                        <strong class="text-cyan-300">Current Status:</strong> System operating normally with <span class="text-emerald-400 font-semibold">LOW</span> danger level.
                                    </p>
                                </div>
                                <div class="text-xs text-slate-500 mt-1 ml-2">Just now</div>
                            </div>
                        </div>
                    </div>

                    <!-- Typing Indicator -->
                    <div id="typing-indicator" class="hidden flex gap-3 mb-4">
                        <div class="w-8 h-8 bg-gradient-to-br from-cyan-500 to-blue-600 rounded-full flex items-center justify-center flex-shrink-0">
                            <i class="fas fa-robot text-white text-sm"></i>
                        </div>
                        <div class="chat-bubble-ai p-4">
                            <div class="flex gap-1">
                                <div class="typing-indicator"></div>
                                <div class="typing-indicator"></div>
                                <div class="typing-indicator"></div>
                            </div>
                        </div>
                    </div>

                    <!-- Suggested Questions -->
                    <div id="suggested-questions" class="mb-4">
                        <div class="text-xs text-slate-400 mb-2 ml-2">Suggested questions:</div>
                        <div class="flex flex-wrap gap-2">
                            <button onclick="askQuestion('What is the current danger level?')" class="px-3 py-2 bg-white/5 hover:bg-white/10 border border-white/10 rounded-lg text-xs text-white transition-all">
                                What is the current danger level?
                            </button>
                            <button onclick="askQuestion('Which stage is most vulnerable?')" class="px-3 py-2 bg-white/5 hover:bg-white/10 border border-white/10 rounded-lg text-xs text-white transition-all">
                                Which stage is most vulnerable?
                            </button>
                            <button onclick="askQuestion('Explain P3 warning status')" class="px-3 py-2 bg-white/5 hover:bg-white/10 border border-white/10 rounded-lg text-xs text-white transition-all">
                                Explain P3 warning status
                            </button>
                        </div>
                    </div>

                    <!-- Chat Input -->
                    <div class="flex gap-3">
                        <input 
                            type="text" 
                            id="chat-input" 
                            placeholder="Ask Guardian AI about system status, threats, or recommendations..."
                            class="flex-1 px-4 py-3 bg-white/5 border border-white/10 rounded-lg text-white placeholder-slate-500 focus:outline-none focus:border-cyan-500/50 focus:ring-2 focus:ring-cyan-500/20"
                            onkeypress="handleKeyPress(event)"
                        >
                        <button 
                            onclick="sendMessage()" 
                            class="px-6 py-3 bg-gradient-to-r from-cyan-600 to-blue-600 hover:from-cyan-700 hover:to-blue-700 rounded-lg text-white font-semibold transition-all shadow-lg hover:shadow-xl flex items-center gap-2"
                        >
                            <i class="fas fa-paper-plane"></i>
                            Send
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- System Visualization -->
        <div class="mt-6 glass-effect rounded-xl p-6 border border-white/10">
            <h3 class="text-lg font-semibold text-white mb-4 flex items-center gap-2">
                <i class="fas fa-diagram-project text-cyan-400"></i>
                Digital Twin Visualization
            </h3>
            <div class="flex items-center justify-around">
                <!-- Tank 1 -->
                <div class="flex flex-col items-center">
                    <div class="text-sm font-semibold text-slate-300 mb-2">Raw Water Tank</div>
                    <div class="tank">
                        <div id="tank1-water" class="tank-water bg-emerald-500" style="height: 50%">
                            <div class="absolute inset-0 flex items-center justify-center">
                                <span id="tank1-level" class="text-2xl font-bold text-slate-900 drop-shadow-lg">50%</span>
                            </div>
                        </div>
                    </div>
                    <div class="mt-2 text-xs text-slate-400 mono">LIT301</div>
                </div>

                <!-- Flow Arrow -->
                <div class="flex flex-col items-center">
                    <i class="fas fa-chevron-right text-cyan-400 text-3xl pulse-slow"></i>
                    <div class="text-xs text-slate-400 mt-1 mono">MV101</div>
                </div>

                <!-- Tank 2 -->
                <div class="flex flex-col items-center">
                    <div class="text-sm font-semibold text-slate-300 mb-2">UF Feed Tank</div>
                    <div class="tank">
                        <div id="tank2-water" class="tank-water bg-emerald-500" style="height: 60%">
                            <div class="absolute inset-0 flex items-center justify-center">
                                <span id="tank2-level" class="text-2xl font-bold text-slate-900 drop-shadow-lg">60%</span>
                            </div>
                        </div>
                    </div>
                    <div class="mt-2 text-xs text-slate-400 mono">LIT101</div>
                </div>

                <!-- Flow Arrow -->
                <div class="flex flex-col items-center">
                    <i class="fas fa-chevron-right text-cyan-400 text-3xl pulse-slow"></i>
                    <div class="text-xs text-slate-400 mt-1 mono">P301</div>
                </div>

                <!-- Tank 3 -->
                <div class="flex flex-col items-center">
                    <div class="text-sm font-semibold text-slate-300 mb-2">RO Feed Tank</div>
                    <div class="tank">
                        <div id="tank3-water" class="tank-water bg-emerald-500" style="height: 45%">
                            <div class="absolute inset-0 flex items-center justify-center">
                                <span id="tank3-level" class="text-2xl font-bold text-slate-900 drop-shadow-lg">45%</span>
                            </div>
                            <div id="tank3-alert" class="absolute top-2 left-2 hidden">
                                <i class="fas fa-exclamation-triangle text-red-600 text-xl animate-bounce"></i>
                            </div>
                        </div>
                    </div>
                    <div class="mt-2 text-xs text-slate-400 mono">LIT401</div>
                </div>
            </div>
        </div>
    </main>

    <script>
        // Mock Data
        const processStages = [
            { id: 'P1', name: 'Raw Water Intake', status: 'normal', health: 98 },
            { id: 'P2', name: 'Chemical Dosing', status: 'normal', health: 95 },
            { id: 'P3', name: 'Ultrafiltration', status: 'warning', health: 72 },
            { id: 'P4', name: 'Dechlorination', status: 'normal', health: 94 },
            { id: 'P5', name: 'RO Treatment', status: 'normal', health: 96 },
            { id: 'P6', name: 'Final Backwash', status: 'normal', health: 97 }
        ];

        // State
        let currentDangerLevel = 'LOW';
        let systemHealth = 92;
        let chatHistory = [];
        let alertLog = [];
        let tankAnimationInterval = null;

        // AI Response Templates
        const aiResponses = {
            dangerLevel: {
                low: "✅ <strong>Danger Level: LOW</strong><br><br>All systems operating within normal parameters. No immediate threats detected. I'm continuously monitoring all sensors and actuators for any anomalies.",
                medium: "⚠️ <strong>Danger Level: MEDIUM</strong><br><br>I've detected some irregularities in the system. Stage P3 (Ultrafiltration) is showing warning signs with 72% health. This could indicate sensor drift or early-stage attack patterns. I recommend increased monitoring.",
                high: "🚨 <strong>Danger Level: HIGH</strong><br><br>ALERT: Coordinated attack detected across multiple sensors! LIT301 and MV101 are showing synchronized anomalies. Tank levels rising beyond safe limits. Immediate intervention required!",
                critical: "🔴 <strong>Danger Level: CRITICAL</strong><br><br>EMERGENCY: System under active cyber-attack! Multiple process stages compromised. Physical safety limits exceeded. Executing emergency shutdown protocols and alerting operators immediately!"
            },
            vulnerabilities: "Based on my analysis, <strong>P3 (Ultrafiltration)</strong> is the most vulnerable stage:<br><br>• <strong>Monitoring Risk:</strong> 70%<br>• <strong>Control Risk:</strong> 80%<br>• <strong>Actuation Risk:</strong> 90%<br><br>This stage lacks adequate redundancy in sensor validation and has weak rate-of-change constraints. An attacker could manipulate tank levels without immediate detection.",
            p3Warning: "P3 (Ultrafiltration) is currently at <strong>WARNING status</strong> with 72% health due to:<br><br>• Elevated sensor noise on LIT301<br>• Irregular valve response patterns<br>• Flow rate inconsistencies with expected digital twin predictions<br><br>While not yet critical, this warrants close monitoring. I recommend running correlation analysis across all P3 sensors.",
            statusReport: "📊 <strong>Comprehensive System Status</strong><br><br><strong>Overall Health:</strong> 92%<br><strong>Active Alerts:</strong> 1 warning<br><strong>Anomalies Detected (24h):</strong> 3<br><br><strong>Stage Status:</strong><br>• P1-P2: Optimal ✅<br>• P3: Warning ⚠️<br>• P4-P6: Optimal ✅<br><br><strong>Recommendations:</strong><br>1. Investigate P3 sensor calibration<br>2. Review access logs for unusual patterns<br>3. Consider deploying additional monitoring on ultrafiltration stage",
            scan: "🔍 <strong>Full System Scan Initiated</strong><br><br>Scanning all 51 sensors and actuators across 6 process stages...<br><br><strong>Results:</strong><br>✅ 48 components: Normal<br>⚠️ 2 components: Needs attention (LIT301, FIT301)<br>❌ 1 component: Degraded performance (P3 pump)<br><br><strong>Threat Assessment:</strong> No active attacks detected, but sensor drift patterns suggest potential reconnaissance activity.",
            attack: "⚡ <strong>Attack Simulation Executed</strong><br><br>Simulating <strong>Multi-Sensor Coordinated Attack</strong> at 75% intensity...<br><br><strong>AI Analysis:</strong><br>Detected coordinated anomalies across LIT301, FIT301, and MV101. Attack pattern indicates attempt to overflow Tank 3 while masking sensor readings. <br><br><strong>Predicted Impact:</strong> Tank level exceeding safe limits by 18% within 2.5 minutes.<br><br><strong>Recommended Response:</strong> Emergency valve closure + operator alert activated.",
            mitigations: "🛡️ <strong>Recommended Mitigations</strong><br><br>1. <strong>Multi-Sensor Correlation (94% effective)</strong><br>   Deploy AI model to detect coordinated anomalies<br><br>2. <strong>Rate-of-Change Limits (97% effective)</strong><br>   Implement physical constraints on tank levels<br><br>3. <strong>Real-time Dashboard (85% effective)</strong><br>   Alert operators when digital twin diverges from actuals<br><br>Applying all three would increase system resilience by +36%.",
            help: "🤖 <strong>How I Can Help</strong><br><br>I can assist you with:<br><br>• Assess current danger levels and threat landscape<br>• Explain specific stage status and health metrics<br>• Identify vulnerabilities across the system<br>• Simulate attack scenarios and predict impacts<br>• Recommend security mitigations<br>• Generate comprehensive status reports<br>• Analyze sensor data for anomalies<br><br>Just ask me anything about the SWaT system security!"
        };

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            renderProcessStagesMini();
            startTankAnimation();
            addAlert('System initialized', 'All sensors operational', 'info');
            addAlert('P3 Warning', 'Ultrafiltration stage health at 72%', 'warning');
        });

        // Render Mini Process Stages
        function renderProcessStagesMini() {
            const container = document.getElementById('process-stages-mini');
            container.innerHTML = processStages.map(stage => {
                const statusColors = {
                    normal: 'bg-emerald-500',
                    warning: 'bg-amber-500',
                    attack: 'bg-red-500'
                };
                const statusIcons = {
                    normal: 'fa-check-circle',
                    warning: 'fa-exclamation-circle',
                    attack: 'fa-times-circle'
                };
                
                return `
                    <div class="flex items-center justify-between p-3 bg-white/5 rounded-lg border border-white/10">
                        <div class="flex items-center gap-3">
                            <div class="w-8 h-8 rounded-lg ${statusColors[stage.status]} flex items-center justify-center">
                                <i class="fas ${statusIcons[stage.status]} text-white text-sm"></i>
                            </div>
                            <div>
                                <div class="text-xs font-bold text-cyan-400 mono">${stage.id}</div>
                                <div class="text-xs text-slate-300">${stage.name}</div>
                            </div>
                        </div>
                        <div class="text-right">
                            <div class="text-sm font-bold ${stage.health > 90 ? 'text-emerald-400' : stage.health > 70 ? 'text-amber-400' : 'text-red-400'} mono">
                                ${stage.health}%
                            </div>
                        </div>
                    </div>
                `;
            }).join('');
        }

        // Add Alert
        function addAlert(title, message, type) {
            const container = document.getElementById('alerts-container');
            const colors = {
                info: 'border-blue-500/30 bg-blue-500/10',
                warning: 'border-amber-500/30 bg-amber-500/10',
                danger: 'border-red-500/30 bg-red-500/10'
            };
            const icons = {
                info: 'fa-info-circle text-blue-400',
                warning: 'fa-exclamation-triangle text-amber-400',
                danger: 'fa-exclamation-circle text-red-400'
            };
            
            const alert = document.createElement('div');
            alert.className = `p-3 rounded-lg border ${colors[type]} animate-fadeIn`;
            alert.innerHTML = `
                <div class="flex items-start gap-2">
                    <i class="fas ${icons[type]} text-sm mt-0.5"></i>
                    <div class="flex-1">
                        <div class="text-xs font-semibold text-white">${title}</div>
                        <div class="text-xs text-slate-400 mt-1">${message}</div>
                    </div>
                </div>
            `;
            
            container.insertBefore(alert, container.firstChild);
            alertLog.push({ title, message, type, timestamp: new Date() });
            
            // Keep only last 5 alerts
            while (container.children.length > 5) {
                container.removeChild(container.lastChild);
            }
        }

        // Handle Key Press
        function handleKeyPress(event) {
            if (event.key === 'Enter') {
                sendMessage();
            }
        }

        // Send Message
        function sendMessage() {
            const input = document.getElementById('chat-input');
            const message = input.value.trim();
            
            if (!message) return;
            
            // Add user message
            addChatMessage(message, 'user');
            input.value = '';
            
            // Show typing indicator
            document.getElementById('typing-indicator').classList.remove('hidden');
            document.getElementById('suggested-questions').classList.add('hidden');
            
            // Generate AI response
            setTimeout(() => {
                const response = generateAIResponse(message);
                document.getElementById('typing-indicator').classList.add('hidden');
                addChatMessage(response.text, 'ai');
                
                // Update danger level if changed
                if (response.dangerLevel) {
                    updateDangerLevel(response.dangerLevel);
                }
                
                // Add alert if needed
                if (response.alert) {
                    addAlert(response.alert.title, response.alert.message, response.alert.type);
                }
            }, 1500);
        }

        // Ask Question (from suggested)
        function askQuestion(question) {
            document.getElementById('chat-input').value = question;
            sendMessage();
        }

        // Generate AI Response
        function generateAIResponse(message) {
            const lowerMessage = message.toLowerCase();
            
            // Danger level queries
            if (lowerMessage.includes('danger level') || lowerMessage.includes('threat level') || lowerMessage.includes('how safe')) {
                return {
                    text: aiResponses.dangerLevel[currentDangerLevel.toLowerCase()],
                    dangerLevel: currentDangerLevel
                };
            }
            
            // Vulnerability queries
            if (lowerMessage.includes('vulnerab') || lowerMessage.includes('weak') || lowerMessage.includes('risk')) {
                return {
                    text: aiResponses.vulnerabilities
                };
            }
            
            // P3 specific queries
            if (lowerMessage.includes('p3') || lowerMessage.includes('ultrafiltration') || lowerMessage.includes('warning')) {
                return {
                    text: aiResponses.p3Warning
                };
            }
            
            // Status report
            if (lowerMessage.includes('status') || lowerMessage.includes('report') || lowerMessage.includes('overview')) {
                return {
                    text: aiResponses.statusReport
                };
            }
            
            // Scan
            if (lowerMessage.includes('scan') || lowerMessage.includes('check')) {
                return {
                    text: aiResponses.scan
                };
            }
            
            // Attack simulation
            if (lowerMessage.includes('attack') || lowerMessage.includes('simulate')) {
                return {
                    text: aiResponses.attack,
                    dangerLevel: 'HIGH',
                    alert: {
                        title: 'Attack Simulated',
                        message: 'Multi-sensor coordinated attack detected',
                        type: 'danger'
                    }
                };
            }
            
            // Mitigations
            if (lowerMessage.includes('mitigat') || lowerMessage.includes('fix') || lowerMessage.includes('solution') || lowerMessage.includes('recommend')) {
                return {
                    text: aiResponses.mitigations
                };
            }
            
            // Help
            if (lowerMessage.includes('help') || lowerMessage.includes('what can you')) {
                return {
                    text: aiResponses.help
                };
            }
            
            // Default response
            return {
                text: `I understand you're asking about "${message}". Let me analyze the system...<br><br>Based on current data, I can provide information about:<br>• System danger levels and threats<br>• Vulnerabilities in specific process stages<br>• Attack simulations and predictions<br>• Recommended mitigations<br><br>Could you please be more specific about what aspect you'd like me to analyze?`
            };
        }

        // Add Chat Message
        function addChatMessage(text, sender) {
            const container = document.getElementById('chat-container');
            const isUser = sender === 'user';
            
            const messageDiv = document.createElement('div');
            messageDiv.className = `flex gap-3 ${isUser ? 'justify-end animate-slideInRight' : 'animate-slideIn'}`;
            
            if (isUser) {
                messageDiv.innerHTML = `
                    <div class="flex-1 max-w-md">
                        <div class="chat-bubble-user text-white p-4 shadow-lg">
                            <p class="text-sm leading-relaxed">${text}</p>
                        </div>
                        <div class="text-xs text-slate-500 mt-1 mr-2 text-right">Just now</div>
                    </div>
                    <div class="w-8 h-8 bg-gradient-to-br from-slate-600 to-slate-700 rounded-full flex items-center justify-center flex-shrink-0">
                        <i class="fas fa-user text-white text-sm"></i>
                    </div>
                `;
            } else {
                messageDiv.innerHTML = `
                    <div class="w-8 h-8 bg-gradient-to-br from-cyan-500 to-blue-600 rounded-full flex items-center justify-center flex-shrink-0">
                        <i class="fas fa-robot text-white text-sm"></i>
                    </div>
                    <div class="flex-1 max-w-2xl">
                        <div class="chat-bubble-ai text-white p-4 shadow-lg">
                            <p class="text-sm leading-relaxed">${text}</p>
                        </div>
                        <div class="text-xs text-slate-500 mt-1 ml-2">Just now</div>
                    </div>
                `;
            }
            
            container.appendChild(messageDiv);
            container.scrollTop = container.scrollHeight;
            
            chatHistory.push({ text, sender, timestamp: new Date() });
        }

        // Update Danger Level
        function updateDangerLevel(level) {
            currentDangerLevel = level;
            const badge = document.getElementById('current-danger-badge');
            
            const colors = {
                LOW: { bg: 'bg-emerald-500/20', border: 'border-emerald-500/30', text: 'text-emerald-400' },
                MEDIUM: { bg: 'bg-amber-500/20', border: 'border-amber-500/30', text: 'text-amber-400' },
                HIGH: { bg: 'bg-red-500/20', border: 'border-red-500/30', text: 'text-red-400' },
                CRITICAL: { bg: 'bg-red-600/30', border: 'border-red-600/50', text: 'text-red-300' }
            };
            
            const color = colors[level];
            badge.className = `px-4 py-2 rounded-lg ${color.bg} border ${color.border} danger-badge`;
            badge.innerHTML = `
                <div class="text-xs ${color.text.replace('400', '300')}">Danger Level</div>
                <div class="text-lg font-bold ${color.text} mono">${level}</div>
            `;
            
            // Update system health based on danger level
            const healthMap = { LOW: 92, MEDIUM: 75, HIGH: 58, CRITICAL: 32 };
            systemHealth = healthMap[level];
            document.getElementById('system-health-display').textContent = `${systemHealth}%`;
            document.getElementById('system-health-display').className = `text-6xl font-bold ${color.text} mono`;
        }

        // Quick Actions
        function quickAction(action) {
            const actions = {
                scan: 'Run a full system scan',
                attack: 'Simulate an attack scenario',
                status: 'Generate a detailed status report',
                vulnerabilities: 'Analyze system vulnerabilities'
            };
            
            document.getElementById('chat-input').value = actions[action];
            sendMessage();
        }

        // Tank Animation
        function startTankAnimation() {
            if (tankAnimationInterval) clearInterval(tankAnimationInterval);
            
            tankAnimationInterval = setInterval(() => {
                const dangerMultiplier = { LOW: 1, MEDIUM: 1.5, HIGH: 2.5, CRITICAL: 3.5 };
                const intensity = dangerMultiplier[currentDangerLevel] || 1;
                
                if (currentDangerLevel === 'LOW') {
                    updateTank('tank1', 48 + Math.random() * 4, '#10b981');
                    updateTank('tank2', 58 + Math.random() * 4, '#10b981');
                    updateTank('tank3', 43 + Math.random() * 4, '#10b981');
                    document.getElementById('tank3-alert').classList.add('hidden');
                } else {
                    updateTank('tank1', 48 + Math.random() * 15 * (intensity - 1), getColorForLevel(48 + Math.random() * 15 * (intensity - 1)));
                    updateTank('tank2', 58 + Math.random() * 20 * (intensity - 1), getColorForLevel(58 + Math.random() * 20 * (intensity - 1)));
                    const level3 = 43 + Math.random() * 40 * (intensity - 1);
                    updateTank('tank3', level3, getColorForLevel(level3));
                    
                    if (level3 > 75) {
                        document.getElementById('tank3-alert').classList.remove('hidden');
                    } else {
                        document.getElementById('tank3-alert').classList.add('hidden');
                    }
                }
            }, 1200);
        }

        function updateTank(id, level, color) {
            const water = document.getElementById(`${id}-water`);
            const levelText = document.getElementById(`${id}-level`);
            water.style.height = `${Math.min(level, 100)}%`;
            water.style.backgroundColor = color;
            levelText.textContent = `${Math.round(Math.min(level, 100))}%`;
        }

        function getColorForLevel(level) {
            if (level > 85) return '#ef4444';
            if (level > 70) return '#f59e0b';
            return '#10b981';
        }
    </script>
</body>
</html>

        :root {
            --neon-cyan: #00ffff;
            --neon-magenta: #ff00ff;
            --neon-yellow: #ffff00;
            --deep-space: #0a0e27;
            --void-black: #030712;
            --electric-blue: #00d4ff;
            --danger-red: #ff1744;
            --success-green: #00ff9f;
            --warning-amber: #ffab00;
            --grid-color: rgba(0, 255, 255, 0.08);
            --glow-cyan: rgba(0, 255, 255, 0.4);
            --glow-magenta: rgba(255, 0, 255, 0.4);
        }

        @keyframes scanline {
            0% { transform: translateY(-100%); }
            100% { transform: translateY(100vh); }
        }

        @keyframes flicker {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.95; }
        }

        @keyframes pulse-glow {
            0%, 100% { 
                box-shadow: 0 0 5px var(--neon-cyan), 0 0 10px var(--neon-cyan);
            }
            50% { 
                box-shadow: 0 0 10px var(--neon-cyan), 0 0 20px var(--neon-cyan), 0 0 30px var(--neon-cyan);
            }
        }

        @keyframes data-stream {
            0% { transform: translateY(-100%); opacity: 0; }
            10% { opacity: 1; }
            90% { opacity: 1; }
            100% { transform: translateY(100%); opacity: 0; }
        }

        @keyframes glitch-animation {
            0% {
                clip-path: polygon(0 0, 100% 0, 100% 45%, 0 45%);
                transform: translate(0);
            }
            10% {
                clip-path: polygon(0 15%, 100% 15%, 100% 60%, 0 60%);
                transform: translate(-5px, 5px);
            }
            20% {
                clip-path: polygon(0 70%, 100% 70%, 100% 100%, 0 100%);
                transform: translate(5px, -5px);
            }
            30% {
                clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
                transform: translate(0);
            }
            100% {
                clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
                transform: translate(0);
            }
        }

        body {
            font-family: 'Rajdhani', sans-serif;
            background: var(--void-black);
            color: var(--neon-cyan);
            overflow-x: hidden;
            line-height: 1.6;
            position: relative;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                repeating-linear-gradient(
                    0deg,
                    rgba(0, 255, 255, 0.03) 0px,
                    transparent 1px,
                    transparent 2px,
                    rgba(0, 255, 255, 0.03) 3px
                );
            pointer-events: none;
            z-index: 1000;
            animation: flicker 0.15s infinite;
        }

        /* Scanline effect */
        body::after {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 3px;
            background: linear-gradient(transparent, var(--neon-cyan), transparent);
            opacity: 0.3;
            animation: scanline 8s linear infinite;
            pointer-events: none;
            z-index: 999;
        }

        #root {
            position: relative;
            min-height: 100vh;
            z-index: 1;
        }

        /* Animated background grid */
        .cyber-grid {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                linear-gradient(var(--grid-color) 1.5px, transparent 1.5px),
                linear-gradient(90deg, var(--grid-color) 1.5px, transparent 1.5px),
                linear-gradient(var(--neon-magenta) 0.5px, transparent 0.5px),
                linear-gradient(90deg, var(--neon-magenta) 0.5px, transparent 0.5px);
            background-size: 100px 100px, 100px 100px, 20px 20px, 20px 20px;
            background-position: -1px -1px, -1px -1px, -1px -1px, -1px -1px;
            opacity: 0.15;
            pointer-events: none;
            z-index: 0;
            perspective: 1000px;
            transform: rotateX(60deg) scale(1.5);
            transform-origin: center center;
        }

        /* Header */
        .app-header {
            position: relative;
            z-index: 10;
            padding: 1.5rem 3rem;
            background: linear-gradient(135deg, rgba(0, 255, 255, 0.05) 0%, rgba(255, 0, 255, 0.05) 100%);
            border-bottom: 2px solid var(--neon-cyan);
            box-shadow: 0 0 20px var(--glow-cyan);
            backdrop-filter: blur(10px);
        }

        .header-content {
            max-width: 1800px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .app-title {
            font-family: 'Audiowide', cursive;
            font-size: 2.5rem;
            font-weight: 400;
            text-transform: uppercase;
            letter-spacing: 4px;
            background: linear-gradient(90deg, var(--neon-cyan), var(--neon-magenta), var(--neon-cyan));
            background-size: 200% auto;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: shimmer 3s linear infinite;
            text-shadow: 0 0 30px var(--glow-cyan);
            position: relative;
        }

        @keyframes shimmer {
            to { background-position: 200% center; }
        }

        .app-subtitle {
            color: var(--electric-blue);
            font-size: 0.75rem;
            letter-spacing: 3px;
            margin-top: 0.5rem;
            text-transform: uppercase;
            font-family: 'Share Tech Mono', monospace;
            opacity: 0.8;
        }

        .system-status {
            display: flex;
            gap: 2rem;
            align-items: center;
        }

        .status-item {
            font-family: 'Share Tech Mono', monospace;
            font-size: 0.85rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        /* Main container */
        .app-container {
            position: relative;
            z-index: 1;
            padding: 2rem 3rem;
            max-width: 1900px;
            margin: 0 auto;
        }

        /* Navigation tabs */
        .nav-tabs {
            display: flex;
            gap: 0;
            margin-bottom: 2rem;
            background: rgba(0, 0, 0, 0.4);
            border: 1px solid var(--neon-cyan);
            border-radius: 0;
            overflow: hidden;
        }

        .nav-tab {
            flex: 1;
            background: transparent;
            border: none;
            color: var(--neon-cyan);
            padding: 1rem 2rem;
            font-family: 'Rajdhani', sans-serif;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            text-transform: uppercase;
            letter-spacing: 2px;
            border-right: 1px solid rgba(0, 255, 255, 0.2);
        }

        .nav-tab:last-child {
            border-right: none;
        }

        .nav-tab::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 0;
            background: linear-gradient(180deg, var(--neon-cyan), transparent);
            opacity: 0;
            transition: all 0.3s ease;
        }

        .nav-tab:hover {
            background: rgba(0, 255, 255, 0.1);
        }

        .nav-tab.active {
            background: rgba(0, 255, 255, 0.15);
            color: var(--neon-yellow);
            box-shadow: inset 0 0 20px var(--glow-cyan);
        }

        .nav-tab.active::before {
            height: 3px;
            opacity: 1;
        }

        /* Dashboard grid */
        .dashboard-grid {
            display: grid;
            grid-template-columns: repeat(12, 1fr);
            gap: 1.5rem;
        }

        .grid-span-12 { grid-column: span 12; }
        .grid-span-9 { grid-column: span 9; }
        .grid-span-8 { grid-column: span 8; }
        .grid-span-6 { grid-column: span 6; }
        .grid-span-4 { grid-column: span 4; }
        .grid-span-3 { grid-column: span 3; }

        /* Cyber cards */
        .cyber-panel {
            background: linear-gradient(135deg, rgba(0, 20, 40, 0.8) 0%, rgba(10, 14, 39, 0.9) 100%);
            border: 1px solid var(--neon-cyan);
            position: relative;
            overflow: hidden;
            transition: all 0.3s ease;
        }

        .cyber-panel::before {
            content: '';
            position: absolute;
            top: -2px;
            left: -2px;
            right: -2px;
            bottom: -2px;
            background: linear-gradient(45deg, var(--neon-cyan), var(--neon-magenta), var(--neon-cyan));
            background-size: 300% 300%;
            opacity: 0;
            transition: opacity 0.3s ease;
            z-index: -1;
            animation: gradient-shift 3s ease infinite;
        }

        @keyframes gradient-shift {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        .cyber-panel:hover::before {
            opacity: 0.3;
        }

        .cyber-panel:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 30px var(--glow-cyan);
        }

        .panel-header {
            padding: 1rem 1.5rem;
            background: rgba(0, 255, 255, 0.05);
            border-bottom: 1px solid rgba(0, 255, 255, 0.3);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .panel-title {
            font-family: 'Audiowide', cursive;
            font-size: 1.1rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            color: var(--neon-cyan);
        }

        .panel-badge {
            background: var(--neon-cyan);
            color: var(--void-black);
            padding: 0.25rem 0.75rem;
            font-size: 0.7rem;
            font-weight: 700;
            letter-spacing: 1px;
            font-family: 'Share Tech Mono', monospace;
        }

        .panel-body {
            padding: 1.5rem;
        }

        /* Metrics */
        .metrics-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
        }

        .metric-card {
            background: rgba(0, 0, 0, 0.5);
            border-left: 3px solid var(--neon-cyan);
            padding: 1.25rem;
            position: relative;
            transition: all 0.3s ease;
        }

        .metric-card::after {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            width: 30%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(0, 255, 255, 0.05));
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .metric-card:hover::after {
            opacity: 1;
        }

        .metric-card.critical {
            border-left-color: var(--danger-red);
        }

        .metric-card.warning {
            border-left-color: var(--warning-amber);
        }

        .metric-card.success {
            border-left-color: var(--success-green);
        }

        .metric-label {
            font-size: 0.7rem;
            color: rgba(0, 255, 255, 0.7);
            text-transform: uppercase;
            letter-spacing: 2px;
            font-family: 'Share Tech Mono', monospace;
            margin-bottom: 0.5rem;
        }

        .metric-value {
            font-size: 2.5rem;
            font-weight: 700;
            font-family: 'Audiowide', cursive;
            line-height: 1;
            margin-bottom: 0.25rem;
        }

        .metric-subtext {
            font-size: 0.75rem;
            opacity: 0.6;
            font-family: 'Share Tech Mono', monospace;
        }

        /* Status indicators */
        .status-dot {
            display: inline-block;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            margin-right: 0.75rem;
            position: relative;
        }

        .status-dot::before {
            content: '';
            position: absolute;
            inset: -3px;
            border-radius: 50%;
            background: inherit;
            opacity: 0.4;
            animation: pulse-ring 2s ease-out infinite;
        }

        @keyframes pulse-ring {
            0% { transform: scale(1); opacity: 0.5; }
            100% { transform: scale(1.5); opacity: 0; }
        }

        .status-safe {
            background: var(--success-green);
            box-shadow: 0 0 10px var(--success-green);
        }

        .status-warning {
            background: var(--warning-amber);
            box-shadow: 0 0 10px var(--warning-amber);
        }

        .status-critical {
            background: var(--danger-red);
            box-shadow: 0 0 10px var(--danger-red);
        }

        .status-analyzing {
            background: var(--electric-blue);
            box-shadow: 0 0 10px var(--electric-blue);
        }

        /* Buttons */
        .cyber-button {
            background: transparent;
            border: 2px solid var(--neon-cyan);
            color: var(--neon-cyan);
            padding: 0.75rem 2rem;
            font-family: 'Rajdhani', sans-serif;
            font-weight: 600;
            font-size: 0.9rem;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 2px;
            clip-path: polygon(0 0, calc(100% - 10px) 0, 100% 10px, 100% 100%, 10px 100%, 0 calc(100% - 10px));
        }

        .cyber-button::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: var(--neon-cyan);
            transition: left 0.4s ease;
            z-index: -1;
        }

        .cyber-button:hover {
            color: var(--void-black);
            box-shadow: 0 0 20px var(--glow-cyan);
        }

        .cyber-button:hover::before {
            left: 0;
        }

        .cyber-button.danger {
            border-color: var(--danger-red);
            color: var(--danger-red);
        }

        .cyber-button.danger::before {
            background: var(--danger-red);
        }

        .cyber-button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        /* Process flow visualization */
        .process-flow {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 2rem;
            background: rgba(0, 0, 0, 0.4);
            position: relative;
        }

        .process-stage {
            flex: 1;
            text-align: center;
            padding: 1.5rem 1rem;
            background: linear-gradient(135deg, rgba(0, 255, 255, 0.1), rgba(0, 255, 255, 0.05));
            border: 2px solid var(--neon-cyan);
            position: relative;
            transition: all 0.3s ease;
            clip-path: polygon(10% 0, 100% 0, 90% 100%, 0 100%);
            margin: 0 -10px;
        }

        .process-stage:first-child {
            clip-path: polygon(0 0, 100% 0, 90% 100%, 0 100%);
            margin-left: 0;
        }

        .process-stage:last-child {
            clip-path: polygon(10% 0, 100% 0, 100% 100%, 0 100%);
            margin-right: 0;
        }

        .process-stage:hover {
            transform: scale(1.05);
            box-shadow: 0 0 30px var(--glow-cyan);
            z-index: 10;
        }

        .process-stage.vulnerable {
            border-color: var(--danger-red);
            background: linear-gradient(135deg, rgba(255, 23, 68, 0.2), rgba(255, 23, 68, 0.1));
            animation: warning-flash 2s ease-in-out infinite;
        }

        @keyframes warning-flash {
            0%, 100% { box-shadow: 0 0 10px rgba(255, 23, 68, 0.3); }
            50% { box-shadow: 0 0 30px rgba(255, 23, 68, 0.8), 0 0 60px rgba(255, 23, 68, 0.4); }
        }

        .stage-number {
            font-size: 0.7rem;
            opacity: 0.6;
            font-family: 'Share Tech Mono', monospace;
        }

        .stage-name {
            font-size: 1rem;
            font-weight: 700;
            margin-top: 0.5rem;
            font-family: 'Rajdhani', sans-serif;
        }

        .stage-status {
            font-size: 0.7rem;
            margin-top: 0.5rem;
            font-family: 'Share Tech Mono', monospace;
        }

        /* Attack cards */
        .attack-card {
            background: rgba(0, 0, 0, 0.6);
            border-left: 4px solid var(--warning-amber);
            padding: 1.25rem;
            margin-bottom: 1rem;
            transition: all 0.3s ease;
            position: relative;
        }

        .attack-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 3px;
            height: 0;
            background: var(--neon-cyan);
            transition: height 0.3s ease;
        }

        .attack-card:hover {
            background: rgba(0, 0, 0, 0.8);
            transform: translateX(5px);
        }

        .attack-card:hover::before {
            height: 100%;
        }

        .attack-card.critical {
            border-left-color: var(--danger-red);
        }

        .attack-card.high {
            border-left-color: var(--warning-amber);
        }

        .attack-card.medium {
            border-left-color: var(--electric-blue);
        }

        .attack-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 0.75rem;
        }

        .attack-name {
            font-size: 1.1rem;
            font-weight: 700;
            color: var(--neon-cyan);
            font-family: 'Rajdhani', sans-serif;
        }

        .attack-severity {
            padding: 0.25rem 0.75rem;
            font-size: 0.7rem;
            font-weight: 700;
            letter-spacing: 1px;
            font-family: 'Share Tech Mono', monospace;
        }

        .attack-description {
            font-size: 0.9rem;
            line-height: 1.6;
            color: rgba(0, 255, 255, 0.8);
            margin-bottom: 0.75rem;
        }

        .attack-meta {
            display: flex;
            gap: 2rem;
            font-size: 0.75rem;
            font-family: 'Share Tech Mono', monospace;
            color: rgba(0, 255, 255, 0.6);
            margin-top: 1rem;
            padding-top: 1rem;
            border-top: 1px solid rgba(0, 255, 255, 0.2);
        }

        .attack-meta-item strong {
            color: var(--neon-cyan);
        }

        /* Vulnerability list */
        .vulnerability-list {
            max-height: 600px;
            overflow-y: auto;
        }

        .vulnerability-item {
            background: rgba(0, 0, 0, 0.5);
            border-left: 4px solid var(--neon-cyan);
            padding: 1.25rem;
            margin-bottom: 1rem;
            transition: all 0.3s ease;
        }

        .vulnerability-item:hover {
            background: rgba(0, 0, 0, 0.7);
            transform: translateX(5px);
            box-shadow: -5px 0 20px rgba(0, 255, 255, 0.2);
        }

        .vuln-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 0.75rem;
        }

        .vuln-title {
            font-size: 1rem;
            font-weight: 700;
            color: var(--neon-cyan);
        }

        .vuln-severity-badge {
            padding: 0.25rem 0.75rem;
            font-size: 0.65rem;
            font-weight: 700;
            letter-spacing: 1px;
        }

        .vuln-description {
            font-size: 0.85rem;
            line-height: 1.6;
            color: rgba(0, 255, 255, 0.7);
            margin-bottom: 0.75rem;
        }

        .vuln-score {
            display: inline-block;
            font-family: 'Share Tech Mono', monospace;
            font-size: 0.75rem;
            margin-top: 0.5rem;
        }

        .vuln-mitigation {
            margin-top: 1rem;
            padding: 1rem;
            background: rgba(0, 255, 159, 0.05);
            border-left: 3px solid var(--success-green);
            font-size: 0.85rem;
            line-height: 1.6;
        }

        .vuln-mitigation strong {
            color: var(--success-green);
            display: block;
            margin-bottom: 0.5rem;
        }

        /* Console */
        .console {
            background: #000;
            padding: 1rem;
            font-family: 'Share Tech Mono', monospace;
            font-size: 0.8rem;
            max-height: 400px;
            overflow-y: auto;
            border: 1px solid var(--neon-cyan);
        }

        .console-line {
            margin-bottom: 0.25rem;
            display: flex;
            gap: 1rem;
        }

        .console-timestamp {
            color: rgba(0, 255, 255, 0.5);
            flex-shrink: 0;
        }

        .console-message {
            color: var(--neon-cyan);
        }

        .console-line.info .console-message {
            color: var(--electric-blue);
        }

        .console-line.warning .console-message {
            color: var(--warning-amber);
        }

        .console-line.error .console-message {
            color: var(--danger-red);
        }

        .console-line.success .console-message {
            color: var(--success-green);
        }

        /* Form elements */
        .cyber-select {
            background: rgba(0, 0, 0, 0.6);
            border: 1px solid var(--neon-cyan);
            color: var(--neon-cyan);
            padding: 0.75rem 1rem;
            font-family: 'Rajdhani', sans-serif;
            font-size: 0.9rem;
            cursor: pointer;
            width: 100%;
            transition: all 0.3s ease;
        }

        .cyber-select:focus {
            outline: none;
            box-shadow: 0 0 15px var(--glow-cyan);
            border-color: var(--neon-yellow);
        }

        .cyber-input {
            background: rgba(0, 0, 0, 0.6);
            border: 1px solid var(--neon-cyan);
            color: var(--neon-cyan);
            padding: 0.75rem 1rem;
            font-family: 'Share Tech Mono', monospace;
            width: 100%;
            transition: all 0.3s ease;
        }

        .cyber-input:focus {
            outline: none;
            box-shadow: 0 0 15px var(--glow-cyan);
            border-color: var(--neon-yellow);
        }

        /* Loading animation */
        .loading-spinner {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(0, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: var(--neon-cyan);
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* Data stream visualization */
        .data-stream {
            position: absolute;
            top: 0;
            width: 2px;
            height: 100px;
            background: linear-gradient(transparent, var(--neon-cyan), transparent);
            animation: data-stream 3s linear infinite;
        }

        /* Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }

        ::-webkit-scrollbar-track {
            background: rgba(0, 0, 0, 0.5);
        }

        ::-webkit-scrollbar-thumb {
            background: var(--neon-cyan);
            border-radius: 0;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: var(--neon-magenta);
        }

        /* Responsive */
        @media (max-width: 1200px) {
            .grid-span-9, .grid-span-8, .grid-span-6, .grid-span-4, .grid-span-3 {
                grid-column: span 12 !important;
            }

            .process-stage {
                clip-path: none !important;
                margin: 0.5rem 0 !important;
            }

            .process-flow {
                flex-direction: column;
            }
        }

        /* Chart containers */
        .chart-container {
            min-height: 300px;
            background: rgba(0, 0, 0, 0.3);
            padding: 1rem;
        }

        /* Defense recommendation cards */
        .defense-card {
            background: rgba(0, 255, 159, 0.05);
            border: 1px solid var(--success-green);
            padding: 1.25rem;
            margin-bottom: 1rem;
            transition: all 0.3s ease;
        }

        .defense-card:hover {
            background: rgba(0, 255, 159, 0.1);
            box-shadow: 0 0 20px rgba(0, 255, 159, 0.2);
        }

        .defense-title {
            font-size: 1rem;
            font-weight: 700;
            color: var(--success-green);
            margin-bottom: 0.75rem;
            font-family: 'Rajdhani', sans-serif;
        }

        .defense-description {
            font-size: 0.85rem;
            line-height: 1.6;
            color: rgba(0, 255, 255, 0.8);
        }

        .defense-type {
            display: inline-block;
            margin-top: 0.75rem;
            padding: 0.25rem 0.75rem;
            background: var(--success-green);
            color: var(--void-black);
            font-size: 0.7rem;
            font-weight: 700;
            letter-spacing: 1px;
        }
    </style>
</head>
<body>
    <div class="cyber-grid"></div>
    <div id="root"></div>

    <script type="text/babel">
        const { useState, useEffect, useCallback, useMemo } = React;

        // ==================== MOCK DATA GENERATORS ====================
        
        const generateSWaTData = () => {
            const sensors = ['FIT-101', 'LIT-101', 'AIT-201', 'FIT-301', 'LIT-301', 'DPIT-301', 'FIT-401', 'AIT-501', 'PIT-501', 'FIT-601'];
            const data = [];
            const now = Date.now();
            
            for (let i = 0; i < 200; i++) {
                const timestamp = new Date(now - (200 - i) * 30000);
                const point = { 
                    timestamp: timestamp.toISOString(),
                    time: timestamp.getTime()
                };
                
                sensors.forEach(sensor => {
                    const baseValue = 50 + Math.sin(i / 10) * 20;
                    const noise = (Math.random() - 0.5) * 10;
                    point[sensor] = Math.max(0, Math.min(100, baseValue + noise)).toFixed(2);
                });
                
                data.push(point);
            }
            
            return data;
        };

        const generateAttackScenarios = () => {
            return [
                {
                    id: 1,
                    name: 'Stealthy Sensor Drift Attack',
                    type: 'VAE-Generated',
                    model: 'Variational Autoencoder',
                    confidence: 0.89,
                    affectedSensors: ['LIT-101', 'FIT-101', 'MV-101'],
                    description: 'Gradual drift in water level sensors (LIT-101) over 45-minute window, designed to mask overflow conditions while staying below anomaly detection thresholds. Attack manipulates readings by 0.3% per minute.',
                    severity: 'high',
                    exploitability: 0.82,
                    impact: 'Tank overflow, potential equipment damage, undetected for avg. 38 minutes',
                    technique: 'Time-series manipulation with gradual deviation accumulation'
                },
                {
                    id: 2,
                    name: 'Coordinated Multi-Pump Attack',
                    type: 'TimeGAN-Generated',
                    model: 'Temporal Generative Adversarial Network',
                    confidence: 0.94,
                    affectedSensors: ['P-101', 'P-102', 'P-201', 'MV-101', 'MV-201'],
                    description: 'Simultaneous activation of conflicting pump commands across P1 and P2 stages. Creates hydraulic instability and pressure spikes that can damage equipment while appearing as normal operational variation.',
                    severity: 'critical',
                    exploitability: 0.91,
                    impact: 'System-wide pressure instability, pump burnout risk, cascade failure potential',
                    technique: 'Synchronized actuator manipulation with temporal correlation'
                },
                {
                    id: 3,
                    name: 'Delayed Chemical Injection',
                    type: 'VAE-Generated',
                    model: 'Variational Autoencoder',
                    confidence: 0.76,
                    affectedSensors: ['AIT-201', 'FIT-301', 'P-203'],
                    description: 'Introduces 8-15 second delays in chemical dosing system response time, causing pH imbalance in ultrafiltration stage. Delay is variable enough to avoid pattern detection but consistent enough to cause process degradation.',
                    severity: 'medium',
                    exploitability: 0.68,
                    impact: 'Water quality degradation, membrane fouling, increased maintenance cycles',
                    technique: 'Response-time manipulation with stochastic delay injection'
                },
                {
                    id: 4,
                    name: 'Multi-Stage Cascade Failure',
                    type: 'Diffusion-Generated',
                    model: 'Diffusion-based Time Series Generator',
                    confidence: 0.87,
                    affectedSensors: ['LIT-101', 'LIT-301', 'DPIT-301', 'P-301', 'P-302', 'FIT-401'],
                    description: 'Sequential attack progressing through P1→P3→P4 stages. Initial trigger in raw water storage cascades through ultrafiltration to RO feed, exploiting lack of inter-stage correlation monitoring.',
                    severity: 'critical',
                    exploitability: 0.88,
                    impact: 'Complete system shutdown required, 4-6 hour recovery time, potential membrane damage',
                    technique: 'Cross-stage temporal correlation exploitation'
                },
                {
                    id: 5,
                    name: 'Phantom Sensor Injection',
                    type: 'TimeGAN-Generated',
                    model: 'Temporal Generative Adversarial Network',
                    confidence: 0.81,
                    affectedSensors: ['DPIT-301', 'FIT-401', 'AIT-501'],
                    description: 'Injects synthetic sensor readings that are statistically normal but physically impossible given current system state. Creates "ghost" process conditions that confuse control logic.',
                    severity: 'high',
                    exploitability: 0.79,
                    impact: 'Control logic confusion, unnecessary equipment activation, energy waste',
                    technique: 'Physics-decoupled synthetic data generation'
                },
                {
                    id: 6,
                    name: 'Oscillation Amplification',
                    type: 'Diffusion-Generated',
                    model: 'Diffusion-based Time Series Generator',
                    confidence: 0.73,
                    affectedSensors: ['PIT-501', 'FIT-601', 'P-501', 'P-601'],
                    description: 'Amplifies natural system oscillations in RO stage by introducing resonant frequency perturbations. Stays within normal bounds individually but creates destructive interference patterns.',
                    severity: 'medium',
                    exploitability: 0.71,
                    impact: 'Accelerated equipment wear, reduced membrane lifespan, energy inefficiency',
                    technique: 'Resonance-based perturbation with frequency matching'
                }
            ];
        };

        const generateVulnerabilities = () => {
            return [
                {
                    id: 1,
                    title: 'Missing Sensor Redundancy: LIT-101',
                    severity: 'critical',
                    stage: 'P1',
                    cvssScore: 9.1,
                    description: 'Critical single point of failure in water level monitoring for raw water storage tank. No backup sensor or independent validation mechanism detected. Attack window: unlimited duration with no automated detection.',
                    exploitability: 0.94,
                    impact: 'Complete loss of level monitoring, overflow risk, equipment damage, potential environmental hazard',
                    affectedSensors: ['LIT-101'],
                    mitigation: 'Install redundant level sensor LIT-101-B with independent power supply and communication channel. Implement cross-validation logic comparing LIT-101 with flow rates (FIT-101) and pump status (P-101/P-102).',
                    detectionRule: 'IF |LIT-101 - predicted_level(FIT-101, P-101)| > 5% FOR 60s THEN ALERT',
                    estimatedCost: '$8,500',
                    implementationTime: '2 weeks'
                },
                {
                    id: 2,
                    title: 'Insufficient Alarm Threshold: AIT-201',
                    severity: 'high',
                    stage: 'P2',
                    cvssScore: 7.8,
                    description: 'pH sensor alarm threshold set to ±0.8 pH units from setpoint (15% deviation). Industry best practice recommends ±0.3 pH units (5% deviation) for critical water treatment processes. Creates 12-18 minute attack window before alarm triggers.',
                    exploitability: 0.82,
                    impact: 'Delayed response to chemical imbalance, membrane damage risk, water quality violations',
                    affectedSensors: ['AIT-201'],
                    mitigation: 'Reduce alarm threshold to ±0.3 pH units. Implement predictive alerting using pH trend analysis and chemical dosing correlation. Add rate-of-change alarm (>0.1 pH/min).',
                    detectionRule: 'IF |AIT-201 - setpoint| > 0.3 OR delta_pH > 0.1/min THEN ALERT',
                    estimatedCost: '$1,200',
                    implementationTime: '3 days'
                },
                {
                    id: 3,
                    title: 'Unmonitored State Transitions: MV-201',
                    severity: 'high',
                    stage: 'P2',
                    cvssScore: 8.2,
                    description: 'Chemical dosing valve (MV-201) state changes are not logged, validated, or correlated with process requirements. No verification that valve commands match pH setpoint or flow conditions. Enables covert manipulation.',
                    exploitability: 0.87,
                    impact: 'Unauthorized chemical dosing, potential overdose/underdose conditions, audit trail gaps',
                    affectedSensors: ['MV-201', 'AIT-201', 'P-203'],
                    mitigation: 'Implement comprehensive valve state logging with timestamp correlation. Add validation logic: MV-201 commands must align with AIT-201 feedback and P-203 status. Create audit trail for all valve operations with anomaly detection on unexpected transitions.',
                    detectionRule: 'LOG all MV-201 transitions; IF transition_unexpected(MV-201, AIT-201, P-203) THEN ALERT',
                    estimatedCost: '$3,800',
                    implementationTime: '1 week'
                },
                {
                    id: 4,
                    title: 'Response Time Monitoring Gap: P-301/P-302',
                    severity: 'medium',
                    stage: 'P3',
                    cvssScore: 6.4,
                    description: 'UF feed pumps (P-301/P-302) activation delays are not monitored or verified. Normal response time: <800ms. Attack can inject 3-5 second delays without detection, creating pressure transients and flow instability.',
                    exploitability: 0.68,
                    impact: 'Pressure transients, membrane stress, reduced filtration efficiency, premature equipment failure',
                    affectedSensors: ['P-301', 'P-302', 'DPIT-301', 'FIT-301'],
                    mitigation: 'Implement response time monitoring with <1000ms threshold. Log pump command timestamp, acknowledgment timestamp, and measured flow response. Alert on delays >1000ms or failed activations.',
                    detectionRule: 'IF pump_response_time(P-301|P-302) > 1000ms THEN ALERT',
                    estimatedCost: '$2,400',
                    implementationTime: '5 days'
                },
                {
                    id: 5,
                    title: 'Cross-Stage Correlation Blind Spot',
                    severity: 'critical',
                    stage: 'System-wide',
                    cvssScore: 9.3,
                    description: 'No automated correlation or anomaly detection across P1-P6 stages. Each stage operates independently with local control loops. Enables cascading failures and multi-stage attacks to propagate undetected until catastrophic failure.',
                    exploitability: 0.93,
                    impact: 'Undetected cascade failures, extended attack windows, complete system compromise possible',
                    affectedSensors: ['All stages P1-P6'],
                    mitigation: 'Deploy ML-based cross-stage anomaly correlation engine. Monitor flow balance: sum(inflows) = sum(outflows) ± 2%. Track temporal correlations: P1 level changes should correlate with P3 flow within 8-12 minutes. Implement digital twin for physics-based validation.',
                    detectionRule: 'CORRELATE(all_stages) using ML model; IF correlation_anomaly > threshold THEN ALERT',
                    estimatedCost: '$45,000',
                    implementationTime: '8 weeks'
                },
                {
                    id: 6,
                    title: 'Inadequate Flow Balance Validation',
                    severity: 'high',
                    stage: 'P3-P4',
                    cvssScore: 7.6,
                    description: 'Flow measurements between UF and RO stages (FIT-301, FIT-401) are not cross-validated. Mass balance equations not enforced. Attackers can inject phantom flow readings creating 15-20% discrepancies without triggering alarms.',
                    exploitability: 0.76,
                    impact: 'Inaccurate process control, potential membrane overload, undetected bypass conditions',
                    affectedSensors: ['FIT-301', 'FIT-401', 'LIT-301'],
                    mitigation: 'Implement real-time mass balance validation: FIT-301 output should equal FIT-401 input ±3% accounting for tank level changes (LIT-301). Add sensor cross-validation using redundant measurement principles.',
                    detectionRule: 'IF |FIT-301 - FIT-401 - delta(LIT-301)| > 3% FOR 120s THEN ALERT',
                    estimatedCost: '$5,600',
                    implementationTime: '2 weeks'
                },
                {
                    id: 7,
                    title: 'Pressure Spike Detection Disabled',
                    severity: 'medium',
                    stage: 'P5',
                    cvssScore: 6.8,
                    description: 'RO pressure transmitter (PIT-501) configured for average sampling (10s window) without rate-of-change monitoring. Transient pressure spikes <10s duration go undetected despite potential to damage membranes.',
                    exploitability: 0.64,
                    impact: 'Membrane damage from pressure spikes, reduced membrane life, unexpected downtime',
                    affectedSensors: ['PIT-501', 'P-501'],
                    mitigation: 'Enable high-frequency sampling (1s intervals) with rate-of-change alarm. Threshold: >50 psi/s rate of change. Implement pressure spike logging and correlation with pump status changes.',
                    detectionRule: 'IF delta_pressure(PIT-501) > 50_psi/s THEN ALERT',
                    estimatedCost: '$1,800',
                    implementationTime: '4 days'
                }
            ];
        };

        const generateDefenseStrategies = () => {
            return {
                preventive: [
                    {
                        id: 1,
                        title: 'Sensor Redundancy Implementation',
                        description: 'Deploy backup sensors for all critical measurement points (LIT-101, AIT-201, DPIT-301, PIT-501). Use 2-out-of-3 voting logic for safety-critical decisions.',
                        type: 'PREVENTIVE',
                        priority: 'High',
                        coverage: ['P1', 'P2', 'P3', 'P5']
                    },
                    {
                        id: 2,
                        title: 'Input Validation & Range Checking',
                        description: 'Implement strict range checking and rate-of-change limits on all sensor inputs. Reject physically impossible values based on equipment specifications and process physics.',
                        type: 'PREVENTIVE',
                        priority: 'Critical',
                        coverage: ['All Stages']
                    },
                    {
                        id: 3,
                        title: 'State Machine Hardening',
                        description: 'Add state transition validation to prevent illegal process sequences. Implement formal specification of allowed state transitions with automated enforcement.',
                        type: 'PREVENTIVE',
                        priority: 'High',
                        coverage: ['P2', 'P3', 'P4']
                    },
                    {
                        id: 4,
                        title: 'Communication Channel Encryption',
                        description: 'Encrypt all sensor data and control commands using TLS 1.3. Implement certificate-based authentication for all field devices.',
                        type: 'PREVENTIVE',
                        priority: 'Medium',
                        coverage: ['Network Layer']
                    }
                ],
                reactive: [
                    {
                        id: 5,
                        title: 'ML-Based Anomaly Detection',
                        description: 'Real-time monitoring using trained VAE model with 0.95 confidence threshold. Detects deviations from normal operational patterns within 30-60 seconds.',
                        type: 'REACTIVE',
                        priority: 'Critical',
                        coverage: ['All Stages']
                    },
                    {
                        id: 6,
                        title: 'Cross-Stage Correlation Engine',
                        description: 'Automated correlation engine detects cascading failures across P1-P6 stages. Uses temporal and causal relationship models to identify multi-stage attacks.',
                        type: 'REACTIVE',
                        priority: 'Critical',
                        coverage: ['System-wide']
                    },
                    {
                        id: 7,
                        title: 'Emergency Shutdown Logic',
                        description: 'Automated safe-state procedures triggered on critical threshold violations. Graceful degradation protocol preserves equipment while preventing catastrophic failure.',
                        type: 'REACTIVE',
                        priority: 'High',
                        coverage: ['All Stages']
                    },
                    {
                        id: 8,
                        title: 'Forensic Logging System',
                        description: 'Comprehensive logging of all sensor readings, control commands, and state changes with tamper-evident storage. Enables post-incident analysis and attack attribution.',
                        type: 'REACTIVE',
                        priority: 'Medium',
                        coverage: ['System-wide']
                    }
                ]
            };
        };

        // ==================== MAIN APP COMPONENT ====================

        const SWaTGuardianDashboard = () => {
            const [activeTab, setActiveTab] = useState('overview');
            const [swatData, setSwatData] = useState([]);
            const [attackScenarios, setAttackScenarios] = useState([]);
            const [vulnerabilities, setVulnerabilities] = useState([]);
            const [defenseStrategies, setDefenseStrategies] = useState({ preventive: [], reactive: [] });
            const [selectedAttack, setSelectedAttack] = useState(null);
            const [simulationRunning, setSimulationRunning] = useState(false);
            const [generativeModel, setGenerativeModel] = useState('VAE');
            const [consoleLog, setConsoleLog] = useState([]);
            const [systemMetrics, setSystemMetrics] = useState({
                vulnerabilitiesFound: 0,
                criticalVulns: 0,
                attacksGenerated: 0,
                twinSyncStatus: 98.7
            });
            const [digitalTwinState, setDigitalTwinState] = useState({
                p1_level: 52.3,
                p1_flow: 45.8,
                p2_pH: 7.2,
                p2_chemical: 'NORMAL',
                p3_pressure: 2.4,
                p3_flow: 42.1,
                p4_turbidity: 0.8,
                p5_ro_pressure: 15.2,
                p5_permeate: 38.5,
                p6_output: 40.2
            });

            // Initialize data on mount
            useEffect(() => {
                const data = generateSWaTData();
                const attacks = generateAttackScenarios();
                const vulns = generateVulnerabilities();
                const defenses = generateDefenseStrategies();
                
                setSwatData(data);
                setAttackScenarios(attacks);
                setVulnerabilities(vulns);
                setDefenseStrategies(defenses);
                
                setSystemMetrics({
                    vulnerabilitiesFound: vulns.length,
                    criticalVulns: vulns.filter(v => v.severity === 'critical').length,
                    attacksGenerated: attacks.length,
                    twinSyncStatus: 98.7
                });

                addLog('System initialized successfully', 'success');
                addLog(`Loaded ${data.length} SWaT datapoints`, 'info');
                addLog('Digital Twin synchronized', 'info');
                addLog(`Generated ${attacks.length} novel attack scenarios`, 'warning');
                addLog(`Identified ${vulns.length} vulnerabilities (${vulns.filter(v => v.severity === 'critical').length} critical)`, 'error');
            }, []);

            const addLog = useCallback((message, type = 'info') => {
                const timestamp = new Date().toLocaleTimeString('en-US', { hour12: false });
                setConsoleLog(prev => [...prev, { timestamp, message, type }]);
            }, []);

            const runAttackSimulation = useCallback((attack) => {
                setSimulationRunning(true);
                setSelectedAttack(attack);
                addLog(`[SIMULATION] Initiating attack: ${attack.name}`, 'warning');
                addLog(`[SIMULATION] Model: ${attack.model}`, 'info');
                addLog(`[SIMULATION] Confidence: ${(attack.confidence * 100).toFixed(1)}%`, 'info');
                
                // Simulate attack progression
                setTimeout(() => {
                    addLog(`[SIMULATION] Injecting attack into Digital Twin`, 'warning');
                    addLog(`[SIMULATION] Affected sensors: ${attack.affectedSensors.join(', ')}`, 'warning');
                }, 1000);

                setTimeout(() => {
                    // Update digital twin state based on attack
                    setDigitalTwinState(prev => {
                        const newState = { ...prev };
                        if (attack.id === 1) {
                            newState.p1_level = 87.4;
                            newState.p1_flow = 52.1;
                        } else if (attack.id === 2) {
                            newState.p3_pressure = 4.8;
                            newState.p3_flow = 68.3;
                        } else if (attack.id === 3) {
                            newState.p2_pH = 9.3;
                            newState.p2_chemical = 'ALARM';
                        } else if (attack.id === 4) {
                            newState.p1_level = 91.2;
                            newState.p3_pressure = 5.1;
                            newState.p4_turbidity = 3.2;
                        }
                        return newState;
                    });
                    
                    addLog(`[SIMULATION] Digital Twin state updated`, 'warning');
                    addLog(`[SIMULATION] Attack impact: ${attack.impact}`, 'error');
                }, 2000);

                setTimeout(() => {
                    addLog(`[DETECTION] Safety threshold violated!`, 'error');
                    addLog(`[DETECTION] Anomaly score: ${(attack.confidence * 1.1).toFixed(2)}`, 'error');
                }, 3000);

                setTimeout(() => {
                    addLog(`[SIMULATION] Simulation complete`, 'success');
                    addLog(`[ANALYSIS] Severity: ${attack.severity.toUpperCase()}`, 'error');
                    addLog(`[ANALYSIS] Exploitability: ${(attack.exploitability * 100).toFixed(0)}%`, 'error');
                    addLog(`[RECOMMENDATION] Review mitigation strategies`, 'info');
                    setSimulationRunning(false);
                }, 4000);
            }, [addLog]);

            const generateNewAttacks = useCallback(() => {
                addLog(`[AI] Training ${generativeModel} model on SWaT dataset...`, 'info');
                addLog(`[AI] Processing 200 datapoints across 6 process stages`, 'info');
                
                setTimeout(() => {
                    addLog(`[AI] Model training complete`, 'success');
                    addLog(`[AI] Generating novel attack patterns...`, 'info');
                }, 1500);

                setTimeout(() => {
                    const newAttacks = generateAttackScenarios();
                    setAttackScenarios(newAttacks);
                    setSystemMetrics(prev => ({
                        ...prev,
                        attacksGenerated: newAttacks.length
                    }));
                    addLog(`[AI] Generated ${newAttacks.length} attack scenarios`, 'success');
                    addLog(`[AI] Confidence range: 73-94%`, 'info');
                }, 3000);
            }, [generativeModel, addLog]);

            // Render different tab content
            const renderOverview = () => (
                <div className="dashboard-grid">
                    {/* Metrics row */}
                    <div className="grid-span-12">
                        <div className="metrics-grid">
                            <div className="metric-card">
                                <div className="metric-label">System Status</div>
                                <div className="metric-value">
                                    <span className="status-dot status-analyzing"></span>
                                    ACTIVE
                                </div>
                                <div className="metric-subtext">All systems operational</div>
                            </div>
                            <div className="metric-card critical">
                                <div className="metric-label">Critical Vulnerabilities</div>
                                <div className="metric-value">{systemMetrics.criticalVulns}</div>
                                <div className="metric-subtext">Immediate attention required</div>
                            </div>
                            <div className="metric-card warning">
                                <div className="metric-label">Total Vulnerabilities</div>
                                <div className="metric-value">{systemMetrics.vulnerabilitiesFound}</div>
                                <div className="metric-subtext">Across all process stages</div>
                            </div>
                            <div className="metric-card">
                                <div className="metric-label">AI-Generated Attacks</div>
                                <div className="metric-value">{systemMetrics.attacksGenerated}</div>
                                <div className="metric-subtext">Novel patterns identified</div>
                            </div>
                            <div className="metric-card success">
                                <div className="metric-label">Digital Twin Sync</div>
                                <div className="metric-value">{systemMetrics.twinSyncStatus.toFixed(1)}%</div>
                                <div className="metric-subtext">Real-time synchronization</div>
                            </div>
                        </div>
                    </div>

                    {/* Process flow */}
                    <div className="grid-span-9">
                        <div className="cyber-panel">
                            <div className="panel-header">
                                <div className="panel-title">Process Flow Diagram</div>
                                <div className="panel-badge">6 STAGES</div>
                            </div>
                            <div className="panel-body">
                                <div className="process-flow">
                                    {[
                                        { name: 'Raw Water', stage: 'P1', vulns: 2 },
                                        { name: 'Chemical', stage: 'P2', vulns: 2 },
                                        { name: 'UF Feed', stage: 'P3', vulns: 2 },
                                        { name: 'RO Feed', stage: 'P4', vulns: 1 },
                                        { name: 'RO', stage: 'P5', vulns: 1 },
                                        { name: 'Product', stage: 'P6', vulns: 0 }
                                    ].map((stage, idx) => {
                                        const isVulnerable = vulnerabilities.some(v => 
                                            v.stage === stage.stage && v.severity === 'critical'
                                        );
                                        return (
                                            <div 
                                                key={idx} 
                                                className={`process-stage ${isVulnerable ? 'vulnerable' : ''}`}
                                            >
                                                <div className="stage-number">{stage.stage}</div>
                                                <div className="stage-name">{stage.name}</div>
                                                <div className="stage-status">
                                                    {stage.vulns > 0 ? `⚠️ ${stage.vulns} vulns` : '✓ Secure'}
                                                </div>
                                            </div>
                                        );
                                    })}
                                </div>
                                <div style={{marginTop: '1.5rem', fontSize: '0.85rem', color: 'rgba(0,255,255,0.6)', textAlign: 'center'}}>
                                    Red borders indicate stages with critical security vulnerabilities
                                </div>
                            </div>
                        </div>
                    </div>

                    {/* Digital Twin State */}
                    <div className="grid-span-3">
                        <div className="cyber-panel">
                            <div className="panel-header">
                                <div className="panel-title">Digital Twin</div>
                                <div className="panel-badge">LIVE</div>
                            </div>
                            <div className="panel-body" style={{fontSize: '0.85rem'}}>
                                {Object.entries(digitalTwinState).map(([key, value]) => {
                                    const isAlert = (typeof value === 'number' && value > 80) || value === 'ALARM';
                                    return (
                                        <div key={key} style={{
                                            marginBottom: '0.75rem',
                                            display: 'flex',
                                            justifyContent: 'space-between',
                                            padding: '0.5rem',
                                            background: isAlert ? 'rgba(255, 23, 68, 0.1)' : 'transparent',
                                            borderLeft: isAlert ? '2px solid var(--danger-red)' : 'none'
                                        }}>
                                            <span style={{opacity: 0.7, fontFamily: 'Share Tech Mono, monospace'}}>
                                                {key.toUpperCase().replace(/_/g, ' ')}:
                                            </span>
                                            <span style={{
                                                fontFamily: 'Audiowide, cursive',
                                                fontWeight: 'bold',
                                                color: isAlert ? 'var(--danger-red)' : 'var(--neon-cyan)'
                                            }}>
                                                {typeof value === 'number' ? value.toFixed(1) : value}
                                            </span>
                                        </div>
                                    );
                                })}
                            </div>
                        </div>
                    </div>

                    {/* Recent Vulnerabilities */}
                    <div className="grid-span-6">
                        <div className="cyber-panel">
                            <div className="panel-header">
                                <div className="panel-title">Top Vulnerabilities</div>
                                <div className="panel-badge">CRITICAL</div>
                            </div>
                            <div className="panel-body">
                                {vulnerabilities.slice(0, 3).map(vuln => (
                                    <div key={vuln.id} className="vulnerability-item" style={{
                                        borderLeftColor: vuln.severity === 'critical' ? 'var(--danger-red)' : 
                                                        vuln.severity === 'high' ? 'var(--warning-amber)' : 
                                                        'var(--electric-blue)',
                                        marginBottom: '1rem'
                                    }}>
                                        <div className="vuln-header">
                                            <div className="vuln-title">[{vuln.stage}] {vuln.title}</div>
                                        </div>
                                        <div className="vuln-description">{vuln.description.slice(0, 150)}...</div>
                                        <div className="vuln-score">
                                            CVSS: {vuln.cvssScore} | Exploitability: {(vuln.exploitability * 100).toFixed(0)}%
                                        </div>
                                    </div>
                                ))}
                            </div>
                        </div>
                    </div>

                    {/* Attack Summary */}
                    <div className="grid-span-6">
                        <div className="cyber-panel">
                            <div className="panel-header">
                                <div className="panel-title">Generated Attacks</div>
                                <div className="panel-badge">AI-POWERED</div>
                            </div>
                            <div className="panel-body">
                                {attackScenarios.slice(0, 3).map(attack => (
                                    <div key={attack.id} className={`attack-card ${attack.severity}`} style={{marginBottom: '1rem'}}>
                                        <div className="attack-header">
                                            <div className="attack-name">{attack.name}</div>
                                        </div>
                                        <div className="attack-description">
                                            {attack.description.slice(0, 120)}...
                                        </div>
                                        <div style={{fontSize: '0.75rem', marginTop: '0.5rem', fontFamily: 'Share Tech Mono, monospace'}}>
                                            <strong>Model:</strong> {attack.type} | <strong>Confidence:</strong> {(attack.confidence * 100).toFixed(0)}%
                                        </div>
                                    </div>
                                ))}
                            </div>
                        </div>
                    </div>
                </div>
            );

            const renderAttackGeneration = () => (
                <div className="dashboard-grid">
                    <div className="grid-span-12">
                        <div className="cyber-panel">
                            <div className="panel-header">
                                <div className="panel-title">Generative AI Attack Modeling</div>
                                <div className="panel-badge">ML-POWERED</div>
                            </div>
                            <div className="panel-body">
                                <div style={{marginBottom: '2rem'}}>
                                    <label style={{fontSize: '0.9rem', display: 'block', marginBottom: '0.75rem', letterSpacing: '1px'}}>
                                        SELECT GENERATIVE MODEL:
                                    </label>
                                    <select 
                                        className="cyber-select"
                                        value={generativeModel}
                                        onChange={(e) => setGenerativeModel(e.target.value)}
                                        style={{maxWidth: '400px'}}
                                    >
                                        <option value="VAE">Variational Autoencoder (VAE)</option>
                                        <option value="TimeGAN">TimeGAN - Temporal Generative Adversarial Network</option>
                                        <option value="Diffusion">Diffusion-based Time Series Generator</option>
                                    </select>
                                    
                                    <button 
                                        className="cyber-button"
                                        onClick={generateNewAttacks}
                                        style={{marginTop: '1rem'}}
                                    >
                                        Generate Novel Attack Patterns
                                    </button>
                                </div>

                                <div>
                                    <h4 style={{marginBottom: '1.5rem', fontSize: '1.1rem', letterSpacing: '2px'}}>
                                        GENERATED ATTACK SCENARIOS ({attackScenarios.length})
                                    </h4>
                                    
                                    <div style={{maxHeight: '700px', overflowY: 'auto'}}>
                                        {attackScenarios.map(attack => (
                                            <div key={attack.id} className={`attack-card ${attack.severity}`}>
                                                <div className="attack-header">
                                                    <div className="attack-name">{attack.name}</div>
                                                    <div className="attack-severity" style={{
                                                        background: attack.severity === 'critical' ? 'var(--danger-red)' : 
                                                                   attack.severity === 'high' ? 'var(--warning-amber)' : 
                                                                   'var(--electric-blue)',
                                                        color: 'var(--void-black)'
                                                    }}>
                                                        {attack.severity.toUpperCase()}
                                                    </div>
                                                </div>
                                                
                                                <div className="attack-description">
                                                    {attack.description}
                                                </div>

                                                <div className="attack-meta">
                                                    <div className="attack-meta-item">
                                                        <strong>Model:</strong> {attack.model}
                                                    </div>
                                                    <div className="attack-meta-item">
                                                        <strong>Confidence:</strong> {(attack.confidence * 100).toFixed(1)}%
                                                    </div>
                                                    <div className="attack-meta-item">
                                                        <strong>Exploitability:</strong> {(attack.exploitability * 100).toFixed(0)}%
                                                    </div>
                                                </div>

                                                <div style={{marginTop: '1rem', paddingTop: '1rem', borderTop: '1px solid rgba(0,255,255,0.2)'}}>
                                                    <div style={{fontSize: '0.85rem', marginBottom: '0.75rem'}}>
                                                        <strong>Affected Sensors:</strong> {attack.affectedSensors.join(', ')}
                                                    </div>
                                                    <div style={{fontSize: '0.85rem', marginBottom: '0.75rem'}}>
                                                        <strong>Technique:</strong> {attack.technique}
                                                    </div>
                                                    <div style={{fontSize: '0.85rem', marginBottom: '1rem', color: 'rgba(255, 23, 68, 0.9)'}}>
                                                        <strong>Impact:</strong> {attack.impact}
                                                    </div>
                                                    
                                                    <button 
                                                        className="cyber-button danger"
                                                        onClick={() => runAttackSimulation(attack)}
                                                        disabled={simulationRunning}
                                                    >
                                                        {simulationRunning && selectedAttack?.id === attack.id ? 
                                                            <span><span className="loading-spinner"></span> Simulating...</span> :
                                                            'Run Attack Simulation'
                                                        }
                                                    </button>
                                                </div>
                                            </div>
                                        ))}
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            );

            const renderVulnerabilities = () => (
                <div className="dashboard-grid">
                    <div className="grid-span-8">
                        <div className="cyber-panel">
                            <div className="panel-header">
                                <div className="panel-title">Vulnerability Analysis</div>
                                <div className="panel-badge">{vulnerabilities.length} FOUND</div>
                            </div>
                            <div className="panel-body">
                                <div className="vulnerability-list">
                                    {vulnerabilities.map(vuln => (
                                        <div key={vuln.id} className="vulnerability-item" style={{
                                            borderLeftColor: vuln.severity === 'critical' ? 'var(--danger-red)' : 
                                                            vuln.severity === 'high' ? 'var(--warning-amber)' : 
                                                            'var(--electric-blue)'
                                        }}>
                                            <div className="vuln-header">
                                                <div className="vuln-title">
                                                    [{vuln.stage}] {vuln.title}
                                                </div>
                                                <div className="vuln-severity-badge" style={{
                                                    background: vuln.severity === 'critical' ? 'var(--danger-red)' : 
                                                               vuln.severity === 'high' ? 'var(--warning-amber)' : 
                                                               'var(--electric-blue)',
                                                    color: 'var(--void-black)'
                                                }}>
                                                    {vuln.severity.toUpperCase()}
                                                </div>
                                            </div>
                                            
                                            <div className="vuln-description">
                                                {vuln.description}
                                            </div>

                                            <div style={{display: 'flex', gap: '2rem', marginTop: '0.75rem', fontSize: '0.8rem', fontFamily: 'Share Tech Mono, monospace'}}>
                                                <div>
                                                    <strong>CVSS Score:</strong> {vuln.cvssScore}/10
                                                </div>
                                                <div>
                                                    <strong>Exploitability:</strong> {(vuln.exploitability * 100).toFixed(0)}%
                                                </div>
                                                <div>
                                                    <strong>Impact:</strong> HIGH
                                                </div>
                                            </div>

                                            <div style={{marginTop: '1rem', fontSize: '0.85rem'}}>
                                                <strong style={{color: 'var(--danger-red)'}}>Affected Systems:</strong>
                                                <div style={{marginTop: '0.5rem', opacity: 0.8}}>
                                                    {vuln.affectedSensors.join(', ')}
                                                </div>
                                            </div>

                                            <div className="vuln-mitigation">
                                                <strong>🛡️ Recommended Mitigation:</strong>
                                                {vuln.mitigation}
                                            </div>

                                            <div style={{
                                                marginTop: '1rem',
                                                padding: '0.75rem',
                                                background: 'rgba(0, 0, 0, 0.5)',
                                                fontFamily: 'Share Tech Mono, monospace',
                                                fontSize: '0.75rem',
                                                borderLeft: '2px solid var(--electric-blue)'
                                            }}>
                                                <strong>Detection Rule:</strong><br/>
                                                <code style={{color: 'var(--neon-cyan)'}}>{vuln.detectionRule}</code>
                                            </div>

                                            <div style={{marginTop: '1rem', display: 'flex', gap: '2rem', fontSize: '0.75rem', opacity: 0.7}}>
                                                <div>
                                                    <strong>Est. Cost:</strong> {vuln.estimatedCost}
                                                </div>
                                                <div>
                                                    <strong>Implementation:</strong> {vuln.implementationTime}
                                                </div>
                                            </div>
                                        </div>
                                    ))}
                                </div>
                            </div>
                        </div>
                    </div>

                    <div className="grid-span-4">
                        <div className="cyber-panel">
                            <div className="panel-header">
                                <div className="panel-title">Severity Distribution</div>
                            </div>
                            <div className="panel-body">
                                <div id="severityChart" className="chart-container"></div>
                            </div>
                        </div>

                        <div className="cyber-panel" style={{marginTop: '1.5rem'}}>
                            <div className="panel-header">
                                <div className="panel-title">Stage Risk Map</div>
                            </div>
                            <div className="panel-body">
                                <div id="stageRiskChart" className="chart-container"></div>
                            </div>
                        </div>

                        <div className="cyber-panel" style={{marginTop: '1.5rem'}}>
                            <div className="panel-header">
                                <div className="panel-title">Exploitability vs Impact</div>
                            </div>
                            <div className="panel-body">
                                <div id="exploitabilityChart" className="chart-container"></div>
                            </div>
                        </div>
                    </div>
                </div>
            );

            const renderMitigation = () => (
                <div className="dashboard-grid">
                    <div className="grid-span-12">
                        <div className="cyber-panel">
                            <div className="panel-header">
                                <div className="panel-title">Cyber Defense Strategies</div>
                                <div className="panel-badge">AI-GENERATED</div>
                            </div>
                            <div className="panel-body">
                                <div style={{display: 'grid', gridTemplateColumns: 'repeat(2, 1fr)', gap: '2rem', marginTop: '1rem'}}>
                                    {/* Preventive Controls */}
                                    <div>
                                        <h3 style={{
                                            marginBottom: '1.5rem',
                                            color: 'var(--success-green)',
                                            fontFamily: 'Audiowide, cursive',
                                            letterSpacing: '2px'
                                        }}>
                                            PREVENTIVE CONTROLS
                                        </h3>
                                        
                                        {defenseStrategies.preventive.map(defense => (
                                            <div key={defense.id} className="defense-card">
                                                <div className="defense-title">{defense.title}</div>
                                                <div className="defense-description">{defense.description}</div>
                                                <div style={{marginTop: '0.75rem', fontSize: '0.75rem'}}>
                                                    <strong>Coverage:</strong> {defense.coverage.join(', ')}
                                                </div>
                                                <div className="defense-type">{defense.priority} PRIORITY</div>
                                            </div>
                                        ))}
                                    </div>

                                    {/* Reactive Controls */}
                                    <div>
                                        <h3 style={{
                                            marginBottom: '1.5rem',
                                            color: 'var(--warning-amber)',
                                            fontFamily: 'Audiowide, cursive',
                                            letterSpacing: '2px'
                                        }}>
                                            REACTIVE CONTROLS
                                        </h3>
                                        
                                        {defenseStrategies.reactive.map(defense => (
                                            <div key={defense.id} className="defense-card">
                                                <div className="defense-title">{defense.title}</div>
                                                <div className="defense-description">{defense.description}</div>
                                                <div style={{marginTop: '0.75rem', fontSize: '0.75rem'}}>
                                                    <strong>Coverage:</strong> {defense.coverage.join(', ')}
                                                </div>
                                                <div className="defense-type" style={{background: 'var(--warning-amber)'}}>
                                                    {defense.priority} PRIORITY
                                                </div>
                                            </div>
                                        ))}
                                    </div>
                                </div>

                                {/* What-If Simulation */}
                                <div style={{marginTop: '3rem', padding: '2rem', background: 'rgba(0, 0, 0, 0.5)', border: '1px solid var(--neon-cyan)'}}>
                                    <h3 style={{
                                        marginBottom: '1.5rem',
                                        fontFamily: 'Audiowide, cursive',
                                        letterSpacing: '2px',
                                        fontSize: '1.2rem'
                                    }}>
                                        WHAT-IF DEFENSE SIMULATION
                                    </h3>
                                    
                                    <p style={{marginBottom: '1.5rem', fontSize: '0.95rem', lineHeight: '1.8'}}>
                                        Test the effectiveness of proposed mitigation strategies by re-running all {attackScenarios.length} generated 
                                        attacks with defenses active. Compare attack success rates, detection times, and system resilience metrics.
                                    </p>

                                    <div style={{display: 'grid', gridTemplateColumns: 'repeat(3, 1fr)', gap: '1rem', marginBottom: '1.5rem'}}>
                                        <div className="metric-card">
                                            <div className="metric-label">Baseline Attack Success</div>
                                            <div className="metric-value" style={{fontSize: '2rem', color: 'var(--danger-red)'}}>78%</div>
                                        </div>
                                        <div className="metric-card success">
                                            <div className="metric-label">With Defenses Active</div>
                                            <div className="metric-value" style={{fontSize: '2rem', color: 'var(--success-green)'}}>23%</div>
                                        </div>
                                        <div className="metric-card success">
                                            <div className="metric-label">Risk Reduction</div>
                                            <div className="metric-value" style={{fontSize: '2rem', color: 'var(--success-green)'}}>71%</div>
                                        </div>
                                    </div>

                                    <button className="cyber-button" onClick={() => {
                                        addLog('[SIMULATION] Starting What-If defense simulation...', 'info');
                                        addLog('[SIMULATION] Testing all defenses against generated attacks', 'info');
                                        setTimeout(() => {
                                            addLog('[SIMULATION] Attack success rate reduced from 78% to 23%', 'success');
                                            addLog('[SIMULATION] Mean detection time: 42 seconds (vs 18 minutes baseline)', 'success');
                                        }, 2000);
                                    }}>
                                        Run Defense Simulation
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            );

            // Update charts when vulnerabilities tab is active
            useEffect(() => {
                if (activeTab === 'vulnerabilities' && vulnerabilities.length > 0) {
                    // Severity Distribution Pie Chart
                    const severityCounts = vulnerabilities.reduce((acc, v) => {
                        acc[v.severity] = (acc[v.severity] || 0) + 1;
                        return acc;
                    }, {});

                    const severityData = [{
                        values: Object.values(severityCounts),
                        labels: Object.keys(severityCounts).map(s => s.toUpperCase()),
                        type: 'pie',
                        marker: {
                            colors: ['#ff1744', '#ffab00', '#00d4ff'],
                            line: { color: '#0a0e27', width: 2 }
                        },
                        textfont: { color: '#00ffff', family: 'Rajdhani' }
                    }];

                    const severityLayout = {
                        paper_bgcolor: 'rgba(0,0,0,0)',
                        plot_bgcolor: 'rgba(0,0,0,0)',
                        font: { color: '#00ffff', family: 'Rajdhani' },
                        showlegend: true,
                        legend: { font: { color: '#00ffff' } },
                        margin: { t: 20, b: 20, l: 20, r: 20 }
                    };

                    Plotly.newPlot('severityChart', severityData, severityLayout, {displayModeBar: false});

                    // Stage Risk Bar Chart
                    const stages = ['P1', 'P2', 'P3', 'P4', 'P5', 'P6'];
                    const stageRisks = stages.map(stage => {
                        const stageVulns = vulnerabilities.filter(v => v.stage === stage);
                        return stageVulns.reduce((sum, v) => sum + v.exploitability * v.cvssScore, 0);
                    });

                    const stageData = [{
                        x: stages,
                        y: stageRisks,
                        type: 'bar',
                        marker: {
                            color: stageRisks,
                            colorscale: [[0, '#00d4ff'], [0.5, '#ffab00'], [1, '#ff1744']],
                            line: { color: '#00ffff', width: 1 }
                        }
                    }];

                    const stageLayout = {
                        paper_bgcolor: 'rgba(0,0,0,0)',
                        plot_bgcolor: 'rgba(0,0,0,0)',
                        font: { color: '#00ffff', family: 'Rajdhani' },
                        xaxis: { 
                            title: 'Process Stage', 
                            gridcolor: 'rgba(0,255,255,0.1)',
                            color: '#00ffff'
                        },
                        yaxis: { 
                            title: 'Risk Score', 
                            gridcolor: 'rgba(0,255,255,0.1)',
                            color: '#00ffff'
                        },
                        margin: { t: 20, b: 50, l: 60, r: 20 }
                    };

                    Plotly.newPlot('stageRiskChart', stageData, stageLayout, {displayModeBar: false});

                    // Exploitability vs Impact Scatter
                    const scatterData = [{
                        x: vulnerabilities.map(v => v.exploitability * 100),
                        y: vulnerabilities.map(v => v.cvssScore),
                        mode: 'markers',
                        type: 'scatter',
                        marker: {
                            size: 12,
                            color: vulnerabilities.map(v => 
                                v.severity === 'critical' ? '#ff1744' : 
                                v.severity === 'high' ? '#ffab00' : '#00d4ff'
                            ),
                            line: { color: '#00ffff', width: 1 }
                        },
                        text: vulnerabilities.map(v => v.title),
                        hovertemplate: '<b>%{text}</b><br>Exploitability: %{x}%<br>CVSS: %{y}<extra></extra>'
                    }];

                    const scatterLayout = {
                        paper_bgcolor: 'rgba(0,0,0,0)',
                        plot_bgcolor: 'rgba(0,0,0,0)',
                        font: { color: '#00ffff', family: 'Rajdhani' },
                        xaxis: { 
                            title: 'Exploitability %', 
                            gridcolor: 'rgba(0,255,255,0.1)',
                            color: '#00ffff',
                            range: [0, 100]
                        },
                        yaxis: { 
                            title: 'CVSS Score', 
                            gridcolor: 'rgba(0,255,255,0.1)',
                            color: '#00ffff',
                            range: [0, 10]
                        },
                        margin: { t: 20, b: 50, l: 60, r: 20 }
                    };

                    Plotly.newPlot('exploitabilityChart', scatterData, scatterLayout, {displayModeBar: false});
                }
            }, [activeTab, vulnerabilities]);

            return (
                <>
                    <div className="app-header">
                        <div className="header-content">
                            <div>
                                <h1 className="app-title">SWaT Guardian Twin</h1>
                                <div className="app-subtitle">
                                    Generative AI + Digital Twin Cybersecurity Intelligence Platform
                                </div>
                            </div>
                            <div className="system-status">
                                <div className="status-item">
                                    <span className="status-dot status-analyzing"></span>
                                    <span>SYSTEM ACTIVE</span>
                                </div>
                                <div className="status-item">
                                    <span>SYNC: {systemMetrics.twinSyncStatus}%</span>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div className="app-container">
                        <div className="nav-tabs">
                            <button 
                                className={`nav-tab ${activeTab === 'overview' ? 'active' : ''}`}
                                onClick={() => setActiveTab('overview')}
                            >
                                Overview
                            </button>
                            <button 
                                className={`nav-tab ${activeTab === 'attacks' ? 'active' : ''}`}
                                onClick={() => setActiveTab('attacks')}
                            >
                                Attack Generation
                            </button>
                            <button 
                                className={`nav-tab ${activeTab === 'vulnerabilities' ? 'active' : ''}`}
                                onClick={() => setActiveTab('vulnerabilities')}
                            >
                                Vulnerabilities
                            </button>
                            <button 
                                className={`nav-tab ${activeTab === 'mitigation' ? 'active' : ''}`}
                                onClick={() => setActiveTab('mitigation')}
                            >
                                Mitigation
                            </button>
                        </div>

                        {activeTab === 'overview' && renderOverview()}
                        {activeTab === 'attacks' && renderAttackGeneration()}
                        {activeTab === 'vulnerabilities' && renderVulnerabilities()}
                        {activeTab === 'mitigation' && renderMitigation()}

                        {/* System Console */}
                        <div className="dashboard-grid" style={{marginTop: '2rem'}}>
                            <div className="grid-span-12">
                                <div className="cyber-panel">
                                    <div className="panel-header">
                                        <div className="panel-title">System Console</div>
                                        <div className="panel-badge">REAL-TIME LOGS</div>
                                    </div>
                                    <div className="panel-body" style={{padding: 0}}>
                                        <div className="console">
                                            {consoleLog.slice(-15).map((log, idx) => (
                                                <div key={idx} className={`console-line ${log.type}`}>
                                                    <span className="console-timestamp">{log.timestamp}</span>
                                                    <span className="console-message">{log.message}</span>
                                                </div>
                                            ))}
                                            {consoleLog.length === 0 && (
                                                <div className="console-line info">
                                                    <span className="console-message">Waiting for system events...</span>
                                                </div>
                                            )}
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </>
            );
        };

        // Render app
        ReactDOM.render(<SWaTGuardianDashboard />, document.getElementById('root'));
    </script>
</body>
</html>


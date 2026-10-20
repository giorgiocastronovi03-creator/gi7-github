<!DOCTYPE html>
<html lang="it" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GI/7 // Cyber Lab & Software Hub</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        cyber: {
                            bg: '#0a0d14',
                            surface: '#121721',
                            card: '#18202e',
                            border: '#232d3f',
                            cyan: '#00f0ff',
                            emerald: '#10b981',
                            orange: '#f59e0b',
                            red: '#ef4444',
                            purple: '#a855f7',
                            muted: '#64748b'
                        }
                    },
                    fontFamily: {
                        mono: ['JetBrains Mono', 'Fira Code', 'monospace'],
                        sans: ['Inter', 'sans-serif']
                    }
                }
            }
        }
    </script>
    
    <!-- Google Fonts & Lucide Icons -->
    <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://unpkg.com/lucide@latest"></script>
    
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0a0d14;
            color: #cbd5e1;
        }
        .font-mono {
            font-family: 'JetBrains Mono', monospace;
        }
        
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0a0d14;
        }
        ::-webkit-scrollbar-thumb {
            background: #232d3f;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #00f0ff;
        }

        .scanlines::before {
            content: " ";
            display: block;
            position: fixed;
            top: 0; left: 0; bottom: 0; right: 0;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.03), rgba(0, 255, 0, 0.01), rgba(0, 0, 255, 0.03));
            z-index: 99;
            background-size: 100% 3px, 6px 100%;
            pointer-events: none;
            opacity: 0.6;
        }

        .glow-cyan {
            box-shadow: 0 0 15px rgba(0, 240, 255, 0.15);
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between selection:bg-cyber-cyan selection:text-black">

    <!-- Top Banner Telemetry Bar -->
    <div class="border-b border-cyber-border bg-cyber-bg/90 backdrop-blur sticky top-0 z-40">
        <div class="max-w-7xl mx-auto px-4 h-12 flex items-center justify-between font-mono text-xs text-cyber-muted">
            <div class="flex items-center gap-4">
                <span class="flex items-center gap-1.5 text-cyber-cyan font-bold tracking-wider">
                    <span class="w-2 h-2 rounded-full bg-cyber-cyan animate-pulse"></span>
                    GI/7 // NODE_01
                </span>
                <span class="hidden md:inline text-cyber-border">|</span>
                <span class="hidden md:inline">SYSTEM: <span class="text-emerald-400">READ-ONLY (STATIC)</span></span>
                <span class="hidden md:inline text-cyber-border">|</span>
                <span class="hidden md:inline">FOCUS: HTB · CISCO · DEV</span>
            </div>
            <div class="flex items-center gap-3">
                <button id="toggle-scanlines" title="Toggle CRT Scanlines" class="px-2 py-1 rounded bg-cyber-surface hover:text-cyber-cyan border border-cyber-border transition flex items-center gap-1">
                    <i data-lucide="tv" class="w-3.5 h-3.5"></i> CRT
                </button>
            </div>
        </div>
    </div>

    <!-- Main Navigation Header -->
    <header class="border-b border-cyber-border bg-cyber-surface/50 backdrop-blur">
        <div class="max-w-7xl mx-auto px-4 py-4 flex flex-col md:flex-row items-center justify-between gap-4">
            
            <!-- Logo Brand -->
            <div class="flex items-center gap-3 cursor-pointer" onclick="switchTab('home')">
                <div class="w-10 h-10 rounded bg-cyber-cyan/10 border border-cyber-cyan/40 flex items-center justify-center text-cyber-cyan font-mono font-bold text-lg glow-cyan">
                    GI
                </div>
                <div>
                    <h1 class="text-xl font-bold font-mono text-white tracking-wide flex items-center gap-2">
                        GI/7 <span class="text-xs px-2 py-0.5 rounded bg-cyber-cyan/10 border border-cyber-cyan/30 text-cyber-cyan font-normal">v3.0-STATIC</span>
                    </h1>
                    <p class="text-xs text-cyber-muted font-mono">HTB Writeups · Cisco Labs · Software Projects</p>
                </div>
            </div>

            <!-- Navigation Tabs -->
            <nav class="flex items-center gap-1 bg-cyber-bg p-1 rounded-lg border border-cyber-border font-mono text-xs md:text-sm">
                <button onclick="switchTab('home')" id="tab-home" class="nav-btn px-4 py-2 rounded-md font-medium transition flex items-center gap-2 text-cyber-cyan bg-cyber-surface border border-cyber-cyan/30">
                    <i data-lucide="terminal" class="w-4 h-4"></i> ~/reports
                </button>
                <button onclick="switchTab('categories')" id="tab-categories" class="nav-btn px-4 py-2 rounded-md font-medium transition flex items-center gap-2 text-cyber-muted hover:text-white">
                    <i data-lucide="folder-tree" class="w-4 h-4"></i> ~/categories
                </button>
                <button onclick="switchTab('timeline')" id="tab-timeline" class="nav-btn px-4 py-2 rounded-md font-medium transition flex items-center gap-2 text-cyber-muted hover:text-white">
                    <i data-lucide="git-commit" class="w-4 h-4"></i> ~/timeline
                </button>
                <button onclick="switchTab('about')" id="tab-about" class="nav-btn px-4 py-2 rounded-md font-medium transition flex items-center gap-2 text-cyber-muted hover:text-white">
                    <i data-lucide="user" class="w-4 h-4"></i> ~/about
                </button>
            </nav>

            <div class="hidden md:flex items-center gap-2 font-mono text-xs text-cyber-muted border border-cyber-border/80 px-3 py-1.5 rounded-lg bg-cyber-bg">
                <i data-lucide="lock" class="w-3.5 h-3.5 text-cyber-cyan"></i> Protected Repo
            </div>
        </div>
    </header>

    <!-- Main Content Area -->
    <main class="max-w-7xl mx-auto px-4 py-8 flex-grow w-full">

        <!-- TAB 1: REPORTS FEED (Home) -->
        <section id="sec-home" class="tab-content space-y-6">
            <div class="bg-cyber-surface border border-cyber-border p-4 rounded-xl flex flex-col md:flex-row gap-4 items-center justify-between">
                <div class="relative w-full md:w-96">
                    <i data-lucide="search" class="w-4 h-4 absolute left-3 top-3 text-cyber-muted"></i>
                    <input type="text" id="search-input" onkeyup="filterReports()" placeholder="Search target IP, box name, Cisco protocol, or project..." 
                           class="w-full bg-cyber-bg border border-cyber-border rounded-lg pl-9 pr-4 py-2 text-xs font-mono text-white placeholder-cyber-muted focus:outline-none focus:border-cyber-cyan">
                </div>

                <div class="flex flex-wrap items-center gap-2 w-full md:w-auto text-xs font-mono">
                    <button onclick="setCategoryFilter('ALL')" class="cat-filter-btn px-3 py-1.5 rounded-lg border border-cyber-cyan/50 bg-cyber-cyan/10 text-cyber-cyan font-bold">ALL</button>
                    <button onclick="setCategoryFilter('HTB Machine')" class="cat-filter-btn px-3 py-1.5 rounded-lg border border-cyber-border bg-cyber-bg text-cyber-muted hover:text-white">HTB MACHINES</button>
                    <button onclick="setCategoryFilter('Cisco Lab')" class="cat-filter-btn px-3 py-1.5 rounded-lg border border-cyber-border bg-cyber-bg text-cyber-muted hover:text-white">CISCO LABS</button>
                    <button onclick="setCategoryFilter('Software Project')" class="cat-filter-btn px-3 py-1.5 rounded-lg border border-cyber-border bg-cyber-bg text-cyber-muted hover:text-white">SOFTWARE PROJECTS</button>
                </div>
            </div>

            <div id="reports-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6"></div>
        </section>

        <!-- TAB 2: CATEGORIES -->
        <section id="sec-categories" class="tab-content hidden space-y-8">
            <div class="border-b border-cyber-border pb-4">
                <h2 class="text-2xl font-bold font-mono text-white flex items-center gap-2">
                    <i data-lucide="folder-tree" class="text-cyber-cyan"></i> ~/categories & taxonomy
                </h2>
                <p class="text-xs text-cyber-muted font-mono mt-1">Organized knowledge base across HTB machines, network topologies, and codebases.</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <div onclick="filterByCategoryPage('HTB Machine')" class="bg-cyber-surface border border-cyber-border p-6 rounded-xl hover:border-cyber-cyan transition cursor-pointer group">
                    <div class="flex items-center justify-between mb-4">
                        <div class="p-3 bg-red-500/10 text-red-400 rounded-lg border border-red-500/20 group-hover:scale-110 transition">
                            <i data-lucide="box" class="w-6 h-6"></i>
                        </div>
                        <span id="cat-count-htb" class="text-xs font-mono px-2 py-1 bg-cyber-bg border border-cyber-border rounded text-cyber-cyan">0 Reports</span>
                    </div>
                    <h3 class="text-lg font-bold font-mono text-white mb-2 group-hover:text-cyber-cyan transition">HTB Machines</h3>
                    <p class="text-xs text-cyber-muted leading-relaxed">Box writeups including initial reconnaissance, entry vectors, privilege escalation, and root flags.</p>
                </div>

                <div onclick="filterByCategoryPage('Cisco Lab')" class="bg-cyber-surface border border-cyber-border p-6 rounded-xl hover:border-cyber-cyan transition cursor-pointer group">
                    <div class="flex items-center justify-between mb-4">
                        <div class="p-3 bg-cyber-cyan/10 text-cyber-cyan rounded-lg border border-cyber-cyan/20 group-hover:scale-110 transition">
                            <i data-lucide="network" class="w-6 h-6"></i>
                        </div>
                        <span id="cat-count-cisco" class="text-xs font-mono px-2 py-1 bg-cyber-bg border border-cyber-border rounded text-cyber-cyan">0 Reports</span>
                    </div>
                    <h3 class="text-lg font-bold font-mono text-white mb-2 group-hover:text-cyber-cyan transition">Cisco Labs</h3>
                    <p class="text-xs text-cyber-muted leading-relaxed">Routing & switching configurations, GNS3/Packet Tracer topologies, OSPF, BGP, VXLAN, and security policies.</p>
                </div>

                <div onclick="filterByCategoryPage('Software Project')" class="bg-cyber-surface border border-cyber-border p-6 rounded-xl hover:border-cyber-cyan transition cursor-pointer group">
                    <div class="flex items-center justify-between mb-4">
                        <div class="p-3 bg-emerald-500/10 text-emerald-400 rounded-lg border border-emerald-500/20 group-hover:scale-110 transition">
                            <i data-lucide="code-2" class="w-6 h-6"></i>
                        </div>
                        <span id="cat-count-software" class="text-xs font-mono px-2 py-1 bg-cyber-bg border border-cyber-border rounded text-cyber-cyan">0 Reports</span>
                    </div>
                    <h3 class="text-lg font-bold font-mono text-white mb-2 group-hover:text-cyber-cyan transition">Software Projects</h3>
                    <p class="text-xs text-cyber-muted leading-relaxed">Custom security tools, Python automation scripts, web apps, and system utility repositories.</p>
                </div>
            </div>

            <div class="bg-cyber-surface border border-cyber-border p-6 rounded-xl">
                <h3 class="text-sm font-bold font-mono text-white mb-4 flex items-center gap-2">
                    <i data-lucide="hash" class="text-cyber-cyan"></i> Active Topic Tags
                </h3>
                <div id="tags-cloud" class="flex flex-wrap gap-2 text-xs font-mono"></div>
            </div>
        </section>

        <!-- TAB 3: TIMELINE / LAB LOG -->
        <section id="sec-timeline" class="tab-content hidden space-y-8">
            <div class="border-b border-cyber-border pb-4">
                <h2 class="text-2xl font-bold font-mono text-white flex items-center gap-2">
                    <i data-lucide="git-commit" class="text-cyber-cyan"></i> ~/timeline & lab log
                </h2>
                <p class="text-xs text-cyber-muted font-mono mt-1">Chronological history of certifications, machine roots, and project releases.</p>
            </div>

            <div id="timeline-container" class="relative border-l-2 border-cyber-border ml-4 md:ml-8 space-y-8 py-2"></div>
        </section>

        <!-- TAB 4: ABOUT ME -->
        <section id="sec-about" class="tab-content hidden space-y-8">
            <div class="border-b border-cyber-border pb-4">
                <h2 class="text-2xl font-bold font-mono text-white flex items-center gap-2">
                    <i data-lucide="user" class="text-cyber-cyan"></i> ~/about operator
                </h2>
                <p class="text-xs text-cyber-muted font-mono mt-1">Profile, credentials, lab architecture, and research focus.</p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                <div class="lg:col-span-2 space-y-6">
                    <div class="bg-cyber-surface border border-cyber-border p-6 rounded-xl space-y-4">
                        <div class="flex items-center gap-4">
                            <div class="w-16 h-16 rounded-xl bg-cyber-cyan/10 border border-cyber-cyan/30 flex items-center justify-center font-mono text-2xl font-bold text-cyber-cyan glow-cyan">
                                GI
                            </div>
                            <div>
                                <h3 class="text-xl font-bold text-white font-mono">GI/7 Security & Network Engineer</h3>
                                <p class="text-xs text-cyber-cyan font-mono mt-0.5">Focus: Offensive Security · Cisco Enterprise Routing/Switching · Software Dev</p>
                            </div>
                        </div>
                        <p class="text-sm text-cyber-muted leading-relaxed font-sans">
                            Benvenuto nella mia piattaforma personale di reportistica. Questo hub documenta le mie analisi dettagliate sulle macchine Hack The Box, la progettazione di topologie di rete Cisco avanzate e il codice sorgente dei miei progetti software.
                        </p>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <div class="bg-cyber-surface border border-cyber-border p-4 rounded-xl space-y-2">
                            <div class="text-xs font-mono text-cyber-cyan flex items-center gap-1.5 font-bold">
                                <i data-lucide="terminal" class="w-4 h-4"></i> HTB / Pentesting
                            </div>
                            <ul class="text-xs text-cyber-muted space-y-1 font-mono">
                                <li>• Active Directory Exploitation</li>
                                <li>• Linux & Windows PrivEsc</li>
                                <li>• Web App Pentesting</li>
                                <li>• Reverse Shells & Payloads</li>
                            </ul>
                        </div>

                        <div class="bg-cyber-surface border border-cyber-border p-4 rounded-xl space-y-2">
                            <div class="text-xs font-mono text-cyber-cyan flex items-center gap-1.5 font-bold">
                                <i data-lucide="network" class="w-4 h-4"></i> Cisco Networking
                            </div>
                            <ul class="text-xs text-cyber-muted space-y-1 font-mono">
                                <li>• OSPF / BGP Routing</li>
                                <li>• VLANs & Trunking</li>
                                <li>• IPsec VPNs & Hardening</li>
                                <li>• GNS3 / Packet Tracer</li>
                            </ul>
                        </div>

                        <div class="bg-cyber-surface border border-cyber-border p-4 rounded-xl space-y-2">
                            <div class="text-xs font-mono text-cyber-cyan flex items-center gap-1.5 font-bold">
                                <i data-lucide="code" class="w-4 h-4"></i> Development
                            </div>
                            <ul class="text-xs text-cyber-muted space-y-1 font-mono">
                                <li>• Python Security Tooling</li>
                                <li>• Bash Scripting</li>
                                <li>• C / C++ Basics</li>
                                <li>• Web Applications</li>
                            </ul>
                        </div>
                    </div>
                </div>

                <div class="space-y-6">
                    <div class="bg-cyber-surface border border-cyber-border p-6 rounded-xl space-y-4">
                        <h4 class="text-xs font-bold font-mono text-white tracking-wider uppercase border-b border-cyber-border pb-2">
                            Pwn & Lab Telemetry
                        </h4>
                        <div class="space-y-3 font-mono text-xs">
                            <div class="flex justify-between items-center">
                                <span class="text-cyber-muted">HTB Rooted Machines</span>
                                <span id="stat-htb-count" class="text-cyber-cyan font-bold">0</span>
                            </div>
                            <div class="flex justify-between items-center">
                                <span class="text-cyber-muted">Cisco Topologies</span>
                                <span id="stat-cisco-count" class="text-cyber-emerald font-bold">0</span>
                            </div>
                            <div class="flex justify-between items-center">
                                <span class="text-cyber-muted">Software Repos</span>
                                <span id="stat-software-count" class="text-cyber-orange font-bold">0</span>
                            </div>
                        </div>
                    </div>

                    <div class="bg-cyber-surface border border-cyber-border p-6 rounded-xl space-y-3 font-mono text-xs">
                        <h4 class="text-xs font-bold text-white tracking-wider uppercase border-b border-cyber-border pb-2">
                            Connect Node
                        </h4>
                        <a href="https://hackthebox.com" target="_blank" class="flex items-center justify-between text-cyber-muted hover:text-cyber-cyan transition py-1">
                            <span>Hack The Box Profile</span>
                            <i data-lucide="external-link" class="w-3.5 h-3.5"></i>
                        </a>
                        <a href="https://github.com" target="_blank" class="flex items-center justify-between text-cyber-muted hover:text-cyber-cyan transition py-1">
                            <span>GitHub Repositories</span>
                            <i data-lucide="external-link" class="w-3.5 h-3.5"></i>
                        </a>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="border-t border-cyber-border bg-cyber-surface/30 mt-12 py-6">
        <div class="max-w-7xl mx-auto px-4 flex flex-col md:flex-row items-center justify-between gap-4 font-mono text-xs text-cyber-muted">
            <div>
                © <span id="year">2026</span> <span class="text-cyber-cyan font-bold">GI/7</span> — HTB · Cisco Labs · Software Hub
            </div>
            <div class="flex items-center gap-4">
                <span>Immutable Static Site</span>
                <span>•</span>
                <span class="text-emerald-400">Git Protected</span>
            </div>
        </div>
    </footer>

    <!-- READER MODAL -->
    <div id="modal-reader" class="fixed inset-0 bg-black/85 backdrop-blur-md z-50 hidden flex items-center justify-center p-4 overflow-y-auto">
        <div class="bg-cyber-surface border border-cyber-cyan/40 rounded-xl w-full max-w-4xl p-6 md:p-8 space-y-6 glow-cyan max-h-[90vh] overflow-y-auto relative">
            <button onclick="closeReaderModal()" class="absolute top-6 right-6 text-cyber-muted hover:text-white font-mono text-2xl">&times;</button>
            <div id="reader-header" class="space-y-2 border-b border-cyber-border pb-4"></div>
            <div id="reader-body" class="space-y-6 font-mono text-xs md:text-sm text-slate-300 leading-relaxed"></div>
            <div class="border-t border-cyber-border pt-4 flex items-center justify-between">
                <button id="reader-export-md" class="px-3 py-1.5 rounded bg-cyber-bg border border-cyber-border text-cyber-cyan hover:border-cyber-cyan font-mono text-xs flex items-center gap-1.5">
                    <i data-lucide="file-text" class="w-3.5 h-3.5"></i> Export Markdown
                </button>
                <button onclick="closeReaderModal()" class="px-3 py-1.5 rounded bg-cyber-bg border border-cyber-border text-cyber-muted hover:text-white font-mono text-xs">
                    Close
                </button>
            </div>
        </div>
    </div>

    <!-- DATA MATRIX & LOGIC -->
    <script>
        /*
         * DATA MATRIX: Inserisci qui i tuoi report ed eventi timeline.
         */
        const REPORTS_DATA = [
            {
                id: 'rep_htb_01',
                pillar: 'HTB Machine',
                title: 'Lame',
                date: '2026-10-21',
                summary: 'Writeup iniziale per la macchina Lame su Hack The Box.',
                content: `1. Nmap Scan\n# nmap -sC -sV -oA nmap/lame 10.10.10.3\n\n2. Vulnerability Exploitation\n- Samba 3.0.20 usermap script exploit (CVE-2007-2447)\n- Privilege Escalation: Root immediato tramite exploit Samba.`,
                tags: ['smb', 'samba', 'privesc', 'linux'],
                htbOs: 'Linux',
                htbDiff: 'Easy',
                htbIp: '10.10.10.3',
                htbStatus: 'USER & ROOT'
            }
        ];

        const TIMELINE_DATA = [
            {
                id: 'tl_01',
                date: 'Ottobre 2026',
                title: 'Inizializzazione Blog GI/7',
                desc: 'Deploy della piattaforma static-only su GitHub Pages con architettura Git-only.'
            }
        ];

        let currentFilterCategory = 'ALL';
        let activeReadingReportId = null;

        document.addEventListener('DOMContentLoaded', () => {
            renderReports();
            renderTimeline();
            updateStats();
            lucide.createIcons();
            document.getElementById('year').innerText = new Date().getFullYear();

            document.getElementById('toggle-scanlines').addEventListener('click', () => {
                document.body.classList.toggle('scanlines');
            });
        });

        function switchTab(tabName) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('text-cyber-cyan', 'bg-cyber-surface', 'border', 'border-cyber-cyan/30');
                btn.classList.add('text-cyber-muted');
            });

            document.getElementById(`sec-${tabName}`).classList.remove('hidden');
            const activeNav = document.getElementById(`tab-${tabName}`);
            activeNav.classList.add('text-cyber-cyan', 'bg-cyber-surface', 'border', 'border-cyber-cyan/30');
            activeNav.classList.remove('text-cyber-muted');
            
            if (tabName === 'categories') renderCategoriesView();
        }

        function setCategoryFilter(category) {
            currentFilterCategory = category;
            document.querySelectorAll('.cat-filter-btn').forEach(btn => {
                if(btn.innerText === category || (category === 'HTB Machine' && btn.innerText.includes('HTB')) || (category === 'Cisco Lab' && btn.innerText.includes('CISCO')) || (category === 'Software Project' && btn.innerText.includes('SOFTWARE'))) {
                    btn.className = "cat-filter-btn px-3 py-1.5 rounded-lg border border-cyber-cyan/50 bg-cyber-cyan/10 text-cyber-cyan font-bold";
                } else {
                    btn.className = "cat-filter-btn px-3 py-1.5 rounded-lg border border-cyber-border bg-cyber-bg text-cyber-muted hover:text-white";
                }
            });
            renderReports();
        }

        function filterReports() {
            renderReports();
        }

        function renderReports() {
            const grid = document.getElementById('reports-grid');
            const searchVal = document.getElementById('search-input').value.toLowerCase();

            let filtered = REPORTS_DATA.filter(r => {
                const matchesCategory = (currentFilterCategory === 'ALL') || (r.pillar === currentFilterCategory);
                const matchesSearch = r.title.toLowerCase().includes(searchVal) || 
                                      r.summary.toLowerCase().includes(searchVal) ||
                                      (r.tags && r.tags.some(t => t.toLowerCase().includes(searchVal))) ||
                                      (r.htbIp && r.htbIp.includes(searchVal));
                return matchesCategory && matchesSearch;
            });

            if (filtered.length === 0) {
                grid.innerHTML = `
                    <div class="col-span-full border border-dashed border-cyber-border rounded-xl p-12 text-center space-y-4">
                        <div class="w-12 h-12 rounded-full bg-cyber-surface border border-cyber-border text-cyber-muted flex items-center justify-center mx-auto font-mono text-xl">!</div>
                        <h3 class="text-base font-bold font-mono text-white">Nessun Report Trovato</h3>
                        <p class="text-xs text-cyber-muted max-w-md mx-auto font-mono">
                            Modifica l'array <code>REPORTS_DATA</code> dentro <code>index.html</code> per aggiungere report.
                        </p>
                    </div>
                `;
                return;
            }

            grid.innerHTML = filtered.map(r => {
                let badgeColor = "bg-cyber-cyan/10 border-cyber-cyan/30 text-cyber-cyan";
                let iconName = "file-text";

                if (r.pillar === 'HTB Machine') {
                    badgeColor = "bg-red-500/10 border-red-500/30 text-red-400";
                    iconName = "box";
                } else if (r.pillar === 'Cisco Lab') {
                    badgeColor = "bg-cyber-cyan/10 border-cyber-cyan/30 text-cyber-cyan";
                    iconName = "network";
                } else if (r.pillar === 'Software Project') {
                    badgeColor = "bg-emerald-500/10 border-emerald-500/30 text-emerald-400";
                    iconName = "code-2";
                }

                return `
                    <div onclick="openReaderModal('${r.id}')" class="bg-cyber-surface border border-cyber-border rounded-xl p-5 hover:border-cyber-cyan transition cursor-pointer flex flex-col justify-between group">
                        <div class="space-y-3">
                            <div class="flex items-center justify-between text-xs font-mono">
                                <span class="px-2 py-0.5 rounded border ${badgeColor} flex items-center gap-1">
                                    <i data-lucide="${iconName}" class="w-3 h-3"></i> ${r.pillar}
                                </span>
                                <span class="text-cyber-muted">${r.date}</span>
                            </div>

                            <h3 class="text-base font-bold font-mono text-white group-hover:text-cyber-cyan transition">${r.title}</h3>

                            ${r.pillar === 'HTB Machine' ? `
                                <div class="flex items-center gap-2 font-mono text-xs text-cyber-muted bg-cyber-bg p-2 rounded border border-cyber-border/50">
                                    <span>OS: <strong class="text-white">${r.htbOs}</strong></span>
                                    <span>•</span>
                                    <span>Diff: <strong class="text-cyber-orange">${r.htbDiff}</strong></span>
                                    <span>•</span>
                                    <span>IP: <strong class="text-cyber-cyan">${r.htbIp || 'N/A'}</strong></span>
                                </div>
                            ` : ''}

                            <p class="text-xs text-cyber-muted line-clamp-2 leading-relaxed">${r.summary}</p>
                        </div>

                        <div class="mt-4 pt-3 border-t border-cyber-border/50 flex items-center justify-between">
                            <div class="flex flex-wrap gap-1">
                                ${(r.tags || []).slice(0, 3).map(t => `<span class="text-[10px] font-mono px-1.5 py-0.5 bg-cyber-bg rounded text-cyber-muted">#${t}</span>`).join('')}
                            </div>
                            <span class="text-xs font-mono text-cyber-cyan group-hover:translate-x-1 transition flex items-center gap-1">
                                Read <i data-lucide="arrow-right" class="w-3 h-3"></i>
                            </span>
                        </div>
                    </div>
                `;
            }).join('');

            lucide.createIcons();
        }

        function openReaderModal(id) {
            const report = REPORTS_DATA.find(r => r.id === id);
            if (!report) return;

            activeReadingReportId = id;
            const header = document.getElementById('reader-header');
            const body = document.getElementById('reader-body');

            header.innerHTML = `
                <div class="flex items-center gap-2 text-xs font-mono text-cyber-cyan mb-1">
                    <span class="px-2 py-0.5 bg-cyber-cyan/10 border border-cyber-cyan/30 rounded">${report.pillar}</span>
                    <span>• ${report.date}</span>
                </div>
                <h2 class="text-2xl font-bold font-mono text-white">${report.title}</h2>
                <p class="text-xs text-cyber-muted font-mono">${report.summary}</p>
            `;

            let metaBlock = '';
            if (report.pillar === 'HTB Machine') {
                metaBlock = `
                    <div class="grid grid-cols-2 md:grid-cols-4 gap-3 bg-cyber-bg p-4 rounded-lg border border-cyber-border font-mono text-xs">
                        <div><span class="text-cyber-muted block">OS:</span><strong class="text-white">${report.htbOs}</strong></div>
                        <div><span class="text-cyber-muted block">DIFFICULTY:</span><strong class="text-cyber-orange">${report.htbDiff}</strong></div>
                        <div><span class="text-cyber-muted block">TARGET IP:</span><strong class="text-cyber-cyan">${report.htbIp || 'N/A'}</strong></div>
                        <div><span class="text-cyber-muted block">PWN STATUS:</span><strong class="text-emerald-400">${report.htbStatus}</strong></div>
                    </div>
                `;
            }

            body.innerHTML = `
                ${metaBlock}
                <div class="bg-cyber-bg p-4 rounded-lg border border-cyber-border whitespace-pre-wrap font-mono text-xs md:text-sm text-slate-200">
${escapeHTML(report.content)}
                </div>
            `;

            document.getElementById('reader-export-md').onclick = () => exportReportMarkdown(report);
            document.getElementById('modal-reader').classList.remove('hidden');
            lucide.createIcons();
        }

        function closeReaderModal() {
            document.getElementById('modal-reader').classList.add('hidden');
            activeReadingReportId = null;
        }

        function renderTimeline() {
            const container = document.getElementById('timeline-container');
            if (TIMELINE_DATA.length === 0) {
                container.innerHTML = `<div class="text-xs font-mono text-cyber-muted pl-4">Nessun evento registrato nella timeline.</div>`;
                return;
            }

            container.innerHTML = TIMELINE_DATA.map(e => `
                <div class="relative pl-6 group">
                    <div class="absolute -left-[9px] top-1 w-4 h-4 rounded-full bg-cyber-bg border-2 border-cyber-cyan group-hover:bg-cyber-cyan transition"></div>
                    <div class="bg-cyber-surface border border-cyber-border p-4 rounded-xl space-y-1">
                        <span class="text-xs font-mono text-cyber-cyan font-bold">${e.date}</span>
                        <h4 class="text-sm font-bold font-mono text-white">${e.title}</h4>
                        <p class="text-xs text-cyber-muted font-mono">${e.desc}</p>
                    </div>
                </div>
            `).join('');
        }

        function renderCategoriesView() {
            const htbCount = REPORTS_DATA.filter(r => r.pillar === 'HTB Machine').length;
            const ciscoCount = REPORTS_DATA.filter(r => r.pillar === 'Cisco Lab').length;
            const swCount = REPORTS_DATA.filter(r => r.pillar === 'Software Project').length;

            document.getElementById('cat-count-htb').innerText = `${htbCount} Reports`;
            document.getElementById('cat-count-cisco').innerText = `${ciscoCount} Reports`;
            document.getElementById('cat-count-software').innerText = `${swCount} Reports`;

            const allTags = new Set();
            REPORTS_DATA.forEach(r => (r.tags || []).forEach(t => allTags.add(t)));
            
            const cloud = document.getElementById('tags-cloud');
            if(allTags.size === 0) {
                cloud.innerHTML = `<span class="text-cyber-muted">Nessun tag presente nei report.</span>`;
            } else {
                cloud.innerHTML = Array.from(allTags).map(tag => `
                    <button onclick="filterByTag('${tag}')" class="px-2.5 py-1 bg-cyber-bg border border-cyber-border rounded hover:border-cyber-cyan text-cyber-cyan transition">
                        #${tag}
                    </button>
                `).join('');
            }
        }

        function filterByCategoryPage(cat) {
            switchTab('home');
            setCategoryFilter(cat);
        }

        function filterByTag(tag) {
            switchTab('home');
            document.getElementById('search-input').value = tag;
            filterReports();
        }

        function updateStats() {
            document.getElementById('stat-htb-count').innerText = REPORTS_DATA.filter(r => r.pillar === 'HTB Machine').length;
            document.getElementById('stat-cisco-count').innerText = REPORTS_DATA.filter(r => r.pillar === 'Cisco Lab').length;
            document.getElementById('stat-software-count').innerText = REPORTS_DATA.filter(r => r.pillar === 'Software Project').length;
        }

        function exportReportMarkdown(report) {
            const md = `# ${report.title}\nDate: ${report.date}\nPillar: ${report.pillar}\nSummary: ${report.summary}\n\n## Writeup / Content\n\`\`\`\n${report.content}\n\`\`\`\n`;
            const blob = new Blob([md], { type: 'text/markdown' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `${report.title.toLowerCase().replace(/\s+/g, '_')}_report.md`;
            a.click();
        }

        function escapeHTML(str) {
            return str.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
        }
    </script>
</body>
</html>
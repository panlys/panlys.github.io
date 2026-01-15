<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Vortex Biotech | Device Health</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0a0a0a;
            color: white;
            overflow: hidden;
        }

        .triangle-container {
            filter: drop-shadow(0 0 20px rgba(16, 185, 129, 0.2));
            transition: all 0.5s ease-in-out;
        }

        .glow-active { filter: drop-shadow(0 0 30px rgba(16, 185, 129, 0.6)); }
        .glow-service { filter: drop-shadow(0 0 30px rgba(245, 158, 11, 0.6)); }
        .glow-offline { filter: drop-shadow(0 0 30px rgba(239, 68, 68, 0.6)); }

        /* Toblerone Shape Simulation */
        .toblerone {
            width: 0;
            height: 0;
            border-left: 100px solid transparent;
            border-right: 100px solid transparent;
            border-bottom: 173px solid currentColor;
            transition: border-bottom-color 0.5s ease;
        }
    </style>
</head>
<body class="flex flex-col items-center justify-between min-h-screen p-8">

    <div class="w-full flex justify-between items-start pt-4">
        <div>
            <h1 class="text-xl font-bold tracking-tighter italic">VORTEX</h1>
            <p class="text-[10px] uppercase tracking-[0.2em] text-gray-500">Biotech Systems</p>
        </div>
        <div class="text-right">
            <p id="location-name" class="text-sm font-medium">Executive Office</p>
            <p id="last-update" class="text-[10px] text-gray-500 italic">Syncing...</p>
        </div>
    </div>

    <div class="flex flex-col items-center justify-center flex-1 w-full">
        <div id="status-glow" class="triangle-container mb-8 transition-all duration-1000">
            <div id="main-triangle" class="toblerone text-emerald-500"></div>
        </div>
        
        <div class="text-center">
            <h2 id="status-text" class="text-4xl font-light tracking-widest uppercase mb-2 text-emerald-500">Active</h2>
            <div class="flex items-center justify-center gap-2">
                <span class="relative flex h-2 w-2">
                    <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-75"></span>
                    <span id="status-dot" class="relative inline-flex rounded-full h-2 w-2 bg-emerald-500"></span>
                </span>
                <p id="sub-status" class="text-xs text-gray-400 font-medium tracking-wide">AIR PURIFICATION OPTIMIZED</p>
            </div>
        </div>
    </div>

    <div class="grid grid-cols-2 gap-4 w-full max-w-sm mb-12">
        <div class="bg-white/5 border border-white/10 p-4 rounded-2xl">
            <p class="text-[10px] text-gray-500 uppercase mb-1">LED Intensity</p>
            <p class="text-lg font-semibold" id="val-intensity">98.2%</p>
        </div>
        <div class="bg-white/5 border border-white/10 p-4 rounded-2xl">
            <p class="text-[10px] text-gray-500 uppercase mb-1">Fan Speed</p>
            <p class="text-lg font-semibold" id="val-fan">2400 RPM</p>
        </div>
        <div class="bg-white/5 border border-white/10 p-4 rounded-2xl">
            <p class="text-[10px] text-gray-500 uppercase mb-1">Uptime</p>
            <p class="text-lg font-semibold" id="val-uptime">1,240h</p>
        </div>
        <div class="bg-white/5 border border-white/10 p-4 rounded-2xl">
            <p class="text-[10px] text-gray-500 uppercase mb-1">Efficiency</p>
            <p class="text-lg font-semibold" id="val-efficiency">High</p>
        </div>
    </div>

    <div class="fixed bottom-4 left-4 right-4 bg-white/5 p-2 rounded-full flex justify-around text-[10px] uppercase font-bold tracking-tighter border border-white/10 backdrop-blur-md">
        <button onclick="setStatus('healthy')" class="px-4 py-2 rounded-full text-emerald-500">Healthy</button>
        <button onclick="setStatus('service')" class="px-4 py-2 rounded-full text-amber-500">Service</button>
        <button onclick="setStatus('offline')" class="px-4 py-2 rounded-full text-red-500">Offline</button>
    </div>

    <script>
        // Initialize Lucide icons
        lucide.createIcons();

        function setStatus(state) {
            const triangle = document.getElementById('main-triangle');
            const glow = document.getElementById('status-glow');
            const text = document.getElementById('status-text');
            const sub = document.getElementById('sub-status');
            const dot = document.getElementById('status-dot');

            // Reset classes
            glow.className = "triangle-container mb-8 transition-all duration-1000";
            
            if (state === 'healthy') {
                triangle.style.borderBottomColor = '#10b981';
                glow.classList.add('glow-active');
                text.innerText = "Active";
                text.className = "text-4xl font-light tracking-widest uppercase mb-2 text-emerald-500";
                sub.innerText = "AIR PURIFICATION OPTIMIZED";
                dot.className = "relative inline-flex rounded-full h-2 w-2 bg-emerald-500";
            } else if (state === 'service') {
                triangle.style.borderBottomColor = '#f59e0b';
                glow.classList.add('glow-service');
                text.innerText = "Service";
                text.className = "text-4xl font-light tracking-widest uppercase mb-2 text-amber-500";
                sub.innerText = "MAINTENANCE RECOMMENDED";
                dot.className = "relative inline-flex rounded-full h-2 w-2 bg-amber-500";
            } else {
                triangle.style.borderBottomColor = '#ef4444';
                glow.classList.add('glow-offline');
                text.innerText = "Offline";
                text.className = "text-4xl font-light tracking-widest uppercase mb-2 text-red-500";
                sub.innerText = "SYSTEM HARDWARE ERROR";
                dot.className = "relative inline-flex rounded-full h-2 w-2 bg-red-500";
            }
        }

        // Simulating the 10s Update
        function updateTime() {
            const now = new Date();
            document.getElementById('last-update').innerText = "Last Sync: " + now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit', second: '2-digit' });
        }

        setInterval(updateTime, 10000);
        updateTime();
        setStatus('healthy');
    </script>
</body>
</html>

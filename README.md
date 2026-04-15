# FIGIT-TOY-APP
A little coded fidget toy application:

```html
<!DOCTYPE html>
<html class="light" lang="en">
<head>
    <meta charset="utf-8"/>
    <meta content="width=device-width, initial-scale=1.0" name="viewport"/>
    <title>RBAG_FIDGET_GAMES_AUDIO</title>
    <link href="https://fonts.googleapis.com/css2?family=Newsreader:ital,wght@0,400;0,700;1,400;1,700&family=Space+Grotesk:wght@300;400;700&display=swap" rel="stylesheet"/>
    <link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:wght@100..700,0..1&display=swap" rel="stylesheet"/>
    <script src="https://cdn.tailwindcss.com?plugins=forms,container-queries"></script>
    <script id="tailwind-config">
        tailwind.config = {
            darkMode: "class",
            theme: {
                extend: {
                    colors: {
                        "primary-fixed": "#00fc40",
                        "secondary": "#a400a4",
                        "tertiary-fixed": "#00e3fd",
                        "surface": "#f6f6f6",
                        "on-surface": "#2d2f2f",
                        "surface-container": "#e7e8e8",
                        "surface-container-low": "#f0f1f1",
                        "primary": "#006b15",
                        "on-primary": "#d1ffc6",
                    },
                    fontFamily: {
                        "headline": ["Newsreader", "serif"],
                        "body": ["Space Grotesk", "sans-serif"],
                        "label": ["Space Grotesk", "monospace"]
                    },
                    borderRadius: {"DEFAULT": "0px"},
                },
            },
        }
    </script>
    <style>
        .material-symbols-outlined {
            font-variation-settings: 'FILL' 0, 'wght' 400, 'GRAD' 0, 'opsz' 24;
        }
        body { min-height: 100vh; }
        #dodge-square { transition: background-color 0.1s; }
        .glitch-text { text-shadow: 2px 2px #ff00ff, -2px -2px #00e3fd; }
    </style>
</head>
<body class="bg-surface text-on-surface font-body selection:bg-primary-fixed selection:text-black">
    <header class="fixed top-0 left-0 w-full z-50 flex items-center justify-between px-4 h-16 bg-[#f6f6f6] border-b-4 border-black shadow-[4px_4px_0px_0px_rgba(0,0,0,1)]">
        <div class="flex items-center gap-2">
            <span class="material-symbols-outlined text-[#00FF41]">toys</span>
            <h1 class="font-headline text-3xl italic font-black tracking-tighter text-[#00FF41]">RBAG_FIDGET_BOX</h1>
        </div>
        <nav class="hidden md:flex gap-6 font-label text-xs uppercase tracking-widest">
            <button onclick="beep(440, 'square', 0.1)" class="text-[#ff00ff] underline decoration-4 hover:bg-[#00FF41] hover:text-black px-1">GAMES</button>
            <button onclick="beep(220, 'sawtooth', 0.1)" class="text-black hover:bg-[#00FF41] hover:text-black px-1">TRASH</button>
            <button onclick="beep(880, 'sine', 0.1)" class="text-black hover:bg-[#00FF41] hover:text-black px-1">HELP?</button>
        </nav>
        <span class="material-symbols-outlined text-[#00FF41]">extension</span>
    </header>

    <main class="pt-24 pb-32 px-6 max-w-7xl mx-auto">
        <div class="mb-12 border-4 border-black p-6 bg-surface-container shadow-[8px_8px_0px_0px_rgba(0,0,0,1)] relative overflow-hidden">
            <div class="absolute top-0 right-0 p-2 bg-black text-white font-label text-[10px] uppercase">v0.99.2-audio-patch</div>
            <h2 class="font-headline text-5xl italic font-bold mb-4 leading-tight glitch-text">SONIC_ANARCHY.exe</h2>
            <p class="font-label text-sm uppercase max-w-xl border-l-4 border-primary p-2 bg-surface-container-lowest">Audio Engine: INITIALIZED. Click to interact. Wear headphones for maximum irritation.</p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-12 gap-6 items-start">
            <!-- Game 1: Click the Pixel -->
            <div class="md:col-span-7 border-4 border-black bg-white shadow-[12px_12px_0px_0px_#00fc40] flex flex-col">
                <div class="bg-black text-white p-2 font-label text-xs flex justify-between items-center">
                    <span>CLICK_THE_PIXEL.APP</span>
                    <div class="flex gap-1">
                        <div class="w-3 h-3 bg-gray-500 border border-white"></div>
                        <div class="w-3 h-3 bg-red-600 border border-white"></div>
                    </div>
                </div>
                <div class="p-6 bg-gradient-to-br from-primary-fixed to-secondary text-white min-h-[400px] flex flex-col justify-center items-center relative group overflow-hidden" id="pixel-game-container">
                    <div class="absolute w-6 h-6 bg-white cursor-pointer hidden z-20 border-2 border-black" id="target-pixel"></div>
                    <div class="text-center pointer-events-none" id="pixel-game-message">
                        <p class="font-headline text-4xl italic font-bold drop-shadow-md">SOUND_CHECK</p>
                        <p class="font-label text-xs mt-2 uppercase tracking-tighter opacity-80">Now with 100% more synthesized beeps.</p>
                    </div>
                </div>
                <div class="p-4 border-t-4 border-black flex justify-between items-center bg-surface-container-low">
                    <span class="font-label font-bold text-lg">SCORE: <span id="pixel-score">0000</span></span>
                    <button class="bg-primary text-on-primary px-6 py-2 border-2 border-black font-label uppercase font-bold shadow-[4px_4px_0px_0px_rgba(0,0,0,1)] active:translate-x-1 active:translate-y-1 active:shadow-none" id="pixel-start-btn">START_EXE</button>
                </div>
            </div>

            <!-- Game 2: Avoid the Square -->
            <div class="md:col-span-5 border-4 border-black bg-[#ff00ff] shadow-[8px_8px_0px_0px_#000000] rotate-1">
                <div class="bg-white border-b-4 border-black p-2 font-label text-xs font-bold uppercase">Avoid_The_Square.sys</div>
                <div class="aspect-square bg-black p-8 flex items-center justify-center relative overflow-hidden" id="dodge-container">
                    <div class="w-16 h-16 bg-[#00FF41] border-4 border-white absolute cursor-crosshair z-10" id="dodge-square" style="left: 50%; top: 50%; transform: translate(-50%, -50%);"></div>
                    <div class="absolute inset-0 bg-red-600/90 hidden items-center justify-center z-20" id="dodge-overlay">
                        <div class="text-white text-center">
                            <h4 class="font-headline text-5xl font-black italic">GAME OVER</h4>
                            <button class="mt-4 bg-white text-black px-4 py-2 font-label text-xs uppercase font-bold border-2 border-black" onclick="resetDodge()">REBOOT_SYSTEM</button>
                        </div>
                    </div>
                </div>
                <div class="p-4 bg-yellow-300">
                    <h3 class="font-headline text-2xl font-black italic mb-2">DODGE_OR_DIE</h3>
                    <button class="w-full bg-black text-white p-3 font-label uppercase font-bold text-center hover:skew-x-2 transition-transform" id="dodge-start-btn">INITIALIZE_CHAOS</button>
                </div>
            </div>

            <!-- Game 3: Randomizer -->
            <div class="md:col-span-4 border-4 border-black bg-surface-container-lowest shadow-[8px_8px_0px_0px_#00e3fd] -rotate-2">
                <div class="p-4 border-b-4 border-black bg-tertiary-fixed flex items-center gap-2">
                    <span class="material-symbols-outlined">question_mark</span>
                    <span class="font-label font-bold uppercase text-xs">SHAPE_GEN_V1</span>
                </div>
                <div class="p-10 flex flex-col items-center justify-center gap-6">
                    <div class="w-32 h-32 bg-secondary border-8 border-black shadow-[4px_4px_0px_0px_#000000] transition-all duration-300" id="random-shape" style="border-radius: 20% 0% 80% 0%;"></div>
                    <button class="bg-white border-4 border-black p-2 font-label text-xs uppercase font-bold hover:bg-tertiary-fixed transition-colors" id="shape-gen-btn">SPIT_NEW_SHAPE</button>
                </div>
            </div>
        </div>
    </main>

    <footer class="w-full py-10 px-6 flex flex-col gap-4 items-start bg-yellow-300 border-t-4 border-black mt-20">
        <p class="font-mono text-[10px] text-black">©1998 RBAG - AUDIO ENGINE v1.0 [WEB_AUDIO_API]</p>
    </footer>

    <script>
        // --- AUDIO ENGINE ---
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();

        function beep(freq = 440, type = 'sine', duration = 0.1, volume = 0.1) {
            if (audioCtx.state === 'suspended') audioCtx.resume();
            const oscillator = audioCtx.createOscillator();
            const gainNode = audioCtx.createGain();

            oscillator.type = type;
            oscillator.frequency.setValueAtTime(freq, audioCtx.currentTime);
            
            gainNode.gain.setValueAtTime(volume, audioCtx.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.0001, audioCtx.currentTime + duration);

            oscillator.connect(gainNode);
            gainNode.connect(audioCtx.destination);

            oscillator.start();
            oscillator.stop(audioCtx.currentTime + duration);
        }

        function playSlide(startFreq, endFreq, duration) {
            if (audioCtx.state === 'suspended') audioCtx.resume();
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.frequency.setValueAtTime(startFreq, audioCtx.currentTime);
            osc.frequency.exponentialRampToValueAtTime(endFreq, audioCtx.currentTime + duration);
            gain.gain.setValueAtTime(0.1, audioCtx.currentTime);
            gain.gain.linearRampToValueAtTime(0, audioCtx.currentTime + duration);
            osc.connect(gain);
            gain.connect(audioCtx.destination);
            osc.start();
            osc.stop(audioCtx.currentTime + duration);
        }

        // --- CLICK_THE_PIXEL LOGIC ---
        let pixelScore = 0;
        const pixelBtn = document.getElementById('pixel-start-btn');
        const pixel = document.getElementById('target-pixel');
        const pixelScoreDisplay = document.getElementById('pixel-score');
        const pixelContainer = document.getElementById('pixel-game-container');
        const pixelMessage = document.getElementById('pixel-game-message');

        function movePixel() {
            const rect = pixelContainer.getBoundingClientRect();
            pixel.style.left = Math.random() * (rect.width - 40) + 'px';
            pixel.style.top = Math.random() * (rect.height - 40) + 'px';
        }

        pixelBtn.addEventListener('click', () => {
            beep(660, 'sine', 0.2);
            pixelBtn.innerText = 'RESET_EXE';
            pixel.classList.remove('hidden');
            pixelMessage.classList.add('opacity-10');
            movePixel();
        });

        pixel.addEventListener('mousedown', (e) => {
            e.stopPropagation();
            beep(880 + (pixelScore * 20), 'square', 0.05, 0.05); // Increasing pitch
            pixelScore++;
            pixelScoreDisplay.innerText = pixelScore.toString().padStart(4, '0');
            movePixel();
        });

        // --- DODGE_OR_DIE LOGIC ---
        const dodgeSquare = document.getElementById('dodge-square');
        const dodgeContainer = document.getElementById('dodge-container');
        const dodgeOverlay = document.getElementById('dodge-overlay');
        const dodgeBtn = document.getElementById('dodge-start-btn');
        let dodgeActive = false;
        let dodgePos = { x: 0, y: 0, dx: 5, dy: 5 };

        function updateDodge() {
            if (!dodgeActive) return;
            const cRect = dodgeContainer.getBoundingClientRect();
            dodgePos.x += dodgePos.dx;
            dodgePos.y += dodgePos.dy;

            if (dodgePos.x <= 0 || dodgePos.x + 64 >= cRect.width) {
                dodgePos.dx *= -1.05;
                beep(110, 'sawtooth', 0.05, 0.02);
            }
            if (dodgePos.y <= 0 || dodgePos.y + 64 >= cRect.height) {
                dodgePos.dy *= -1.05;
                beep(110, 'sawtooth', 0.05, 0.02);
            }

            dodgeSquare.style.left = dodgePos.x + 'px';
            dodgeSquare.style.top = dodgePos.y + 'px';
            requestAnimationFrame(updateDodge);
        }

        function triggerGameOver() {
            if (!dodgeActive) return;
            dodgeActive = false;
            playSlide(200, 50, 0.5); // Death slide
            dodgeOverlay.classList.remove('hidden');
            dodgeOverlay.classList.add('flex');
        }

        function resetDodge() {
            beep(440, 'sine', 0.1);
            dodgeActive = false;
            dodgeOverlay.classList.add('hidden');
            dodgePos = { x: 10, y: 10, dx: 5, dy: 5 };
            dodgeSquare.style.left = '10px';
            dodgeSquare.style.top = '10px';
            dodgeBtn.innerText = 'INITIALIZE_CHAOS';
        }

        dodgeBtn.addEventListener('click', () => {
            if (dodgeActive) return;
            playSlide(100, 800, 0.3); // Start slide
            dodgeActive = true;
            dodgeBtn.innerText = 'RUNNING...';
            updateDodge();
        });

        dodgeSquare.addEventListener('mouseover', triggerGameOver);

        // --- SHAPE_GEN LOGIC ---
        const shapeBtn = document.getElementById('shape-gen-btn');
        const shape = document.getElementById('random-shape');
        const colors = ['#a400a4', '#00fc40', '#00e3fd', '#ffbdf3', '#ff00ff', '#facc15', '#006b15'];

        shapeBtn.addEventListener('click', () => {
            beep(Math.random() * 1000 + 200, 'triangle', 0.1, 0.05);
            const r = () => Math.floor(Math.random() * 100);
            shape.style.borderRadius = `${r()}% ${r()}% ${r()}% ${r()}% / ${r()}% ${r()}% ${r()}% ${r()}%`;
            shape.style.transform = `rotate(${Math.random() * 360}deg) scale(${0.8 + Math.random() * 0.4})`;
            shape.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
        });
    </script>
</body>
</html>

```


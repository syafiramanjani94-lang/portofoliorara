<html lang="id" class="dark scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> // Cyber Terminal Edition</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- FontAwesome & Google Fonts -->
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500;600;700&family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        cyber: {
                            black: '#030712',
                            darker: '#0b0f19',
                            dark: '#111827',
                            card: '#151d2f',
                            accent: '#8b5cf6',
                            purple: '#a855f7',
                            blue: '#3b82f6',
                            cyan: '#06b6d4',
                            neonGreen: '#10b981',
                            pink: '#ec4899',
                        }
                    },
                    fontFamily: {
                        mono: ['"Fira Code"', 'monospace'],
                        sans: ['"Plus Jakarta Sans"', 'sans-serif'],
                    },
                    animation: {
                        'spin-slow': 'spin 16s linear infinite',
                        'spin-reverse': 'spin-reverse 10s linear infinite',
                        'pulse-glow': 'pulseGlow 3s ease-in-out infinite',
                        'float': 'float 4s ease-in-out infinite',
                    },
                    keyframes: {
                        'spin-reverse': {
                            '0%': { transform: 'rotate(360deg)' },
                            '100%': { transform: 'rotate(0deg)' },
                        },
                        pulseGlow: {
                            '0%, 100%': { opacity: '0.7', filter: 'drop-shadow(0 0 15px rgba(139, 92, 246, 0.6))' },
                            '50%': { opacity: '1', filter: 'drop-shadow(0 0 30px rgba(6, 182, 212, 0.8))' },
                        },
                        float: {
                            '0%, 100%': { transform: 'translateY(0px)' },
                            '50%': { transform: 'translateY(-10px)' },
                        }
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #030712;
            color: #cbd5e1;
            overflow-x: hidden;
            font-family: 'Plus Jakarta Sans', sans-serif;
        }

        .code-font {
            font-family: 'Fira Code', monospace;
        }

        /* Custom Cyber Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #030712;
        }
        ::-webkit-scrollbar-thumb {
            background: #1e293b;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #8b5cf6;
        }

        /* Dual Glowing Frame Avatar */
        .cyber-avatar-ring-1 {
            position: absolute;
            inset: -12px;
            border-radius: 1rem;
            border: 2px dashed rgba(139, 92, 246, 0.6);
            animation: pulse-glow 4s ease-in-out infinite;
        }
        .cyber-avatar-ring-2 {
            position: absolute;
            inset: -5px;
            border-radius: 1rem;
            border: 2px solid transparent;
            border-top-color: #06b6d4;
            border-bottom-color: #ec4899;
            animation: pulse-glow 3s ease-in-out infinite alternate;
        }

        /* Glassmorphism Panel */
        .cyber-glass {
            background: rgba(15, 23, 42, 0.75);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }

        .cyber-glass-hover:hover {
            border-color: rgba(139, 92, 246, 0.5);
            box-shadow: 0 0 25px -5px rgba(139, 92, 246, 0.3);
        }

        /* Gradient Text Helper */
        .text-gradient-cyber {
            background: linear-gradient(135deg, #06b6d4 0%, #a855f7 50%, #ec4899 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        /* Heart Floating Particles */
        .floating-heart {
            position: fixed;
            pointer-events: none;
            z-index: 9999;
            animation: floatUpAndFade 1.2s ease-out forwards;
        }

        @keyframes floatUpAndFade {
            0% {
                opacity: 1;
                transform: translateY(0) scale(1) rotate(0deg);
            }
            100% {
                opacity: 0;
                transform: translateY(-80px) scale(1.6) rotate(20deg);
            }
        }

        .fade-in-up {
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.7s ease, transform 0.7s ease;
        }
        .fade-in-up.is-visible {
            opacity: 1;
            transform: translateY(0);
        }
    </style>
</head>

<body class="selection:bg-cyber-accent selection:text-white relative">

    <!-- Matrix Code Rain Background -->
    <canvas id="matrixCanvas" class="fixed inset-0 w-full h-full pointer-events-none z-0 opacity-20"></canvas>

    <!-- Top Status Diagnostics Bar -->
    <div class="fixed top-0 left-0 right-0 z-40 bg-cyber-black/90 border-b border-slate-800 text-xs code-font py-1.5 px-4 backdrop-blur-md">
        <div class="max-w-6xl mx-auto flex justify-between items-center text-slate-400">
            <div class="flex items-center space-x-3">
                <span class="flex items-center text-emerald-400 font-bold">
                    <span class="w-2 h-2 rounded-full bg-emerald-500 animate-ping mr-2"></span>
                    SYSTEM_ONLINE
                </span>
                <span class="hidden sm:inline text-slate-600">|</span>
                <span class="hidden sm:inline">FAKULTAS TEKNIK & INFORMATIKA</span>
            </div>
            <div class="flex items-center space-x-4">
                <button id="sfxToggleBtn" class="hover:text-cyber-cyan transition-colors flex items-center space-x-1 px-2 py-0.5 rounded bg-slate-900 border border-slate-800">
                    <i id="sfxIcon" class="fas fa-volume-up text-cyber-neonGreen"></i>
                    <span id="sfxStatus">SOUND ON </span>
                </button>
                <div class="text-cyber-cyan font-bold">
                    <i class="far fa-clock mr-1"></i>
                    <span id="headerClock">00:00:00 WIB</span>
                </div>
            </div>
        </div>
    </div>

    <!-- Navigation Bar -->
    <nav class="fixed top-8 left-0 right-0 z-30 py-3 transition-all">
        <div class="max-w-6xl mx-auto px-4">
            <div class="cyber-glass rounded-xl px-5 py-3 flex justify-between items-center border border-slate-800 shadow-2xl">
                <a href="#beranda" class="flex items-center space-x-2 group">
                    <div class="w-8 h-8 rounded-lg bg-gradient-to-tr from-cyber-accent to-cyber-cyan flex items-center justify-center text-white font-bold code-font text-sm shadow-[0_0_15px_rgba(139,92,246,0.5)] group-hover:scale-105 transition-transform">
                        r
                    </div>
                    <span class="text-lg font-bold code-font text-white tracking-tight">
                        rara<span class="text-cyber-accent">.</span>
                    </span>
                </a>

                <!-- Desktop Menu Links -->
                <div class="hidden md:flex items-center space-x-8 text-sm font-medium code-font">
                    <a href="#beranda" class="hover:text-cyber-cyan transition-colors text-slate-300 flex items-center gap-1">
                        <span class="text-cyber-purple"></span>beranda
                    </a>
                    <a href="#tentang" class="hover:text-cyber-cyan transition-colors text-slate-300 flex items-center gap-1">
                        <span class="text-cyber-purple"></span>tentang saya
                    </a>
                    <a href="#jam" class="hover:text-cyber-cyan transition-colors text-slate-300 flex items-center gap-1">
                        <span class="text-cyber-purple"></span>jam cyber
                    </a>
                    <a href="#kontak" class="hover:text-cyber-cyan transition-colors text-slate-300 flex items-center gap-1">
                        <span class="text-cyber-purple"></span>kontak
                    </a>
                </div>

                <!-- CTA Button -->
                <a href="#kontak" class="px-4 py-2 rounded-lg bg-gradient-to-r from-cyber-accent to-cyber-blue text-white text-xs font-semibold code-font hover:shadow-[0_0_20px_rgba(139,92,246,0.6)] transition-all hidden sm:flex items-center gap-2">
                    <i class="fas fa-paper-plane"></i> Hubungi Saya
                </a>

                <!-- Mobile Menu Button -->
                <button id="mobileMenuBtn" class="md:hidden text-slate-300 hover:text-white p-2">
                    <i class="fas fa-bars text-xl"></i>
                </button>
            </div>
        </div>

        <!-- Mobile Dropdown Menu -->
        <div id="mobileMenu" class="hidden md:hidden max-w-6xl mx-4 mt-2 cyber-glass rounded-xl p-4 border border-slate-800 space-y-2 code-font text-sm">
            <a href="#beranda" class="mobile-link block p-2 rounded hover:bg-slate-800 text-slate-200">/beranda</a>
            <a href="#tentang" class="mobile-link block p-2 rounded hover:bg-slate-800 text-slate-200">/tentang-saya</a>
            <a href="#jam" class="mobile-link block p-2 rounded hover:bg-slate-800 text-slate-200">/jam-cyber</a>
            <a href="#kontak" class="mobile-link block p-2 rounded hover:bg-slate-800 text-slate-200">/kontak</a>
        </div>
    </nav>

    <!-- 1. BERANDA SECTION -->
    <section id="beranda" class="min-h-screen pt-36 pb-20 flex items-center relative border-b border-slate-800/80">
        <div class="max-w-6xl mx-auto px-4 w-full">
            <div class="grid lg:grid-cols-12 gap-12 items-center">
                
                <!-- Hero Text -->
                <div class="lg:col-span-7 text-center lg:text-left fade-in-up">
                    <div class="inline-flex items-center gap-2 px-3.5 py-1.5 rounded-full bg-cyber-accent/10 border border-cyber-accent/30 text-cyber-purple text-xs font-mono mb-6">
                        <span class="w-2 h-2 rounded-full bg-cyber-purple animate-pulse"></span>
                        <span>Mahasiswa Informatika</span>
                    </div>

                    <h1 class="text-4xl sm:text-6xl font-extrabold text-white tracking-tight mb-6 leading-tight">
                        UNIVERSITAS BINA SARANA <br>
                        <span class="text-gradient-cyber">INFORMATIKA</span>
                    </h1>

                    <p class="text-slate-400 text-base sm:text-lg mb-8 max-w-2xl mx-auto lg:mx-0 leading-relaxed">
                         𝑯𝒆𝒍𝒍𝒐 𝒆𝒗𝒆𝒓𝒚𝒐𝒏𝒆! 𝒔𝒂𝒚𝒂<span class="text-slate-400 font-semibold"> 𝑺𝒚𝒂𝒇𝒊𝒓𝒂 𝑴𝒂𝒏𝒋𝒂𝒏𝒊</span>. 𝒔𝒂𝒚𝒂 𝒂𝒅𝒂𝒍𝒂𝒉 𝒎𝒂𝒉𝒂𝒔𝒊𝒔𝒘𝒂 𝒅𝒂𝒓𝒊 𝒑𝒓𝒐𝒅𝒊 𝒊𝒏𝒇𝒐𝒓𝒎𝒂𝒕𝒊𝒌𝒂,𝒇𝒂𝒌𝒖𝒍𝒕𝒂𝒔 𝒕𝒆𝒌𝒏𝒊𝒌 & 𝒊𝒏𝒇𝒐𝒓𝒎𝒂𝒕𝒊𝒌𝒂
                    </p>

                    <!-- Dynamic Role Badge -->
                    <div class="cyber-glass rounded-xl p-3 inline-block border border-slate-800 text-left mb-8 w-full max-w-md">
                        <div class="text-[11px] text-slate-500 font-mono mb-1">SELAMAT DATANG..</div>
                        <div class="font-mono text-sm text-cyber-cyan flex items-center">
                            <span class="text-pink-500 mr-2">&gt;</span>
                            <span id="typedRole">MAHASISWA UBSI</span>
                            <span class="animate-pulse text-white ml-1">|</span>
                        </div>
                    </div>

                    <div class="flex flex-wrap gap-4 justify-center lg:justify-start">
                        <a href="#kontak" class="px-6 py-3.5 rounded-xl bg-gradient-to-r from-cyber-accent via-cyber-purple to-cyber-blue text-white font-semibold text-sm code-font shadow-[0_0_25px_rgba(139,92,246,0.4)] hover:shadow-[0_0_35px_rgba(139,92,246,0.7)] hover:scale-105 transition-all flex items-center gap-2">
                            <i class="fas fa-paper-plane"></i> Kontak Saya
                        </a>
                        <a href="#jam" class="px-6 py-3.5 rounded-xl cyber-glass border border-slate-700 hover:border-cyber-cyan text-slate-200 hover:text-cyber-cyan font-semibold text-sm code-font transition-all flex items-center gap-2">
                            <i class="far fa-clock"></i> Lihat Jam 
                        </a>
                    </div>
                </div>

                <!-- Glowing Avatar Picture Frame -->
                <div class="lg:col-span-5 flex justify-center fade-in-up">
                    <div class="relative w-64 h-64 sm:w-80 sm:h-80 my-4">
                        <!-- Rotating Glowing Rings -->
                        <div class="cyber-avatar-ring-1"></div>
                        <div class="cyber-avatar-ring-2"></div>
                        
                        <!-- Backlight Glow -->
                        <div class="absolute inset-0 rounded-2xl bg-gradient-to-tr from-cyber-accent via-cyber-cyan to-cyber-purple blur-2xl opacity-40 animate-pulse-glow"></div>

                        <!-- Profile Image Container -->
                        <div class="relative w-full h-full rounded-2xl overflow-hidden border-4 border-cyber-black p-1 shadow-2xl z-10 bg-slate-900">
                            <img src="https://lh3.googleusercontent.com/d/1L16H2TywZyYCpUVkqdt194f2ntg0ae79" onerror="this.src='https://placehold.co/400x400/0f172a/a855f7?text=syafira'" alt="Foto Profil syafira" class="w-full h-full object-cover rounded-2xl hover:scale-110 transition-transform duration-500 filter brightness-105">
                        </div>

                        <!-- Floating Stat Badges -->
                        <div class="absolute -top-2 -right-2 z-20 cyber-glass border border-slate-700/80 rounded-lg px-3 py-1.5 text-xs font-mono text-slate-200 shadow-xl animate-float">
                            <i class="fas fa-award text-yellow-400 mr-1"></i> <span class="text-cyber-neonGreen font-bold">Akreditasi Unggul</span>
                        </div>

                        <div class="absolute -bottom-2 -left-2 z-20 cyber-glass border border-slate-700/80 rounded-lg px-3 py-1.5 text-xs font-mono text-slate-200 shadow-xl animate-float" style="animation-delay: 1.5s;">
                            <i class="fas fa-graduation-cap text-cyber-purple mr-1"></i> <span class="text-cyber-cyan font-bold">Kuliah?</span>BSIAja
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </section>

    <!-- 2. TENTANG SAYA SECTION -->
    <section id="tentang" class="py-24 relative border-b border-slate-800">
        <div class="max-w-6xl mx-auto px-4">
            <div class="text-center mb-16 fade-in-up">
                <h2 class="text-3xl font-bold text-white code-font">
                    <span class="text-cyber-purple">Tentang Saya</span> 
                </h2>
                <div class="w-20 h-1 bg-gradient-to-r from-cyber-accent to-cyber-cyan mx-auto rounded-full mt-3"></div>
            </div>

            <div class="grid lg:grid-cols-12 gap-8 items-center">
                
                <!-- IDE Visual Code Editor Card -->
                <div class="lg:col-span-7 fade-in-up">
                    <div class="cyber-glass rounded-xl overflow-hidden border border-slate-800 shadow-2xl">
                        <!-- IDE Header Bar -->
                        <div class="bg-slate-900 px-4 py-2.5 border-b border-slate-800 flex items-center justify-between text-xs font-mono text-slate-400">
                            <div class="flex items-center space-x-2">
                                <div class="w-3 h-3 rounded-full bg-red-500/80"></div>
                                <div class="w-3 h-3 rounded-full bg-yellow-500/80"></div>
                                <div class="w-3 h-3 rounded-full bg-green-500/80"></div>
                                <span class="ml-2 text-slate-300">JANGAN LUPA KLIK!!!</span>
                            </div>
                            <span class="text-slate-600">LOVE</span>
                        </div>

                        <!-- IDE Code Body (Dihapus kodenya & diganti Love Warna-Warni Muter 90 Derajat) -->
                        <div class="p-8 sm:p-12 flex flex-col items-center justify-center min-h-[300px] bg-slate-950 relative overflow-hidden">
                            <style>
                                @keyframes rotate90deg {
                                    0% {
                                        transform: rotate(0deg) scale(1);
                                        filter: drop-shadow(0 0 15px rgba(236, 72, 153, 0.6));
                                    }
                                    50% {
                                        transform: rotate(90deg) scale(1.15);
                                        filter: drop-shadow(0 0 35px rgba(6, 182, 212, 0.9));
                                    }
                                    100% {
                                        transform: rotate(0deg) scale(1);
                                        filter: drop-shadow(0 0 15px rgba(236, 72, 153, 0.6));
                                    }
                                }
                                @keyframes rainbowGradient {
                                    0% { background-position: 0% 50%; }
                                    50% { background-position: 100% 50%; }
                                    100% { background-position: 0% 50%; }
                                }
                                .rainbow-love-icon {
                                    background: linear-gradient(135deg, #ec4899, #8b5cf6, #3b82f6, #06b6d4, #10b981, #f59e0b, #ef4444);
                                    background-size: 300% 300%;
                                    -webkit-background-clip: text;
                                    -webkit-text-fill-color: transparent;
                                    animation: rotate90deg 3.5s ease-in-out infinite, rainbowGradient 5s ease infinite;
                                }
                                .emit-light {
                                    filter: drop-shadow(0 0 60px rgba(255, 255, 255, 0.9)) drop-shadow(0 0 100px rgba(236, 72, 153, 1)) !important;
                                }
                                .bubble-love {
                                    position: fixed;
                                    pointer-events: none;
                                    z-index: 9999;
                                    animation: floatBubble 2.5s ease-out forwards;
                                    background: radial-gradient(circle at 30% 30%, rgba(255,255,255,0.9), rgba(255,192,203,0.3));
                                    border: 1px solid rgba(255, 255, 255, 0.6);
                                    border-radius: 50%;
                                    display: flex;
                                    align-items: center;
                                    justify-content: center;
                                    box-shadow: inset 0 0 10px rgba(255,255,255,0.8), 0 0 15px rgba(236,72,153,0.6);
                                }
                                .bubble-love i {
                                    color: rgba(236, 72, 153, 0.9);
                                    text-shadow: 0 0 5px rgba(255,255,255,0.8);
                                }
                                @keyframes floatBubble {
                                    0% { opacity: 1; transform: translateY(0) scale(0.5); }
                                    50% { opacity: 0.9; transform: translateY(-120px) scale(1.3) translateX(30px); }
                                    100% { opacity: 0; transform: translateY(-250px) scale(1.5) translateX(-30px); }
                                }
                            </style>
                            
                            <div class="text-center p-4">
                                <button id="bigLoveBtn" class="cursor-pointer focus:outline-none transition-transform hover:scale-110 active:scale-95" title="Klik untuk putar 360° & putar lagu romansa!">
                                    <i id="bigLoveIcon" class="fas fa-heart text-8xl sm:text-9xl rainbow-love-icon inline-block"></i>
                                </button>
                                <p class="text-xs font-mono text-slate-400 mt-6 tracking-widest uppercase">LOVE MY SELF</p>
                                <div class="mt-4 flex flex-wrap items-center justify-center gap-2 text-xs font-mono">
                                    <button id="song1Btn" class="px-3 py-1.5 rounded-full bg-cyber-accent text-white border border-cyber-accent shadow-[0_0_10px_rgba(139,92,246,0.5)] transition-all">Lagu 1: Romansa</button>
                                    <button id="song2Btn" class="px-3 py-1.5 rounded-full bg-slate-900 text-slate-400 border border-slate-700 hover:text-white transition-all">Lagu 2: Suara Gelembung</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Text Description & Highlights -->
                <div class="lg:col-span-5 space-y-6 fade-in-up">
                    <h3 class="text-2xl font-bold text-white leading-snug">
                        𝑩𝑬𝑹𝑭𝑰𝑲𝑰𝑹 𝑳𝑶𝑮𝑰𝑲𝑨 𝑼𝑵𝑻𝑼𝑲 𝑷𝑬𝑹𝑲𝑬𝑴𝑩𝑨𝑵𝑮𝑨𝑵 𝑫𝑰 𝑨𝑹𝑬𝑨 𝑻𝑬𝑲𝑵𝑶𝑳𝑶𝑮𝑰 
                    </h3>
                    <p class="text-slate-400 text-sm leading-relaxed">
                        Sebagai mahasiswa Informatika, saya memiliki passion tinggi dalam memahami bagaimana perangkat lunak bekerja dari balik layar mulai dari struktur data, efisiensi algoritma, hingga desain antarmuka pengguna.
                    </p>
                    <p class="text-slate-400 text-sm leading-relaxed">
                        Saya terbiasa memecahkan masalah logika, mempelajari teknologi baru dengan cepat, dan bekerja baik secara individu maupun dalam tim project.
                    </p>

                    <!-- Tech Skill Badges -->
                    <div class="pt-2">
                        <div class="text-xs font-mono text-slate-500 mb-3">pendidikan:</div>
                        <div class="flex flex-wrap gap-2 font-mono text-xs">
                            <span class="px-3 py-1 rounded-lg bg-slate-900 border border-slate-800 text-cyan-400">TK AL-HIDAYAH 2</span>
                            <span class="px-3 py-1 rounded-lg bg-slate-900 border border-slate-800 text-yellow-400">SDN KELAPA GADING TIMUR 01</span>
                            <span class="px-3 py-1 rounded-lg bg-slate-900 border border-slate-800 text-blue-400">SMPN 123</span>
                            <span class="px-3 py-1 rounded-lg bg-slate-900 border border-slate-800 text-purple-400">SMAN 45</span>
                            <span class="px-3 py-1 rounded-lg bg-slate-900 border border-slate-800 text-emerald-400">UNIVERSITAS BINA SARANA INFORMATIKA</span>
                            <span class="px-3 py-1 rounded-lg bg-slate-900 border border-slate-800  
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </section>

    <!-- 3. JAM CYBER MENARIK SECTION -->
    <section id="jam" class="py-24 bg-cyber-darker relative border-b border-slate-800">
        <div class="max-w-6xl mx-auto px-4">
            <div class="text-center mb-12 fade-in-up">
                <h2 class="text-3xl font-bold text-white code-font">
                    <span class="text-cyber-cyan">Jam</span> 
                </h2>
                <p class="text-slate-400 text-xs sm:text-sm font-mono mt-2"></p>
            </div

            <!-- Main Interactive HUD Clock Container -->
            <div class="max-w-3xl mx-auto cyber-glass rounded-2xl p-6 sm:p-10 border border-slate-700 shadow-2xl relative overflow-hidden fade-in-up">
                
                <!-- Background Glowing HUD Grid Accent -->
                <div class="absolute -right-16 -top-16 w-60 h-60 rounded-full bg-cyber-cyan/10 blur-3xl pointer-events-none"></div>
                <div class="absolute -left-16 -bottom-16 w-60 h-60 rounded-full bg-cyber-purple/10 blur-3xl pointer-events-none"></div>

                <!-- Clock Header Tools -->
                <div class="flex flex-wrap items-center justify-between gap-4 border-b border-slate-800 pb-4 mb-8 text-xs font-mono">
                    <div class="flex items-center space-x-2 text-cyber-cyan">
                        <i class="fas fa-satellite-dish animate-pulse"></i>
                        <span>TIME</span>
                    </div>

                    <!-- Timezone Switcher Buttons -->
                    <div class="flex items-center space-x-1 bg-slate-900 p-1 rounded-lg border border-slate-800">
                        <button onclick="setTimezone('WIB')" id="tzWIB" class="tz-btn px-2.5 py-1 rounded text-white bg-cyber-accent font-bold transition-all">WIB</button>
                        <button onclick="setTimezone('UTC')" id="tzUTC" class="tz-btn px-2.5 py-1 rounded text-slate-400 hover:text-white transition-all">UTC</button>
                        <button onclick="setTimezone('JST')" id="tzJST" class="tz-btn px-2.5 py-1 rounded text-slate-400 hover:text-white transition-all">JST</button>
                        <button onclick="setTimezone('EST')" id="tzEST" class="tz-btn px-2.5 py-1 rounded text-slate-400 hover:text-white transition-all">EST</button>
                    </div>
                </div>

                <!-- Main Display Row: Circular SVG Ring & Glowing Digits -->
                <div class="grid md:grid-cols-12 gap-8 items-center text-center md:text-left">
                    
                    <!-- SVG Seconds Progress Circle -->
                    <div class="md:col-span-4 flex justify-center">
                        <div class="relative w-40 h-40 flex items-center justify-center">
                            <svg class="w-full h-full -rotate-90 transform" viewBox="0 0 100 100">
                                <circle cx="50" cy="50" r="42" stroke="#1e293b" stroke-width="6" fill="transparent"/>
                                <circle id="svgSecondCircle" cx="50" cy="50" r="42" stroke="#06b6d4" stroke-width="6" fill="transparent" stroke-dasharray="263.89" stroke-dashoffset="0" stroke-linecap="round" class="transition-all duration-300"/>
                            </svg>
                            <div class="absolute inset-0 flex flex-col items-center justify-center font-mono">
                                <span class="text-xs text-slate-500 uppercase">Detik</span>
                                <span id="clockSeconds" class="text-3xl font-bold text-cyber-cyan">00</span>
                                <span id="clockMillis" class="text-[10px] text-cyber-purple font-bold">.000</span>
                            </div>
                        </div>
                    </div>

                    <!-- Large Digital Clock Display -->
                    <div class="md:col-span-8 space-y-2">
                        <div class="text-xs font-mono text-slate-400 flex items-center justify-center md:justify-start gap-2">
                            <i class="far fa-calendar-alt text-cyber-purple"></i>
                            <span id="clockFullDate">Senin, 01 Januari 2026</span>
                        </div>

                        <div class="font-mono text-4xl sm:text-6xl font-black text-white tracking-wider drop-shadow-[0_0_20px_rgba(6,182,212,0.5)]">
                            <span id="clockHours">00</span>:<span id="clockMinutes">00</span>
                            <span id="clockPeriod" class="text-lg sm:text-2xl text-cyber-purple font-normal">WIB</span>
                        </div>

                        <!-- Interactive Binary Clock Matrix -->
                        <div class="pt-4 border-t border-slate-800/80">
                            <div class="text-[10px] font-mono text-slate-500 mb-2 uppercase">Jam Biner (Binary Time Matrix):</div>
                            <div id="binaryMatrix" class="flex justify-center md:justify-start gap-3 font-mono text-[11px]">
                                <!-- Dynamically populated by JS -->
                            </div>
                        </div>
                    </div>

                </div>

            </div>
        </div>
    </section>

    <!-- 4. KONTAK SECTION -->
    <section id="kontak" class="py-24 relative border-b border-slate-800">
        <div class="max-w-5xl mx-auto px-4">
            <div class="text-center mb-16 fade-in-up">
                <h2 class="text-3xl font-bold text-white code-font">
                    <span class="text-cyber-purple">Kontak</span>
                </h2>
                <p class="text-slate-400 text-sm mt-2">Hubungi saya melalui sosial media</p>
            </div>

            <div class="grid md:grid-cols-12 gap-8 items-start">
                
                <!-- Left Details -->
                <div class="md:col-span-5 space-y-6 fade-in-up">
                    <div class="cyber-glass p-6 rounded-xl border border-slate-800 space-y-6">
                        <h3 class="text-lg font-bold text-white code-font border-b border-slate-800 pb-3">
                            kontak pesan
                        </h3>
                        
                        <div class="flex items-center space-x-4">
                            <div class="w-10 h-10 rounded-lg bg-slate-900 border border-slate-800 flex items-center justify-center text-cyber-cyan">
                                <i class="fas fa-envelope"></i>
                            </div>
                            <div>
                                <div class="text-[11px] text-slate-500 uppercase font-mono">Email</div>
                                <a href="mailto:syafiramanjani94@gmail.com" class="text-sm font-mono text-slate-200 hover:text-cyber-cyan transition-colors">syafiramanjani94@gmail.com</a>
                            </div>
                        </div>

                        <div class="flex items-center space-x-4">
                            <div class="w-10 h-10 rounded-lg bg-slate-900 border border-slate-800 flex items-center justify-center text-pink-500">
                                <i class="fab fa-instagram"></i>
                            </div>
                            <div>
                                <div class="text-[11px] text-slate-500 uppercase font-mono">Instagram</div>
                                <a href="https://instagram.com/xsyrara13" target="_blank" class="text-sm font-mono text-slate-200 hover:text-pink-500 transition-colors">@xsyrara13</a>
                            </div>
                        </div>

                        <div class="pt-4 border-t border-slate-800">
                            <div class="text-xs text-slate-500 font-mono mb-3">Sosial Media:</div>
                            <div class="flex space-x-3">
                                <a href="https://instagram.com/xsyrara13" target="_blank" class="w-9 h-9 rounded-lg bg-slate-900 border border-slate-800 hover:border-pink-500 flex items-center justify-center text-slate-400 hover:text-pink-500 transition-all"><i class="fab fa-instagram"></i></a>
                                <a href="mailto:syafiramanjani94@gmail.com" class="w-9 h-9 rounded-lg bg-slate-900 border border-slate-800 hover:border-cyber-cyan flex items-center justify-center text-slate-400 hover:text-cyber-cyan transition-all"><i class="fas fa-envelope"></i></a>
                                <a href="https://wa.me/" target="_blank" class="w-9 h-9 rounded-lg bg-slate-900 border border-slate-800 hover:border-emerald-500 flex items-center justify-center text-slate-400 hover:text-emerald-500 transition-all"><i class="fab fa-whatsapp"></i></a>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Right Form -->
                <div class="md:col-span-7 fade-in-up">
                    <form id="contactForm" class="cyber-glass rounded-xl p-6 sm:p-8 border border-slate-800 space-y-4">
                        <div class="text-xs font-mono text-slate-500 mb-2 flex items-center justify-between border-b border-slate-800 pb-3">
                            <span>jangan lupa diisi dibawah ini</span>
                            <span class="text-cyber-neonGreen">mengirim pesan</span>
                        </div>

                        <div>
                            <label class="block text-xs font-mono text-slate-400 mb-1">nama pengirim:</label>
                            <input type="text" id="contactName" required placeholder="Masukkan nama Anda" class="w-full px-4 py-2.5 bg-cyber-black border border-slate-700 rounded-lg text-slate-200 text-sm font-mono focus:outline-none focus:border-cyber-accent transition-colors">
                        </div>

                        <div>
                            <label class="block text-xs font-mono text-slate-400 mb-1">email pengirim:</label>
                            <input type="email" id="contactEmail" required placeholder="nama@domain.com" class="w-full px-4 py-2.5 bg-cyber-black border border-slate-700 rounded-lg text-slate-200 text-sm font-mono focus:outline-none focus:border-cyber-accent transition-colors">
                        </div>

                        <div>
                            <label class="block text-xs font-mono text-slate-400 mb-1">isi pesan:</label>
                            <textarea id="contactMessage" rows="4" required placeholder="Tuliskan pesan Anda di sini..." class="w-full px-4 py-2.5 bg-cyber-black border border-slate-700 rounded-lg text-slate-200 text-sm font-mono focus:outline-none focus:border-cyber-accent transition-colors resize-none"></textarea>
                        </div>

                        <button type="submit" id="submitBtn" class="w-full py-3 bg-gradient-to-r from-cyber-accent to-cyber-blue text-white font-mono text-sm rounded-lg hover:shadow-[0_0_20px_rgba(139,92,246,0.5)] transition-all flex items-center justify-center space-x-2">
                            <i class="fas fa-paper-plane"></i>
                            <span id="submitBtnText">kirim Pesan</span>
                        </button>

                        <div id="formAlert" class="hidden text-xs font-mono p-3 rounded bg-slate-900 text-center"></div>
                    </form>
                </div>

            </div>
        </div>
    </section>

    <!-- 5. PENUTUP (FOOTER) SECTION WITH 360 DEGREE LOVE BUTTON -->
    <footer class="py-12 bg-cyber-black border-t border-slate-800/80 text-center text-xs font-mono text-slate-500 relative">
        <div class="max-w-6xl mx-auto px-4 space-y-4">
            
            <!-- Interactive Love Icon Trigger -->
            <div class="flex items-center justify-center space-x-2 text-sm text-slate-400">
                <span>Dibuat dengan</span>
                
                <!-- Interactive 360 Degree Rotating Love Button -->
                <button id="loveBtn" class="inline-flex items-center justify-center w-9 h-9 rounded-full bg-slate-900 border border-slate-800 text-pink-500 hover:text-pink-400 hover:border-pink-500/50 cursor-pointer transition-all duration-700 ease-in-out hover:scale-125 focus:outline-none shadow-lg" title="Klik saya untuk putaran 360°!">
                    <i id="loveIcon" class="fas fa-heart text-base transition-transform duration-700"></i>
                </button>
                
                <span>oleh <span class="text-slate-200 font-bold"syafira</span></span>
            </div>

            <!-- Total Love Click Counter -->
            <div class="text-[11px] text-slate-600">
                Putaran Love diklik: <span id="loveCount" class="text-pink-400 font-bold">0</span> kali
            </div>

            <p class="text-slate-600"> <span id="footerYear"></span> syafira.S.KOM</p>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', () => {

            // 1. Matrix Background Animation Canvas
            const canvas = document.getElementById('matrixCanvas');
            const ctx = canvas.getContext('2d');

            function resizeCanvas() {
                canvas.width = window.innerWidth;
                canvas.height = window.innerHeight;
            }
            resizeCanvas();
            window.addEventListener('resize', resizeCanvas);

            const matrixChars = "0101010101<>/{};=+$#@ALEXDEV";
            const fontSize = 14;
            let columns = Math.floor(canvas.width / fontSize);
            let drops = Array(columns).fill(1);

            function drawMatrix() {
                ctx.fillStyle = "rgba(3, 7, 18, 0.08)";
                ctx.fillRect(0, 0, canvas.width, canvas.height);

                ctx.fillStyle = "#06b6d4";
                ctx.font = `${fontSize}px 'Fira Code', monospace`;

                for (let i = 0; i < drops.length; i++) {
                    const text = matrixChars.charAt(Math.floor(Math.random() * matrixChars.length));
                    ctx.fillText(text, i * fontSize, drops[i] * fontSize);

                    if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
                        drops[i] = 0;
                    }
                    drops[i]++;
                }
            }
            setInterval(drawMatrix, 45);

            // 2. Audio Synth for Interaction Effects
            let sfxEnabled = true;
            const sfxToggleBtn = document.getElementById('sfxToggleBtn');
            const sfxStatus = document.getElementById('sfxStatus');
            const sfxIcon = document.getElementById('sfxIcon');

            function playSoundEffect(freq = 800, duration = 0.06, type = 'sine') {
                if (!sfxEnabled) return;
                try {
                    const ctxAudio = new (window.AudioContext || window.webkitAudioContext)();
                    const osc = ctxAudio.createOscillator();
                    const gain = ctxAudio.createGain();
                    osc.type = type;
                    osc.frequency.setValueAtTime(freq, ctxAudio.currentTime);
                    osc.frequency.exponentialRampToValueAtTime(freq / 2, ctxAudio.currentTime + duration);
                    gain.gain.setValueAtTime(0.08, ctxAudio.currentTime);
                    gain.gain.exponentialRampToValueAtTime(0.01, ctxAudio.currentTime + duration);
                    osc.connect(gain);
                    gain.connect(ctxAudio.destination);
                    osc.start();
                    osc.stop(ctxAudio.currentTime + duration);
                } catch(e){}
            }

            sfxToggleBtn.addEventListener('click', () => {
                sfxEnabled = !sfxEnabled;
                if (sfxEnabled) {
                    sfxStatus.textContent = 'SOUND ON';
                    sfxIcon.className = 'fas fa-volume-up text-cyber-neonGreen';
                    playSoundEffect(1000);
                } else {
                    sfxStatus.textContent = 'SOUND Of';
                    sfxIcon.className = 'fas fa-volume-mute text-slate-500';
                }
            });

            // 3. Dynamic Typing Effect in Hero Section
            const roles = [
                "saya dari prodi informatika ",
                "fakultas teknik & informatika",
                "universitas bina sarana informatika",
                "Kuliah?BSIAJA"
            ];
            let roleIdx = 0, charIdx = 0, isDeleting = false;
            const typedEl = document.getElementById('typedRole');

            function typeLoop() {
                const current = roles[roleIdx];
                if (isDeleting) {
                    typedEl.textContent = current.substring(0, charIdx - 1);
                    charIdx--;
                } else {
                    typedEl.textContent = current.substring(0, charIdx + 1);
                    charIdx++;
                }

                if (!isDeleting && charIdx === current.length) {
                    isDeleting = true;
                    setTimeout(typeLoop, 2200);
                } else if (isDeleting && charIdx === 0) {
                    isDeleting = false;
                    roleIdx = (roleIdx + 1) % roles.length;
                    setTimeout(typeLoop, 400);
                } else {
                    setTimeout(typeLoop, isDeleting ? 35 : 75);
                }
            }
            typeLoop();

            // 4. Interactive Cyber HUD Clock Station Logic
            let selectedTimezone = 'WIB';

            window.setTimezone = function(tz) {
                selectedTimezone = tz;
                document.querySelectorAll('.tz-btn').forEach(btn => {
                    btn.classList.remove('bg-cyber-accent', 'text-white', 'font-bold');
                    btn.classList.add('text-slate-400');
                });
                const activeBtn = document.getElementById(`tz${tz}`);
                if (activeBtn) {
                    activeBtn.classList.add('bg-cyber-accent', 'text-white', 'font-bold');
                    activeBtn.classList.remove('text-slate-400');
                }
                playSoundEffect(600, 0.04);
            };

            function updateClock() {
                const now = new Date();
                
                // Adjust for timezone offset
                let tzOffsetHours = 7; // Default WIB UTC+7
                if (selectedTimezone === 'UTC') tzOffsetHours = 0;
                if (selectedTimezone === 'JST') tzOffsetHours = 9;
                if (selectedTimezone === 'EST') tzOffsetHours = -5;

                const utcTime = now.getTime() + (now.getTimezoneOffset() * 60000);
                const localDate = new Date(utcTime + (3600000 * tzOffsetHours));

                const h = String(localDate.getHours()).padStart(2, '0');
                const m = String(localDate.getMinutes()).padStart(2, '0');
                const s = String(localDate.getSeconds()).padStart(2, '0');
                const ms = String(localDate.getMilliseconds()).padStart(3, '0');

                // Header quick clock
                document.getElementById('headerClock').textContent = `${h}:${m}:${s} ${selectedTimezone}`;

                // Main Clock Display
                document.getElementById('clockHours').textContent = h;
                document.getElementById('clockMinutes').textContent = m;
                document.getElementById('clockSeconds').textContent = s;
                document.getElementById('clockMillis').textContent = `.${ms}`;
                document.getElementById('clockPeriod').textContent = selectedTimezone;

                // Date String
                const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
                document.getElementById('clockFullDate').textContent = localDate.toLocaleDateString('id-ID', options);

                // SVG Circular Seconds Dash
                const svgCircle = document.getElementById('svgSecondCircle');
                const secNum = localDate.getSeconds();
                const totalDash = 263.89; // 2 * PI * 42
                const offset = totalDash - (secNum / 60) * totalDash;
                svgCircle.style.strokeDashoffset = offset;

                // Binary Clock Visualizer Update
                const binaryMatrix = document.getElementById('binaryMatrix');
                const bH = parseInt(h).toString(2).padStart(6, '0');
                const bM = parseInt(m).toString(2).padStart(6, '0');
                const bS = parseInt(s).toString(2).padStart(6, '0');

                binaryMatrix.innerHTML = `
                    <div class="flex flex-col items-center"><span class="text-slate-500 text-[9px]">JAM</span><span class="text-cyber-cyan font-bold">${bH}</span></div>
                    <span class="text-slate-600">:</span>
                    <div class="flex flex-col items-center"><span class="text-slate-500 text-[9px]">MENIT</span><span class="text-cyber-purple font-bold">${bM}</span></div>
                    <span class="text-slate-600">:</span>
                    <div class="flex flex-col items-center"><span class="text-slate-500 text-[9px]">DETIK</span><span class="text-emerald-400 font-bold">${bS}</span></div>
                `;
            }
            setInterval(updateClock, 50); // Fast interval for smooth milliseconds

            // 5. PENUTUP (FOOTER): 360 DEGREE ROTATING LOVE BUTTON & PARTICLES
            let currentLoveRotation = 0;
            let loveClickCount = 0;
            const loveBtn = document.getElementById('loveBtn');
            const loveIcon = document.getElementById('loveIcon');
            const loveCountEl = document.getElementById('loveCount');

            // Interactive Big Love Icon inside BiodataInformatika.ts (360° + Romantic Melody)
            const bigLoveBtn = document.getElementById('bigLoveBtn');
            const bigLoveIcon = document.getElementById('bigLoveIcon');
            let bigLoveRotation = 0;

            function playRomanticMelody() {
                // Hentikan lagu youtube (Shape of My Heart) jika sedang diputar
                if (window.ytPlayerInstance && typeof window.ytPlayerInstance.pauseVideo === 'function') {
                    window.ytPlayerInstance.pauseVideo();
                }
                try {
                    const AudioCtx = window.AudioContext || window.webkitAudioContext;
                    const ctx = new AudioCtx();
                    
                    // Romantic Melody Tone Progression (D-Major / Canon style romance notes)
                    const notes = [
                        { note: 293.66, dur: 0.40 }, // D4
                        { note: 440.00, dur: 0.40 }, // A4
                        { note: 493.88, dur: 0.40 }, // B4
                        { note: 369.99, dur: 0.40 }, // F#4
                        { note: 392.00, dur: 0.40 }, // G4
                        { note: 293.66, dur: 0.40 }, // D4
                        { note: 392.00, dur: 0.40 }, // G4
                        { note: 440.00, dur: 0.50 }, // A4
                        { note: 587.33, dur: 0.45 }, // D5
                        { note: 554.37, dur: 0.35 }, // C#5
                        { note: 493.88, dur: 0.45 }, // B4
                        { note: 440.00, dur: 0.35 }, // A4
                        { note: 392.00, dur: 0.45 }, // G4
                        { note: 369.99, dur: 0.35 }, // F#4
                        { note: 392.00, dur: 0.45 }, // G4
                        { note: 440.00, dur: 0.70 }, // A4
                    ];

                    let now = ctx.currentTime;
                    notes.forEach((item) => {
                        const osc = ctx.createOscillator();
                        const gain = ctx.createGain();
                        
                        osc.type = 'sine'; // Soft, sweet romantic tone
                        osc.frequency.setValueAtTime(item.note, now);
                        
                        gain.gain.setValueAtTime(0.001, now);
                        gain.gain.linearRampToValueAtTime(0.12, now + 0.04);
                        gain.gain.exponentialRampToValueAtTime(0.001, now + item.dur - 0.02);
                        
                        osc.connect(gain);
                        gain.connect(ctx.destination);
                        
                        osc.start(now);
                        osc.stop(now + item.dur);
                        
                        now += item.dur;
                    });
                } catch(e){}
            }

            // --- YT API SETUP UNTUK LAGU SHAPE OF MY HEART ---
            const ytDiv = document.createElement('div');
            ytDiv.id = 'ytPlayerDiv';
            ytDiv.style.display = 'none';
            document.body.appendChild(ytDiv);

            window.ytPlayerInstance = null;
            window.onYouTubeIframeAPIReady = function() {
                window.ytPlayerInstance = new YT.Player('ytPlayerDiv', {
                    height: '0',
                    width: '0',
                    videoId: 'OT5msu-dap8', // ID Youtube dari link yang Anda berikan
                    playerVars: { 'autoplay': 0, 'controls': 0 }
                });
            };

            const ytScript = document.createElement('script');
            ytScript.src = "https://www.youtube.com/iframe_api";
            document.head.appendChild(ytScript);

            function playBubbleSequence() {
                try {
                    const AudioCtx = window.AudioContext || window.webkitAudioContext;
                    const ctx = new AudioCtx();
                    
                    // Membuat rentetan suara gelembung (bubble pop) yang lucu
                    for(let i = 0; i < 7; i++) {
                        const osc = ctx.createOscillator();
                        const gain = ctx.createGain();
                        const now = ctx.currentTime + (i * 0.1); 
                        
                        osc.type = 'sine';
                        const startFreq = 300 + Math.random() * 300;
                        // Nada dinaikkan cepat untuk mensimulasikan suara "plop"
                        osc.frequency.setValueAtTime(startFreq, now);
                        osc.frequency.exponentialRampToValueAtTime(startFreq + 600, now + 0.1);
                        
                        gain.gain.setValueAtTime(0, now);
                        gain.gain.linearRampToValueAtTime(0.5, now + 0.02);
                        gain.gain.exponentialRampToValueAtTime(0.01, now + 0.1);
                        
                        osc.connect(gain);
                        gain.connect(ctx.destination);
                        
                        osc.start(now);
                        osc.stop(now + 0.1);
                    }
                } catch(e){}
            }

            let currentBigLoveSong = 1;
            const song1Btn = document.getElementById('song1Btn');
            const song2Btn = document.getElementById('song2Btn');
            
            if (song1Btn && song2Btn) {
                song1Btn.addEventListener('click', () => {
                    currentBigLoveSong = 1;
                    song1Btn.className = "px-3 py-1.5 rounded-full bg-cyber-accent text-white border border-cyber-accent shadow-[0_0_10px_rgba(139,92,246,0.5)] transition-all";
                    song2Btn.className = "px-3 py-1.5 rounded-full bg-slate-900 text-slate-400 border border-slate-700 hover:text-white transition-all";
                    if (window.ytPlayerInstance && typeof window.ytPlayerInstance.pauseVideo === 'function') {
                        window.ytPlayerInstance.pauseVideo();
                    }
                });
                song2Btn.addEventListener('click', () => {
                    currentBigLoveSong = 2;
                    song2Btn.className = "px-3 py-1.5 rounded-full bg-pink-500 text-white border border-pink-500 shadow-[0_0_10px_rgba(236,72,153,0.5)] transition-all";
                    song1Btn.className = "px-3 py-1.5 rounded-full bg-slate-900 text-slate-400 border border-slate-700 hover:text-white transition-all";
                });
            }

            function createBubbleLove(x, y) {
                const bubble = document.createElement('div');
                bubble.className = 'bubble-love';
                const size = Math.random() * 25 + 20;
                bubble.style.width = `${size}px`;
                bubble.style.height = `${size}px`;
                
                const offsetX = (Math.random() - 0.5) * 150;
                bubble.style.left = `${x + offsetX}px`;
                bubble.style.top = `${y}px`;
                
                const innerHeart = document.createElement('i');
                innerHeart.className = 'fas fa-heart';
                innerHeart.style.fontSize = `${size/2}px`;
                bubble.appendChild(innerHeart);

                document.body.appendChild(bubble);

                setTimeout(() => {
                    bubble.remove();
                }, 2500);
            }

            if (bigLoveBtn && bigLoveIcon) {
                bigLoveBtn.addEventListener('click', () => {
                    bigLoveRotation += 360;
                    
                    // Stop default ambient 90deg animation temporarily to execute 360deg spin
                    bigLoveIcon.style.animation = 'none';
                    bigLoveIcon.offsetHeight; // Trigger reflow
                    bigLoveIcon.style.transition = 'transform 0.9s cubic-bezier(0.34, 1.56, 0.64, 1)';
                    bigLoveIcon.style.transform = `rotate(${bigLoveRotation}deg) scale(1.25)`;

                    const rect = bigLoveBtn.getBoundingClientRect();
                    const centerX = rect.left + rect.width / 2;
                    const centerY = rect.top + rect.height / 2;

                    if (currentBigLoveSong === 1) {
                        // Play romantic melody tune
                        playRomanticMelody();
                        
                        // Normal hearts
                        for (let i = 0; i < 8; i++) {
                            createFloatingHeart(centerX, centerY);
                        }
                    } else if (currentBigLoveSong === 2) {
                        // Play Bubble Sound Effect
                        playBubbleSequence();
                        
                        // Emit Light (Cahaya)
                        bigLoveIcon.classList.add('emit-light');
                        setTimeout(() => bigLoveIcon.classList.remove('emit-light'), 900);

                        // Bubble Love Particles
                        for (let i = 0; i < 15; i++) {
                            setTimeout(() => {
                                createBubbleLove(centerX, centerY);
                            }, i * 50); // Keluarkan satu per satu dengan delay singkat
                        }
                    }

                    // Reset back to normal size smoothly
                    setTimeout(() => {
                        bigLoveIcon.style.transform = `rotate(${bigLoveRotation % 360}deg) scale(1)`;
                    }, 900);
                });
            }

            loveBtn.addEventListener('click', (e) => {
                // Increment total rotation by 360 degrees
                currentLoveRotation += 360;
                loveClickCount++;

                // Rotate the heart icon smoothly 360 degrees
                loveIcon.style.transform = `rotate(${currentLoveRotation}deg) scale(1.3)`;
                setTimeout(() => {
                    loveIcon.style.transform = `rotate(${currentLoveRotation}deg) scale(1)`;
                }, 300);

                // Update counter text
                loveCountEl.textContent = loveClickCount;

                // Play high pitch love chime sound
                playSoundEffect(1200, 0.15, 'triangle');

                // Spawn floating heart particles near button
                const rect = loveBtn.getBoundingClientRect();
                for (let i = 0; i < 5; i++) {
                    createFloatingHeart(rect.left + rect.width / 2, rect.top);
                }
            });

            function createFloatingHeart(x, y) {
                const heart = document.createElement('i');
                heart.className = 'fas fa-heart floating-heart text-pink-500';
                
                // Random offset
                const offsetX = (Math.random() - 0.5) * 40;
                heart.style.left = `${x + offsetX}px`;
                heart.style.top = `${y}px`;
                heart.style.fontSize = `${Math.random() * 12 + 14}px`;

                document.body.appendChild(heart);

                setTimeout(() => {
                    heart.remove();
                }, 1200);
            }

            // 6. Mobile Navigation Toggle
            const mobileMenuBtn = document.getElementById('mobileMenuBtn');
            const mobileMenu = document.getElementById('mobileMenu');

            mobileMenuBtn.addEventListener('click', () => {
                mobileMenu.classList.toggle('hidden');
            });

            document.querySelectorAll('.mobile-link').forEach(link => {
                link.addEventListener('click', () => {
                    mobileMenu.classList.add('hidden');
                });
            });

            // 7. Scroll Animation Observer
            const fadeElements = document.querySelectorAll('.fade-in-up');
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('is-visible');
                    }
                });
            }, { threshold: 0.1 });

            fadeElements.forEach(el => observer.observe(el));

            // Footer year setting
            document.getElementById('footerYear').textContent = new Date().getFullYear();

            // 8. Contact Form Handling Simulation
            const contactForm = document.getElementById('contactForm');
            const submitBtnText = document.getElementById('submitBtnText');
            const formAlert = document.getElementById('formAlert');

            contactForm.addEventListener('submit', (e) => {
                e.preventDefault();
                submitBtnText.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Mengirim...';

                setTimeout(() => {
                    submitBtnText.textContent = 'kirim Pesan';
                    formAlert.className = 'text-xs font-mono p-3 rounded bg-emerald-950 border border-emerald-500 text-emerald-400 text-center block';
                    formAlert.innerHTML = 'HTTP 200 OK — Pesan Anda telah berhasil terkirim!';
                    contactForm.reset();

                    setTimeout(() => {
                        formAlert.className = 'hidden';
                    }, 5000);
                }, 1200);
            });

        });
    </script>

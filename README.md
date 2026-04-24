<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>I LOVE U - Glowing Flower</title>
    <style>
        /* Pengaturan Dasar */
        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            background-color: #030508;
            font-family: 'Courier New', Courier, monospace;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        /* Container Utama */
        .container {
            position: relative;
            z-index: 10;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
        }

        /* Teks I LOVE U */
        h1 {
            color: #e0f7fa;
            font-size: 3rem;
            letter-spacing: 5px;
            margin-bottom: 20px;
            text-shadow: 
                0 0 5px #fff,
                0 0 10px #fff,
                0 0 20px #00e5ff,
                0 0 40px #00e5ff,
                0 0 80px #00e5ff;
            animation: pulsate 2.5s infinite alternate;
        }

        @keyframes pulsate {
            0% { opacity: 0.8; text-shadow: 0 0 5px #fff, 0 0 10px #00e5ff, 0 0 20px #00e5ff; }
            100% { opacity: 1; text-shadow: 0 0 5px #fff, 0 0 20px #00e5ff, 0 0 40px #00e5ff, 0 0 80px #00e5ff; }
        }

        /* Area Bunga & SVG */
        .flower-wrapper {
            position: relative;
            width: 300px;
            height: 400px;
            margin-bottom: 30px;
            filter: drop-shadow(0 0 10px rgba(0, 229, 255, 0.5));
        }

        svg {
            width: 100%;
            height: 100%;
            overflow: visible;
        }

        /* Animasi Menggambar Batang (Stroke) */
        .stem {
            stroke: #aaffea;
            stroke-width: 4;
            fill: transparent;
            stroke-dasharray: 1000;
            stroke-dashoffset: 1000;
            animation: drawStem 4s ease-in-out forwards;
        }

        @keyframes drawStem {
            to { stroke-dashoffset: 0; }
        }

        /* Animasi Munculnya Daun & Kelopak */
        .leaf {
            fill: #88ffdb;
            opacity: 0;
            transform-origin: 0 0;
            animation: growLeaf 1.5s ease forwards;
        }

        .center-bud {
            fill: #e0f7fa;
            opacity: 0;
            transform-origin: 0 0;
            animation: popBud 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
        }

        .petal {
            fill: #d4ffff;
            opacity: 0;
            transform-origin: 0 0;
            animation: openPetal 2.5s cubic-bezier(0.25, 1, 0.5, 1) forwards;
        }

        @keyframes growLeaf {
            0% { opacity: 0; transform: scale(0); }
            100% { opacity: 1; transform: scale(1); filter: drop-shadow(0 0 5px #00e5ff); }
        }

        @keyframes popBud {
            0% { opacity: 0; transform: scale(0); }
            100% { opacity: 1; transform: scale(1); filter: drop-shadow(0 0 10px #fff); }
        }

        @keyframes openPetal {
            /* Efek mekar: membesar dari ukuran 0 dan memutar perlahan membuka */
            0% { opacity: 0; transform: scale(0) rotate(calc(var(--r) - 45deg)); }
            60% { opacity: 1; transform: scale(1.05) rotate(calc(var(--r) + 5deg)); }
            100% { opacity: 1; transform: scale(1) rotate(var(--r)); filter: drop-shadow(0 0 8px #00e5ff); }
        }

        /* Pengaturan Urutan Waktu Mekar (Delay) */
        .f1 .center-bud { animation-delay: 2.5s; }
        .f1 .petal { animation-delay: 2.8s; }

        .f2 .center-bud { animation-delay: 3.5s; }
        .f2 .petal { animation-delay: 3.8s; }

        .f3 .center-bud { animation-delay: 4.5s; }
        .f3 .petal { animation-delay: 4.8s; }

        /* Animasi Bunga Tertiup Angin Lembut */
        .flower-group {
            transform-origin: 150px 400px; /* Titik tumpu di bawah (akar) */
            animation: sway 5s ease-in-out infinite alternate;
        }

        @keyframes sway {
            0% { transform: rotate(-3deg); }
            100% { transform: rotate(3deg); }
        }

        /* Tombol Discord */
        .discord-btn {
            padding: 12px 30px;
            color: #00e5ff;
            font-weight: bold;
            text-decoration: none;
            border: 2px solid #00e5ff;
            border-radius: 25px;
            background: transparent;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 2px;
            box-shadow: 0 0 10px rgba(0, 229, 255, 0.3), inset 0 0 10px rgba(0, 229, 255, 0.3);
            position: relative;
            overflow: hidden;
        }

        .discord-btn:hover {
            background: #00e5ff;
            color: #030508;
            box-shadow: 0 0 20px #00e5ff, 0 0 40px #00e5ff;
            transform: translateY(-2px);
        }

        /* Efek Partikel / Kunang-kunang */
        .particle {
            position: absolute;
            background: #fff;
            border-radius: 50%;
            box-shadow: 0 0 10px #fff, 0 0 20px #00e5ff;
            pointer-events: none;
            z-index: 1;
            opacity: 0;
        }

        @keyframes floatParticle {
            0% { transform: translateY(0) scale(1); opacity: 0; }
            20% { opacity: 0.8; }
            80% { opacity: 0.5; }
            100% { transform: translateY(-200px) scale(0); opacity: 0; }
        }

    </style>
</head>
<body>

    <!-- Wadah Efek Kunang-Kunang -->
    <div id="particles-container" style="position: absolute; width: 100%; height: 100%; top: 0; left: 0;"></div>

    <div class="container">
        <h1>I LOVE U</h1>
        
        <div class="flower-wrapper">
            <!-- Gambar Bunga Vektor SVG -->
            <svg viewBox="0 0 300 400">
                <g class="flower-group">
                    
                    <!-- Batang Kiri -->
                    <path class="stem" d="M 150 400 Q 100 300 80 180" />
                    <!-- Batang Tengah -->
                    <path class="stem" d="M 150 400 Q 160 250 150 100" />
                    <!-- Batang Kanan -->
                    <path class="stem" d="M 150 400 Q 200 300 220 200" />

                    <!-- Daun Batang Bawah (Fern-like) -->
                    <g transform="translate(150, 350)">
                        <path class="leaf" style="animation-delay: 1.2s;" d="M 0 0 Q -30 -10 -40 -30 Q -10 -20 0 0" />
                        <path class="leaf" style="animation-delay: 1.4s;" d="M 0 0 Q 30 -10 40 -30 Q 10 -20 0 0" />
                    </g>
                    <g transform="translate(145, 300)">
                        <path class="leaf" style="animation-delay: 1.8s;" d="M 0 0 Q -40 -15 -50 -40 Q -15 -30 0 0" />
                    </g>
                    <g transform="translate(155, 320)">
                        <path class="leaf" style="animation-delay: 2.2s;" d="M 0 0 Q 40 -15 50 -40 Q 15 -30 0 0" />
                    </g>

                    <!-- Bunga Kiri (Mekar Kedua) -->
                    <g class="f2" transform="translate(80, 180)">
                        <path class="petal" style="--r: 0deg;" d="M 0 0 Q -15 -20 0 -35 Q 15 -20 0 0" />
                        <path class="petal" style="--r: 72deg;" d="M 0 0 Q -15 -20 0 -35 Q 15 -20 0 0" />
                        <path class="petal" style="--r: 144deg;" d="M 0 0 Q -15 -20 0 -35 Q 15 -20 0 0" />
                        <path class="petal" style="--r: 216deg;" d="M 0 0 Q -15 -20 0 -35 Q 15 -20 0 0" />
                        <path class="petal" style="--r: 288deg;" d="M 0 0 Q -15 -20 0 -35 Q 15 -20 0 0" />
                        <circle class="center-bud" cx="0" cy="0" r="5" />
                    </g>

                    <!-- Bunga Tengah (Mekar Pertama) -->
                    <g class="f1" transform="translate(150, 100) scale(1.2)">
                        <path class="petal" style="--r: 0deg;" d="M 0 0 Q -15 -25 0 -40 Q 15 -25 0 0" />
                        <path class="petal" style="--r: 60deg;" d="M 0 0 Q -15 -25 0 -40 Q 15 -25 0 0" />
                        <path class="petal" style="--r: 120deg;" d="M 0 0 Q -15 -25 0 -40 Q 15 -25 0 0" />
                        <path class="petal" style="--r: 180deg;" d="M 0 0 Q -15 -25 0 -40 Q 15 -25 0 0" />
                        <path class="petal" style="--r: 240deg;" d="M 0 0 Q -15 -25 0 -40 Q 15 -25 0 0" />
                        <path class="petal" style="--r: 300deg;" d="M 0 0 Q -15 -25 0 -40 Q 15 -25 0 0" />
                        <circle class="center-bud" cx="0" cy="0" r="6" />
                    </g>

                    <!-- Bunga Kanan (Mekar Ketiga) -->
                    <g class="f3" transform="translate(220, 200)">
                        <path class="petal" style="--r: 0deg;" d="M 0 0 Q -15 -20 0 -35 Q 15 -20 0 0" />
                        <path class="petal" style="--r: 72deg;" d="M 0 0 Q -15 -20 0 -35 Q 15 -20 0 0" />
                        <path class="petal" style="--r: 144deg;" d="M 0 0 Q -15 -20 0 -35 Q 15 -20 0 0" />
                        <path class="petal" style="--r: 216deg;" d="M 0 0 Q -15 -20 0 -35 Q 15 -20 0 0" />
                        <path class="petal" style="--r: 288deg;" d="M 0 0 Q -15 -20 0 -35 Q 15 -20 0 0" />
                        <circle class="center-bud" cx="0" cy="0" r="5" />
                    </g>

                </g>
            </svg>
        </div>

        <!-- Tombol Link Menuju Discord -->
        <a href="https://discord.com/channels/1497257884952690688/1497258018843132085" target="_blank" class="discord-btn">Join Discord</a>
    </div>

    <!-- Script untuk membuat efek kunang-kunang / partikel melayang -->
    <script>
        const particlesContainer = document.getElementById('particles-container');
        const particleCount = 40; // Jumlah partikel maksimal

        function createParticle() {
            const particle = document.createElement('div');
            particle.classList.add('particle');

            // Posisi acak
            const x = Math.random() * window.innerWidth;
            const y = Math.random() * window.innerHeight * 0.8 + window.innerHeight * 0.2; // Mulai dari bawah ke tengah
            
            // Ukuran acak
            const size = Math.random() * 4 + 1;
            
            // Durasi dan delay animasi acak
            const duration = Math.random() * 3 + 3; // 3 hingga 6 detik
            const delay = Math.random() * 5;

            particle.style.left = `${x}px`;
            particle.style.top = `${y}px`;
            particle.style.width = `${size}px`;
            particle.style.height = `${size}px`;
            particle.style.animation = `floatParticle ${duration}s ease-in ${delay}s infinite`;

            particlesContainer.appendChild(particle);
        }

        // Generate partikel
        for (let i = 0; i < particleCount; i++) {
            createParticle();
        }
    </script>
</body>
</html>

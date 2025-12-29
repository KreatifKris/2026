

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>World Countdown 2026</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700;900&display=swap" rel="stylesheet">
    <style>
        /* --- CSS STYLING & ANIMATION --- */
        :root {
            --primary-color: #FFD700; /* Emas untuk highlight */
            --bg-dark: #121212;
            --text-light: #ffffff;
        }

        body {
            margin: 0;
            padding: 20px;
            font-family: 'Montserrat', sans-serif;
            background-color: var(--bg-dark);
            color: var(--text-light);
            min-height: 100vh;
        }

        header {
            text-align: center;
            margin-bottom: 40px;
            padding: 20px;
        }

        h1 {
            font-size: 3rem;
            font-weight: 900;
            text-transform: uppercase;
            letter-spacing: 3px;
            margin: 0;
            background: linear-gradient(to right, #ffffff, var(--primary-color));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: titleShine 3s infinite alternate;
        }

        /* Grid Container untuk kartu */
        .world-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 25px;
            max-width: 1400px;
            margin: 0 auto;
        }

        /* Struktur Kartu Negara */
        .country-card {
            position: relative;
            height: 300px; /* Tinggi tetap agar seragam */
            border-radius: 20px;
            overflow: hidden; /* Penting agar gambar tidak keluar batas saat di-zoom */
            box-shadow: 0 10px 20px rgba(0,0,0,0.5);
            background-color: #2a2a2a; /* Warna dasar loading */
        }

        /* Layer Gambar Latar Belakang dengan Animasi */
        .card-bg-image {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background-size: cover;
            background-position: center;
            z-index: 0;
            /* Animasi Ken Burns (Slow Zoom & Pan) */
            animation: kenBurnsEffect 25s infinite alternate ease-in-out;
        }

        /* Layer Overlay Gelap agar teks terbaca */
        .card-overlay {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(to top, rgba(0,0,0,0.9) 10%, rgba(0,0,0,0.3) 60%);
            z-index: 1;
        }

        /* Konten Teks di atas gambar */
        .card-content {
            position: relative;
            z-index: 2;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: flex-end; /* Teks di bagian bawah */
            padding: 25px;
            box-sizing: border-box;
        }

        .location-title {
            font-size: 1.8rem;
            font-weight: 700;
            margin: 0;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.8);
        }

        .timezone-sub {
            font-size: 0.9rem;
            color: var(--primary-color);
            margin-bottom: 15px;
            font-weight: 400;
        }

        /* Styling Timer */
        .timer-box {
            display: flex;
            gap: 10px;
        }

        .time-segment {
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(5px);
            padding: 8px 12px;
            border-radius: 8px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.2);
            flex: 1;
        }

        .time-num {
            display: block;
            font-size: 1.5rem;
            font-weight: 900;
            font-variant-numeric: tabular-nums; /* Agar lebar angka konsisten */
        }

        .time-label {
            font-size: 0.6rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            opacity: 0.8;
        }

        /* Pesan Selamat Tahun Baru */
        .celebration-msg {
            display: none; /* Hidden by default */
            color: var(--primary-color);
            font-size: 1.4rem;
            font-weight: 900;
            text-align: center;
            animation: pulseText 1s infinite;
        }

        /* --- KEYFRAME ANIMATIONS --- */
        @keyframes kenBurnsEffect {
            0% { transform: scale(1) translate(0, 0); }
            50% { transform: scale(1.1) translate(-2%, 1%); }
            100% { transform: scale(1.2) translate(1%, -2%); }
        }

        @keyframes titleShine {
            from { filter: brightness(100%); }
            to { filter: brightness(130%); text-shadow: 0 0 20px var(--primary-color); }
        }

        @keyframes pulseText {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.7; transform: scale(0.95); }
        }

        /* Responsif untuk layar kecil */
        @media (max-width: 600px) {
            h1 { font-size: 2rem; }
            .world-grid { grid-template-columns: 1fr; }
            .country-card { height: 250px; }
            .time-num { font-size: 1.2rem; }
        }
    </style>
</head>
<body>

    <header>
        <h1>🌏 Menuju Tahun 2026</h1>
    </header>

    <main class="world-grid" id="grid-container">
        </main>

    <script>
        // --- KONFIGURASI DATA ---
        // Saya menggunakan gambar dari Unsplash Source untuk kualitas tinggi.
        // Setiap objek merepresentasikan satu lokasi.
        const locationsData = [
            {
                city: "Jakarta",
                country: "Indonesia (WIB)",
                zone: "Asia/Jakarta",
                // Gambar Monas/Jakarta
                imgUrl: "https://images.unsplash.com/photo-1568226363616-6e4988582725?q=80&w=800&auto=format&fit=crop"
            },
            {
                city: "Bali",
                country: "Indonesia (WITA)",
                zone: "Asia/Makassar",
                // Gambar Pura Ulun Danu Bratan
                imgUrl: "https://images.unsplash.com/photo-1537996194471-e657df975ab4?q=80&w=800&auto=format&fit=crop"
            },
            {
                city: "Tokyo",
                country: "Jepang",
                zone: "Asia/Tokyo",
                // Gambar Gunung Fuji & Pagoda Chureito
                imgUrl: "https://images.unsplash.com/photo-1524413840807-0c3cb6fa808d?q=80&w=800&auto=format&fit=crop"
            },
            {
                city: "Sydney",
                country: "Australia",
                zone: "Australia/Sydney",
                // Gambar Sydney Opera House
                imgUrl: "https://images.unsplash.com/photo-1506973035872-a47069f6d711?q=80&w=800&auto=format&fit=crop"
            },
            {
                city: "Dubai",
                country: "Uni Emirat Arab",
                zone: "Asia/Dubai",
                // Gambar Burj Khalifa
                imgUrl: "https://images.unsplash.com/photo-1512453979798-5ea266f8880c?q=80&w=800&auto=format&fit=crop"
            },
            {
                city: "Paris",
                country: "Prancis",
                zone: "Europe/Paris",
                // Gambar Menara Eiffel
                imgUrl: "https://images.unsplash.com/photo-1502602898657-3e91760cbb34?q=80&w=800&auto=format&fit=crop"
            },
            {
                city: "London",
                country: "Inggris",
                zone: "Europe/London",
                // Gambar Big Ben
                imgUrl: "https://images.unsplash.com/photo-1529655683826-aba9b3e77383?q=80&w=800&auto=format&fit=crop"
            },
            {
                city: "New York",
                country: "Amerika Serikat",
                zone: "America/New_York",
                // Gambar Patung Liberty / Skyline NYC
                imgUrl: "https://images.unsplash.com/photo-1496442226666-8d4d0e62e6e9?q=80&w=800&auto=format&fit=crop"
            }
        ];

        const TARGET_YEAR = 2026;
        const container = document.getElementById('grid-container');

        // --- FUNGSI INISIALISASI (Membuat HTML) ---
        function createCards() {
            locationsData.forEach((loc, index) => {
                const cardHTML = `
                    <div class="country-card">
                        <div class="card-bg-image" style="background-image: url('${loc.imgUrl}')"></div>
                        
                        <div class="card-overlay"></div>
                        
                        <div class="card-content">
                            <h2 class="location-title">${loc.city}, ${loc.country}</h2>
                            <div class="timezone-sub">${loc.zone}</div>
                            
                            <div class="timer-box" id="timer-box-${index}">
                                <div class="time-segment">
                                    <span class="time-num" id="d-${index}">00</span>
                                    <span class="time-label">Hari</span>
                                </div>
                                <div class="time-segment">
                                    <span class="time-num" id="h-${index}">00</span>
                                    <span class="time-label">Jam</span>
                                </div>
                                <div class="time-segment">
                                    <span class="time-num" id="m-${index}">00</span>
                                    <span class="time-label">Mnt</span>
                                </div>
                                <div class="time-segment">
                                    <span class="time-num" id="s-${index}">00</span>
                                    <span class="time-label">Dtk</span>
                                </div>
                            </div>
                             <div class="celebration-msg" id="msg-${index}">
                                🎉 HAPPY NEW YEAR 2026! 🎆
                            </div>
                        </div>
                    </div>
                `;
                // Menambahkan string HTML ke container
                container.insertAdjacentHTML('beforeend', cardHTML);
            });
        }

        // --- FUNGSI UPDATE TIMER (Logika Waktu) ---
        function updateAllTimers() {
            const now = new Date();

            locationsData.forEach((loc, index) => {
                // 1. Mendapatkan waktu saat ini di Zona Waktu target
                // Trik: Ubah waktu browser ke string waktu lokal zona tersebut
                const nowInTargetZoneStr = now.toLocaleString('en-US', { timeZone: loc.zone });
                const nowInTargetZone = new Date(nowInTargetZoneStr);

                // 2. Tentukan target waktu: 1 Januari 2026, 00:00:00 di zona tersebut
                const targetDate = new Date(TARGET_YEAR, 0, 1, 0, 0, 0); // Bulan dimulai dari 0 (Jan = 0)

                // 3. Hitung selisih (milidetik)
                const diff = targetDate - nowInTargetZone;

                const timerBoxEl = document.getElementById(`timer-box-${index}`);
                const msgEl = document.getElementById(`msg-${index}`);

                if (diff <= 0) {
                    // Waktu Habis / Sudah Tahun Baru
                    if (timerBoxEl.style.display !== 'none') {
                        timerBoxEl.style.display = 'none';
                        msgEl.style.display = 'block';
                    }
                } else {
                    // Kalkulasi matematik standar
                    const days = Math.floor(diff / (1000 * 60 * 60 * 24));
                    const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                    const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
                    const seconds = Math.floor((diff % (1000 * 60)) / 1000);

                    // Update angka di HTML, tambahkan '0' di depan jika satuan
                    document.getElementById(`d-${index}`).textContent = days;
                    document.getElementById(`h-${index}`).textContent = String(hours).padStart(2, '0');
                    document.getElementById(`m-${index}`).textContent = String(minutes).padStart(2, '0');
                    document.getElementById(`s-${index}`).textContent = String(seconds).padStart(2, '0');
                }
            });
        }

        // --- JALANKAN PROGRAM ---
        createCards(); // Buat struktur HTML dulu
        updateAllTimers(); // Jalankan sekali agar tidak delay saat loading
        setInterval(updateAllTimers, 1000); // Update setiap detik
    </script>
</body>

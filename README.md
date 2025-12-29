
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Countdown Menuju 2026 - Global</title>
    <style>
        /* --- CSS STYLING --- */
        :root {
            --bg-color: #0f172a;
            --card-bg: #1e293b;
            --text-color: #f8fafc;
            --accent-color: #38bdf8;
            --completed-color: #4ade80;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
        }

        h1 {
            text-align: center;
            margin-bottom: 40px;
            font-size: 2.5rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            text-shadow: 0 0 10px rgba(56, 189, 248, 0.5);
        }

        .grid-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            width: 100%;
            max-width: 1200px;
        }

        .card {
            background-color: var(--card-bg);
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: transform 0.3s ease;
        }

        .card:hover {
            transform: translateY(-5px);
            border-color: var(--accent-color);
        }

        .city-name {
            font-size: 1.5rem;
            font-weight: bold;
            margin-bottom: 5px;
            color: var(--accent-color);
        }

        .timezone-info {
            font-size: 0.8rem;
            color: #94a3b8;
            margin-bottom: 20px;
        }

        .timer {
            display: flex;
            justify-content: center;
            gap: 10px;
            font-family: 'Courier New', Courier, monospace;
        }

        .time-unit {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .number {
            font-size: 2rem;
            font-weight: bold;
            background: rgba(0, 0, 0, 0.3);
            padding: 10px;
            border-radius: 8px;
            min-width: 50px;
            display: inline-block;
        }

        .label {
            font-size: 0.7rem;
            margin-top: 5px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .celebration {
            display: none;
            color: var(--completed-color);
            font-weight: bold;
            font-size: 1.2rem;
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }

        footer {
            margin-top: 50px;
            font-size: 0.8rem;
            color: #64748b;
        }
    </style>
</head>
<body>

    <h1>Countdown Menuju 2026 🎆</h1>

    <div class="grid-container" id="countdown-grid">
        </div>

    <footer>
        Dibuat secara otomatis dengan HTML, CSS & JS
    </footer>

    <script>
        // --- KONFIGURASI KOTA & ZONA WAKTU ---
        // Anda bisa menambah atau menghapus kota di sini
        // Gunakan format IANA Timezone (contoh: 'Asia/Jakarta')
        const locations = [
            { city: 'Sydney', country: 'Australia', zone: 'Australia/Sydney' },
            { city: 'Tokyo', country: 'Jepang', zone: 'Asia/Tokyo' },
            { city: 'Jakarta', country: 'Indonesia (WIB)', zone: 'Asia/Jakarta' },
            { city: 'Bali', country: 'Indonesia (WITA)', zone: 'Asia/Makassar' }, // Makassar mewakili WITA
            { city: 'London', country: 'Inggris', zone: 'Europe/London' },
            { city: 'New York', country: 'USA', zone: 'America/New_York' },
            { city: 'Los Angeles', country: 'USA', zone: 'America/Los_Angeles' }
        ];

        const targetYear = 2026;

        function initCountdowns() {
            const container = document.getElementById('countdown-grid');
            
            // Generate HTML untuk setiap lokasi
            locations.forEach((loc, index) => {
                const card = document.createElement('div');
                card.className = 'card';
                card.innerHTML = `
                    <div class="city-name">${loc.city}</div>
                    <div class="timezone-info">${loc.country}</div>
                    <div class="timer" id="timer-${index}">
                        <div class="time-unit">
                            <span class="number" id="d-${index}">00</span>
                            <span class="label">Hari</span>
                        </div>
                        <div class="time-unit">
                            <span class="number" id="h-${index}">00</span>
                            <span class="label">Jam</span>
                        </div>
                        <div class="time-unit">
                            <span class="number" id="m-${index}">00</span>
                            <span class="label">Menit</span>
                        </div>
                        <div class="time-unit">
                            <span class="number" id="s-${index}">00</span>
                            <span class="label">Detik</span>
                        </div>
                    </div>
                    <div class="celebration" id="msg-${index}">
                        🎉 SELAMAT TAHUN BARU 2026! 🎉
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function updateTimers() {
            const now = new Date();

            locations.forEach((loc, index) => {
                // 1. Dapatkan waktu saat ini di zona waktu target
                // Kita mengonversi waktu 'now' ke string waktu lokal zona tersebut
                const nowInZoneString = now.toLocaleString('en-US', { timeZone: loc.zone });
                const nowInZone = new Date(nowInZoneString);

                // 2. Buat target waktu (1 Januari 2026, 00:00:00)
                // Kita asumsikan targetnya adalah relatif terhadap waktu lokal zona tersebut
                const targetDate = new Date(`January 1, ${targetYear} 00:00:00`);

                // 3. Hitung selisih
                const diff = targetDate - nowInZone;

                const timerEl = document.getElementById(`timer-${index}`);
                const msgEl = document.getElementById(`msg-${index}`);

                if (diff <= 0) {
                    // Jika waktu habis (sudah tahun baru di sana)
                    timerEl.style.display = 'none';
                    msgEl.style.display = 'block';
                } else {
                    // Kalkulasi waktu
                    const days = Math.floor(diff / (1000 * 60 * 60 * 24));
                    const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                    const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
                    const seconds = Math.floor((diff % (1000 * 60)) / 1000);

                    // Update DOM
                    document.getElementById(`d-${index}`).innerText = days;
                    document.getElementById(`h-${index}`).innerText = hours < 10 ? '0' + hours : hours;
                    document.getElementById(`m-${index}`).innerText = minutes < 10 ? '0' + minutes : minutes;
                    document.getElementById(`s-${index}`).innerText = seconds < 10 ? '0' + seconds : seconds;
                }
            });
        }

        // Jalankan inisialisasi
        initCountdowns();
        
        // Jalankan update pertama kali agar tidak ada delay 1 detik
        updateTimers();

        // Set interval update setiap 1 detik
        setInterval(updateTimers, 1000);

    </script>
</body>

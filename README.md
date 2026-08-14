<!DOCTYPE html>
<html lang="hu">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Maci kérdése</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(145deg, #ffe6f0 0%, #ffccdd 100%);
            font-family: 'Segoe UI', 'Helvetica Neue', Arial, sans-serif;
            padding: 20px;
            transition: all 0.5s ease;
        }

        /* ========== 1. OLDAL - KÉRDÉS ========== */
        .page {
            display: none;
            width: 100%;
            max-width: 600px;
            animation: fadeIn 0.6s ease;
        }

        .page.active {
            display: block;
        }

        @keyframes fadeIn {
            0% { opacity: 0; transform: translateY(30px) scale(0.95); }
            100% { opacity: 1; transform: translateY(0) scale(1); }
        }

        .card {
            width: 100%;
            background: white;
            border-radius: 50px 50px 40px 40px;
            padding: 40px 30px 45px;
            box-shadow: 0 25px 50px -10px rgba(200, 80, 120, 0.3);
            text-align: center;
            border: 2px solid rgba(255, 255, 255, 0.5);
        }

        /* MACI */
        .bear {
            position: relative;
            display: inline-block;
            margin-bottom: 20px;
        }

        .bear-emoji {
            font-size: 130px;
            line-height: 1;
            display: block;
            filter: drop-shadow(0 10px 15px rgba(150, 70, 90, 0.2));
            transition: all 0.3s ease;
        }

        .heart {
            position: absolute;
            bottom: 8px;
            right: -5px;
            font-size: 48px;
            animation: heartbeat 1.4s ease-in-out infinite;
            filter: drop-shadow(0 4px 8px rgba(255, 50, 80, 0.4));
        }

        @keyframes heartbeat {
            0%, 100% { transform: scale(1); }
            15% { transform: scale(1.25); }
            30% { transform: scale(1); }
            45% { transform: scale(1.15); }
            60% { transform: scale(1); }
        }

        h1 {
            font-size: 2.2rem;
            font-weight: 700;
            color: #4a2c3a;
            margin: 15px 0 35px;
            letter-spacing: -0.5px;
            line-height: 1.2;
        }

        h1 span {
            background: linear-gradient(135deg, #f9a8c8, #f472b6);
            padding: 0 12px;
            border-radius: 40px;
            color: white;
            display: inline-block;
            box-shadow: 0 4px 12px rgba(244, 114, 182, 0.3);
        }

        .buttons {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 40px;
            flex-wrap: wrap;
            margin-top: 10px;
            min-height: 100px;
        }

        .btn {
            border: none;
            font-weight: 700;
            border-radius: 60px;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
            letter-spacing: 0.5px;
            box-shadow: 0 8px 18px rgba(0, 0, 0, 0.06);
            padding: 16px 48px;
            font-size: 1.5rem;
            min-width: 100px;
        }

        .btn-yes {
            background: #4caf84;
            color: white;
            box-shadow: 0 8px 20px rgba(76, 175, 132, 0.35);
        }

        .btn-yes:hover {
            background: #3d9d75;
            box-shadow: 0 12px 28px rgba(76, 175, 132, 0.45);
        }

        .btn-no {
            background: #f2f2f2;
            color: #5a4a4a;
            box-shadow: 0 8px 18px rgba(0, 0, 0, 0.04);
            min-width: 80px;
        }

        .btn-no:hover {
            background: #e5e5e5;
        }

        .no-message {
            margin-top: 20px;
            font-size: 1.3rem;
            font-weight: 600;
            color: #d45a7a;
            min-height: 50px;
            padding: 10px 16px;
            border-radius: 50px;
            display: inline-block;
            opacity: 0;
            transform: translateY(10px);
            transition: all 0.3s ease;
        }

        .no-message.show {
            opacity: 1;
            transform: translateY(0);
        }

        .no-message.crying {
            animation: shake 0.5s ease;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            20% { transform: translateX(-10px); }
            40% { transform: translateX(10px); }
            60% { transform: translateX(-6px); }
            80% { transform: translateX(6px); }
        }

        /* ========== 2. OLDAL - NAPTÁR ========== */
        .page-date .card {
            padding: 35px 25px 40px;
        }

        .page-date h2 {
            font-size: 2rem;
            color: #4a2c3a;
            margin-bottom: 10px;
        }

        .page-date .subtitle {
            font-size: 1.1rem;
            color: #7a5a6a;
            margin-bottom: 25px;
        }

        .calendar-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 8px;
            max-width: 450px;
            margin: 0 auto 25px;
        }

        .calendar-header {
            font-weight: 700;
            color: #d45a7a;
            font-size: 0.85rem;
            padding: 8px 0;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .calendar-day {
            aspect-ratio: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.1rem;
            font-weight: 600;
            border-radius: 16px;
            background: #faf0f4;
            color: #4a2c3a;
            cursor: pointer;
            transition: all 0.25s ease;
            border: 2px solid transparent;
            position: relative;
            user-select: none;
        }

        .calendar-day.empty {
            background: transparent;
            cursor: default;
        }

        .calendar-day:not(.empty):hover {
            background: #f9d4e0;
            transform: scale(1.05);
            border-color: #f472b6;
        }

        .calendar-day.selected {
            background: #4caf84;
            color: white;
            border-color: #3d9d75;
            transform: scale(1.08);
            box-shadow: 0 6px 20px rgba(76, 175, 132, 0.35);
        }

        .calendar-day.selected:hover {
            background: #3d9d75;
        }

        .calendar-day .emoji-bear {
            position: absolute;
            bottom: -4px;
            right: -4px;
            font-size: 0.6rem;
        }

        .calendar-day.locked {
            cursor: default;
            opacity: 0.6;
            pointer-events: none;
        }

        .calendar-day.locked.selected {
            opacity: 1;
            pointer-events: none;
        }

        .selected-date-display {
            font-size: 1.1rem;
            color: #4a2c3a;
            margin: 10px 0 5px;
            min-height: 30px;
            font-weight: 500;
        }

        .selected-date-display span {
            color: #d45a7a;
            font-weight: 700;
        }

        .btn-confirm {
            background: linear-gradient(135deg, #f9a8c8, #f472b6);
            color: white;
            border: none;
            padding: 16px 50px;
            font-size: 1.3rem;
            font-weight: 700;
            border-radius: 60px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 8px 25px rgba(244, 114, 182, 0.3);
            opacity: 0.5;
            pointer-events: none;
            margin-top: 5px;
        }

        .btn-confirm.active {
            opacity: 1;
            pointer-events: auto;
        }

        .btn-confirm.active:hover {
            transform: scale(1.05);
            box-shadow: 0 12px 35px rgba(244, 114, 182, 0.45);
        }

        .btn-confirm.active:active {
            transform: scale(0.95);
        }

        .btn-confirm.hidden {
            display: none;
        }

        .btn-back {
            background: transparent;
            border: 2px solid #e0c8d0;
            color: #7a5a6a;
            padding: 10px 24px;
            font-size: 0.95rem;
            border-radius: 40px;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 15px;
        }

        .btn-back:hover {
            background: #f5e8ec;
            border-color: #d45a7a;
        }

        /* ========== 3. OLDAL - FILM ========== */
        .page-movie .card {
            padding: 45px 30px 50px;
            background: linear-gradient(145deg, #1a0a1a, #2d1a2d);
            border: 3px solid #f472b6;
            box-shadow: 0 30px 60px -15px rgba(200, 50, 100, 0.5);
        }

        .page-movie .bear-emoji {
            font-size: 150px;
            filter: drop-shadow(0 0 30px rgba(244, 114, 182, 0.3));
        }

        .page-movie .heart {
            font-size: 55px;
            animation: heartbeat 0.8s ease-in-out infinite;
        }

        .movie-title {
            font-size: 2.8rem;
            font-weight: 900;
            color: #fff;
            margin: 20px 0 15px;
            line-height: 1.2;
            text-shadow: 0 0 30px rgba(244, 114, 182, 0.3);
        }

        .movie-title .highlight {
            background: linear-gradient(135deg, #f9a8c8, #f472b6, #ec4899);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            display: inline-block;
            animation: shimmer 2s ease-in-out infinite;
        }

        @keyframes shimmer {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .movie-emoji {
            font-size: 4rem;
            margin: 10px 0;
            display: inline-block;
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(-5deg); }
            50% { transform: translateY(-15px) rotate(5deg); }
        }

        .movie-sub {
            font-size: 1.2rem;
            color: #f9d4e0;
            margin-top: 10px;
            opacity: 0.8;
        }

        .movie-date-display {
            font-size: 1.1rem;
            color: #f9a8c8;
            background: rgba(255, 255, 255, 0.08);
            padding: 10px 24px;
            border-radius: 40px;
            display: inline-block;
            margin: 15px 0 20px;
            border: 1px solid rgba(244, 114, 182, 0.2);
        }

        .btn-restart {
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid #f472b6;
            color: #f9d4e0;
            padding: 12px 30px;
            font-size: 1rem;
            border-radius: 40px;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 10px;
        }

        .btn-restart:hover {
            background: rgba(244, 114, 182, 0.2);
            transform: scale(1.05);
        }

        /* KONFETTI (CSS) */
        .confetti-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 999;
            overflow: hidden;
        }

        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            border-radius: 2px;
            animation: confettiFall linear forwards;
        }

        @keyframes confettiFall {
            0% {
                transform: translateY(-10vh) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(110vh) rotate(720deg);
                opacity: 0;
            }
        }

        /* MOBIL */
        @media (max-width: 480px) {
            .card { padding: 30px 18px 35px; }
            h1 { font-size: 1.7rem; }
            .bear-emoji { font-size: 100px; }
            .heart { font-size: 36px; bottom: 5px; right: 0; }
            .btn { padding: 14px 28px; font-size: 1.2rem; min-width: 80px; }
            .buttons { gap: 25px; }

            .calendar-grid { gap: 5px; max-width: 100%; }
            .calendar-day { font-size: 0.95rem; border-radius: 12px; }
            .page-date h2 { font-size: 1.6rem; }
            .btn-confirm { padding: 14px 30px; font-size: 1.1rem; }

            .movie-title { font-size: 2rem; }
            .page-movie .bear-emoji { font-size: 110px; }
            .movie-emoji { font-size: 3rem; }
            .page-movie .heart { font-size: 40px; }
        }

        @media (max-width: 380px) {
            .calendar-day { font-size: 0.8rem; border-radius: 10px; }
            .calendar-header { font-size: 0.7rem; }
            .movie-title { font-size: 1.6rem; }
        }
    </style>
</head>
<body>

    <!-- ==================== KONFETTI TÁROLÓ ==================== -->
    <div class="confetti-container" id="confettiContainer"></div>

    <!-- ==================== 1. OLDAL: KÉRDÉS ==================== -->
    <div class="page active" id="pageQuestion">
        <div class="card">
            <div class="bear">
                <span class="bear-emoji">🧸</span>
                <span class="heart">❤️</span>
            </div>

            <h1>
                Will you go <br><span>on a date</span> with me?
            </h1>

            <div class="buttons">
                <button class="btn btn-yes" id="yesBtn">Yes</button>
                <button class="btn btn-no" id="noBtn">No</button>
            </div>

            <div id="noMessage" class="no-message"></div>
        </div>
    </div>

    <!-- ==================== 2. OLDAL: NAPTÁR ==================== -->
    <div class="page page-date" id="pageDate">
        <div class="card">
            <div class="bear">
                <span class="bear-emoji">🧸</span>
                <span class="heart">❤️</span>
            </div>

            <h2>📅 Pick a date</h2>
            <p class="subtitle">Choose a day for our special date! ✨</p>

            <div class="calendar-grid" id="calendarGrid"></div>

            <div class="selected-date-display">
                💕 <span id="dateText">No date selected yet</span>
            </div>

            <button class="btn-confirm" id="confirmDateBtn">✅ Let's go! 🥰</button>

            <button class="btn-back" id="backBtn">⬅ Back</button>
        </div>
    </div>

    <!-- ==================== 3. OLDAL: FILM ==================== -->
    <div class="page page-movie" id="pageMovie">
        <div class="card">
            <div class="bear">
                <span class="bear-emoji">🧸</span>
                <span class="heart">💖</span>
            </div>

            <div class="movie-emoji">🎬🍿</div>

            <div class="movie-title">
                We are gonna see a <br>
                <span class="highlight">movie in 4DX!!</span>
            </div>

            <div class="movie-emoji" style="animation-delay: 0.5s;">🤩🤩</div>

            <div class="movie-date-display" id="movieDateDisplay">
                📅 <span id="movieDateText">Loading...</span>
            </div>

            <div class="movie-sub">✨ It's gonna be amazing! ✨</div>

            <button class="btn-restart" id="restartBtn">🔄 Start over</button>
        </div>
    </div>

    <script>
        // ============================================================
        // 1. OLDAL: KÉRDÉS LOGIKA
        // ============================================================
        const yesBtn = document.getElementById('yesBtn');
        const noBtn = document.getElementById('noBtn');
        const noMessage = document.getElementById('noMessage');
        const pageQuestion = document.getElementById('pageQuestion');
        const pageDate = document.getElementById('pageDate');
        const pageMovie = document.getElementById('pageMovie');

        const messages = [
            "Wrong answer 😤",
            "Don't do this 😠",
            "I'm gonna cry 😢",
            "Please? 🥺",
            "I'll be sad 💔",
            "One more time? 🙏",
            "You're breaking my heart 💔😭",
            "OK, I'll wait... ⏳",
            "Pretty please? 🥺👉👈",
            "I'll bring flowers 🌸",
            "Just say yes! 😩",
            "I'm not giving up! 💪",
            "My heart hurts 💔",
            "Please, for me? 🥹",
            "I'll be so happy! 🥰",
            "Don't be so mean! 😭",
            "I'll cry a river 🌊😭",
            "You're my only hope! 🌟",
            "I love you! ❤️",
            "OK, I'll keep asking... 🔄"
        ];

        let noCount = 0;
        let yesClicked = false;

        function updateButtonSizes() {
            const yesScale = 1 + (noCount * 0.15);
            yesBtn.style.transform = `scale(${yesScale})`;
            yesBtn.style.fontSize = `${1.5 + (noCount * 0.12)}rem`;
            yesBtn.style.padding = `${16 + (noCount * 2)}px ${48 + (noCount * 4)}px`;

            const noScale = Math.max(0.1, 1 - (noCount * 0.12));
            noBtn.style.transform = `scale(${noScale})`;
            noBtn.style.fontSize = `${Math.max(0.6, 1.5 - (noCount * 0.1))}rem`;
            noBtn.style.padding = `${Math.max(4, 16 - (noCount * 1.2))}px ${Math.max(10, 48 - (noCount * 3.5))}px`;
            noBtn.style.minWidth = `${Math.max(30, 80 - (noCount * 4))}px`;
            noBtn.style.opacity = Math.max(0.1, 1 - (noCount * 0.04));

            if (noScale < 0.05) {
                noBtn.style.minWidth = '5px';
                noBtn.style.padding = '2px 4px';
                noBtn.style.fontSize = '0.3rem';
            }
        }

        function showNoMessage(text) {
            noMessage.textContent = text;
            noMessage.className = 'no-message show crying';
            const bear = document.querySelector('#pageQuestion .bear');
            bear.style.animation = 'shake 0.5s ease';
            setTimeout(() => { bear.style.animation = ''; }, 500);
        }

        function goToDatePage() {
            yesClicked = true;
            pageQuestion.classList.remove('active');
            pageDate.classList.add('active');
            generateCalendar();
            document.querySelector('#pageDate .bear-emoji').textContent = '🧸✨';
        }

        yesBtn.addEventListener('click', goToDatePage);

        noBtn.addEventListener('click', () => {
            if (yesClicked) return;
            noCount++;
            const messageIndex = Math.min(noCount - 1, messages.length - 1);
            showNoMessage(messages[messageIndex]);
            updateButtonSizes();

            if (noCount >= 10) {
                document.querySelector('#pageQuestion .bear-emoji').textContent = '😭';
                document.querySelector('#pageQuestion .heart').style.animation = 'none';
                document.querySelector('#pageQuestion .heart').textContent = '💔';
            }
            if (noCount >= 20) {
                noBtn.style.minWidth = '1px';
                noBtn.style.padding = '1px 2px';
                noBtn.style.fontSize = '0.1rem';
                noBtn.style.opacity = '0.05';
            }
        });

        document.getElementById('backBtn').addEventListener('click', () => {
            pageDate.classList.remove('active');
            pageQuestion.classList.add('active');
            document.querySelector('#pageQuestion .bear-emoji').textContent = '🧸';
            document.querySelector('#pageQuestion .heart').style.animation = 'heartbeat 1.4s ease-in-out infinite';
            document.querySelector('#pageQuestion .heart').textContent = '❤️';
        });

        // ============================================================
        // 2. OLDAL: NAPTÁR LOGIKA
        // ============================================================
        const calendarGrid = document.getElementById('calendarGrid');
        const dateText = document.getElementById('dateText');
        const confirmBtn = document.getElementById('confirmDateBtn');
        const movieDateText = document.getElementById('movieDateText');

        let selectedDate = null;

        const startDate = new Date(2026, 7, 15);
        const endDate = new Date(2026, 8, 1);
        const totalDays = Math.floor((endDate - startDate) / (1000 * 60 * 60 * 24)) + 1;
        const weekdays = ['H', 'K', 'Sze', 'Cs', 'P', 'Szo', 'V'];

        function generateCalendar() {
            calendarGrid.innerHTML = '';

            weekdays.forEach(day => {
                const header = document.createElement('div');
                header.className = 'calendar-header';
                header.textContent = day;
                calendarGrid.appendChild(header);
            });

            const date15 = new Date(2026, 7, 15);
            const dayOffset = date15.getDay();

            for (let i = 0; i < dayOffset; i++) {
                const empty = document.createElement('div');
                empty.className = 'calendar-day empty';
                calendarGrid.appendChild(empty);
            }

            for (let i = 0; i < totalDays; i++) {
                const currentDate = new Date(2026, 7, 15 + i);
                const day = currentDate.getDate();
                const month = currentDate.getMonth();
                const year = currentDate.getFullYear();

                const dayEl = document.createElement('div');
                dayEl.className = 'calendar-day';
                dayEl.textContent = day;

                const isSept1 = (month === 8 && day === 1);
                const dateStr = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                dayEl.dataset.date = dateStr;

                if (isSept1) {
                    const bearIcon = document.createElement('span');
                    bearIcon.className = 'emoji-bear';
                    bearIcon.textContent = '🧸';
                    dayEl.appendChild(bearIcon);
                }

                dayEl.addEventListener('click', () => {
                    if (document.querySelector('.calendar-day.locked')) return;
                    document.querySelector('.calendar-day.selected')?.classList.remove('selected');
                    dayEl.classList.add('selected');
                    selectedDate = dateStr;

                    const options = { year: 'numeric', month: 'long', day: 'numeric', weekday: 'long' };
                    const formatted = new Date(dateStr).toLocaleDateString('hu-HU', options);
                    dateText.textContent = formatted;

                    confirmBtn.classList.add('active');
                });

                calendarGrid.appendChild(dayEl);
            }

            confirmBtn.classList.remove('active');
            dateText.textContent = 'No date selected yet';
        }

        // ============================================================
        // KONFETTI
        // ============================================================
        function launchConfetti() {
            const container = document.getElementById('confettiContainer');
            const colors = ['#f472b6', '#f9a8c8', '#ec4899', '#fbbf24', '#34d399', '#60a5fa', '#a78bfa', '#fb923c'];

            for (let i = 0; i < 120; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * 100 + '%';
                confetti.style.width = Math.random() * 8 + 4 + 'px';
                confetti.style.height = Math.random() * 8 + 4 + 'px';
                confetti.style.background = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.borderRadius = Math.random() > 0.5 ? '50%' : '2px';
                confetti.style.animationDuration = Math.random() * 2 + 2 + 's';
                confetti.style.animationDelay = Math.random() * 1.5 + 's';
                container.appendChild(confetti);

                setTimeout(() => {
                    confetti.remove();
                }, 5000);
            }
        }

        // ============================================================
        // 3. OLDAL: FILM MEGJELENÍTÉS
        // ============================================================
        function showMoviePage(dateStr) {
            pageDate.classList.remove('active');
            pageMovie.classList.add('active');

            const options = { year: 'numeric', month: 'long', day: 'numeric', weekday: 'long' };
            const formatted = new Date(dateStr).toLocaleDateString('hu-HU', options);
            movieDateText.textContent = formatted;

            // Konfetti
            setTimeout(launchConfetti, 300);
            setTimeout(launchConfetti, 1000);
            setTimeout(launchConfetti, 2000);

            // Extra boldog maci
            document.querySelector('#pageMovie .bear-emoji').textContent = '🧸🥳';
            document.querySelector('#pageMovie .heart').style.animation = 'heartbeat 0.5s ease-in-out infinite';
        }

        // ============================================================
        // CONFIRM GOMB
        // ============================================================
        confirmBtn.addEventListener('click', () => {
            if (!selectedDate) return;

            // Összes nap lockolása
            document.querySelectorAll('.calendar-day:not(.empty)').forEach(el => {
                el.classList.add('locked');
            });

            confirmBtn.classList.add('hidden');

            // Film oldal megjelenítése
            showMoviePage(selectedDate);
        });

        // ============================================================
        // RESTART
        // ============================================================
        document.getElementById('restartBtn').addEventListener('click', () => {
            // Visszaállítás
            pageMovie.classList.remove('active');
            pageQuestion.classList.add('active');

            // Minden visszaállít
            yesClicked = false;
            noCount = 0;
            selectedDate = null;

            // Gombok visszaállítása
            yesBtn.style.transform = 'scale(1)';
            yesBtn.style.fontSize = '1.5rem';
            yesBtn.style.padding = '16px 48px';

            noBtn.style.transform = 'scale(1)';
            noBtn.style.fontSize = '1.5rem';
            noBtn.style.padding = '16px 48px';
            noBtn.style.minWidth = '80px';
            noBtn.style.opacity = '1';
            noBtn.style.display = 'inline-block';

            noMessage.className = 'no-message';
            noMessage.textContent = '';

            document.querySelector('#pageQuestion .bear-emoji').textContent = '🧸';
            document.querySelector('#pageQuestion .heart').textContent = '❤️';
            document.querySelector('#pageQuestion .heart').style.animation = 'heartbeat 1.4s ease-in-out infinite';

            confirmBtn.classList.remove('hidden');
            confirmBtn.classList.remove('active');
            confirmBtn.textContent = '✅ Let\'s go! 🥰';

            document.querySelector('#pageDate .bear-emoji').textContent = '🧸';

            // Konfetti eltüntetése
            document.getElementById('confettiContainer').innerHTML = '';

            // Naptár újragenerálása
            generateCalendar();
        });

        // ============================================================
        // KEYBOARD SHORTCUTS
        // ============================================================
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape') {
                if (pageMovie.classList.contains('active')) {
                    document.getElementById('restartBtn').click();
                } else if (pageDate.classList.contains('active')) {
                    document.getElementById('backBtn').click();
                }
            }
        });

        // Alapból generáljuk a naptárat
        generateCalendar();
    </script>
</body>
</html>

<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>স্টাইলিশ লাইভ টাইম ও ডেট</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@500&display=swap');

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background: linear-gradient(135deg, #667eea, #764ba2);
            font-family: 'Orbitron', sans-serif;
            color: #fff;
        }

        .clock-container {
            background: rgba(0,0,0,0.3);
            padding: 40px 60px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.4);
            text-align: center;
            animation: glow 2s infinite alternate;
        }

        .time {
            font-size: 64px;
            font-weight: bold;
            letter-spacing: 3px;
            margin-bottom: 20px;
        }

        .date {
            font-size: 28px;
        }

        @keyframes glow {
            0% { text-shadow: 0 0 10px #fff; }
            100% { text-shadow: 0 0 20px #ffeb3b, 0 0 30px #ff9800; }
        }
    </style>
</head>
<body>
    <div class="clock-container">
        <div class="time" id="time">00:00:00</div>
        <div class="date" id="date">01-01-1970, সোমবার</div>
    </div>

    <script>
        function updateClock() {
            const now = new Date();

            // সময়
            let hours = now.getHours();
            let minutes = now.getMinutes();
            let seconds = now.getSeconds();

            hours = hours < 10 ? '0' + hours : hours;
            minutes = minutes < 10 ? '0' + minutes : minutes;
            seconds = seconds < 10 ? '0' + seconds : seconds;

            document.getElementById('time').textContent = `${hours}:${minutes}:${seconds}`;

            // তারিখ
            const days = ['রবিবার', 'সোমবার', 'মঙ্গলবার', 'বুধবার', 'বৃহস্পতিবার', 'শুক্রবার', 'শনিবার'];
            const dayName = days[now.getDay()];

            const day = now.getDate() < 10 ? '0' + now.getDate() : now.getDate();
            const month = (now.getMonth() + 1) < 10 ? '0' + (now.getMonth() + 1) : (now.getMonth() + 1);
            const year = now.getFullYear();

            document.getElementById('date').textContent = `${day}-${month}-${year}, ${dayName}`;
        }

        setInterval(updateClock, 1000);
        updateClock();
    </script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Award-Winning Stopwatch Game</title>
    <style>
        body {
            background: linear-gradient(to right, #1e3c72, #2a5298);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            font-family: 'Arial', sans-serif;
        }
        canvas {
            background-color: #000000;
            border: 5px solid #ffffff;
            border-radius: 10px;
        }
        .buttons {
            margin-top: 20px;
        }
        button {
            display: inline-block;
            margin: 0 10px;
            padding: 10px 20px;
            font-size: 16px;
            color: #ffffff;
            background-color: #4caf50;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #45a049;
        }
        .datetime {
            color: #ffffff;
            font-size: 18px;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="datetime" id="datetime"></div>
    <canvas id="gameCanvas" width="250" height="250"></canvas>
    <div class="buttons">
        <button onclick="startTimer()">Start</button>
        <button onclick="stopTimer()">Stop</button>
        <button onclick="resetTimer()">Reset</button>
    </div>

    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const datetimeDiv = document.getElementById('datetime');

        let counter = 0;
        let isRunning = false;
        let timer;

        function formatTime(t) {
            let tenthOfASecond = t % 10;
            let seconds = Math.floor(t / 10) % 60;
            let minutes = Math.floor(t / 600);
            return `${minutes}:${seconds < 10 ? '0' : ''}${seconds}.${tenthOfASecond}`;
        }

        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.beginPath();
            ctx.arc(125, 125, 100, 0, 2 * Math.PI, false);
            ctx.fillStyle = '#ffeb3b';
            ctx.fill();
            ctx.lineWidth = 5;
            ctx.strokeStyle = '#f44336';
            ctx.stroke();
            ctx.fillStyle = '#ffffff';
            ctx.font = '42px Arial';
            ctx.fillText(formatTime(counter), 50, 140);

            // Date and time
            const now = new Date();
            const date = now.toLocaleDateString();
            const time = now.toLocaleTimeString();
            ctx.fillStyle = '#ffffff';
            ctx.font = '14px Arial';
            ctx.fillText(date, 10, 20); // Date in the left corner
            ctx.fillText(time, 150, 20); // Time in the right corner
        }

        function startTimer() {
            if (!isRunning) {
                isRunning = true;
                timer = setInterval(() => {
                    counter++;
                    draw();
                }, 100);
            }
        }

        function stopTimer() {
            if (isRunning) {
                clearInterval(timer);
                isRunning = false;
                draw();
            }
        }

        function resetTimer() {
            clearInterval(timer);
            counter = 0;
            isRunning = false;
            draw();
        }

        // Initial draw
        draw();
        setInterval(() => {
            draw();
        }, 1000);
    </script>
</body>
</html>

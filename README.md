# Express
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Example</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #fff;
        }
        .container {
            width: 100%;
            height: 100vh;
            background: #3c5077;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        #confetti {
            position: fixed;
            top: 0;
            left: 0;
            pointer-events: none;
        }
        #popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            padding: 60px;
            border-radius: 40px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }
        #OK {
            width: 100%;
            margin-top: 50px;
            padding: 10px 0;
            background: #6fd649;
            color: #fff;
            border: 0;
            outline: none;
            font-size: 18px;
            border-radius: 4px;
            cursor: pointer;
            box-shadow: 0 5px 5px rgba(0, 0, 0, 0.2);
        }
        #btn {
            padding: 2px 40px;
            cursor: pointer;
            background: hwb(102 76% 11%);
            border: 0;
            outline: none;
            font-size: 22px;
            font-weight: 500;
            border-radius: 30px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Guess my name:</h1>
        <input type="text" id="nameInput">
        <button id="btn" onclick="showLove()">Submit</button>
    </div>
    <div id="popup">
        <h1>You are the only moon that keeps the tides of my ocean-heart at control</h1>
        <h2>Would You Like to Go on a Date With Me.....</h2>
        <button id="OK" onclick="closePopup()">OK</button>
    </div>
    <canvas id="confetti"></canvas>
    <script>
        function showLove() {
            var name = document.getElementById('nameInput').value.toLowerCase();
            if (name === 'chinmaya' || name === 'chinmay') {
                document.getElementById('popup').style.display = 'block';
                startConfetti();
            } else {
                alert('Invalid');
            }
        }

        function closePopup() {
            document.getElementById('popup').style.display = 'none';
        }

        function startConfetti() {
            var confettiCanvas = document.getElementById('confetti');
            var confettiCtx = confettiCanvas.getContext('2d');
            confettiCanvas.width = window.innerWidth;
            confettiCanvas.height = window.innerHeight;

            var confettiColors = ['#FF7F00', '#FFD700', '#008000', '#33FF33', '#00BFFF', '#0000FF', '#4B0082', '#9400D3'];
            var numConfetti = 100;

            function randomInRange(min, max) {
                return Math.random() * (max - min) + min;
            }

            function createConfetti() {
                for (var i = 0; i < numConfetti; i++) {
                    var color = confettiColors[Math.floor(randomInRange(0, confettiColors.length))];
                    var size = randomInRange(8, 12);
                    var xPos = randomInRange(0, confettiCanvas.width);
                    var yPos = randomInRange(0, confettiCanvas.height);
                    var angle = randomInRange(0, 2 * Math.PI);
                    var velocity = randomInRange(2, 4);

                    confettiCtx.beginPath();
                    confettiCtx.arc(xPos, yPos, size, 0, 2 * Math.PI, false);
                    confettiCtx.fillStyle = color;
                    confettiCtx.fill();

                    var xVel = velocity * Math.cos(angle);
                    var yVel = velocity * Math.sin(angle);

                    confetti.push({
                        x: xPos,
                        y: yPos,
                        size: size,
                        xVel: xVel,
                        yVel: yVel,
                        color: color
                    });
                }
            }

            function updateConfetti() {
                for (var i = 0; i < confetti.length; i++) {
                    var confetto = confetti[i];

                    confetto.x += confetto.xVel;
                    confetto.y += confetto.yVel;

                    // Apply gravity
                    confetto.yVel += 0.2;

                    // Fade out confetti
                    confetto.size -= 0.2;

                    if (confetto.size <= 0) {
                        confetti.splice(i, 1);
                        i--;
                    }
                }
            }

            function drawConfetti() {
                confettiCtx.clearRect(0, 0, confettiCanvas.width, confettiCanvas.height);

                for (var i = 0; i < confetti.length; i++) {
                    var confetto = confetti[i];

                    confettiCtx.beginPath();
                    confettiCtx.arc(confetto.x, confetto.y, confetto.size, 0, 2 * Math.PI, false);
                    confettiCtx.fillStyle = confetto.color;
                    confettiCtx.fill();
                }
            }

            var confetti = [];
            createConfetti();

            function animateConfetti() {
                updateConfetti();
                drawConfetti();

                requestAnimationFrame(animateConfetti);
            }

            animateConfetti();
        }
    </script>
</body>
</html>

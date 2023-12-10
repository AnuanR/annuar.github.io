<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>growth</title>
    <style>
        body {
            overflow: hidden;
            margin: 0;
            background-color: darkblue;
            font-family:Arial, sans-serif;
        }

        .info-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
            color: red;
        }

        .circle {
            width: 100px;
            height: 100px;
            background-color: yellow;
            position: absolute;
            animation: bounce 1s infinite;
            border-radius: 50%;
            transition: transform 0.2s ease-in-out;
        }

        .frozen-circle {
            width: 50px;
            height: 50px;
            background-color: greenyellow;
            border-radius: 50%;
            position: absolute;
            display: none; 
        }

        .circle:hover{
            animation-play-state: paused;
        }

        @keyframes bounce{
            0%, 100%{
                transform: translate(70px,0);
            }
            25% {
                transform: translate(800px,0);
            }
            50% {
                transform: translate(700px,800px);
            }
            75% {
                transform: translate(0, 800px);
            }
            90% {
                transform: translate(400px, 1800px);
            }
            100% {
                transform: translate(0, 400px);
            }
        }
    </style>
</head>
<body>
    
    <div class="circle"></div>
    <div class="frozen-circle"></div>
    <div class="info-text">Catch the circle! 
        When you do, another circle will appear to show it reset at random.</div>

    <script>
        const circle = document.querySelector('.circle');
        const frozenCircle = document.querySelector('.frozen-circle');
        const infoText = document.querySelector('.info-text');
        let isHovered = false;


        function randomizePosition(element) {
        const maxX = window.innerWidth - circle.clientWidth;
        const maxY = window.innerHeight - circle.clientHeight;

        const randomX = Math.floor(Math.random() * maxX);
        const randomY = Math.floor(Math.random() * maxY);

        element.style.transform = `translate(${randomX}px, ${randomY}px)`;
        }

        circle.addEventListener('mouseover', function () {
            if (!isHovered){
                circle.style.animation = 'none';
                setTimeout(() => {
                    circle.style.animation = 'bounce 1s infinite';
                randomizePosition(circle);
            });

            frozenCircle.style.display = 'block';
            randomizePosition(frozenCircle);
        }
        });

        circle.addEventListener('animationiteration', function () {
            if (!isHovered){
           frozenCircle.style.display = 'none';
            }
        });

        circle.addEventListener('click', function () {
            isHovered = true;
            circle.style.animationPlayState = 'paused';
            frozenCircle.style.display = 'none';
            infoText.style.display = 'none';
        });

    </script>


</body>
</html>

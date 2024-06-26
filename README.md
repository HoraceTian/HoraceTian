<!-- 在你的README.md中插入这个代码段 -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            margin: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: black;
            overflow: hidden;
            color: white;
            font-family: Arial, sans-serif;
        }
        h1 {
            position: absolute;
            z-index: 10;
            font-size: 3em;
        }
        canvas {
            position: absolute;
            top: 0;
            left: 0;
        }
    </style>
    <title>Particle Effect</title>
</head>
<body>
    <h1>Hi, I'm Horace</h1>
    <canvas id="canvas"></canvas>
    <script>
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        const stars = [];

        function Star(x, y) {
            this.x = x;
            this.y = y;
            this.radius = Math.random() * 1.5;
            this.alpha = Math.random();
            this.dx = (Math.random() - 0.5) * 0.5;
            this.dy = (Math.random() - 0.5) * 0.5;
        }

        Star.prototype.draw = function() {
            ctx.beginPath();
            ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2, false);
            ctx.fillStyle = `rgba(255, 255, 255, ${this.alpha})`;
            ctx.fill();
            ctx.closePath();
        };

        Star.prototype.update = function() {
            this.x += this.dx;
            this.y += this.dy;

            if (this.x - this.radius > canvas.width || this.x + this.radius < 0 ||
                this.y - this.radius > canvas.height || this.y + this.radius < 0) {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.dx = (Math.random() - 0.5) * 0.5;
                this.dy = (Math.random() - 0.5) * 0.5;
            }

            this.draw();
        };

        function init() {
            for (let i = 0; i < 150; i++) {
                const x = Math.random() * canvas.width;
                const y = Math.random() * canvas.height;
                stars.push(new Star(x, y));
            }
        }

        function animate() {
            requestAnimationFrame(animate);
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            stars.forEach(star => star.update());
        }

        init();
        animate();
    </script>
</body>
</html>



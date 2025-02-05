<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dynamic Sky Background</title>
    <style>
        * { margin: 0; padding: 0; overflow: hidden; }
        body { background: linear-gradient(to bottom, #87CEEB, #ffffff); height: 100vh; width: 100vw; }
        .cloud { position: absolute; top: 0; left: 100%; width: 200px; opacity: 0.8; }
        .object { position: absolute; top: 50px; left: 100%; width: 80px; opacity: 1; }
    </style>
</head>
<body>
    <canvas id="skyCanvas"></canvas>
    <script>
        const canvas = document.getElementById("skyCanvas");
        const ctx = canvas.getContext("2d");
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        
        const clouds = [];
        const objects = [];
        const objectImages = [
            "🚀", "🛸", "🦅", "🐉", "🛩️", "🦄", "🎈", "🌠", "🦜", "🦇"
        ];
        
        function createCloud() {
            return { x: canvas.width, y: Math.random() * canvas.height / 2, speed: 1 + Math.random() };
        }
        
        function createObject() {
            const today = new Date().getDate();
            const objectIndex = today % objectImages.length;
            return { x: canvas.width, y: Math.random() * canvas.height, speed: 2 + Math.random() * 3, emoji: objectImages[objectIndex] };
        }
        
        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.font = "50px Arial";
            
            clouds.forEach(cloud => {
                ctx.fillStyle = "rgba(255, 255, 255, 0.8)";
                ctx.beginPath();
                ctx.arc(cloud.x, cloud.y, 50, 0, Math.PI * 2);
                ctx.fill();
                cloud.x -= cloud.speed;
            });
            
            objects.forEach(obj => {
                ctx.fillText(obj.emoji, obj.x, obj.y);
                obj.x -= obj.speed;
            });
            
            clouds.forEach((cloud, index) => { if (cloud.x < -50) clouds.splice(index, 1); });
            objects.forEach((obj, index) => { if (obj.x < -50) objects.splice(index, 1); });
            
            requestAnimationFrame(draw);
        }
        
        setInterval(() => clouds.push(createCloud()), 3000);
        setInterval(() => objects.push(createObject()), 15000);
        
        draw();
    </script>
</body>
</html>

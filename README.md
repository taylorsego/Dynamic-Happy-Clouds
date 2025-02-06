<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dynamic Sky Background</title>
    <style>
        * { margin: 0; padding: 0; overflow: hidden; }
        body { 
            background: linear-gradient(to bottom, #6FA3EF, #BBD2E1); /* More realistic sky gradient */
            height: 100vh; 
            width: 100vw; 
            position: relative; 
        }
        canvas { position: absolute; top: 0; left: 0; }
    </style>
</head>
<body>
    <canvas id="skyCanvas"></canvas>
    <script>
        const canvas = document.getElementById("skyCanvas");
        const ctx = canvas.getContext("2d");
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        const cloudImage = new Image();
        cloudImage.src = "https://upload.wikimedia.org/wikipedia/commons/1/15/Clouds_over_the_Atlantic_Ocean.jpg"; // Realistic cloud image

        const objectImages = [
            "🚀", "🛸", "🦅", "🐉", "🛩️", "🦄", "🎈", "🌠", "🦜", "🦇"
        ];
        
        const clouds = [];
        const objects = [];
        
        function createCloud() {
            return { 
                x: canvas.width, 
                y: Math.random() * canvas.height / 2, 
                speed: 0.5 + Math.random(), 
                opacity: Math.random() * 0.5 + 0.5,
                scale: Math.random() * 0.5 + 0.5 
            };
        }
        
        function createObject() {
            const today = new Date().getDate();
            const objectIndex = today % objectImages.length;
            return { 
                x: canvas.width, 
                y: Math.random() * canvas.height, 
                speed: 2 + Math.random() * 2, 
                emoji: objectImages[objectIndex],
                angle: Math.random() * Math.PI 
            };
        }
        
        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.font = "50px Arial";
            
            clouds.forEach(cloud => {
                ctx.globalAlpha = cloud.opacity;
                ctx.drawImage(cloudImage, cloud.x, cloud.y, 150 * cloud.scale, 90 * cloud.scale);
                cloud.x -= cloud.speed;
            });
            ctx.globalAlpha = 1;
            
            objects.forEach(obj => {
                ctx.save();
                ctx.translate(obj.x, obj.y);
                ctx.rotate(Math.sin(Date.now() / 500 + obj.angle) * 0.1);
                ctx.fillText(obj.emoji, 0, 0);
                ctx.restore();
                obj.x -= obj.speed;
            });
            
            clouds.forEach((cloud, index) => { if (cloud.x < -150) clouds.splice(index, 1); });
            objects.forEach((obj, index) => { if (obj.x < -50) objects.splice(index, 1); });
            
            requestAnimationFrame(draw);
        }
        
        setInterval(() => clouds.push(createCloud()), 2500);
        setInterval(() => objects.push(createObject()), 12000);
        
        draw();
    </script>
</body>
</html>

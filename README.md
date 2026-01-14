<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Birthday Rinkal 🎉</title>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: 'Segoe UI', sans-serif;
    background: linear-gradient(135deg, #ff758c, #ff7eb3);
    text-align: center;
    color: white;
    overflow-x: hidden;
}

/* Title */
h1 {
    font-size: clamp(2.2rem, 6vw, 3.5rem);
    margin-top: 20px;
    animation: glow 2s infinite alternate;
}

@keyframes glow {
    from { text-shadow: 0 0 10px #fff; }
    to { text-shadow: 0 0 35px #ffeb3b; }
}

/* Message */
.message {
    font-size: clamp(1rem, 4vw, 1.4rem);
    max-width: 90%;
    margin: 20px auto;
    line-height: 1.6;
    animation: fadeIn 3s ease;
}

@keyframes fadeIn {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
}

/* Cake */
.cake {
    width: min(220px, 70vw);
    margin: 20px auto;
    animation: bounce 2s infinite;
    transition: 1.5s;
}

.cut {
    transform: scale(1.2) rotate(10deg);
}

@keyframes bounce {
    0%,100% { transform: translateY(0); }
    50% { transform: translateY(-20px); }
}

/* Gallery */
.gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
    gap: 12px;
    padding: 20px;
}

.gallery img {
    width: 100%;
    aspect-ratio: 1 / 1;
    object-fit: cover;
    border-radius: 15px;
    box-shadow: 0 0 15px rgba(255,255,255,0.6);
    transition: transform 0.4s;
}

.gallery img:hover {
    transform: scale(1.1);
}

/* Hearts */
.heart {
    position: fixed;
    bottom: -20px;
    font-size: 22px;
    animation: floatUp linear infinite;
}

@keyframes floatUp {
    from { transform: translateY(0); opacity: 1; }
    to { transform: translateY(-110vh); opacity: 0; }
}

/* Fireworks */
canvas {
    position: fixed;
    inset: 0;
    z-index: -1;
}
</style>
</head>

<body>

<!-- Music -->
<audio autoplay loop>
  <source src="birthday.mp3" type="audio/mpeg">
</audio>

<canvas id="fireworks"></canvas>

<h1>🎉 Happy Birthday Rinkal 🎂</h1>

<p class="message">
Dear Rinkal 💖<br><br>
Today is not just a birthday,  
it’s a celebration of your beautiful smile,  
your kind heart, and the joy you bring 🌸  
<br><br>
May your life sparkle brighter than fireworks ✨  
and may happiness follow you forever 💕
</p>

<img src="cake.png" class="cake" id="cake">

<h2>📸 Sweet Memories</h2>

<div class="gallery">
    <img src="photo1.jpg">
    <img src="photo2.jpg">
    <img src="photo3.jpg">
    <img src="photo4.jpg">
</div>

<script>
/* Auto Cake Cut */
setTimeout(() => {
    document.getElementById("cake").classList.add("cut");
}, 5000);

/* Floating Hearts */
for (let i = 0; i < 35; i++) {
    let h = document.createElement("div");
    h.innerHTML = "❤️";
    h.className = "heart";
    h.style.left = Math.random() * 100 + "vw";
    h.style.animationDuration = (Math.random() * 4 + 4) + "s";
    document.body.appendChild(h);
}

/* Fireworks + Name */
const canvas = document.getElementById("fireworks");
const ctx = canvas.getContext("2d");
canvas.width = innerWidth;
canvas.height = innerHeight;

let particles = [];

function explode(x, y, text = "") {
    for (let i = 0; i < 120; i++) {
        particles.push({
            x, y,
            dx: (Math.random() - 0.5) * 6,
            dy: (Math.random() - 0.5) * 6,
            life: 80,
            color: `hsl(${Math.random()*360},100%,60%)`,
            text
        });
    }
}

function draw() {
    ctx.clearRect(0,0,canvas.width,canvas.height);

    particles.forEach((p,i) => {
        p.x += p.dx;
        p.y += p.dy;
        p.life--;

        ctx.fillStyle = p.color;
        ctx.beginPath();
        ctx.arc(p.x, p.y, 2, 0, Math.PI*2);
        ctx.fill();

        if(p.text){
            ctx.font = "bold 40px Arial";
            ctx.fillText(p.text, canvas.width/2 - 120, canvas.height/3);
        }

        if(p.life <= 0) particles.splice(i,1);
    });

    requestAnimationFrame(draw);
}

setInterval(() => {
    explode(Math.random()*canvas.width, Math.random()*canvas.height/2);
}, 900);

/* Name Firework */
setTimeout(() => {
    explode(canvas.width/2, canvas.height/3, "RINKAL");
}, 3000);

draw();
</script>

</body>
</html>

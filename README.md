<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Valentine's Day</title>

<style>
body {
    margin: 0;
    font-family: 'Poppins', sans-serif;
    text-align: center;
    background: linear-gradient(to bottom, #ffe6eb, #fff0f5);
    overflow-x: hidden;
}

header {
    background: #ff4d6d;
    padding: 20px;
    color: white;
    font-size: 30px;
    font-weight: bold;
}

.hero {
    margin-top: 40px;
}

.hero img {
    width: 350px;
    max-width: 90%;
    border-radius: 20px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.2);
}

/* Gallery */
.gallery {
    margin: 120px 0;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.fade-img {
    width: 320px;
    margin: 30px 0;
    border-radius: 20px;
    opacity: 0;
    transform: translateY(40px);
    transition: 1s ease;
}

.fade-img.show {
    opacity: 1;
    transform: translateY(0);
}

/* Popup */
.popup {
    position: fixed;
    bottom: 40px;
    left: 50%;
    transform: translateX(-50%);
    background: white;
    padding: 25px 35px;
    border-radius: 25px;
    box-shadow: 0 15px 35px rgba(0,0,0,0.2);
}

button {
    padding: 12px 30px;
    margin: 10px;
    font-size: 18px;
    border: none;
    border-radius: 40px;
    cursor: pointer;
    position: relative;
}

#yesBtn {
    background: #ff4d6d;
    color: white;
}

#noBtn {
    background: #aaa;
    color: white;
    position: absolute;
}

/* Confetti canvas */
canvas {
    position: fixed;
    pointer-events: none;
    top: 0;
    left: 0;
}
</style>
</head>

<body>

<header>❤️ Happy Valentine's Day</header>

<div class="hero">
    <img id="mainGif" src="https://media.tenor.com/_zKc8qSx5S0AAAAC/cat-kiss-catkiss.gif">
</div>

<div class="gallery">
    <img src="photo1.jpg" class="fade-img">
    <img src="photo2.jpg" class="fade-img">
    <img src="photo3.jpg" class="fade-img">
</div>

<div class="popup" id="popup">
    <h2>Will you be Valentine?</h2>
    <button id="yesBtn">YES</button>
    <button id="noBtn">NO</button>
    <div>
        <img id="responseGif" style="display:none; width:250px; border-radius:15px;">
    </div>
</div>

<canvas id="confetti"></canvas>

<script>
// Fade in
const fadeImages = document.querySelectorAll('.fade-img');
window.addEventListener('scroll', () => {
    fadeImages.forEach(img => {
        if(img.getBoundingClientRect().top < window.innerHeight - 100){
            img.classList.add('show');
        }
    });
});

// Running NO button
const noBtn = document.getElementById("noBtn");
const popup = document.getElementById("popup");

popup.addEventListener("mousemove", (e) => {
    const rect = noBtn.getBoundingClientRect();
    const distance = Math.hypot(
        e.clientX - rect.left,
        e.clientY - rect.top
    );

    if(distance < 100){
        const randomX = Math.random() * (popup.offsetWidth - noBtn.offsetWidth);
        const randomY = Math.random() * (popup.offsetHeight - noBtn.offsetHeight);
        noBtn.style.left = randomX + "px";
        noBtn.style.top = randomY + "px";
    }
});

// YES button
const yesBtn = document.getElementById("yesBtn");
const responseGif = document.getElementById("responseGif");

yesBtn.addEventListener("click", () => {
    responseGif.style.display = "block";
    responseGif.src = "https://media.tenor.com/l4DqFqvZq9QAAAAC/yippee-cat-kitty.gif";
    startConfetti();
});

// Confetti
const canvas = document.getElementById("confetti");
const ctx = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let pieces = [];

function startConfetti(){
    for(let i=0;i<150;i++){
        pieces.push({
            x: Math.random()*canvas.width,
            y: Math.random()*canvas.height - canvas.height,
            size: Math.random()*8+4,
            speed: Math.random()*3+2,
            color: hsl(${Math.random()*360},100%,50%)
        });
    }
    requestAnimationFrame(updateConfetti);
}

function updateConfetti(){
    ctx.clearRect(0,0,canvas.width,canvas.height);
    pieces.forEach(p=>{
        p.y += p.speed;
        ctx.fillStyle = p.color;
        ctx.fillRect(p.x,p.y,p.size,p.size);
    });
    requestAnimationFrame(updateConfetti);
}
</script>

</body>
</html>

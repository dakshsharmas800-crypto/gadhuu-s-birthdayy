# gadhuu-s-birthdayy
myy darlings birthdayy
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Happy Birthday Vanni 🎂</title>
  <link rel="stylesheet" href="style.css" />
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
</head>
<body>

  <section class="hero">
    <h1 class="glow">Happy 17th Birthday <span>Vanni!</span> 🎉</h1>
    <h2 class="subtitle">You make the world brighter 💖</h2>
    <button id="celebrate">Celebrate!</button>
  </section>

  <section class="cake-section">
    <div class="cake">
      <div class="layer bottom"></div>
      <div class="layer middle"></div>
      <div class="layer top"></div>
      <div class="candle">
        <div class="flame"></div>
      </div>
    </div>
    <p class="msg">Wishing you happiness, love, and magical memories today 🌈</p>
  </section>

  <canvas id="confetti"></canvas>

  <script src="script.js"></script>
</body>
</html>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: linear-gradient(120deg, #ffb6c1, #e7c6ff);
  color: white;
  font-family: "Poppins", sans-serif;
  overflow-x: hidden;
}

/* Hero section */
.hero {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 2rem;
}

.glow {
  font-size: 3em;
  animation: glow 2s ease-in-out infinite alternate;
}

.glow span {
  color: #fff89a;
}

.subtitle {
  font-size: 1.2em;
  margin: 10px 0 20px;
  opacity: 0.9;
}

@keyframes glow {
  from { text-shadow: 0 0 10px #ff6b81, 0 0 20px #ff6b81; }
  to { text-shadow: 0 0 30px #ffa502, 0 0 60px #ffa502; }
}

button {
  background: #ff6b81;
  border: none;
  color: white;
  cursor: pointer;
  padding: 12px 30px;
  border-radius: 25px;
  font-size: 1.1em;
  transition: 0.3s ease;
}

button:hover {
  background: #ff4757;
  transform: scale(1.1);
}

/* Cake section */
.cake-section {
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: radial-gradient(circle, #ffe0f0, #ffb6c1);
}

.cake {
  position: relative;
  width: 120px;
  height: 150px;
}

.layer {
  position: absolute;
  width: 100%;
  border-radius: 10px;
  left: 0;
}

.bottom {
  height: 40px;
  bottom: 0;
  background: #ff6b81;
}

.middle {
  height: 35px;
  bottom: 40px;
  background: #f8a5c2;
}

.top {
  height: 30px;
  bottom: 75px;
  background: #f78fb3;
}

.candle {
  position: absolute;
  width: 10px;
  height: 40px;
  background: #fff;
  left: calc(50% - 5px);
  bottom: 105px;
  border-radius: 5px;
}

.flame {
  width: 15px;
  height: 25px;
  background: radial-gradient(circle, #fff59d, #ffa502);
  border-radius: 50%;
  position: absolute;
  top: -30px;
  left: -2.5px;
  animation: flicker 0.4s infinite;
}

@keyframes flicker {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.7; transform: scale(1.2); }
}

.msg {
  font-size: 1.3em;
  text-align: center;
  margin-top: 40px;
  color: #fff;
  width: 80%;
  max-width: 500px;
  line-height: 1.5;
}

/* Confetti Canvas */
#confetti {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

/* Responsive */
@media (max-width: 768px) {
  .glow {
    font-size: 2em;
  }
  .msg {
    font-size: 1em;
  }
}
const canvas = document.getElementById("confetti");
const ctx = canvas.getContext("2d");
canvas.width = innerWidth;
canvas.height = innerHeight;

const confettiPieces = [];
for (let i = 0; i < 200; i++) {
  confettiPieces.push({
    x: Math.random() * canvas.width,
    y: Math.random() * canvas.height,
    r: Math.random() * 5 + 2,
    color: `hsl(${Math.random() * 360}, 100%, 75%)`,
    speed: Math.random() * 3 + 1
  });
}

function drawConfetti() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  confettiPieces.forEach((p) => {
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
    ctx.fillStyle = p.color;
    ctx.fill();
  });
}

function updateConfetti() {
  confettiPieces.forEach((p) => {
    p.y += p.speed;
    if (p.y > canvas.height) p.y = -10;
  });
}

function animateConfetti() {
  drawConfetti();
  updateConfetti();
  requestAnimationFrame(animateConfetti);
}

document.getElementById("celebrate").addEventListener("click", () => {
  gsap.fromTo(".cake", 
    { scale: 0.8, opacity: 0 }, 
    { scale: 1, opacity: 1, duration: 1, ease: "bounce.out" }
  );
  animateConfetti();
});

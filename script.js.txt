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

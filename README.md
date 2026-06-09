<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Raiyan Birthday Miner 🎂⛏️</title>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: "Courier New", monospace;
  }

  body {
    overflow: hidden;
    background: linear-gradient(#87CEEB, #4caf50);
    height: 100vh;
    text-align: center;
  }

  h1 {
    margin-top: 20px;
    color: #2b1d0e;
    text-shadow: 3px 3px 0 #000;
  }

  .score {
    margin: 10px auto;
    padding: 10px;
    width: 200px;
    background: #8b5a2b;
    border: 4px solid #3b1f0e;
    color: white;
    font-size: 20px;
  }

  .game-area {
    position: relative;
    width: 100%;
    height: 75vh;
    margin-top: 10px;
    border-top: 4px solid #2b1d0e;
  }

  /* ✅ FIXED BLOCK (no image needed) */
  .block {
    position: absolute;
    width: 55px;
    height: 55px;
    background: linear-gradient(145deg, #7a4b20, #5a3617);
    border: 3px solid #2b1d0e;
    box-shadow: inset 0 0 10px rgba(0,0,0,0.5);
    cursor: pointer;
    transition: transform 0.1s;
  }

  .block:active {
    transform: scale(0.85);
  }

  .creeper {
    position: fixed;
    bottom: -200px;
    left: 50%;
    transform: translateX(-50%);
    transition: 0.6s;
  }

  .creeper img {
    width: 160px;
  }

  .message {
    position: fixed;
    inset: 0;
    display: none;
    justify-content: center;
    align-items: center;
    background: rgba(0,0,0,0.85);
  }

  .card {
    background: #4caf50;
    padding: 30px;
    border: 6px solid #2b1d0e;
    color: white;
    text-shadow: 2px 2px 0 #000;
  }
</style>
</head>

<body>

<h1>⛏️ Raiyan Birthday Miner 🎂</h1>
<div class="score">Score: <span id="score">0</span></div>

<div class="game-area" id="gameArea"></div>

<!-- Creeper -->
<div class="creeper" id="creeper">
  <img src="https://i.imgur.com/4QfKuz1.png">
</div>

<!-- Win -->
<div class="message" id="message">
  <div class="card">
    <h2>🎉 Happy Birthday Raiyan! 🎂</h2>
    <p>You mined all blocks like a pro miner ⛏️💚</p>
  </div>
</div>

<script>
let score = 0;

const scoreEl = document.getElementById("score");
const gameArea = document.getElementById("gameArea");
const creeper = document.getElementById("creeper");
const message = document.getElementById("message");

function playBreakSound() {
  const ctx = new (window.AudioContext || window.webkitAudioContext)();
  const osc = ctx.createOscillator();
  const gain = ctx.createGain();

  osc.type = "square";
  osc.frequency.value = 180;

  gain.gain.value = 0.2;

  osc.connect(gain);
  gain.connect(ctx.destination);

  osc.start();
  osc.stop(ctx.currentTime + 0.15);
}

// ✅ FIXED SPAWN LOGIC
for (let i = 0; i < 12; i++) {
  const block = document.createElement("div");
  block.classList.add("block");

  const x = Math.random() * (window.innerWidth - 60);
  const y = Math.random() * (window.innerHeight * 0.6);

  block.style.left = x + "px";
  block.style.top = y + "px";

  block.addEventListener("click", () => {
    block.remove();
    score++;
    scoreEl.textContent = score;

    playBreakSound();

    if (score % 3 === 0) {
      creeper.style.bottom = "20px";
      setTimeout(() => {
        creeper.style.bottom = "-200px";
      }, 700);
    }

    if (score === 12) {
      message.style.display = "flex";
    }
  });

  gameArea.appendChild(block);
}
</script>

</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>💣 Mines - V3.32</title>
<style>
  :root {
    --bg-dark: #0f172a;
    --panel: #1e293b;
    --text: #f8fafc;
    --primary: #22c55e;
    --danger: #ef4444;
    --success: #10b981;
    --neutral: #334155;
  }
  * {
    box-sizing: border-box;
  }
  body {
    margin: 0;
    padding: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: var(--bg-dark);
    color: var(--text);
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
  }
  .container {
    width: 100%;
    max-width: 420px;
    background-color: var(--panel);
    border-radius: 12px;
    box-shadow: 0 0 20px rgba(0,0,0,0.5);
    padding: 30px 40px;
    position: relative;
    text-align: center;
  }
  .rainbow-text {
    background-image: linear-gradient(to right, red, orange, yellow, green, cyan, blue, violet);
    -webkit-background-clip: text;
    color: transparent;
    font-weight: bold;
    font-size: 1.8rem;
    animation: rainbow 3s infinite linear;
  }
  @keyframes rainbow {
    0% { filter: hue-rotate(0deg); }
    100% { filter: hue-rotate(360deg); }
  }
  .logo {
    position: absolute;
    top: 20px;
    left: 20px;
    font-size: 1.5rem;
    font-weight: bold;
    color: red;
    animation: blink 1.5s infinite;
  }
  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.3; }
  }
  .support {
    margin-top: 30px;
    font-size: 0.9rem;
  }
  .support a {
    color: #60a5fa;
    text-decoration: underline;
    display: inline-flex;
    align-items: center;
    gap: 6px;
  }
  .discord-badge {
    width: 18px;
    height: 18px;
    background: url('https://cdn.jsdelivr.net/gh/simple-icons/simple-icons/icons/discord.svg') no-repeat center center;
    background-size: contain;
    filter: invert(100%);
    display: inline-block;
    vertical-align: middle;
  }
  .game-grid {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 10px;
    margin: 20px 0;
  }
  .tile {
    width: 60px;
    height: 60px;
    background-color: var(--neutral);
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.2rem;
    cursor: pointer;
    transition: background 0.3s;
    user-select: none;
  }
  .tile.safe {
    background-color: var(--success);
  }
  .tile.bomb {
    background-color: var(--danger);
  }
  .seed-box, .bomb-count-box {
    margin-top: 15px;
    font-size: 0.9rem;
    color: #94a3b8;
  }
  .keytime {
    margin-top: 8px;
    font-size: 0.85rem;
    color: #a3a3a3;
    font-style: italic;
  }
  input[type="number"], input[type="text"] {
    background: transparent;
    border: none;
    color: #94a3b8;
    font-size: 1rem;
    width: 140px;
    text-align: center;
  }
</style>
</head>
<body>
<div class="container">
  <div class="logo">🔥 M7OP</div>
  <h2 class="rainbow-text">💣 Mines - V3.32</h2>
  <div class="game-grid" id="grid"></div>

  <div class="seed-box">
    📝 Seed: <input type="text" id="seedInput" placeholder="Enter seed" />
  </div>

  <div class="bomb-count-box">
    💣 Number of Mines: 
    <input type="number" id="bombInput" min="1" max="24" value="5" />
  </div>

  <div class="support">
    🛠️ Support: <a href="https://discord.com" target="_blank">
      <span class="discord-badge" aria-hidden="true"></span> Join Discord
    </a>
  </div>
  <div class="keytime">keytime : 120min</div>
</div>

<script>
  const tiles = 25;
  let bombs = 5;
  let bombIndexes = new Set();

  function generateBombs(seed, bombsCount) {
    // Simple seeded random generator (xorshift)
    function xorshift(seed) {
      let x = seed.charCodeAt(0) || 1;
      let y = seed.charCodeAt(1) || 2;
      let z = seed.charCodeAt(2) || 3;
      let w = seed.charCodeAt(3) || 4;
      return function() {
        let t = x ^ (x << 11);
        x = y; y = z; z = w;
        w = w ^ (w >> 19) ^ (t ^ (t >> 8));
        return Math.abs(w);
      }
    }
    const rand = xorshift(seed);
    let bombsSet = new Set();
    while (bombsSet.size < bombsCount) {
      bombsSet.add(rand() % tiles);
    }
    return bombsSet;
  }

  function startGame(seed, bombsCount) {
    const grid = document.getElementById('grid');
    grid.innerHTML = '';
    bombIndexes = generateBombs(seed, bombsCount);

    for (let i = 0; i < tiles; i++) {
      const tile = document.createElement('div');
      tile.className = 'tile';
      tile.addEventListener('click', () => {
        if (tile.classList.contains('revealed')) return;
        tile.classList.add('revealed');
        if (bombIndexes.has(i)) {
          tile.classList.add('bomb');
          tile.textContent = '💣';
        } else {
          tile.classList.add('safe');
          tile.textContent = '✅';
        }
      });
      grid.appendChild(tile);
    }
  }

  const seedInput = document.getElementById('seedInput');
  const bombInput = document.getElementById('bombInput');

  seedInput.value = Math.random().toString(36).substring(2, 8);
  bombInput.value = bombs;

  function reloadGame() {
    bombs = Math.min(Math.max(parseInt(bombInput.value) || 5, 1), 24);
    startGame(seedInput.value, bombs);
  }

  seedInput.addEventListener('change', reloadGame);
  bombInput.addEventListener('change', reloadGame);

  reloadGame();
</script>
</body>
</html>

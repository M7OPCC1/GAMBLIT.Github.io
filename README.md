/*
  Mines Game CSS Stylesheet
  Extracted from the HTML file
*/

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


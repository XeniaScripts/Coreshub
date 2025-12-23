<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CORE'S HUB</title>

  <!-- Particle.js -->
  <script src="https://cdn.jsdelivr.net/npm/particles.js@2.0.0/particles.min.js"></script>

  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', sans-serif; }

    body {
      min-height: 100vh;
      color: white;
      background: radial-gradient(circle at top, #1b1f4b, #05010d 70%);
      overflow-x: hidden;
      text-align: center;
    }

    /* Floating galaxy animation */
    body::before {
      content: "";
      position: fixed;
      inset: 0;
      background: url('https://i.imgur.com/9aK0F0L.png') no-repeat center center;
      background-size: cover;
      opacity: 0.15;
      animation: floatGalaxy 60s linear infinite;
      z-index: -2;
    }

    @keyframes floatGalaxy { from { transform: translateY(0); } to { transform: translateY(-1000px); } }

    #particles-js {
      position: fixed;
      inset: 0;
      z-index: -1;
    }

    header {
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      padding: 0 20px;
    }

    header h1 {
      font-size: 4rem;
      letter-spacing: 4px;
      background: linear-gradient(90deg, #7f7cff, #c77dff);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      animation: glow 3s infinite;
      margin-bottom: 20px;
    }

    .roblox-logo {
      width: 100px;
      max-width: 30%;
      height: auto;
      margin-bottom: 20px;
      animation: float 4s ease-in-out infinite;
    }

    @keyframes float { 0%,100% { transform: translateY(0); } 50% { transform: translateY(-15px); } }

    .scroll-btn {
      margin-top: 40px;
      padding: 15px 40px;
      border-radius: 30px;
      border: none;
      background: linear-gradient(90deg, #6a5cff, #9d4edd);
      color: #fff;
      font-size: 1rem;
      cursor: pointer;
      box-shadow: 0 0 25px rgba(157,78,221,.8);
      transition: .3s;
    }

    .scroll-btn:hover { box-shadow: 0 0 45px rgba(157,78,221,1); transform: scale(1.1); }

    section { padding: 60px 5%; max-width: 1200px; margin: 0 auto; }

    h2 { font-size: 2.5rem; margin-bottom: 40px; background: linear-gradient(90deg,#9d4edd,#5a4bff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }

    .script-card {
      background: rgba(255,255,255,0.06);
      border-radius: 20px;
      padding: 25px;
      margin-bottom: 40px;
      box-shadow: 0 0 40px rgba(138,43,226,0.3);
      transition: .3s;
      word-wrap: break-word;
    }

    .script-card:hover { box-shadow: 0 0 70px rgba(138,43,226,0.9); transform: scale(1.02); }

    .script-card h3 { color: #d8b4ff; margin-bottom: 15px; }

    .code-box { background: rgba(0,0,0,0.7); border-radius: 15px; padding: 20px; font-family: monospace; margin-bottom: 15px; white-space: pre-wrap; word-break: break-word; }

    .copy-btn { padding: 10px 25px; border: none; border-radius: 20px; background: linear-gradient(90deg,#7b2cbf,#5a4bff); color: white; cursor: pointer; transition: .3s; }

    .copy-btn:hover { box-shadow: 0 0 30px #9d4edd; transform: scale(1.1); }

    .admin { margin-top: 50px; padding: 30px; background: rgba(0,0,0,0.6); border-radius: 20px; }

    input, textarea { width: 100%; padding: 12px; margin-bottom: 15px; border-radius: 10px; border: none; outline: none; }

    @keyframes glow { 0%,100% { text-shadow: 0 0 20px #7f7cff; } 50% { text-shadow: 0 0 40px #c77dff; } }

    /* Mobile adjustments */
    @media (max-width: 600px) {
      header h1 { font-size: 3rem; }
      h2 { font-size: 2rem; }
      .scroll-btn, .copy-btn { padding: 18px 35px; font-size: 1.1rem; }
      .roblox-logo { max-width: 50%; }
    }
  </style>
</head>
<body>

<div id="particles-js"></div>

<header>
  <img class="roblox-logo" src="https://upload.wikimedia.org/wikipedia/commons/7/7e/Roblox_Logo_2022.svg" alt="Roblox Logo">
  <h1>CORE'S HUB</h1>
  <button class="scroll-btn" onclick="document.getElementById('scripts').scrollIntoView({behavior:'smooth'})">View Scripts</button>
</header>

<section id="scripts">
  <h2>Scripts</h2>
  <div id="scriptContainer"></div>

  <div class="admin">
    <h3>Admin Add Script (Only You)</h3>
    <input id="game" placeholder="Game Name">
    <textarea id="script" placeholder="Paste script here"></textarea>
    <button class="copy-btn" onclick="addScript()">Add Script</button>
  </div>
</section>

<script>
  function copyToClipboard(text) {
    const textarea = document.createElement('textarea');
    textarea.value = text;
    textarea.style.position = 'fixed';
    textarea.style.opacity = '0';
    document.body.appendChild(textarea);
    textarea.focus();
    textarea.select();
    try { document.execCommand('copy'); alert('Script copied to clipboard!'); }
    catch (err) { alert('Copy failed. Please copy manually.'); }
    document.body.removeChild(textarea);
  }

  function addScript() {
    const ADMIN_PASSWORD = "coreshubontop1234@";
    const entered = prompt("Admin Password Required");
    if (entered !== ADMIN_PASSWORD) { alert("Incorrect password."); return; }

    const game = document.getElementById('game').value.trim();
    const script = document.getElementById('script').value.trim();
    if (!game || !script) return;

    const div = document.createElement('div');
    div.className = 'script-card';
    div.innerHTML = `<h3>${game}</h3><div class="code-box">${script}</div><button class="copy-btn">Copy Script</button>`;
    div.querySelector('.copy-btn').addEventListener('click', () => copyToClipboard(script));

    document.getElementById('scriptContainer').appendChild(div);
    document.getElementById('game').value = '';
    document.getElementById('script').value = '';
  }

  particlesJS('particles-js', {
    particles: { number: { value: 80 }, color: { value: '#ffffff' }, size: { value: 2 }, move: { speed: 1 }, line_linked: { enable: false } }
  });
</script>

</body>
</html>

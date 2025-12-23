<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CORE'S HUB</title>

<script src="https://cdn.jsdelivr.net/npm/particles.js@2.0.0/particles.min.js"></script>

<style>
* { margin:0; padding:0; box-sizing:border-box; font-family:'Segoe UI',sans-serif; }
body { min-height:100vh; color:white; overflow-x:hidden; text-align:center; background: radial-gradient(circle at top, #0b0c1a, #05010d 70%); position:relative; }
body::before { content:""; position:fixed; inset:0; background: radial-gradient(circle, #0b0c1a 0%, #05010d 100%); z-index:-3; }
#particles-js { position:fixed; inset:0; z-index:-2; }

/* Header */
header { height:100vh; display:flex; flex-direction:column; justify-content:center; align-items:center; padding:0 20px; }
header h1 { font-size:4rem; color:#fff; text-transform:uppercase; letter-spacing:4px; text-shadow:0 0 10px #7f7cff,0 0 20px #c77dff,0 0 30px #7f7cff; animation: neonPulse 2s infinite alternate; margin-bottom:20px; }
@keyframes neonPulse { 0% { text-shadow:0 0 10px #7f7cff,0 0 20px #c77dff,0 0 30px #7f7cff; } 100% { text-shadow:0 0 20px #9d4edd,0 0 40px #c77dff,0 0 60px #7f7cff; } }
.scroll-btn { margin-top:40px; padding:18px 40px; border-radius:30px; border:none; background:linear-gradient(90deg,#6a5cff,#9d4edd); color:#fff; font-size:1.1rem; cursor:pointer; box-shadow:0 0 25px rgba(157,78,221,.8); transition:.3s; position:relative; z-index:1; }
.scroll-btn:hover { box-shadow:0 0 45px rgba(157,78,221,1); transform:scale(1.1); }

/* Sections */
section { padding:60px 5%; max-width:1200px; margin:0 auto; position:relative; }
h2 { font-size:2.5rem; margin-bottom:40px; background:linear-gradient(90deg,#9d4edd,#5a4bff); -webkit-background-clip:text; -webkit-text-fill-color:transparent; text-align:center; }

/* Script Cards */
.script-card { background:rgba(0,0,0,0.6); border:2px solid; border-image: linear-gradient(45deg, #7f7cff, #c77dff) 1; border-radius:20px; padding:25px; margin-bottom:40px; box-shadow:0 0 40px rgba(138,43,226,0.5); transition:.4s; word-wrap:break-word; position:relative; overflow:hidden; }
.script-card:hover { box-shadow:0 0 80px rgba(138,43,226,1); transform:scale(1.03); border-image: linear-gradient(45deg, #ff6bcb, #7f7cff) 1; }
.script-card h3 { color:#d8b4ff; margin-bottom:15px; }
.code-box { background:rgba(0,0,0,0.7); border-radius:15px; padding:20px; font-family:monospace; margin-bottom:15px; white-space:pre-wrap; word-break:break-word; border:1px solid #7f7cff; }
.copy-btn, .remove-btn { padding:10px 25px; border:none; border-radius:20px; cursor:pointer; transition:.3s; }
.copy-btn { background:linear-gradient(90deg,#7b2cbf,#5a4bff); color:white; box-shadow:0 0 15px #7f7cff; }
.copy-btn:hover { box-shadow:0 0 35px #9d4edd; transform:scale(1.1); }
.remove-btn { background:linear-gradient(90deg,#ff3b3b,#ff6b6b); color:white; margin-left:10px; box-shadow:0 0 15px #ff6b6b; }
.remove-btn:hover { box-shadow:0 0 35px #ff3b3b; transform:scale(1.1); }

/* Admin Panel */
.admin { margin-top:50px; padding:30px; background:rgba(0,0,0,0.6); border-radius:20px; border:2px solid; border-image: linear-gradient(45deg,#7f7cff,#c77dff) 1; box-shadow:0 0 50px rgba(157,78,221,0.6); }
input, textarea { width:100%; padding:12px; margin-bottom:15px; border-radius:10px; border:1px solid #7f7cff; outline:none; background:rgba(0,0,0,0.5); color:white; }

/* Shooting Stars & Comets */
.shooting-star { position:absolute; width:2px; height:80px; background:white; opacity:0.8; transform:rotate(45deg); animation:shoot 1.5s linear forwards; }
@keyframes shoot { 0% { transform:translateX(0) translateY(0) rotate(45deg); opacity:1; } 100% { transform:translateX(800px) translateY(600px) rotate(45deg); opacity:0; } }
.comet { position:absolute; width:2px; height:100px; background: linear-gradient(to bottom, #fff, rgba(255,255,255,0)); border-radius:50%; opacity:0.9; transform:rotate(45deg); animation:cometMove 3s linear forwards; }
@keyframes cometMove { 0% { transform: translateX(0) translateY(0) rotate(45deg); opacity:1; } 100% { transform: translateX(1000px) translateY(700px) rotate(45deg); opacity:0; } }
.star { position:absolute; width:2px; height:2px; background:white; border-radius:50%; opacity:0.8; animation:twinkle 2s infinite alternate; cursor:pointer; }
@keyframes twinkle { from { opacity:0.3; } to { opacity:1; } }

/* Section Animations */
.fade-up { opacity:0; transform:translateY(50px); transition:all 0.8s ease-out; }
.fade-up.show { opacity:1; transform:translateY(0); }

@media(max-width:600px){ header h1{font-size:3rem;} h2{font-size:2rem;} .scroll-btn,.copy-btn,.remove-btn{padding:18px 35px;font-size:1.1rem;} }
</style>
</head>
<body>

<div id="particles-js"></div>
<header>
  <h1>CORE'S HUB</h1>
  <button class="scroll-btn" onclick="document.getElementById('scripts').scrollIntoView({behavior:'smooth'})">View Scripts</button>
</header>
<section id="scripts">
  <h2 class="fade-up">Scripts</h2>
  <div id="scriptContainer" class="fade-up"></div>

  <div class="admin fade-up">
    <h3>Admin Add Script (Only You)</h3>
    <input id="game" placeholder="Game Name">
    <textarea id="script" placeholder="Paste script here"></textarea>
    <button class="copy-btn" onclick="addScript()">Add Script</button>
  </div>
</section>

<script>
const ADMIN_PASSWORD="coreshubontop1234@";
let scripts = JSON.parse(localStorage.getItem('scripts')||'[]');
const container = document.getElementById('scriptContainer');

function renderScripts(){
  container.innerHTML='';
  scripts.forEach((s,i)=>{
    const div=document.createElement('div');
    div.className='script-card fade-up';
    div.innerHTML=`<h3>${s.game}</h3><div class="code-box">${s.code}</div><button class="copy-btn">Copy Script</button><button class="remove-btn">Remove Script</button>`;
    div.querySelector('.copy-btn').addEventListener('click',()=>copyToClipboard(s.code));
    div.querySelector('.remove-btn').addEventListener('click',()=>removeScript(i));
    container.appendChild(div);
    setTimeout(()=>div.classList.add('show'),50);
  });
}

function addScript(){
  const entered = prompt("Admin Password Required").trim();
  if(entered!==ADMIN_PASSWORD){alert("Incorrect password."); return;}
  const game=document.getElementById('game').value.trim();
  const code=document.getElementById('script').value.trim();
  if(!game||!code) return;
  scripts.push({game:game,code:code});
  localStorage.setItem('scripts',JSON.stringify(scripts));
  document.getElementById('game').value='';
  document.getElementById('script').value='';
  renderScripts();
  showNotification("Script Added!");
}

function removeScript(index){
  const entered = prompt("Admin Password Required to Remove").trim();
  if(entered!==ADMIN_PASSWORD){alert("Incorrect password."); return;}
  scripts.splice(index,1);
  localStorage.setItem('scripts',JSON.stringify(scripts));
  renderScripts();
  showNotification("Script Removed!");
}

function copyToClipboard(text){const t=document.createElement('textarea');t.value=text;t.style.position='fixed';t.style.opacity='0';document.body.appendChild(t);t.focus();t.select();try{document.execCommand('copy');showNotification('Script Copied!');}catch(e){alert('Copy failed.');}document.body.removeChild(t);}

function showNotification(msg){
  const n=document.createElement('div');
  n.textContent=msg;
  n.style.position='fixed';
  n.style.top='20px';
  n.style.left='50%';
  n.style.transform='translateX(-50%)';
  n.style.padding='12px 25px';
  n.style.background='linear-gradient(90deg,#7f7cff,#c77dff)';
  n.style.color='white';
  n.style.borderRadius='20px';
  n.style.boxShadow='0 0 20px rgba(157,78,221,0.7)';
  n.style.zIndex=1000;
  document.body.appendChild(n);
  setTimeout(()=>document.body.removeChild(n),2000);
}

renderScripts();
particlesJS('particles-js',{particles:{number:{value:200},color:{value:'#ffffff'},size:{value:3},move:{speed:1.5},line_linked:{enable:false}}});
function spawnStar(){const star=document.createElement('div');star.className='shooting-star star';star.style.left=Math.random()*window.innerWidth+'px';star.style.top=Math.random()*window.innerHeight/2+'px';star.addEventListener('click',()=>{showNotification('Star Clicked!')});document.body.appendChild(star);setTimeout(()=>document.body.removeChild(star),1500);} setInterval(spawnStar,1000);
function spawnComet(){const comet=document.createElement('div');comet.className='comet';comet.style.left=Math.random()*window.innerWidth+'px';comet.style.top=Math.random()*window.innerHeight/2+'px';document.body.appendChild(comet);setTimeout(()=>document.body.removeChild(comet),3000);} setInterval(spawnComet,3500);
function spawnTwinkle(){const star=document.createElement('div');star.className='star';star.style.left=Math.random()*window.innerWidth+'px';star.style.top=Math.random()*window.innerHeight+'px';document.body.appendChild(star);setTimeout(()=>document.body.removeChild(star),4000);} setInterval(spawnTwinkle,300);

const music=new Audio('https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3');music.loop=true;music.volume=0.2;
document.body.addEventListener('click',()=>{if(music.paused) music.play();},{once:true});
const musicBtn=document.createElement('button');musicBtn.textContent='Toggle Music';musicBtn.className='scroll-btn';musicBtn.style.position='fixed';musicBtn.style.bottom='20px';musicBtn.style.right='20px';musicBtn.onclick=()=>music.paused?music.play():music.pause();document.body.appendChild(musicBtn);
</script>

</body>
</html>

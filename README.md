<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BLACK DRAGON</title>
<script src="https://cdn.jsdelivr.net/npm/particles.js@2.0.0/particles.min.js"></script>
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Segoe UI',sans-serif}
body{min-height:100vh;color:white;text-align:center;background:radial-gradient(circle at top,#1b1f4b,#05010d 70%);overflow-x:hidden}
#particles-js{position:fixed;inset:0;z-index:-1}
.hidden{display:none}

/* Login */
.login{min-height:100vh;display:flex;flex-direction:column;justify-content:center;align-items:center;padding:20px}
.login-box{background:rgba(0,0,0,.6);padding:40px;border-radius:20px;box-shadow:0 0 40px rgba(157,78,221,.6);max-width:400px;width:100%}
.login-box h1{margin-bottom:20px;text-shadow:0 0 20px #9d4edd}
.login-box input{width:100%;padding:14px;border-radius:12px;border:none;margin-bottom:15px}
.login-box button{padding:14px 30px;border:none;border-radius:25px;background:linear-gradient(90deg,#6a5cff,#9d4edd);color:white;font-size:1.1rem;cursor:pointer}

/* Main */
header{height:100vh;display:flex;flex-direction:column;justify-content:center;align-items:center}
header h1{font-size:4rem;text-shadow:0 0 15px #7f7cff,0 0 30px #c77dff}
.scroll-btn{margin-top:40px;padding:18px 40px;border-radius:30px;border:none;background:linear-gradient(90deg,#6a5cff,#9d4edd);color:white;font-size:1.1rem;cursor:pointer}
section{padding:60px 5%;max-width:1200px;margin:auto}
.script-card{background:rgba(255,255,255,.06);border-radius:20px;padding:25px;margin-bottom:40px;box-shadow:0 0 40px rgba(138,43,226,.3)}
.script-card h3{color:#d8b4ff;margin-bottom:15px}
.code-box{background:rgba(0,0,0,.7);border-radius:15px;padding:20px;font-family:monospace;margin-bottom:15px;white-space:pre-wrap}
.copy-btn,.remove-btn{padding:10px 25px;border:none;border-radius:20px;cursor:pointer}
.copy-btn{background:linear-gradient(90deg,#7b2cbf,#5a4bff);color:white}
.remove-btn{background:linear-gradient(90deg,#ff3b3b,#ff6b6b);color:white;margin-left:10px}
.admin{margin-top:50px;padding:30px;background:rgba(0,0,0,.6);border-radius:20px}
input,textarea{width:100%;padding:12px;margin-bottom:15px;border-radius:10px;border:none}
</style>
</head>
<body>
<div id="particles-js"></div>

<!-- LOGIN -->
<div id="login" class="login">
  <div class="login-box">
    <h1>BLACK DRAGON LOGIN</h1>
    <input id="loginPass" placeholder="Enter password">
    <button onclick="login()">Enter</button>
  </div>
</div>

<!-- MAIN SITE -->
<div id="site" class="hidden">
<header>
  <h1>BLACK DRAGON</h1>
  <button class="scroll-btn" onclick="document.getElementById('scripts').scrollIntoView({behavior:'smooth'})">View Scripts</button>
</header>
<section id="scripts">
  <h2>Scripts</h2>
  <div id="scriptContainer"></div>
  <div id="adminPanel" class="admin hidden">
    <h3>Admin Add Script</h3>
    <input id="game" placeholder="Game Name">
    <textarea id="script" placeholder="Paste script here"></textarea>
    <button class="copy-btn" onclick="addScript()">Add Script</button>
  </div>
</section>
</div>

<script>
const MEMBER_PASS="blackdragon10101234@";
const ADMIN_PASS="blackdragonontop67671@";
let role=null;

function login(){
  const p=document.getElementById('loginPass').value.trim();
  if(p===ADMIN_PASS){role='admin';}
  else if(p===MEMBER_PASS){role='member';}
  else{alert('Wrong password');return;}
  document.getElementById('login').classList.add('hidden');
  document.getElementById('site').classList.remove('hidden');
  if(role==='admin') document.getElementById('adminPanel').classList.remove('hidden');
}

let scripts=JSON.parse(localStorage.getItem('scripts')||'[]');
const container=document.getElementById('scriptContainer');

function renderScripts(){
  container.innerHTML='';
  scripts.forEach((s,i)=>{
    const d=document.createElement('div');
    d.className='script-card';
    d.innerHTML=`<h3>${s.game}</h3><div class='code-box'>${s.code}</div><button class='copy-btn'>Copy</button>${role==='admin'?'<button class=remove-btn>Remove</button>':''}`;
    d.querySelector('.copy-btn').onclick=()=>copy(s.code);
    if(role==='admin') d.querySelector('.remove-btn').onclick=()=>removeScript(i);
    container.appendChild(d);
  });
}

function addScript(){
  const g=document.getElementById('game').value.trim();
  const c=document.getElementById('script').value.trim();
  if(!g||!c)return;
  scripts.push({game:g,code:c});
  localStorage.setItem('scripts',JSON.stringify(scripts));
  renderScripts();
}

function removeScript(i){scripts.splice(i,1);localStorage.setItem('scripts',JSON.stringify(scripts));renderScripts();}
function copy(t){const a=document.createElement('textarea');a.value=t;document.body.appendChild(a);a.select();document.execCommand('copy');document.body.removeChild(a);}

renderScripts();
particlesJS('particles-js',{particles:{number:{value:160},color:{value:'#fff'},size:{value:3},move:{speed:1.4},line_linked:{enable:false}}});
</script>
</body>
</html>

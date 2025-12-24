<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>BLACK DRAGON</title>
<script src="https://cdn.jsdelivr.net/npm/particles.js@2.0.0/particles.min.js"></script>
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:Arial,Helvetica,sans-serif}
body{min-height:100vh;background:#05010d;color:white;overflow-x:hidden}
.hidden{display:none}
#particles-js{position:fixed;inset:0;z-index:-1}

/* LOGIN */
.login{min-height:100vh;display:flex;justify-content:center;align-items:center}
.login-box{background:rgba(0,0,0,.75);padding:35px;border-radius:18px;width:100%;max-width:380px;box-shadow:0 0 40px #9d4edd;text-align:center}
.login-box h1{margin-bottom:20px}
.login-box input{width:100%;padding:14px;border-radius:12px;border:none;margin-bottom:15px;font-size:1rem}
.login-box button{padding:14px 30px;border:none;border-radius:25px;background:#9d4edd;color:white;font-size:1.1rem;cursor:pointer}

/* SITE */
header{height:100vh;display:flex;flex-direction:column;justify-content:center;align-items:center}
header h1{font-size:3.5rem;text-shadow:0 0 20px #9d4edd}
.scroll-btn{margin-top:30px;padding:16px 36px;border-radius:28px;border:none;background:#7b2cbf;color:white;font-size:1.1rem}
section{padding:60px 6%;max-width:1100px;margin:auto}
.script-card{background:rgba(255,255,255,.07);border-radius:18px;padding:22px;margin-bottom:30px}
.code-box{background:rgba(0,0,0,.8);padding:18px;border-radius:14px;white-space:pre-wrap;font-family:monospace}
.copy-btn,.remove-btn{margin-top:12px;padding:10px 22px;border:none;border-radius:20px;cursor:pointer}
.copy-btn{background:#5a4bff;color:white}
.remove-btn{background:#ff3b3b;color:white;margin-left:10px}
.admin{margin-top:40px;background:rgba(0,0,0,.7);padding:25px;border-radius:18px}
input,textarea{width:100%;padding:12px;border-radius:10px;border:none;margin-bottom:12px}
</style>
</head>
<body>
<div id="particles-js"></div>

<!-- LOGIN -->
<div id="login" class="login">
  <div class="login-box">
    <h1>BLACK DRAGON LOGIN</h1>
    <input id="pass" type="password" placeholder="Password" autocomplete="off">
    <button onclick="doLogin()">Login</button>
  </div>
</div>

<!-- SITE -->
<div id="site" class="hidden">
<header>
  <h1>BLACK DRAGON</h1>
  <button class="scroll-btn" onclick="document.getElementById('scripts').scrollIntoView({behavior:'smooth'})">View Scripts</button>
</header>
<section id="scripts">
  <h2>Scripts</h2>
  <div id="scriptContainer"></div>
  <div id="adminPanel" class="admin hidden">
    <h3>Add Script (Admin)</h3>
    <input id="game" placeholder="Game Name">
    <textarea id="code" placeholder="Script"></textarea>
    <button class="copy-btn" onclick="addScript()">Add</button>
  </div>
</section>
</div>

<script>
const MEMBER='blackdragon10101234@';
const ADMIN='blackdragonontop67671@';
let role='';

function doLogin(){
  const v=document.getElementById('pass').value;
  if(v===ADMIN){role='admin';}
  else if(v===MEMBER){role='member';}
  else{alert('Wrong password');return;}

  document.getElementById('login').style.display='none';
  document.getElementById('site').classList.remove('hidden');
  if(role==='admin') document.getElementById('adminPanel').classList.remove('hidden');
  render();
}

let data=JSON.parse(localStorage.getItem('bd_scripts')||'[]');
const box=document.getElementById('scriptContainer');

function render(){
  box.innerHTML='';
  data.forEach((s,i)=>{
    const d=document.createElement('div');
    d.className='script-card';
    d.innerHTML=`<h3>${s.game}</h3><div class="code-box">${s.code}</div><button class="copy-btn">Copy</button>${role==='admin'?'<button class="remove-btn">Remove</button>':''}`;
    d.querySelector('.copy-btn').onclick=()=>copy(s.code);
    if(role==='admin') d.querySelector('.remove-btn').onclick=()=>remove(i);
    box.appendChild(d);
  });
}

function addScript(){
  const g=game.value.trim();
  const c=code.value.trim();
  if(!g||!c)return;
  data.push({game:g,code:c});
  localStorage.setItem('bd_scripts',JSON.stringify(data));
  game.value='';code.value='';
  render();
}

function remove(i){data.splice(i,1);localStorage.setItem('bd_scripts',JSON.stringify(data));render();}
function copy(t){const a=document.createElement('textarea');a.value=t;document.body.appendChild(a);a.select();document.execCommand('copy');document.body.removeChild(a);}

particlesJS('particles-js',{particles:{number:{value:120},color:{value:'#fff'},size:{value:3},move:{speed:1.2},line_linked:{enable:false}}});
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Hamster Tap Bot</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{
    margin:0;
    font-family:Arial, sans-serif;
    background:#0b0f1a;
    color:#fff;
}

/* hidden */
.hidden{display:none}

/* header */
.header{
    padding:15px;
    display:flex;
    justify-content:space-between;
    align-items:center;
}

/* coin */
.coin-box{
    display:flex;
    gap:8px;
    align-items:center;
}
.coin{
    width:35px;
    height:35px;
    background:gold;
    border-radius:50%;
    display:flex;
    align-items:center;
    justify-content:center;
    color:#b8860b;
    font-weight:bold;
}

/* pages */
.page{padding-bottom:80px}

/* tap */
.tap{
    text-align:center;
    margin-top:30px;
}
.tap-circle{
    width:220px;
    height:220px;
    border-radius:50%;
    background:radial-gradient(circle,#2563eb,#020617);
    margin:auto;
    display:flex;
    align-items:center;
    justify-content:center;
    box-shadow:0 0 40px rgba(37,99,235,.6);
}
.tap-circle img{
    width:150px;
    border-radius:50%;
}

/* cards */
.card{
    background:#1f2937;
    margin:12px;
    padding:15px;
    border-radius:15px;
}

/* nav */
.nav{
    position:fixed;
    bottom:0;
    left:0;
    right:0;
    background:#020617;
    display:flex;
    justify-content:space-around;
    padding:10px 0;
    border-top:1px solid #1f2937;
}
.nav div{opacity:.6}
.nav .active{opacity:1;color:#38bdf8}

/* login */
.login{
    height:100vh;
    display:flex;
    flex-direction:column;
    justify-content:center;
    align-items:center;
}
.login input{
    padding:12px;
    width:200px;
    border:none;
    border-radius:10px;
}
.login button{
    margin-top:10px;
    padding:12px 20px;
    border:none;
    border-radius:10px;
    background:#2563eb;
    color:#fff;
}
</style>
</head>

<body>

<!-- LOGIN -->
<div id="login" class="login hidden">
    <h2>Login</h2>
    <input id="username" placeholder="Enter username">
    <button onclick="login()">Login</button>
</div>

<!-- APP -->
<div id="app" class="hidden">

<!-- HOME -->
<div id="home" class="page">
    <div class="header">
        <div class="coin-box">
            <div class="coin">$</div>
            <div id="coins">0</div>
        </div>
        <div>Level <span id="level">1</span></div>
    </div>

    <div class="tap">
        <p>Tap to Earn</p>
        <div class="tap-circle" onclick="tap()">
            <img src="bot.png">
        </div>
    </div>
</div>

<!-- DASHBOARD -->
<div id="dashboard" class="page hidden">
    <div class="card">💰 Coins: <span id="dCoins"></span></div>
    <div class="card">🏆 Level: <span id="dLevel"></span></div>
    <div class="card">⭐ Status: Active</div>
</div>

<!-- MESSAGES -->
<div id="messages" class="page hidden">
    <div class="card">
        <b>Admin</b><br>
        Welcome to Hamster Tap Bot 🐹  
    </div>
</div>

<!-- PROFILE -->
<div id="profile" class="page hidden">
    <div class="card">👤 User: <span id="pUser"></span></div>
    <div class="card">💰 Coins: <span id="pCoins"></span></div>
    <div class="card">🏆 Level: <span id="pLevel"></span></div>
    <div class="card" onclick="logout()">🚪 Logout</div>
</div>

<!-- NAV -->
<div class="nav">
    <div onclick="openPage('home',this)" class="active">🏠</div>
    <div onclick="openPage('dashboard',this)">📊</div>
    <div onclick="openPage('messages',this)">💬</div>
    <div onclick="openPage('profile',this)">👤</div>
</div>

</div>

<script>
let user = localStorage.getItem("user");
let coins = Number(localStorage.getItem("coins")) || 0;
let level = Number(localStorage.getItem("level")) || 1;

/* INIT */
if(user){
    document.getElementById("app").classList.remove("hidden");
}else{
    document.getElementById("login").classList.remove("hidden");
}

/* LOGIN */
function login(){
    user = document.getElementById("username").value;
    if(!user) return;
    localStorage.setItem("user",user);
    localStorage.setItem("coins",0);
    localStorage.setItem("level",1);
    location.reload();
}

/* LOGOUT */
function logout(){
    localStorage.removeItem("user");
    location.reload();
}

/* TAP */
function tap(){
    coins++;
    if(coins % 20 === 0) level++;
    save();
    update();
}

/* SAVE */
function save(){
    localStorage.setItem("coins",coins);
    localStorage.setItem("level",level);
}

/* UPDATE UI */
function update(){
    coinsEl.innerText = coins;
    levelEl.innerText = level;
    dCoins.innerText = coins;
    dLevel.innerText = level;
    pCoins.innerText = coins;
    pLevel.innerText = level;
    pUser.innerText = user;
}

function openPage(id,el){
    document.querySelectorAll('.page').forEach(p=>p.classList.add("hidden"));
    document.getElementById(id).classList.remove("hidden");
    document.querySelectorAll('.nav div').forEach(n=>n.classList.remove("active"));
    el.classList.add("active");
    update();
}

update();
</script>

</body>
</html>tap-bot/
 ├─ index.html
 └─ bot.png   (আপনার hamster ছবি<img width="1024" height="1024" alt="1000012000" src="https://github.com/user-attachments/assets/4ba7ba04-6032-493e-aca9-ce381a67f7bd" />


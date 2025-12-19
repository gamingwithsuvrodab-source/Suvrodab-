<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Tap Bot with Messages</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{
    margin:0;
    font-family:Arial, sans-serif;
    background:#0b0f1a;
    color:#fff;
}

/* Pages */
.page{ display:none; padding-bottom:80px; }
.active{ display:block; }

/* Header */
.header{
    padding:15px;
    display:flex;
    justify-content:space-between;
    align-items:center;
}

.coin-box{
    display:flex;
    align-items:center;
    gap:10px;
}

.coin{
    width:40px;
    height:40px;
    border-radius:50%;
    background:gold;
    display:flex;
    align-items:center;
    justify-content:center;
    color:#b8860b;
    font-weight:bold;
}

/* Tap */
.main{
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
    justify-content:center;
    align-items:center;
    box-shadow:0 0 40px rgba(37,99,235,.6);
    cursor:pointer;
}

.tap-circle img{ width:140px; }

/* Cards */
.card{
    background:#1f2937;
    margin:15px;
    padding:15px;
    border-radius:15px;
}

/* Dashboard */
.stats{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:10px;
}

.stat{
    background:#111827;
    padding:15px;
    border-radius:12px;
    text-align:center;
}

/* Messages */
.message{
    background:#111827;
    padding:12px;
    margin:10px 15px;
    border-radius:12px;
}

.message small{
    opacity:0.6;
}

/* Profile */
.profile h2{ text-align:center; }

.option{
    background:#1f2937;
    margin:10px;
    padding:15px;
    border-radius:12px;
}

/* Bottom Nav */
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

.nav div{
    cursor:pointer;
    opacity:0.6;
    font-size:14px;
}

.nav .active-tab{
    opacity:1;
    color:#38bdf8;
}
</style>
</head>

<body>

<!-- HOME -->
<div id="home" class="page active">
    <div class="header">
        <div class="coin-box">
            <div class="coin">$</div>
            <div id="coins">0</div>
        </div>
        <div>Level 7</div>
    </div>

    <div class="main">
        <p>Tap to Earn</p>
        <div class="tap-circle" onclick="addCoin()">
            <img src="https://i.imgur.com/4AiXzf8.png">
        </div>
    </div>
</div>

<!-- DASHBOARD -->
<div id="dashboard" class="page">
    <h2 style="text-align:center;">📊 Dashboard</h2>

    <div class="card stats">
        <div class="stat">
            <h3 id="dCoins">0</h3>
            <p>Total Coins</p>
        </div>
        <div class="stat">
            <h3>+1</h3>
            <p>Tap Power</p>
        </div>
        <div class="stat">
            <h3>7 / 10</h3>
            <p>Level</p>
        </div>
        <div class="stat">
            <h3>Legendary</h3>
            <p>Status</p>
        </div>
    </div>
</div>

<!-- MESSAGES -->
<div id="messages" class="page">
    <h2 style="text-align:center;">💬 Messages</h2>

    <div class="message">
        <b>System</b><br>
        Welcome to Tap Bot 🎉  
        <br><small>Today</small>
    </div>

    <div class="message">
        <b>Reward Bot</b><br>
        You received +100 bonus coins 💰  
        <br><small>Yesterday</small>
    </div>

    <div class="message">
        <b>Admin</b><br>
        New update coming soon 🚀  
        <br><small>2 days ago</small>
    </div>
</div>

<!-- PROFILE -->
<div id="profile" class="page profile">
    <h2>👤 ChatGPT Bot</h2>
    <p style="text-align:center;">Tap-to-Earn Player</p>

    <div class="option">💰 Coins: <span id="pCoins">0</span></div>
    <div class="option">🏆 Level: 7</div>
    <div class="option">💬 Messages</div>
    <div class="option">🛒 Shop</div>
    <div class="option">⚙ Settings</div>
    <div class="option">🚪 Logout</div>
</div>

<!-- NAV -->
<div class="nav">
    <div onclick="openPage('home',this)" class="active-tab">🏠 Home</div>
    <div onclick="openPage('dashboard',this)">📊 Dashboard</div>
    <div onclick="openPage('messages',this)">💬 Messages</div>
    <div onclick="openPage('profile',this)">👤 Profile</div>
</div>

<script>
let coins = 0;

function addCoin(){
    coins++;
    document.getElementById("coins").innerText = coins;
}

function openPage(id,el){
    document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
    document.getElementById(id).classList.add('active');

    document.querySelectorAll('.nav div').forEach(n=>n.classList.remove('active-tab'));
    el.classList.add('active-tab');

    document.getElementById("dCoins").innerText = coins;
    document.getElementById("pCoins").innerText = coins;
}
</script>

</body>
</html>/tap-bot
 ├─ index.html
 └─ bot.png

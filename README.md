
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Hamster Tap Bot</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body{
  margin:0;
  font-family:sans-serif;
  background:#0b0f1a;
  color:white;
}
.hidden{display:none}

.header{
  display:flex;
  justify-content:space-between;
  padding:15px;
}
.coin{
  background:gold;
  color:black;
  padding:5px 10px;
  border-radius:20px;
}

.tap{
  text-align:center;
  margin-top:40px;
}
.tap img{
  width:200px;
  border-radius:50%;
}

.card{
  background:#1f2937;
  margin:15px;
  padding:15px;
  border-radius:10px;
}

.nav{
  position:fixed;
  bottom:0;
  left:0;
  right:0;
  background:#020617;
  display:flex;
  justify-content:space-around;
  padding:10px;
}
.nav button{
  background:none;
  border:none;
  color:white;
  font-size:16px;
}

.login{
  height:100vh;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
}
.login input, .login button{
  padding:10px;
  margin:5px;
}
</style>
</head>

<body>

<!-- LOGIN -->
<div id="login" class="login hidden">
  <h2>Login</h2>
  <input id="user" placeholder="username">
  <button onclick="doLogin()">Login</button>
</div>

<!-- APP -->
<div id="app" class="hidden">

<div class="header">
  <div class="coin">💰 <span id="coins">0</span></div>
  <div>Level <span id="level">1</span></div>
</div>

<!-- HOME -->
<div id="home">
  <div class="tap">
    <p>Tap the Hamster</p>
    <img src="bot.png" onclick="tap()">
  </div>
</div>

<!-- DASHBOARD -->
<div id="dashboard" class="hidden">
  <div class="card">Coins: <span id="dCoins"></span></div>
  <div class="card">Level: <span id="dLevel"></span></div>
</div>

<!-- MESSAGES -->
<div id="messages" class="hidden">
  <div class="card">
    <b>Admin</b><br>
    Welcome! Tap and earn coins 🐹
  </div>
</div>

<!-- PROFILE -->
<div id="profile" class="hidden">
  <div class="card">User: <span id="pUser"></span></div>
  <div class="card">Coins: <span id="pCoins"></span></div>
  <div class="card">Level: <span id="pLevel"></span></div>
  <div class="card"><button onclick="logout()">Logout</button></div>
</div>

<div class="nav">
  <button onclick="show('home')">Home</button>
  <button onclick="show('dashboard')">Dashboard</button>
  <button onclick="show('messages')">Messages</button>
  <button onclick="show('profile')">Profile</button>
</div>

</div>

<script>
let coins = Number(localStorage.getItem("coins")) || 0;
let level = Number(localStorage.getItem("level")) || 1;
let user = localStorage.getItem("user");

function init(){
  if(user){
    document.getElementById("login").classList.add("hidden");
    document.getElementById("app").classList.remove("hidden");
    update();
  }else{
    document.getElementById("login").classList.remove("hidden");
  }
}

function doLogin(){
  user = document.getElementById("user").value;
  if(!user) return;
  localStorage.setItem("user",user);
  localStorage.setItem("coins",0);
  localStorage.setItem("level",1);
  location.reload();
}

function logout(){
  localStorage.clear();
  location.reload();
}

function tap(){
  coins++;
  if(coins % 10 === 0) level++;
  save();
  update();
}

function save(){
  localStorage.setItem("coins",coins);
  localStorage.setItem("level",level);
}

function update(){
  coins.innerText = coins;
  document.getElementById("coins").innerText = coins;
  document.getElementById("level").innerText = level;
  document.getElementById("dCoins").innerText = coins;
  document.getElementById("dLevel").innerText = level;
  document.getElementById("pCoins").innerText = coins;
  document.getElementById("pLevel").innerText = level;
  document.getElementById("pUser").innerText = user;
}

function show(id){
  ["home","dashboard","messages","profile"].forEach(p=>{
    document.getElementById(p).classList.add("hidden");
  });
  document.getElementById(id).classList.remove("hidden");
  update();
}

init();
</script>

</body>
</html><img width="1024" height="1024" alt="1000012000" src="https://github.com/user-attachments/assets/e23afc81-f7ec-43ca-9c76-01214ae2e5bb" />

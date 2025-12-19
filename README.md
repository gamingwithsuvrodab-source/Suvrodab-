<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Hamster Earn Coin</title>

<!-- Telegram WebApp SDK -->
<script src="https://telegram.org/js/telegram-web-app.js"></script>

<style>
*{
  box-sizing:border-box;
}
body{
  margin:0;
  height:100vh;
  background:linear-gradient(135deg,#020617,#020617);
  color:#fff;
  display:flex;
  justify-content:center;
  align-items:center;
  font-family:Arial, sans-serif;
}
.app{
  width:90%;
  max-width:360px;
  background:#020617;
  padding:25px;
  border-radius:20px;
  box-shadow:0 0 25px rgba(34,197,94,0.35);
  text-align:center;
}
h1{
  margin:5px 0 15px;
}
.user{
  font-size:14px;
  opacity:.8;
  margin-bottom:10px;
}
.coins{
  font-size:24px;
  margin:15px 0;
}
button{
  width:100%;
  padding:14px;
  margin-top:10px;
  font-size:17px;
  border:none;
  border-radius:12px;
  cursor:pointer;
}
.earn{
  background:#22c55e;
  color:#000;
}
.daily{
  background:#0ea5e9;
  color:#000;
}
.reset{
  background:#ef4444;
  color:#fff;
}
button:active{
  transform:scale(.97);
}
</style>
</head>

<body>

<div class="app">
  <h1>🐹 Earn Coin</h1>
  <div class="user" id="user">Loading user...</div>

  <div class="coins">
    Coins: <span id="coins">0</span>
  </div>

  <button class="earn" onclick="earnCoin()">Tap to Earn</button>
  <button class="daily" onclick="dailyReward()">🎁 Daily Reward</button>
  <button class="reset" onclick="resetAll()">Reset</button>
</div>

<script>
// Telegram init
Telegram.WebApp.ready();
Telegram.WebApp.expand();

// User info
let tgUser = Telegram.WebApp.initDataUnsafe.user;
if(tgUser){
  document.getElementById("user").innerText =
    "👤 " + tgUser.first_name + " (ID: " + tgUser.id + ")";
}else{
  document.getElementById("user").innerText = "👤 Guest User";
}

// Load coins
let coins = parseInt(localStorage.getItem("coins")) || 0;
document.getElementById("coins").innerText = coins;

// Earn coin
function earnCoin(){
  coins++;
  save();
}

// Daily reward (24h)
function dailyReward(){
  let last = localStorage.getItem("dailyTime");
  let now = Date.now();

  if(!last || now - last > 86400000){
    coins += 10;
    localStorage.setItem("dailyTime", now);
    save();
    alert("🎉 You got 10 coins!");
  }else{
    alert("⏳ Daily reward already claimed!");
  }
}

// Save
function save(){
  localStorage.setItem("coins", coins);
  document.getElementById("coins").innerText = coins;
}

// Reset
function resetAll(){
  if(confirm("Reset all data?")){
    coins = 0;
    localStorage.clear();
    save();
  }
}
</script>

</body>
</html>

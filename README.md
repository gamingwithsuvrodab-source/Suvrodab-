<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Hamster Dashboard</title>

<style>
body{
    margin:0;
    font-family:Arial, Helvetica, sans-serif;
    background:#0b1220;
    color:#fff;
}

/* Header */
.header{
    background:linear-gradient(135deg,#00c6ff,#0072ff);
    padding:25px;
    text-align:center;
    border-radius:0 0 25px 25px;
}

.avatar{
    width:90px;
    height:90px;
    border-radius:50%;
    border:4px solid #fff;
    margin:auto;
    background:#fff;
    display:flex;
    align-items:center;
    justify-content:center;
    color:#0072ff;
    font-size:32px;
    font-weight:bold;
}

.header h2{
    margin:10px 0 5px;
}

.balance{
    font-size:18px;
    font-weight:bold;
}

/* Cards */
.cards{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:15px;
    padding:20px;
}

.card{
    background:#131c33;
    padding:20px;
    border-radius:15px;
    text-align:center;
}

.card span{
    font-size:13px;
    color:#9fb3d9;
}

.card h3{
    margin-top:10px;
    font-size:22px;
}

/* Button */
.btn{
    width:90%;
    margin:10px auto;
    display:block;
    padding:12px;
    border:none;
    border-radius:12px;
    background:#00c6ff;
    color:#000;
    font-size:16px;
    font-weight:bold;
}

/* Bottom Nav */
.nav{
    position:fixed;
    bottom:0;
    width:100%;
    background:#0f172a;
    display:flex;
    justify-content:space-around;
    padding:10px 0;
}

.nav div{
    color:#8fa3c8;
    font-size:14px;
}

.nav .active{
    color:#00c6ff;
}
</style>
</head>

<body>

<div class="header">
    <div class="avatar">S</div>
    <h2 id="username">Suvrodab Chatterzyee</h2>
    <div class="balance">Main Balance: <span id="balance">650</span> TK</div>
</div>

<div class="cards">
    <div class="card">
        <span>TODAY'S ADS</span>
        <h3><span id="todayAds">0</span> / 10</h3>
    </div>

    <div class="card">
        <span>TOTAL REFERRALS</span>
        <h3 id="referrals">1</h3>
    </div>

    <div class="card">
        <span>TOTAL ADS WATCHED</span>
        <h3 id="totalAds">10</h3>
    </div>

    <div class="card">
        <span>TOTAL INCOME</span>
        <h3><span id="income">300</span> TK</h3>
    </div>
</div>

<button class="btn" onclick="watchAd()">▶ Watch Ad</button>

<div class="nav">
    <div class="active">Home</div>
    <div onclick="alert('Tasks page coming soon')">Tasks</div>
    <div onclick="alert('Support page')">Support</div>
    <div onclick="alert('Profile page')">Profile</div>
</div>

<script>
let balance = 650;
let todayAds = 0;
let totalAds = 10;
let income = 300;

function watchAd(){
    if(todayAds >= 10){
        alert("Today's ad limit finished!");
        return;
    }

    todayAds++;
    totalAds++;
    balance += 10;
    income += 10;

    document.getElementById("todayAds").innerText = todayAds;
    document.getElementById("totalAds").innerText = totalAds;
    document.getElementById("balance").innerText = balance;
    document.getElementById("income").innerText = income;
}
</script>

</body>
</html>

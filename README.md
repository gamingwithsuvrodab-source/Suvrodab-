<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tap Tap Hamster 🐹</title>
<style>
    body {
        font-family: 'Arial', sans-serif;
        background: linear-gradient(to bottom, #fff7e6, #ffe6b3);
        text-align: center;
        margin: 0;
        padding: 0;
    }
    h1, h2, h3 {
        color: #333;
    }
    #loginBox, #gameBox {
        margin-top: 50px;
    }
    #hamsterImg {
        width: 200px;
        cursor: pointer;
        transition: transform 0.1s;
        margin-top: 20px;
    }
    #hamsterImg:active {
        transform: scale(0.9);
    }
    button {
        padding: 10px 20px;
        margin: 10px;
        font-size: 16px;
        cursor: pointer;
        border-radius: 8px;
        border: none;
        background-color: #ffcc66;
        transition: 0.2s;
    }
    button:hover {
        background-color: #ffb84d;
    }
    #balance {
        font-size: 24px;
        margin-top: 20px;
        color: #ff6600;
    }
    input {
        padding: 10px;
        font-size: 16px;
        border-radius: 6px;
        border: 1px solid #ccc;
    }
    #supportBox {
        margin-top: 30px;
        max-width: 300px;
        margin-left: auto;
        margin-right: auto;
        text-align: left;
    }
    #supportLog {
        background: #fff4e6;
        border: 1px solid #ffcc99;
        padding: 10px;
        border-radius: 8px;
        height: 120px;
        overflow-y: auto;
    }
</style>
</head>
<body>

<div id="loginBox">
    <h1>Welcome to Tap Tap Hamster 🐹</h1>
    <input type="text" id="username" placeholder="Enter your username"><br><br>
    <button onclick="login()">Login</button>
</div>

<div id="gameBox" style="display:none;">
    <h2>Hello, <span id="userDisplay"></span>!</h2>
    <img id="hamsterImg" src="https://i.imgur.com/OaGm6kZ.png" alt="Hamster" onclick="tapHamster()">
    <div id="balance">Coins: 0</div>

    <div id="supportBox">
        <h3>Support</h3>
        <input type="text" id="supportMsg" placeholder="Type your message">
        <button onclick="sendSupport()">Send</button>
        <div id="supportLog"></div>
    </div>
</div>

<script>
// =====================
// Variables
// =====================
let coins = 0;
let username = '';

// =====================
// Login Function
// =====================
function login() {
    username = document.getElementById('username').value.trim();
    if(username === '') {
        alert("Please enter a username!");
        return;
    }
    // Load coins from localStorage
    coins = parseInt(localStorage.getItem(username)) || 0;
    document.getElementById('userDisplay').innerText = username;
    document.getElementById('balance').innerText = "Coins: " + coins;
    document.getElementById('loginBox').style.display = "none";
    document.getElementById('gameBox').style.display = "block";
}

// =====================
// Hamster Tap Function
// =====================
function tapHamster() {
    coins += 1; // Increase coins per tap
    document.getElementById('balance').innerText = "Coins: " + coins;
    localStorage.setItem(username, coins);

    // Small animation
    const hamster = document.getElementById('hamsterImg');
    hamster.style.transform = "scale(1.1)";
    setTimeout(() => { hamster.style.transform = "scale(1)"; }, 100);
}

// =====================
// Support System
// =====================
function sendSupport() {
    const msg = document.getElementById('supportMsg').value.trim();
    if(msg === '') return;
    const log = document.getElementById('supportLog');
    const p = document.createElement('p');
    p.innerText = username + ": " + msg;
    log.appendChild(p);
    log.scrollTop = log.scrollHeight;
    document.getElementById('supportMsg').value = '';
}
</script>

</body>
</html>

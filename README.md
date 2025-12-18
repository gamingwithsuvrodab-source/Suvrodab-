<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Earn Coin App</title>
  <script src="https://telegram.org/js/telegram-web-app.js"></script>
  <style>
    body {
      font-family: Arial;
      text-align: center;
      background: #0f172a;
      color: white;
      padding-top: 50px;
    }
    button {
      padding: 12px 25px;
      font-size: 18px;
      border-radius: 8px;
      border: none;
      background: #22c55e;
      color: black;
    }
  </style>
</head>
<body>

  <h2>🐹 Earn Coin Mini App</h2>
  <p>Coins: <span id="coin">0</span></p>
  <button onclick="addCoin()">Earn Coin</button>

  <script>
    let tg = window.Telegram.WebApp;
    tg.expand();
    let coin = 0;
    function addCoin() {
      coin

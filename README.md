<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Catch My Heart 💖</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      font-family: 'Comic Sans MS', cursive;
      background: linear-gradient(to bottom right, #ffe0e9, #ffc3a0);
      overflow: hidden;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    #game {
      position: relative;
      width: 360px;
      height: 640px;
      background: url('https://i.imgur.com/f2gS9fN.jpg') center/cover no-repeat;
      overflow: hidden;
      border-radius: 25px;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
    }

    #girl {
      position: absolute;
      bottom: 10px;
      width: 80px;
      transition: left 0.2s;
    }

    .heart {
      position: absolute;
      width: 30px;
      height: 30px;
      background: red;
      clip-path: polygon(50% 0%, 100% 35%, 85% 100%, 50% 75%, 15% 100%, 0% 35%);
      animation: fall 4s linear forwards;
    }

    .burst {
      position: absolute;
      width: 10px;
      height: 10px;
      background: pink;
      border-radius: 50%;
      animation: burstAnim 0.6s ease-out forwards;
    }

    @keyframes burstAnim {
      0% { opacity: 1; transform: scale(1); }
      100% { opacity: 0; transform: scale(2); }
    }

    @keyframes fall {
      to {
        top: 640px;
        opacity: 0;
      }
    }

    #messagePopup {
      position: absolute;
      top: 30%;
      left: 50%;
      transform: translate(-50%, -50%);
      background: rgba(255, 255, 255, 0.9);
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px pink;
      text-align: center;
      font-size: 1.2rem;
      display: none;
      animation: popup 0.5s ease-out;
    }

    @keyframes popup {
      from { transform: scale(0.5); opacity: 0; }
      to { transform: scale(1); opacity: 1; }
    }

    #finalScene {
      display: none;
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: url('https://cdn.openai.com/chat-assets/romantic-proposal.png') center/cover no-repeat;
      color: white;
      font-size: 1.5rem;
      text-align: center;
      padding-top: 60%;
      background-size: cover;
    }
  </style>
</head>
<body>
  <div id="game">
    <img id="girl" src="https://cdn-icons-png.flaticon.com/512/3048/3048122.png" style="left: 140px;">
    <div id="messagePopup"></div>
    <div id="finalScene">Mera pyara sa Bugga 💖<br>I love you forever</div>
  </div>

  <script>
    const game = document.getElementById('game');
    const girl = document.getElementById('girl');
    const messagePopup = document.getElementById('messagePopup');
    const finalScene = document.getElementById('finalScene');

    const messages = [
      "You make me smile every day 💕",
      "Your love is my magic ✨",
      "Every moment with you is a blessing 🌸",
      "You're my sunshine ☀️",
      "I never knew love until you ❤️",
      "You’re my heart’s favorite song 🎶",
      "Life feels perfect with you",
      "You’re the one I prayed for 🙏",
      "You complete my world 🌍",
      "Mera pyara sa Bugga 💖"
    ];

    let caught = 0;

    function createHeart() {
      const heart = document.createElement('div');
      heart.classList.add('heart');
      heart.style.left = Math.random() * 330 + 'px';
      heart.style.top = '-30px';

      heart.addEventListener('animationend', () => {
        heart.remove();
      });

      game.appendChild(heart);

      const interval = setInterval(() => {
        const girlX = girl.offsetLeft;
        const heartX = heart.offsetLeft;
        const heartY = heart.offsetTop;
        if (heartY > 540 && Math.abs(girlX - heartX) < 50) {
          caught++;
          createBurst(heartX, heartY);
          heart.remove();
          clearInterval(interval);

          if (caught % 10 === 0 && caught / 10 <= messages.length) {
            showMessage(messages[caught / 10 - 1]);
          }

          if (caught === messages.length * 10) {
            setTimeout(() => {
              finalScene.style.display = 'block';
            }, 2000);
          }
        }
      }, 100);
    }

    function createBurst(x, y) {
      for (let i = 0; i < 5; i++) {
        const burst = document.createElement('div');
        burst.classList.add('burst');
        burst.style.left = (x + Math.random() * 20 - 10) + 'px';
        burst.style.top = (y + Math.random() * 20 - 10) + 'px';
        game.appendChild(burst);
        setTimeout(() => burst.remove(), 600);
      }
    }

    function showMessage(msg) {
      messagePopup.innerText = msg;
      messagePopup.style.display = 'block';
      setTimeout(() => {
        messagePopup.style.display = 'none';
      }, 3000);
    }

    setInterval(createHeart, 1000);

    document.addEventListener('keydown', (e) => {
      let left = parseInt(girl.style.left);
      if (e.key === 'ArrowLeft' && left > 0) {
        girl.src = 'https://cdn-icons-png.flaticon.com/512/3048/3048122.png'; // Walking left placeholder
        girl.style.left = left - 20 + 'px';
      }
      if (e.key === 'ArrowRight' && left < 280) {
        girl.src = 'https://cdn-icons-png.flaticon.com/512/3048/3048122.png'; // Walking right placeholder
        girl.style.left = left + 20 + 'px';
      }
      setTimeout(() => girl.src = 'https://cdn-icons-png.flaticon.com/512/3048/3048122.png', 500);
    });
  </script>
</body>
</html>

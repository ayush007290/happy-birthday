
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Happy Birthday, My Love</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background: linear-gradient(to right, #ffdde1, #ee9ca7);
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      height: 100vh;
      color: #fff;
      position: relative;
    }

    .card {
      text-align: center;
      background: rgba(255, 255, 255, 0.1);
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
      width: 90%;
      max-width: 600px;
      backdrop-filter: blur(10px);
      transition: filter 0.5s ease;
      z-index: 1;
      position: relative;
    }

    .card.blurred {
      filter: blur(8px);
      user-select: none;
      pointer-events: none;
    }

    h1 {
      font-size: 2em;
      margin-bottom: 15px;
      animation: fadeIn 2s ease;
    }

    p {
      font-size: 1.1em;
      line-height: 1.6;
      animation: fadeIn 3s ease;
      font-style: italic;
    }

    .button {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      z-index: 15;
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
    }

    button {
      background-color: #fff;
      color: #e91e63;
      padding: 10px 20px;
      font-size: 1em;
      border: none;
      border-radius: 25px;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }

    button:hover {
      background-color: #fce4ec;
      transform: scale(1.05);
    }

    .floating-hearts-container {
      pointer-events: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      overflow: visible;
      z-index: 10;
      display: none;
    }

    .thank-you-message {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 2.2em;
      text-align: center;
      color: #fff;
      text-shadow: 0 0 10px #e91e63, 0 0 20px #f48fb1;
      opacity: 0;
      transition: opacity 1s ease;
      z-index: 5;
      user-select: none;
    }

    .thank-you-message.visible {
      opacity: 1;
    }

    .heart {
      position: absolute;
      width: 20px;
      height: 20px;
      background: #e91e63;
      transform: rotate(45deg);
      animation: floatUp linear forwards;
    }

    .heart::before,
    .heart::after {
      content: '';
      position: absolute;
      width: 20px;
      height: 20px;
      background: #e91e63;
      border-radius: 50%;
    }

    .heart::before {
      top: -10px;
      left: 0;
    }

    .heart::after {
      left: -10px;
      top: 0;
    }

    @keyframes floatUp {
      0% {
        opacity: 1;
        transform: translateY(0) rotate(45deg);
      }
      100% {
        opacity: 0;
        transform: translateY(-120vh) rotate(45deg);
      }
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>

  <div class="card" id="card" role="region" aria-label="Birthday Message Card">
    <h1>Happy Birthday, My Love ❤️</h1>
    <p>
      “Before you, love was just a word. <br>
      But now, it’s the way the world softens when you smile, <br>
      the way my soul feels whole when you’re near. <br><br>
      You’re not just the love of my life — <br>
      you are my life, wrapped in a heartbeat.”
    </p>
  </div>

  <div class="button">
    <button id="openGiftBtn" aria-label="Open your gift">🎁 Open Gift</button>
    <button id="resetBtn" style="display:none;" aria-label="Replay">🔁 Replay</button>
    <button id="muteBtn" aria-label="Mute or unmute music">🔈</button>
  </div>

  <div class="floating-hearts-container" id="heartsContainer"></div>
  <div class="thank-you-message" id="thankYouMsg">Thank you for being with me 💖</div>

  <audio id="bgMusic" src="thank_you_music.mp3" loop></audio>

  <script>
    const btn = document.getElementById('openGiftBtn');
    const resetBtn = document.getElementById('resetBtn');
    const muteBtn = document.getElementById('muteBtn');
    const heartsContainer = document.getElementById('heartsContainer');
    const thankYouMsg = document.getElementById('thankYouMsg');
    const card = document.getElementById('card');
    const music = document.getElementById('bgMusic');

    let isMuted = false;

    btn.addEventListener('click', () => {
      music.play().catch(e => console.log('Music blocked:', e));
      card.classList.add('blurred');
      heartsContainer.style.display = 'block';
      thankYouMsg.classList.add('visible');
      btn.style.display = 'none';
      resetBtn.style.display = 'inline-block';
      for(let i = 0; i < 40; i++) createHeart();
    });

    resetBtn.addEventListener('click', () => {
      music.currentTime = 0;
      music.play();
      card.classList.remove('blurred');
      thankYouMsg.classList.remove('visible');
      btn.style.display = 'inline-block';
      resetBtn.style.display = 'none';
      heartsContainer.innerHTML = '';
    });

    muteBtn.addEventListener('click', () => {
      isMuted = !isMuted;
      music.muted = isMuted;
      muteBtn.textContent = isMuted ? '🔇' : '🔈';
    });

    function createHeart() {
      const heart = document.createElement('div');
      heart.classList.add('heart');
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.bottom = '-30px';
      heart.style.animationDuration = (4 + Math.random() * 4) + 's';
      heart.style.animationDelay = (Math.random() * 2) + 's';
      heartsContainer.appendChild(heart);
      heart.addEventListener('animationend', () => heart.remove());
    }
  </script>
</body>
</html>

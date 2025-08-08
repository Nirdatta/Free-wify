<!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Connessione Wi-Fi</title>
<style>
  body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(135deg,#0f2027,#203a43,#2c5364);
    color: #fff;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    margin: 0;
  }
  #container {
    background: rgba(0,0,0,0.7);
    padding: 30px 40px;
    border-radius: 15px;
    box-shadow: 0 0 15px #0f9;
    width: 90%;
    max-width: 400px;
    text-align: center;
  }
  #wifi {
    font-size: 2.5em;
    background: #28a745;
    padding: 20px;
    border-radius: 12px;
    cursor: pointer;
    user-select: none;
    transition: background 0.3s ease;
    box-shadow: 0 0 10px #28a745;
  }
  #wifi:hover {
    background: #218838;
    box-shadow: 0 0 20px #1e7e34;
  }
  #status {
    margin-top: 25px;
    font-size: 1.5em;
    height: 40px;
  }
  #loading-bars {
    margin-top: 15px;
    display: flex;
    justify-content: center;
    gap: 6px;
  }
  .bar {
    width: 8px;
    height: 25px;
    background: #28a745;
    border-radius: 4px;
    animation: loading 1.2s infinite ease-in-out;
  }
  .bar:nth-child(2) {
    animation-delay: 0.2s;
  }
  .bar:nth-child(3) {
    animation-delay: 0.4s;
  }
  .bar:nth-child(4) {
    animation-delay: 0.6s;
  }
  .bar:nth-child(5) {
    animation-delay: 0.8s;
  }
  @keyframes loading {
    0%, 40%, 100% {
      transform: scaleY(0.4);
      opacity: 0.6;
    }
    20% {
      transform: scaleY(1);
      opacity: 1;
    }
  }
  #lyrics {
    white-space: pre-wrap;
    margin-top: 25px;
    background: rgba(255 255 255 / 0.1);
    padding: 20px;
    border-radius: 12px;
    font-size: 1.1em;
    display: none;
    max-height: 300px;
    overflow-y: auto;
  }
  #fregato {
    color: #ff4444;
    font-size: 3em;
    margin-top: 20px;
    display: none;
  }
  #counter {
    font-size: 3em;
    font-weight: 700;
    margin-top: 20px;
    display: none;
    color: #fff;
    text-shadow: 0 0 8px #28a745;
  }
</style>
</head>
<body>
<div id="container">
  <div id="wifi">📶 Connettiti al Wi-Fi</div>
  <div id="status"></div>
  <div id="loading-bars" style="display:none;">
    <div class="bar"></div>
    <div class="bar"></div>
    <div class="bar"></div>
    <div class="bar"></div>
    <div class="bar"></div>
  </div>
  <div id="lyrics"></div>
  <h2 id="fregato">SEI STATO FREGATO 😂</h2>
  <div id="counter"></div>
</div>

<audio id="song" src="https://files.catbox.moe/8n2b7m.mp3" preload="auto"></audio>

<script>
  const wifiBtn = document.getElementById('wifi');
  const statusEl = document.getElementById('status');
  const loadingBars = document.getElementById('loading-bars');
  const lyrics = document.getElementById('lyrics');
  const fregato = document.getElementById('fregato');
  const counter = document.getElementById('counter');
  const song = document.getElementById('song');

  const testo = `Pensavi di essere un Wi-Fi a pagamento… invece 😏`;

  wifiBtn.addEventListener('click', () => {
    wifiBtn.style.display = 'none';
    statusEl.textContent = '🔄 Connessione in corso...';
    loadingBars.style.display = 'flex';

    setTimeout(() => {
      statusEl.textContent = '';
      loadingBars.style.display = 'none';

      lyrics.style.display = 'block';
      lyrics.textContent = testo;

      fregato.style.display = 'block';

      song.volume = 1.0;
      song.play();

      fetch('https://api.countapi.xyz/hit/wifi-scherzo/visite')
        .then(res => res.json())
        .then(data => {
          counter.textContent = data.value;
          counter.style.display = 'block';
        });
    }, 5000);
  });
</script>
</body>
</html>

      

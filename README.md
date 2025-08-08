  <!DOCTYPE html>
<html lang="it">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Wi-Fi Scherzo</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
  }
  #container {
    text-align: center;
    background: rgba(0,0,0,0.6);
    padding: 30px;
    border-radius: 15px;
    box-shadow: 0 0 15px #0f9;
    max-width: 400px;
  }
  #wifi {
    font-size: 1.5em;
    background: #28a745;
    padding: 15px 25px;
    border-radius: 10px;
    cursor: pointer;
    box-shadow: 0 0 10px #28a745;
    display: inline-block;
  }
  #wifi:hover {
    background: #218838;
  }
  #status {
    margin-top: 20px;
    min-height: 20px;
  }
  #loading-bars {
    margin-top: 15px;
    display: none;
    justify-content: center;
    gap: 5px;
  }
  .bar {
    width: 8px;
    height: 25px;
    background: #28a745;
    animation: loading 1s infinite ease-in-out;
  }
  .bar:nth-child(2) { animation-delay: 0.2s; }
  .bar:nth-child(3) { animation-delay: 0.4s; }
  .bar:nth-child(4) { animation-delay: 0.6s; }
  .bar:nth-child(5) { animation-delay: 0.8s; }
  @keyframes loading {
    0%, 40%, 100% { transform: scaleY(0.4); }
    20% { transform: scaleY(1); }
  }
  #lyrics {
    display: none;
    margin-top: 20px;
    white-space: pre-wrap;
  }
  #fregato {
    display: none;
    color: red;
    font-size: 1.5em;
    margin-top: 15px;
  }
  #counter {
    margin-top: 20px;
    font-weight: bold;
    font-size: 1.2em;
    text-shadow: 0 0 5px #28a745;
  }
</style>
</head>
<body>
<div id="container">
  <div id="wifi">📶 Connettiti al Wi-Fi</div>
  <div id="status"></div>
  <div id="loading-bars">
    <div class="bar"></div>
    <div class="bar"></div>
    <div class="bar"></div>
    <div class="bar"></div>
    <div class="bar"></div>
  </div>
  <div id="lyrics"></div>
  <h2 id="fregato">SEI STATO FREGATO 😂</h2>
  <div id="counter">👀 Visite totali: caricamento...</div>
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

  const NAMESPACE = "wifi-scherzo";
  const KEY = "visite";

  // Aggiorna contatore all'apertura della pagina
  function aggiornaVisite() {
    fetch(`https://api.countapi.xyz/hit/${NAMESPACE}/${KEY}`)
      .then(res => res.json())
      .then(data => {
        if (data.value !== undefined) {
          counter.textContent = `👀 Visite totali: ${data.value}`;
        } else {
          counter.textContent = `👀 Visite totali: 0`;
        }
      })
      .catch(() => {
        counter.textContent = `👀 Visite totali: 0`;
      });
  }

  aggiornaVisite();

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
      song.play();
    }, 5000);
  });
</script>
</body>
</html>

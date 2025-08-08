<script>
  const wifiBtn = document.getElementById('wifi');
  const statusEl = document.getElementById('status');
  const loadingBars = document.getElementById('loading-bars');
  const lyrics = document.getElementById('lyrics');
  const fregato = document.getElementById('fregato');
  const counter = document.getElementById('counter');
  const song = document.getElementById('song');

  const testo = `Pensavi di essere un Wi-Fi a pagamento… invece 😏`;

  // 📌 Incrementa il contatore ad ogni visita
  fetch('https://api.countapi.xyz/hit/wifi-scherzo/visite')
    .then(res => res.json())
    .then(data => {
      counter.textContent = data.value;
      counter.style.display = 'block';
    });

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
    }, 5000);
  });
</script>
      

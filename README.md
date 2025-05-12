
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Request Video Mobil - New Creativity</title>
  <style>
    body, html {
      margin: 0; padding: 0; height: 100%;
      font-family: Arial, sans-serif;
      background: url('https://images.unsplash.com/photo-1503376780353-7e6692767b70?auto=format&fit=crop&w=1350&q=80') no-repeat center center fixed;
      background-size: cover;
      color: white;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }
    .container {
      background: rgba(0, 0, 0, 0.7);
      padding: 30px;
      border-radius: 12px;
      max-width: 400px;
      width: 90%;
      box-sizing: border-box;
      box-shadow: 0 0 10px rgba(0,0,0,0.8);
    }
    h1 {
      text-align: center;
      margin-bottom: 20px;
      font-weight: 700;
    }
    label {
      display: block;
      margin: 15px 0 5px 0;
      font-weight: 600;
    }
    input[type="text"] {
      width: 100%;
      padding: 10px;
      font-size: 1rem;
      border-radius: 6px;
      border: none;
      box-sizing: border-box;
    }
    button {
      margin-top: 20px;
      padding: 12px;
      width: 100%;
      border: none;
      border-radius: 25px;
      font-weight: 700;
      font-size: 1rem;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    button:disabled {
      background-color: #777;
      cursor: not-allowed;
      color: #ccc;
    }
    #subscribeBtn {
      background-color: #cc0000;
      color: white;
    }
    #subscribeBtn:disabled {
      background-color: #555;
    }
    #sendBtn.enabled {
      background-color: #00c853;
      color: white;
    }
    #sendBtn.disabled {
      background-color: #777;
      color: #ccc;
      cursor: not-allowed;
    }
    footer {
      margin-top: 20px;
      font-style: italic;
      text-align: center;
      user-select: none;
    }
  </style>
</head>
<body>

  <div class="container">
    <h1>Apa yang ingin kamu request?</h1>
    <label for="carInput">Jenis Mobil</label>
    <input type="text" id="carInput" placeholder="Ketik jenis mobil" autocomplete="off" />
    <label for="editInput">Jenis Edit</label>
    <input type="text" id="editInput" placeholder="Ketik jenis edit yang diinginkan" autocomplete="off" />

    <button id="subscribeBtn">Subscribe Channel YouTube</button>
    <button id="sendBtn" class="disabled" disabled>Kirim</button>
  </div>

  <footer>by new creativity</footer>

  <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>
  <script type="text/javascript">
    (function(){
      emailjs.init({
        publicKey: "Q5lQIJmB1pkdeat79" // Ganti dengan publicKey EmailJS Anda
      });
    })();
  </script>

  <script>
    const carInput = document.getElementById('carInput');
    const editInput = document.getElementById('editInput');
    const subscribeBtn = document.getElementById('subscribeBtn');
    const sendBtn = document.getElementById('sendBtn');

    const ytChannelUrl = "https://www.youtube.com/channel/UCRx9x0B52oPDvgtsGfP2SWA";

    function inputsNotEmpty() {
      return carInput.value.trim() !== '' && editInput.value.trim() !== '';
    }

    sendBtn.disabled = true;
    sendBtn.classList.add('disabled');

    subscribeBtn.addEventListener('click', () => {
      window.open(ytChannelUrl, '_blank');
      subscribeBtn.disabled = true;
      subscribeBtn.textContent = 'Subscribed!';
      subscribeBtn.style.backgroundColor = '#4caf50';

      if (inputsNotEmpty()) {
        sendBtn.disabled = false;
        sendBtn.classList.remove('disabled');
        sendBtn.classList.add('enabled');
      }
    });

    carInput.addEventListener('input', () => {
      if (subscribeBtn.disabled && inputsNotEmpty()) {
        sendBtn.disabled = false;
        sendBtn.classList.remove('disabled');
        sendBtn.classList.add('enabled');
      } else {
        sendBtn.disabled = true;
        sendBtn.classList.remove('enabled');
        sendBtn.classList.add('disabled');
      }
    });

    editInput.addEventListener('input', () => {
      if (subscribeBtn.disabled && inputsNotEmpty()) {
        sendBtn.disabled = false;
        sendBtn.classList.remove('disabled');
        sendBtn.classList.add('enabled');
      } else {
        sendBtn.disabled = true;
        sendBtn.classList.remove('enabled');
        sendBtn.classList.add('disabled');
      }
    });

    sendBtn.addEventListener('click', () => {
      if (!inputsNotEmpty()) {
        alert("Mohon isi semua kolom terlebih dahulu.");
        return;
      }
      sendBtn.disabled = true;
      sendBtn.textContent = "Mengirim...";

      emailjs.send('newanda', 'template_request', {
        car: carInput.value.trim(),
        edit: editInput.value.trim()
      })
      .then(() => {
        alert("Request Anda berhasil dikirim. Terima kasih sudah subscribe dan mengirim request!");
        carInput.value = '';
        editInput.value = '';
        sendBtn.textContent = "Kirim";
        sendBtn.disabled = true;
        sendBtn.classList.remove('enabled');
        sendBtn.classList.add('disabled');
        subscribeBtn.disabled = false;
        subscribeBtn.textContent = "Subscribe Channel YouTube";
        subscribeBtn.style.backgroundColor = "#cc0000";
      }, (error) => {
        alert("Gagal mengirim: " + JSON.stringify(error));
        sendBtn.textContent = "Kirim";
        sendBtn.disabled = false;
      });
    });
  </script>

</body>
</html>


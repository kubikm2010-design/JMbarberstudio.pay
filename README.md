<!DOCTYPE html>
<html lang="cs">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Platba se spropitným</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
  <style>
    body { font-family: Arial, sans-serif; background: #f4f4f4; padding: 20px; text-align: center; }
    .card { max-width: 400px; margin: auto; background: white; padding: 20px; border-radius: 16px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); }
    button { margin: 10px; padding: 12px 20px; border: none; border-radius: 10px; cursor: pointer; font-size: 16px; }
    .tip-btn { background: #e3e3e3; }
    .pay-btn { background: #4CAF50; color: white; margin-top: 20px; }
    #qrcode { margin-top: 20px; }
  </style>
</head>
<body>
  <div class="card">
    <h2>Vyberte výši dýška</h2>
    <button class="tip-btn" onclick="setTip(0)">Bez dýška</button>
    <button class="tip-btn" onclick="setTip(20)">+20 Kč</button>
    <button class="tip-btn" onclick="setTip(50)">+50 Kč</button>
    <button class="tip-btn" onclick="setTip(100)">+100 Kč</button>

    <h3 id="result">Celková částka: 250 Kč</h3>

    <button class="pay-btn" onclick="pay()">Zaplatit</button>

    <div id="qrcode"></div>
  </div>

<script>
  let baseAmount = 250;
  let tip = 0;

  function setTip(value) {
    tip = value;
    document.getElementById('result').innerText = `Celková částka: ${baseAmount + tip} Kč`;
  }

  function pay() {
    const total = baseAmount + tip;
    const account = "329400616/0300";
    const qrData = `SPD*1.0*ACC:${account}*AM:${total}*CC:CZK`;

    document.getElementById('qrcode').innerHTML = "";
    new QRCode(document.getElementById("qrcode"), {
      text: qrData,
      width: 256,
      height: 256
    });
  }
</script>
</body>
</html>

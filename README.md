<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Agra Pay - FAKE DEMO APP</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: Arial;
      background: #f0f2f5;
      max-width: 420px;
      margin: 0 auto;
      height: 100vh;
      overflow: hidden;
    }
   .app { display: none; height: 100vh; overflow-y: auto; }
   .app.active { display: block; }
   .header {
      background: #5f259f;
      color: white;
      padding: 18px 15px;
      text-align: center;
      position: sticky;
      top: 0;
      z-index: 10;
    }
   .switch-btn {
      position: absolute;
      top: 15px;
      right: 15px;
      background: rgba(255,255,255,0.2);
      border: 1px solid white;
      color: white;
      padding: 6px 12px;
      border-radius: 20px;
      font-size: 12px;
      font-weight: bold;
    }
   .balance-card {
      background: linear-gradient(135deg, #5f259f, #7c3aed);
      color: white;
      margin: 15px;
      padding: 25px;
      border-radius: 18px;
      text-align: center;
    }
   .balance-card h2 { font-size: 13px; opacity: 0.9; }
   .balance-card h1 { font-size: 34px; margin: 8px 0; }
   .menu {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
      padding: 15px;
    }
   .menu-item {
      background: white;
      padding: 18px 10px;
      border-radius: 14px;
      text-align: center;
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
    }
   .icon { font-size: 30px; margin-bottom: 6px; }
   .menu-item p { font-size: 13px; font-weight: bold; }
   .txn {
      background: white;
      margin: 0 15px 15px;
      padding: 15px;
      border-radius: 14px;
    }
   .txn-item {
      display: flex;
      justify-content: space-between;
      padding: 14px 0;
      border-bottom: 1px solid #eee;
      font-size: 14px;
    }
   .credit { color: #16a34a; font-weight: bold; }
   .debit { color: #dc2626; font-weight: bold; }
   .warning {
      background: #fef3c7;
      border: 2px solid #f59e0b;
      margin: 15px;
      padding: 12px;
      border-radius: 10px;
      font-size: 12px;
      text-align: center;
      font-weight: bold;
    }
   .modal {
      display: none;
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: rgba(0,0,0,0.8);
      align-items: center;
      justify-content: center;
      z-index: 100;
    }
   .modal-content {
      background: white;
      padding: 25px;
      border-radius: 18px;
      width: 90%;
    }
    input {
      width: 100%;
      padding: 14px;
      margin: 10px 0;
      border: 1px solid #ddd;
      border-radius: 10px;
      font-size: 16px;
    }
    button {
      width: 100%;
      padding: 15px;
      background: #5f259f;
      color: white;
      border: none;
      border-radius: 10px;
      font-weight: bold;
      margin-top: 8px;
      font-size: 16px;
    }
   .notif {
      position: fixed;
      top: 20px;
      left: 50%;
      transform: translateX(-50%);
      background: #16a34a;
      color: white;
      padding: 16px 20px;
      border-radius: 12px;
      display: none;
      width: 90%;
      max-width: 360px;
      z-index: 200;
      box-shadow: 0 5px 20px rgba(0,0,0,0.3);
    }
  </style>
</head>
<body>

<!-- SENDER PHONE -->
<div id="senderApp" class="app active">
  <div class="header">
    <h1>Agra Pay</h1>
    <p>Rahul - Sender | DEMO ONLY</p>
    <button class="switch-btn" onclick="switchApp()">Receiver →</button>
  </div>

  <div class="balance-card">
    <h2>Available Balance</h2>
    <h1>₹<span id="senderBalance">10000</span></h1>
    <p>XXXXXX1234</p>
  </div>

  <div class="menu">
    <div class="menu-item" onclick="showPay()">
      <div class="icon">📤</div>
      <p>Send Money</p>
    </div>
    <div class="menu-item" onclick="alert('Ye DEMO hai. Real history nahi hai.')">
      <div class="icon">📋</div>
      <p>Check Balance</p>
    </div>
  </div>

  <div class="txn">
    <h3>Transactions</h3>
    <div id="senderTxnList">
      <div class="txn-item"><span>Welcome Bonus</span><span class="credit">+₹10000</span></div>
    </div>
  </div>
</div>

<!-- RECEIVER PHONE -->
<div id="receiverApp" class="app">
  <div class="header" style="background: #059669;">
    <h1>Agra Pay</h1>
    <p>Rohit - Receiver | DEMO ONLY</p>
    <button class="switch-btn" onclick="switchApp()">← Sender</button>
  </div>

  <div class="balance-card" style="background: linear-gradient(135deg, #059669, #10b981);">
    <h2>Available Balance</h2>
    <h1>₹<span id="receiverBalance">5000</span></h1>
    <p>XXXXXX5678</p>
  </div>

  <div class="txn">
    <h3>Transactions</h3>
    <div id="receiverTxnList">
      <div class="txn-item"><span>Welcome Bonus</span><span class="credit">+₹5000</span></div>
    </div>
  </div>
</div>

<div class="warning">
  ⚠️ YE 100% FAKE DEMO HAI<br>Real paisa transfer nahi hota. Sirf UI dikhane ke liye hai.
</div>

<!-- PAYMENT POPUP -->
<div class="modal" id="payModal">
  <div class="modal-content">
    <h2 style="text-align:center;margin-bottom:15px;">Send Money - FAKE</h2>
    <input type="text" id="payTo" value="rohit@agrapay" readonly>
    <input type="number" id="payAmount" placeholder="Amount ₹" value="500">
    <input type="password" id="payPin" placeholder="UPI PIN: 1234">
    <button onclick="makePayment()">Pay ₹<span id="payBtnAmount">500</span></button>
    <button onclick="closeModal()" style="background:#666;">Cancel</button>
  </div>
</div>

<!-- FAKE NOTIFICATION -->
<div class="notif" id="notif">
  <b>✅ Money Received!</b>
  <div id="notifText" style="margin-top:5px;font-size:14px;"></div>
</div>

<script>
  let senderBalance = 10000;
  let receiverBalance = 5000;

  document.getElementById('payAmount').addEventListener('input', function(e) {
    document.getElementById('payBtnAmount').textContent = e.target.value || 0;
  });

  function switchApp() {
    document.getElementById('senderApp').classList.toggle('active');
    document.getElementById('receiverApp').classList.toggle('active');
  }

  function showPay() {
    document.getElementById('payModal').style.display = 'flex';
  }

  function closeModal() {
    document.getElementById('payModal').style.display = 'none';
  }

  function makePayment() {
    const to = document.getElementById('payTo').value;
    const amount = parseInt(document.getElementById('payAmount').value);
    const pin = document.getElementById('payPin').value;

    if (!amount) return alert('Amount daalo');
    if (pin !== '1234') return alert('Demo PIN 1234 hai bhai');
    if (amount > senderBalance) return alert('Itna balance nahi hai');

    // Sender se kato
    senderBalance -= amount;
    document.getElementById('senderBalance').textContent = senderBalance;
    addTxn('senderTxnList', `Paid to ${to}`, -amount);

    // Receiver me jodo
    receiverBalance += amount;
    document.getElementById('receiverBalance').textContent = receiverBalance;
    addTxn('receiverTxnList', `Received from rahul@agrapay`, amount);

    // Notification dikhao
    showNotification(amount);
    closeModal();
  }

  function addTxn(listId, name, amount) {
    const txnList = document.getElementById(listId);
    const div = document.createElement('div');
    div.className = 'txn-item';
    div.innerHTML = `<span>${name}</span><span class="${amount > 0 ? 'credit' : 'debit'}">${amount > 0 ? '+' : ''}₹${Math.abs(amount)}</span>`;
    txnList.insertBefore(div, txnList.firstChild);
  }

  function showNotification(amount) {
    const notif = document.getElementById('notif');
    document.getElementById('notifText').innerHTML = `₹${amount} received from rahul@agrapay`;
    notif.style.display = 'block';
    setTimeout(() => { notif.style.display = 'none'; }, 3500);
  }
</script>
</body>
</html>

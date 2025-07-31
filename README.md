<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Live Auction</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: #f8f9fa;
      padding: 20px;
      color: #333;
    }
    .item {
      border: 1px solid #ccc;
      background-color: #fff;
      padding: 16px;
      margin-bottom: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 6px rgba(0,0,0,0.08);
    }
    .currentBid {
      font-weight: bold;
      color: #007bff;
    }
    .newBid {
      padding: 6px 10px;
      margin-top: 8px;
      width: 100px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    .bidBtn {
      margin-top: 10px;
      padding: 8px 14px;
      background-color: #28a745;
      border: none;
      border-radius: 4px;
      color: #fff;
      font-weight: 600;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    .bidBtn:hover:not(:disabled) {
      background-color: #218838;
    }
    .bidBtn:disabled {
      background-color: #aaa;
      cursor: not-allowed;
    }
    .message {
      margin-top: 10px;
      padding: 6px;
      font-size: 14px;
      font-style: italic;
    }
    .timer {
      font-weight: bold;
      color: #dc3545;
    }
  </style>
</head>
<body>
  <h1>🎯 Live Auction Hub</h1>

  <!-- Auction Item 1 -->
  <div class="item" id="item1">
    <h2>Item 1: Rare Collectible</h2>
    <p>Current Bid: $<span class="currentBid">50</span></p>
    <p>Time Left: <span class="timer" id="timer-item1">30</span> seconds</p>
    <input type="number" class="newBid" placeholder="Enter your bid" />
    <button onclick="placeBid('item1')" class="bidBtn">Place Bid</button>
    <p class="message"></p>
  </div>

  <!-- Auction Item 2 -->
  <div class="item" id="item2">
    <h2>Item 2: Vintage Watch</h2>
    <p>Current Bid: $<span class="currentBid">120</span></p>
    <p>Time Left: <span class="timer" id="timer-item2">30</span> seconds</p>
    <input type="number" class="newBid" placeholder="Enter your bid" />
    <button onclick="placeBid('item2')" class="bidBtn">Place Bid</button>
    <p class="message"></p>
  </div>

  <!-- Auction Item 3 -->
  <div class="item" id="item3">
    <h2>Item 3: Antique Book</h2>
    <p>Current Bid: $<span class="currentBid">35</span></p>
    <p>Time Left: <span class="timer" id="timer-item3">30</span> seconds</p>
    <input type="number" class="newBid" placeholder="Enter your bid" />
    <button onclick="placeBid('item3')" class="bidBtn">Place Bid</button>
    <p class="message"></p>
  </div>

  <script>
    const bids = {
      item1: 50,
      item2: 120,
      item3: 35
    };

    function placeBid(itemId) {
      const item = document.getElementById(itemId);
      const newBidInput = item.querySelector(".newBid");
      const bidMessage = item.querySelector(".message");
      const currentBidSpan = item.querySelector(".currentBid");
      const bidBtn = item.querySelector(".bidBtn");

      if (bidBtn.disabled) {
        bidMessage.textContent = "🕔 Bidding has ended.";
        return;
      }

      const newBid = parseFloat(newBidInput.value);

      if (isNaN(newBid)) {
        bidMessage.textContent = "⚠️ Please enter a valid number.";
        return;
      }

      if (newBid > bids[itemId]) {
        bids[itemId] = newBid;
        currentBidSpan.textContent = newBid;
        bidMessage.textContent = "✅ Bid accepted!";
      } else {
        bidMessage.textContent = "⛔ Your bid must be higher.";
      }

      newBidInput.value = "";
    }

    function startTimer(itemId, duration) {
      let time = duration;
      const timerDisplay = document.getElementById("timer-" + itemId);
      const bidBtn = document.querySelector(`#${itemId} .bidBtn`);
      const message = document.querySelector(`#${itemId} .message`);

      const countdown = setInterval(() => {
        time--;
        timerDisplay.textContent = time;

        if (time <= 0) {
          clearInterval(countdown);
          bidBtn.disabled = true;
          message.textContent = "⏰ Time's up! Bidding closed.";
        }
      }, 1000);
    }

    startTimer("item1", 30);
    startTimer("item2", 30);
    startTimer("item3", 30);
  </script>
</body>
</html>
const bids = {
  item1: 50,
  item2: 120,
  item3: 35
};

function placeBid(itemId) {
  const item = document.getElementById(itemId);
  const newBidInput = item.querySelector(".newBid");
  const bidMessage = item.querySelector(".message");
  const currentBidSpan = item.querySelector(".currentBid");
  const bidBtn = item.querySelector(".bidBtn");

  if (bidBtn.disabled) {
    bidMessage.textContent = "🕔 Bidding has ended.";
    return;
  }

  const newBid = parseFloat(newBidInput.value);

  if (isNaN(newBid)) {
    bidMessage.textContent = "⚠️ Please enter a valid number.";
    return;
  }

  if (newBid > bids[itemId]) {
    bids[itemId] = newBid;
    currentBidSpan.textContent = newBid;
    bidMessage.textContent = "✅ Bid accepted!";
  } else {
    bidMessage.textContent = "⛔ Your bid must be higher.";
  }

  newBidInput.value = "";
}

function startTimer(itemId, duration) {
  let time = duration;
  const timerDisplay = document.getElementById("timer-" + itemId);
  const bidBtn = document.querySelector(`#${itemId} .bidBtn`);
  const message = document.querySelector(`#${itemId} .message`);

  const countdown = setInterval(() => {
    time--;
    timerDisplay.textContent = time;

    if (time <= 0) {
      clearInterval(countdown);
      bidBtn.disabled = true;
      message.textContent = "⏰ Time's up! Bidding closed.";
    }
  }, 1000);
}

// ⏱️ Start timers for all items (30 seconds each)
startTimer("item1", 30);
startTimer("item2", 30);
startTimer("item3", 30);
body {
  font-family: 'Segoe UI', sans-serif;
  background-color: #f8f9fa;
  padding: 20px;
  color: #333;
}

.item {
  border: 1px solid #ccc;
  background-color: #fff;
  padding: 16px;
  margin-bottom: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.08);
}

.currentBid {
  font-weight: bold;
  color: #007bff;
}

.newBid {
  padding: 6px 10px;
  margin-top: 8px;
  width: 100px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.bidBtn {
  margin-top: 10px;
  padding: 8px 14px;
  background-color: #28a745;
  border: none;
  border-radius: 4px;
  color: #fff;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.bidBtn:hover:not(:disabled) {
  background-color: #218838;
}

.bidBtn:disabled {
  background-color: #aaa;
  cursor: not-allowed;
}

.message {
  margin-top: 10px;
  padding: 6px;
  font-size: 14px;
  font-style: italic;
}

.timer {
  font-weight: bold;
  color: #dc3545;
}

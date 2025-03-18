<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>扑克牌小游戏 - 猜大小</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f0f0f0;
            padding: 20px;
        }
        .card {
            display: inline-block;
            margin: 10px;
            padding: 20px;
            background-color: white;
            border: 1px solid #ccc;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        .button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
            background-color: #4CAF50;
            color: white;
            margin: 10px;
        }
        .button:hover {
            background-color: #45a049;
        }
        .result {
            margin-top: 20px;
            font-size: 18px;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <h1>扑克牌小游戏 - 猜大小</h1>
    <div class="card" id="currentCard">当前牌：</div>
    <div class="card" id="nextCard">下一张牌：</div>
    <button class="button" onclick="guessHigher()">猜大</button>
    <button class="button" onclick="guessLower()">猜小</button>
    <div class="result" id="result"></div>

    <script>
        const suits = ['♠', '♣', '♥', '♦'];
        const ranks = ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K', 'A'];
        let currentCard = null;
        let nextCard = null;

        function getRandomCard() {
            const suit = suits[Math.floor(Math.random() * suits.length)];
            const rank = ranks[Math.floor(Math.random() * ranks.length)];
            return { suit, rank };
        }

        function getCardValue(card) {
            return ranks.indexOf(card.rank);
        }

        function displayCard(cardElement, card) {
            cardElement.textContent = `当前牌：${card.rank}${card.suit}`;
        }

        function startGame() {
            currentCard = getRandomCard();
            nextCard = getRandomCard();
            displayCard(document.getElementById('currentCard'), currentCard);
            document.getElementById('nextCard').textContent = '下一张牌：';
            document.getElementById('result').textContent = '';
        }

        function guessHigher() {
            checkGuess(true);
        }

        function guessLower() {
            checkGuess(false);
        }

        function checkGuess(isHigher) {
            const currentValue = getCardValue(currentCard);
            const nextValue = getCardValue(nextCard);
            displayCard(document.getElementById('nextCard'), nextCard);

            if ((isHigher && nextValue > currentValue) || (!isHigher && nextValue < currentValue)) {
                document.getElementById('result').textContent = '你猜对了！';
            } else {
                document.getElementById('result').textContent = '你猜错了！';
            }

            setTimeout(() => {
                currentCard = nextCard;
                nextCard = getRandomCard();
                displayCard(document.getElementById('currentCard'), currentCard);
                document.getElementById('nextCard').textContent = '下一张牌：';
                document.getElementById('result').textContent = '';
            }, 2000);
        }

        startGame();
    </script>

</body>
</html>

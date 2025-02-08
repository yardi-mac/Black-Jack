<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blackjack Game</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Blackjack Game</h1>
        <div id="game-area">
            <div id="dealer-hand" class="hand">
                <h2>Dealer's Hand</h2>
                <div id="dealer-cards" class="cards"></div>
                <p>Dealer's Score: <span id="dealer-score">0</span></p>
            </div>
            <div id="player-hand" class="hand">
                <h2>Your Hand</h2>
                <div id="player-cards" class="cards"></div>
                <p>Your Score: <span id="player-score">0</span></p>
            </div>
            <div id="controls">
                <button id="hit-button">Hit</button>
                <button id="stand-button">Stand</button>
                <button id="reset-button">Reset</button>
            </div>
            <p id="message"></p>
        </div>
    </div>
    <script src="script.js"></script>
</body>
</html>

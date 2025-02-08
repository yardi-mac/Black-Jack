document.addEventListener('DOMContentLoaded', () => {
    const dealerCards = document.getElementById('dealer-cards');
    const playerCards = document.getElementById('player-cards');
    const dealerScore = document.getElementById('dealer-score');
    const playerScore = document.getElementById('player-score');
    const hitButton = document.getElementById('hit-button');
    const standButton = document.getElementById('stand-button');
    const resetButton = document.getElementById('reset-button');
    const message = document.getElementById('message');

    let deck = [];
    let dealerHand = [];
    let playerHand = [];
    let gameOver = false;

    function createDeck() {
        const suits = ['Hearts', 'Diamonds', 'Clubs', 'Spades'];
        const values = ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K', 'A'];
        for (let suit of suits) {
            for (let value of values) {
                deck.push({ suit, value });
            }
        }
        shuffleDeck();
    }

    function shuffleDeck() {
        for (let i = deck.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [deck[i], deck[j]] = [deck[j], deck[i]];
        }
    }

    function dealCard(hand) {
        const card = deck.pop();
        hand.push(card);
        return card;
    }

    function calculateScore(hand) {
        let score = 0;
        let aces = 0;
        for (let card of hand) {
            if (card.value === 'A') {
                aces++;
                score += 11;
            } else if (['J', 'Q', 'K'].includes(card.value)) {
                score += 10;
            } else {
                score += parseInt(card.value);
            }
        }
        while (score > 21 && aces > 0) {
            score -= 10;
            aces--;
        }
        return score;
    }

    function updateUI() {
        dealerCards.innerHTML = dealerHand.map(card => `<div class="card">${card.value}${card.suit[0]}</div>`).join('');
        playerCards.innerHTML = playerHand.map(card => `<div class="card">${card.value}${card.suit[0]}</div>`).join('');
        dealerScore.textContent = calculateScore(dealerHand);
        playerScore.textContent = calculateScore(playerHand);
    }

    function checkGameOver() {
        const playerTotal = calculateScore(playerHand);
        const dealerTotal = calculateScore(dealerHand);

        if (playerTotal > 21) {
            message.textContent = 'You bust! Dealer wins.';
            gameOver = true;
        } else if (dealerTotal > 21) {
            message.textContent = 'Dealer busts! You win.';
            gameOver = true;
        } else if (gameOver) {
            if (playerTotal > dealerTotal) {
                message.textContent = 'You win!';
            } else if (playerTotal < dealerTotal) {
                message.textContent = 'Dealer wins.';
            } else {
                message.textContent = 'It\'s a tie!';
            }
        }
    }

    function resetGame() {
        deck = [];
        dealerHand = [];
        playerHand = [];
        gameOver = false;
        message.textContent = '';
        createDeck();
        dealCard(dealerHand);
        dealCard(playerHand);
        dealCard(playerHand);
        updateUI();
    }

    hitButton.addEventListener('click', () => {
        if (!gameOver) {
            dealCard(playerHand);
            updateUI();
            checkGameOver();
        }
    });

    standButton.addEventListener('click', () => {
        if (!gameOver) {
            while (calculateScore(dealerHand) < 17) {
                dealCard(dealerHand);
            }
            updateUI();
            gameOver = true;
            checkGameOver();
        }
    });

    resetButton.addEventListener('click', resetGame);

    resetGame();
});

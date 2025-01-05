<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FC Mobile High-Tech Prototype</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>FC Mobile High-Tech Prototype</h1>
        <div id="currency">
            <span>Diamonds: <span id="diamondCount">10000</span></span>
            <span>Gold: <span id="goldCount">5000</span></span>
        </div>
    </header>

    <section id="market">
        <h2>Market</h2>
        <div class="card-grid">
            <!-- Player Cards will be dynamically inserted here -->
        </div>
    </section>

    <section id="team">
        <h2>My Team</h2>
        <div id="teamGrid">
            <!-- Team players will be added here -->
        </div>
    </section>

    <section id="pack">
        <h2>Open Pack</h2>
        <button id="openPack">Open 3000 Diamond Pack</button>
    </section>

    <script src="script.js"></script>
</body>
</html>  


let diamonds = 10000;
let gold = 5000;
let playerCards = [
    { name: "Player 1", rating: 85, image: "https://via.placeholder.com/150", price: 3000 },
    { name: "Player 2", rating: 90, image: "https://via.placeholder.com/150", price: 5000 },
    { name: "Player 3", rating: 80, image: "https://via.placeholder.com/150", price: 2500 },
    { name: "Player 4", rating: 92, image: "https://via.placeholder.com/150", price: 7000 },
];

let team = [];

function updateDiamonds() {
    document.getElementById('diamondCount').textContent = diamonds;
    document.getElementById('goldCount').textContent = gold;
}

function createMarketCard(player) {
    const card = document.createElement('div');
    card.classList.add('card');
    card.innerHTML = `
        <img src="${player.image}" alt="${player.name}">
        <div class="name">${player.name}</div>
        <div class="rating">Rating: ${player.rating}</div>
        <div class="price">Price: ${player.price} Diamonds</div>
        <button onclick="buyPlayer('${player.name}', ${player.price})">Buy</button>
    `;
    return card;
}

function createTeamCard(player) {
    const card = document.createElement('div');
    card.classList.add('card');
    card.innerHTML = `
        <img src="${player.image}" alt="${player.name}">
        <div class="name">${player.name}</div>
        <div class="rating">Rating: ${player.rating}</div>
    `;
    return card;
}

function buyPlayer(name, price) {
    if (diamonds >= price) {
        diamonds -= price;
        updateDiamonds();
        
        const player = playerCards.find(p => p.name === name);
        team.push(player);

        const teamGrid = document.getElementById('teamGrid');
        teamGrid.appendChild(createTeamCard(player));

        const cardGrid = document.getElementById('market').querySelector('.card-grid');
        const cardToRemove = Array.from(cardGrid.children).find(card => card.querySelector('.name').textContent === name);
        cardGrid.removeChild(cardToRemove);
    } else {
        alert('Not enough diamonds!');
    }
}

document.getElementById('openPack').addEventListener('click', function() {
    if (diamonds >= 3000) {
        diamonds -= 3000;
        updateDiamonds();

        const randomPlayer = playerCards[Math.floor(Math.random() * playerCards.length)];
        team.push(randomPlayer);
        
        const teamGrid = document.getElementById('teamGrid');
        teamGrid.appendChild(createTeamCard(randomPlayer));
    } else {
        alert('Not enough diamonds!');
    }
});

function initMarket() {
    const cardGrid = document.getElementById('market').querySelector('.card-grid');
    playerCards.forEach(player => {
        cardGrid.appendChild(createMarketCard(player));
    });
}

initMarket();

/* High-Tech UI Design */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Roboto', sans-serif;
    background-color: #2b2b2b;
    color: white;
    padding: 20px;
    transition: background-color 0.5s ease;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #333;
    padding: 10px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
}

h1 {
    font-size: 2rem;
    color: #f1c40f;
}

#currency span {
    font-size: 1.1rem;
    margin-right: 20px;
}

section {
    margin-top: 30px;
}

button {
    padding: 10px 20px;
    font-size: 1rem;
    background-color: #27ae60;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: all 0.3s ease;
}

button:hover {
    background-color: #2ecc71;
}

.card-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
}

.card {
    background-color: #1abc9c;
    width: 180px;
    padding: 15px;
    border-radius: 10px;
    text-align: center;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.5);
    position: relative;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
    transform: scale(1.05);
    box-shadow: 0 6px 15px rgba(0, 0, 0, 0.7);
}

.card img {
    width: 100%;
    height: 120px;
    object-fit: cover;
    border-radius: 5px;
    margin-bottom: 10px;
}

.card .name {
    font-size: 1.2rem;
    font-weight: bold;
    margin-bottom: 5px;
}

.card .rating {
    font-size: 1.1rem;
    color: #f39c12;
}

#teamGrid {
    display: flex;
    flex-wrap: wrap;
    gap: 15px;
    justify-content: center;
}

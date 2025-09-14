# hacking-game
Simple hacking game 
intex.html 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>Hacker Quest</title>
    <link rel="stylesheet" href="style.css" />
</head>
<body>
    <div id="game-container">
        <h1>Hacker Quest</h1>
        <div id="story"></div>
        <div id="challenge"></div>
        <button id="start-btn">Start Game</button>
        <button id="next-btn" style="display:none;">Next Level</button>
    </div>
    <script src="script.js"></script>
</body>
</html>
style.css
body {
    font-family: Arial, sans-serif;
    background-color: #121212;
    color: #fff;
    text-align: center;
    padding: 20px;
}

#game-container {
    max-width: 600px;
    margin: auto;
}

button {
    background-color: #28a745;
    color: white;
    border: none;
    padding: 12px 24px;
    margin: 10px;
    cursor: pointer;
    border-radius: 5px;
}

button:hover {
    background-color: #218838;
}
script.js
const story = document.getElementById("story");
const challenge = document.getElementById("challenge");
const startBtn = document.getElementById("start-btn");
const nextBtn = document.getElementById("next-btn");

let level = parseInt(localStorage.getItem("level")) || 1;

const levels = {
    1: {
        story: "Welcome, young hacker! Let's start by learning what ethical hacking is.",
        question: "What is ethical hacking?",
        options: ["Breaking into systems", "Authorized testing of systems", "Spreading malware"],
        answer: 1
    },
    2: {
        story: "Great! Now let's learn about penetration testing.",
        question: "Penetration testing is also known as?",
        options: ["Pen testing", "Password cracking", "Data wiping"],
        answer: 0
    },
    3: {
        story: "You're advancing fast! Next is network scanning.",
        question: "Which tool is used for scanning networks?",
        options: ["Nmap", "Photoshop", "Excel"],
        answer: 0
    }
};

function loadLevel() {
    const current = levels[level];
    if (!current) {
        story.innerHTML = "Congratulations! You are now a master hacker ready to explore the world.";
        challenge.innerHTML = "";
        startBtn.style.display = "none";
        nextBtn.style.display = "none";
        return;
    }
    story.innerHTML = current.story;
    challenge.innerHTML = `<p>${current.question}</p>`;
    current.options.forEach((opt, index) => {
        const btn = document.createElement("button");
        btn.textContent = opt;
        btn.addEventListener("click", () => checkAnswer(index));
        challenge.appendChild(btn);
    });
}

function checkAnswer(selected) {
    const current = levels[level];
    if (selected === current.answer) {
        alert("Correct!");
        localStorage.setItem("level", level + 1);
        nextBtn.style.display = "inline-block";
        startBtn.style.display = "none";
    } else {
        alert("Wrong! Try again.");
    }
}

startBtn.addEventListener("click", () => {
    startBtn.style.display = "none";
    loadLevel();
});

nextBtn.addEventListener("click", () => {
    level++;
    localStorage.setItem("level", level);
    nextBtn.style.display = "none";
    loadLevel();
});

// Initialize game
if (level > 1) {
    startBtn.style.display = "none";
    loadLevel();
}
4: {
    story: "Next, learn about password attacks.",
    question: "What is a common method to crack passwords?",
    options: ["Brute force", "Emailing friends", "Ignoring security"],
    answer: 0
},
5: {
    story: "Let's explore Wi-Fi hacking techniques.",
    question: "What is WPA?",
    options: ["A hacking tool", "A Wi-Fi security protocol", "A game"],
    answer: 1
}

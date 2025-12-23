
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>TURBOFLEX – Technical Word Challenge</title>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #0a0a0a;
  color: #00ffe7;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.game-box {
  width: 90%;
  max-width: 400px;
  background: #111;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 15px #00ffe7;
  text-align: center;
}

h1 {
  margin-bottom: 10px;
}

.timer {
  font-size: 18px;
  margin-bottom: 15px;
}

.word {
  font-size: 24px;
  letter-spacing: 3px;
  margin-bottom: 15px;
}

input {
  width: 90%;
  padding: 10px;
  font-size: 16px;
  border-radius: 5px;
  border: none;
  outline: none;
}

button {
  margin-top: 10px;
  padding: 10px 20px;
  background: #00ffe7;
  color: #000;
  border: none;
  border-radius: 5px;
  font-weight: bold;
  cursor: pointer;
}

.score {
  margin-top: 15px;
  font-size: 18px;
}
</style>
</head>

<body>

<div class="game-box">
  <h1>TURBOFLEX</h1>
  <div class="timer">Time Left: <span id="time">120</span>s</div>
  <div class="word" id="scrambledWord">Loading...</div>

  <input type="text" id="userInput" placeholder="Type the correct word">
  <button onclick="checkWord()">SUBMIT</button>

  <div class="score">Score: <span id="score">0</span></div>
</div>

<script>
const words = [
  "java","python","html","css","javascript",
  "compiler","algorithm","database","network",
  "variable","function","array","object","class",
  "inheritance","interface","debug","framework"
];

let currentWord = "";
let score = 0;
let time = 120;

function scramble(word) {
  return word.split('').sort(() => 0.5 - Math.random()).join('');
}

function newWord() {
  currentWord = words[Math.floor(Math.random() * words.length)];
  document.getElementById("scrambledWord").innerText = scramble(currentWord);
  document.getElementById("userInput").value = "";
}

function checkWord() {
  const input = document.getElementById("userInput").value.toLowerCase();
  if (input === currentWord) {
    score++;
    document.getElementById("score").innerText = score;
    newWord();
  }
}

function startTimer() {
  const timer = setInterval(() => {
    time--;
    document.getElementById("time").innerText = time;
    if (time === 0) {
      clearInterval(timer);
      alert("Time Over! Your Score: " + score);
      location.reload();
    }
  }, 1000);
}

newWord();
startTimer();
</script>

</body>
</html>

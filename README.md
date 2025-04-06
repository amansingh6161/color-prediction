<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>Color Prediction</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <div class="container">
      <div class="top-container">
        <h3>Available Points : <span id="points">100</span></h3>
        <span class="timer" id="timer">00:00</span>
      </div>
      <div class="mid-container">
        <div class="mid-container-user">
          <div class="user">
            <h3>User: <span id="user-id">1221</span></h3>
          </div>
          <div id="countdown" class="countdown">
            <h3>Timer: <span id="timerval">10</span></h3>  
          </div>
        </div>
        <div id="result" class="result">
            
        </div>
        <div id="buttons">
          <button class="red-btn" id="red">Join Red</button>
          <button class="green-btn" id="green">Join Green</button>
          <button class="blue-btn" id="blue">Join Blue</button>
        </div>
      </div>
      <div class="btm-container">
        <table id="game-records">
          <thead>
            <tr>
              <th>User ID</th>
              <th>Available Points</th>
              <th>Time</th>
              <th>Status</th>
            </tr>
          </thead>
          <tbody id="game-records-body">
          </tbody>
        </table>
      </div>
    </div>
    <script src="script.js"></script>
  </body>
</html>
[Uploading script.js…]()let timeInSeconds = 0;
let timer = 10;
var pickedColor = "";
let gameRecords = [];
var timerval = "";
function updateTimer() {
  const minutes = Math.floor(timeInSeconds / 60);
  const seconds = timeInSeconds % 60;
  const timerDisplay = document.getElementById("timer");
  timerDisplay.textContent = `${String(minutes).padStart(2, "0")}:${String(
    seconds
  ).padStart(2, "0")}`;
  timerval = `${String(minutes).padStart(2, "0")}:${String(
    seconds
  ).padStart(2, "0")}`;

}
function startTimer() {
  setInterval(function () {
    timeInSeconds++;
    updateTimer();
  }, 1000);
}

function startGame() {
  startCountdown();
  const colors = ["red", "green", "blue"];
  const randomColor = colors[Math.floor(Math.random() * colors.length)];

  setTimeout(function () {
    if (pickedColor === randomColor) {
      var resultElement = document.getElementById("result");
      resultElement.style.color = randomColor;
      resultElement.textContent = "You Win!";
      increasePoints();
      updateUserInfo(
        "1221",
        parseInt(document.getElementById("points").textContent, 10), timerval,
        "Win"
      );
      updateGameRecords(
        "1221",
        parseInt(document.getElementById("points").textContent, 10), timerval,
        "Win"
      );
      setTimeout(function () {
        resultElement.textContent = "";
      }, 5000);
    } else {
      var resultElement = document.getElementById("result");
      resultElement.style.color = randomColor;
      resultElement.textContent = "You Lose!";
      decreasePoints();
      updateUserInfo(
        "1221",
        parseInt(document.getElementById("points").textContent, 10),timerval,
        "Lose"
      );
      updateGameRecords(
        "1221",
        parseInt(document.getElementById("points").textContent, 10),timerval,
        "Lose"
      );

      setTimeout(function () {
        resultElement.textContent = "";
      }, 5000);
    }
  }, 10000);
}
function startCountdown() {
  let Btn1 = document.getElementById("green");
  let Btn2 = document.getElementById("red");
  let Btn3 = document.getElementById("blue");
  Btn1.style.pointerEvents = "none";
  Btn1.disabled = true;
  Btn2.style.pointerEvents = "none";
  Btn2.disabled = true;
  Btn3.style.pointerEvents = "none";
  Btn3.disabled = true;
  var timerInt = setInterval(function () {
    if (timer > 0) {
      timer--;
      document.querySelector("#timerval").textContent = timer;
    } else {
      Btn1.style.pointerEvents = "auto";
      Btn1.disabled = false;
      Btn2.style.pointerEvents = "auto";
      Btn2.disabled = false;
      Btn3.style.pointerEvents = "auto";
      Btn3.disabled = false;
      clearInterval(timerInt);
      timer = 10;
      document.querySelector("#timerval").textContent = timer;
    }
  }, 1000);
}
function increasePoints() {
  let pointsElement = document.getElementById("points");
  var currentPoints = parseInt(pointsElement.textContent, 10);
  currentPoints += 10;
  pointsElement.textContent = currentPoints;
}
function decreasePoints() {
  let pointsElement = document.getElementById("points");
  var currentPoints = parseInt(pointsElement.textContent, 10);
  currentPoints -= 10;
  pointsElement.textContent = currentPoints;
}

function updateUserInfo(userId, points, timer, status) {
  const userIdInfo = document.getElementById("user-id");
  const pointsInfo = document.getElementById("points");
  const timerInfo = document.getElementById("timer");
  const statusInfo = document.getElementById("result");

  userIdInfo.textContent = userId;
  pointsInfo.textContent = points;
  timerInfo.textContent = timer;
  statusInfo.textContent = status;
}
function updateGameRecords(userId, points, timer, status) {
  gameRecords.push({ userId, points, timer, status });

  if (gameRecords.length > 5) {
    gameRecords.shift();
  }
  const gameRecordsTable = document.getElementById("game-records-body");
  gameRecordsTable.innerHTML = "";
  gameRecords.forEach((record) => {
    const row = gameRecordsTable.insertRow();
    const cell1 = row.insertCell(0);
    const cell2 = row.insertCell(1);
    const cell3 = row.insertCell(2);
    const cell4 = row.insertCell(3);
    cell1.textContent = record.userId;
    cell2.textContent = record.points;
    cell3.textContent = record.timer;
    cell4.textContent = record.status;
  });
}
document.getElementById("red").addEventListener("click", function () {
  pickedColor = "red";
  startGame();
});

document.getElementById("green").addEventListener("click", function () {
  pickedColor = "green";
  startGame();
});

document.getElementById("blue").addEventListener("click", function () {
  pickedColor = "blue";
  startGame();
});

startTimer();
[Uploading style.css…]()/* - Primary Color: Navy Blue (#001f3f)
- Secondary Color: Sage Green (#689f38)
- Accent Color: Turquoise Blue (#17a2b8)
- Neutral Color: Light Silver Gray (#dcdcdc)
- Highlight Color: Coral (#ff6b6b) */
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Gilroy';
}
html,body{
    width: 100%;
    height: 100%;
    background-color: #91a3b4;
    display: flex;
    align-items: center;
    justify-content: center;
}
.container{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 20%;
    height: 80%;
    background-color: #dcdcdc;
    border-radius: 5px;
    overflow: hidden;
}

.top-container{
    width: 100%;
    height: 10%;
    background-color: #001f3f;
    color: white;
    border: #001f3f;
    padding: 10px;
    display: flex;
    align-items: center;
}

.top-container h3{
    margin-right: 50px ;
}
.timer{
    font-size: 35px;
    font-weight: 500;
}

.mid-container{
    width: 100%;
    height: 35%;
    background-color: whitesmoke;
    display: flex;
    flex-direction: column;
    font-size: 25px;
}
.mid-container-user{
    padding: 5px 8px;
}
.mid-container-user .user{
    float: left;
}
.mid-container-user .countdown{
    float: right;
}
.result{
    width: 100%;
    height: 100px;
    background-color: rgb(184, 184, 184);
    text-align: center;
    font-weight: 700;
    font-size: 70px ;
}
#buttons{
    display: flex;
    justify-content: space-evenly;
    margin-top: 15px;
    margin-bottom: 15px;
}
button{
  background-image: linear-gradient(#0dccea, #0d70ea);
  border: 0;
  border-radius: 4px;
  box-shadow: rgba(0, 0, 0, .3) 0 5px 15px;
  box-sizing: border-box;
  color: #fff;
  cursor: pointer;
  font-family: Montserrat,sans-serif;
  font-size: 10px;
  font-weight: 800;
  margin: 4px;
  padding: 8px 13px;
  text-align: center;
}
.red-btn{
    background: radial-gradient(circle at 10% 20%, rgb(221, 49, 49) 0%, rgb(119, 0, 0) 90%);
}
.green-btn{
    background: radial-gradient(circle at -1% 57.5%, rgb(19, 170, 82) 0%, rgb(0, 102, 43) 90%);
}
.btm-container{
    width: 100%;
    height: 55%;
    background-color: gainsboro;
    display: flex;
    justify-content: space-evenly;
    align-items: start;
}
#game-records th{
    padding: 10px;
    font-weight: 600;
    text-align: center; 
    border: 1px solid #ccc; 
  }
#game-records td {
    padding: 10px;
    text-align: center; 
    border: 1px solid #ccc; 
  }



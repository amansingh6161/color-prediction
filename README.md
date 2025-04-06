[U<!DOCTYPE html>
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
ploading index (2).html…]()

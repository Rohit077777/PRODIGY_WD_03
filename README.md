<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tic-Tac-Toe</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background-color: #f4f4f4;
    }

    .container {
      text-align: center;
    }

    .game-board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-template-rows: repeat(3, 100px);
      gap: 10px;
      margin: 20px auto;
    }

    .cell {
      width: 100px;
      height: 100px;
      background-color: #fff;
      border: 2px solid #333;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 36px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    .cell:hover {
      background-color: #eee;
    }

    .message {
      margin-top: 20px;
      font-size: 24px;
    }

    .reset-btn {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 18px;
      cursor: pointer;
      border: none;
      background-color: #333;
      color: white;
      border-radius: 5px;
      transition: background-color 0.3s ease;
    }

    .reset-btn:hover {
      background-color: #555;
    }

  </style>
</head>
<body>

  <div class="container">
    <h1>Tic-Tac-Toe</h1>
    <div class="game-board" id="gameBoard">
      <div class="cell" data-index="0"></div>
      <div class="cell" data-index="1"></div>
      <div class="cell" data-index="2"></div>
      <div class="cell" data-index="3"></div>
      <div class="cell" data-index="4"></div>
      <div class="cell" data-index="5"></div>
      <div class="cell" data-index="6"></div>
      <div class="cell" data-index="7"></div>
      <div class="cell" data-index="8"></div>
    </div>
    <div class="message" id="message"></div>
    <button class="reset-btn" id="resetBtn">Reset Game</button>
  </div>

  <script>
    const gameBoard = document.getElementById("gameBoard");
    const messageDisplay = document.getElementById("message");
    const resetBtn = document.getElementById("resetBtn");
    const cells = document.querySelectorAll(".cell");

    let currentPlayer = "X";
    let gameState = ["", "", "", "", "", "", "", "", ""];
    let gameActive = true;

    const winningConditions = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6]
    ];

    function handleCellClick(event) {
      const clickedCell = event.target;
      const clickedCellIndex = parseInt(clickedCell.getAttribute("data-index"));

      if (gameState[clickedCellIndex] !== "" || !gameActive) {
        return;
      }

      gameState[clickedCellIndex] = currentPlayer;
      clickedCell.textContent = currentPlayer;

      checkResult();
    }

    function checkResult() {
      let roundWon = false;

      for (let i = 0; i < winningConditions.length; i++) {
        const winCondition = winningConditions[i];
        const a = gameState[winCondition[0]];
        const b = gameState[winCondition[1]];
        const c = gameState[winCondition[2]];

        if (a === "" || b === "" || c === "") {
          continue;
        }

        if (a === b && b === c) {
          roundWon = true;
          break;
        }
      }

      if (roundWon) {
        messageDisplay.textContent = `Player ${currentPlayer} Wins!`;
        gameActive = false;
        return;
      }

      if (!gameState.includes("")) {
        messageDisplay.textContent = "It's a Draw!";
        gameActive = false;
        return;
      }

      currentPlayer = currentPlayer === "X" ? "O" : "X";
      messageDisplay.textContent = `It's ${currentPlayer}'s Turn`;
    }

    function resetGame() {
      currentPlayer = "X";
      gameState = ["", "", "", "", "", "", "", "", ""];
      gameActive = true;
      messageDisplay.textContent = `It's ${currentPlayer}'s Turn`;

      cells.forEach(cell => {
        cell.textContent = "";
      });
    }

    cells.forEach(cell => {
      cell.addEventListener("click", handleCellClick);
    });

    resetBtn.addEventListener("click", resetGame);

    messageDisplay.textContent = `It's ${currentPlayer}'s Turn`;
  </script>

</body>
</html>


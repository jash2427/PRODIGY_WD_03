# PRODIGY_WD_03
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Tic-Tac-Toe</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #282c34;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }

    h1 {
      font-size: 3rem;
      margin-bottom: 20px;
    }

    #board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-template-rows: repeat(3, 100px);
      gap: 5px;
    }

    .cell {
      width: 100px;
      height: 100px;
      font-size: 2.5rem;
      color: #fff;
      background: #444;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      user-select: none;
    }

    .cell:hover {
      background: #555;
    }

    #status {
      margin-top: 20px;
      font-size: 1.5rem;
    }

    button {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 1rem;
      cursor: pointer;
      border: none;
      background: #61dafb;
      color: #000;
      border-radius: 5px;
    }
  </style>
</head>
<body>

  <h1>Tic-Tac-Toe</h1>
  <div id="board"></div>
  <div id="status">Player X's turn</div>
  <button onclick="resetGame()">Restart Game</button>

  <script>
    const board = document.getElementById("board");
    const statusText = document.getElementById("status");
    let cells = [];
    let currentPlayer = "X";
    let gameActive = true;

    function createBoard() {
      board.innerHTML = '';
      cells = [];
      for (let i = 0; i < 9; i++) {
        const cell = document.createElement("div");
        cell.classList.add("cell");
        cell.dataset.index = i;
        cell.addEventListener("click", handleClick);
        board.appendChild(cell);
        cells.push("");
      }
    }

    function handleClick(e) {
      const index = e.target.dataset.index;

      if (!gameActive || cells[index] !== "") return;

      cells[index] = currentPlayer;
      e.target.textContent = currentPlayer;

      if (checkWin()) {
        statusText.textContent = `Player ${currentPlayer} wins!`;
        gameActive = false;
        return;
      }

      if (cells.every(cell => cell !== "")) {
        statusText.textContent = "It's a draw!";
        gameActive = false;
        return;
      }

      currentPlayer = currentPlayer === "X" ? "O" : "X";
      statusText.textContent = `Player ${currentPlayer}'s turn`;
    }

    function checkWin() {
      const winConditions = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];

      return winConditions.some(condition => {
        const [a, b, c] = condition;
        return cells[a] === currentPlayer &&
               cells[a] === cells[b] &&
               cells[a] === cells[c];
      });
    }

    function resetGame() {
      currentPlayer = "X";
      gameActive = true;
      statusText.textContent = "Player X's turn";
      createBoard();
    }

    createBoard();
  </script>

</body>
</html>

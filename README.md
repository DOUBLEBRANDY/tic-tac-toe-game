# tic-tac-toe-game
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tic Tac Toe Game</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="container">
    <h1>Tic Tac Toe</h1>
    <div id="board" class="board">
      <div class="cell" id="cell-1"></div>
      <div class="cell" id="cell-2"></div>
      <div class="cell" id="cell-3"></div>
      <div class="cell" id="cell-4"></div>
      <div class="cell" id="cell-5"></div>
      <div class="cell" id="cell-6"></div>
      <div class="cell" id="cell-7"></div>
      <div class="cell" id="cell-8"></div>
      <div class="cell" id="cell-9"></div>
    </div>
    <button id="reset-btn" class="btn">Reset Game</button>
  </div>

  <script src="script.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f0f0f0;
}

.container {
  text-align: center;
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  gap: 10px;
  margin-top: 20px;
}

.cell {
  width: 100px;
  height: 100px;
  background-color: #fff;
  border: 1px solid #ccc;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 2rem;
  cursor: pointer;
}

.btn {
  margin-top: 20px;
  padding: 10px 20px;
  font-size: 1rem;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn:hover {
  background-color: #45a049;
}
document.addEventListener('DOMContentLoaded', function() {
  const cells = document.querySelectorAll('.cell');
  const resetButton = document.getElementById('reset-btn');
  let currentPlayer = 'X';
  let gameActive = true;
  let moves = 0;

  // Event listener for each cell click
  cells.forEach(cell => {
    cell.addEventListener('click', handleCellClick);
  });

  // Reset button click event
  resetButton.addEventListener('click', resetGame);

  // Function to handle cell click
  function handleCellClick(e) {
    const cell = e.target;
    const cellIndex = parseInt(cell.id.replace('cell-', ''));

    if (cell.textContent === '' && gameActive) {
      cell.textContent = currentPlayer;
      moves++;

      if (checkWin(currentPlayer)) {
        alert(`${currentPlayer} wins!`);
        gameActive = false;
      } else if (moves === 9) {
        alert('It\'s a draw!');
        gameActive = false;
      } else {
        currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
      }
    }
  }

  // Function to check for a win
  function checkWin(player) {
    const winConditions = [
      [1, 2, 3],
      [4, 5, 6],
      [7, 8, 9],
      [1, 4, 7],
      [2, 5, 8],
      [3, 6, 9],
      [1, 5, 9],
      [3, 5, 7]
    ];

    return winConditions.some(condition => {
      return condition.every(index => {
        return cells[index - 1].textContent === player;
      });
    });
  }

  // Function to reset the game
  function resetGame() {
    cells.forEach(cell => {
      cell.textContent = '';
    });
    currentPlayer = 'X';
    gameActive = true;
    moves = 0;
  }
});

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe Game</title>
    <style>
        body {
            text-align: center;
            font-family: Arial, sans-serif;
        }
        .board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            grid-template-rows: repeat(3, 100px);
            gap: 5px;
            margin: 20px auto;
            width: 320px;
        }
        .cell {
            width: 100px;
            height: 100px;
            font-size: 24px;
            text-align: center;
            line-height: 100px;
            border: 2px solid #333;
            cursor: pointer;
            background: #f0f0f0;
        }
        .cell:hover {
            background: #ddd;
        }
    </style>
</head>
<body>

    <h1>Tic-Tac-Toe</h1>
    <div class="board" id="board"></div>
    <p id="status"></p>
    <button onclick="resetGame()">Restart Game</button>

    <script>
        const board = document.getElementById("board");
        let currentPlayer = "X";
        let cells = Array(9).fill(null);

        function createBoard() {
            board.innerHTML = "";
            cells.forEach((_, i) => {
                const cell = document.createElement("div");
                cell.classList.add("cell");
                cell.dataset.index = i;
                cell.addEventListener("click", handleClick);
                board.appendChild(cell);
            });
        }

        function handleClick(event) {
            const index = event.target.dataset.index;
            if (!cells[index]) {
                cells[index] = currentPlayer;
                event.target.textContent = currentPlayer;
                if (checkWinner()) {
                    document.getElementById("status").textContent = `${currentPlayer} Wins!`;
                    board.childNodes.forEach(cell => cell.removeEventListener("click", handleClick));
                } else {
                    currentPlayer = currentPlayer === "X" ? "O" : "X";
                }
            }
        }

        function checkWinner() {
            const winPatterns = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8],
                [0, 3, 6], [1, 4, 7], [2, 5, 8],
                [0, 4, 8], [2, 4, 6]
            ];
            return winPatterns.some(pattern => {
                const [a, b, c] = pattern;
                return cells[a] && cells[a] === cells[b] && cells[a] === cells[c];
            });
        }

        function resetGame() {
            cells.fill(null);
            currentPlayer = "X";
            document.getElementById("status").textContent = "";
            createBoard();
        }

        createBoard();
    </script>

</body>
</html>

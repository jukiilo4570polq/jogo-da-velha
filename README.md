# jogo-da-velha
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogo da Velha</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin-top: 50px; }
        .board { display: grid; grid-template-columns: repeat(3, 100px); gap: 5px; justify-content: center; }
        .cell { width: 100px; height: 100px; font-size: 2em; background: #f3f3f3; border: 1px solid #000; display: flex; justify-content: center; align-items: center; cursor: pointer; }
        .cell:hover { background: #ddd; }
        h1 { color: #333; }
        button { margin-top: 20px; padding: 10px 20px; font-size: 1.2em; cursor: pointer; }
    </style>
</head>
<body>
    <h1>Jogo da Velha</h1>
    <div class="board" id="board"></div>
    <button onclick="resetGame()">Reiniciar</button>

    <script>
        const board = document.getElementById("board");
        let cells = ["", "", "", "", "", "", "", "", ""];
        let currentPlayer = "X";

        function createBoard() {
            board.innerHTML = "";
            cells.forEach((value, index) => {
                let cell = document.createElement("div");
                cell.classList.add("cell");
                cell.innerText = value;
                cell.onclick = () => makeMove(index);
                board.appendChild(cell);
            });
        }

        function makeMove(index) {
            if (!cells[index]) {
                cells[index] = currentPlayer;
                currentPlayer = currentPlayer === "X" ? "O" : "X";
                createBoard();
                checkWinner();
            }
        }

        function checkWinner() {
            const winPatterns = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8],
                [0, 3, 6], [1, 4, 7], [2, 5, 8],
                [0, 4, 8], [2, 4, 6]
            ];
            for (let pattern of winPatterns) {
                const [a, b, c] = pattern;
                if (cells[a] && cells[a] === cells[b] && cells[a] === cells[c]) {
                    alert(`Jogador ${cells[a]} venceu!`);
                    resetGame();
                    return;
                }
            }
            if (!cells.includes("")) {
                alert("Empate!");
                resetGame();
            }
        }

        function resetGame() {
            cells = ["", "", "", "", "", "", "", "", ""];
            currentPlayer = "X";
            createBoard();
        }

        createBoard();
    </script>
</body>
</html>

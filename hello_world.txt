// Tic Tac Toe Game in JavaScript

const board = [
    ['', '', ''],
    ['', '', ''],
    ['', '', '']
];

let currentPlayer = 'X';

function printBoard() {
    console.log(board.map(row => row.join(' | ')).join('\n---------\n'));
}

function makeMove(row, col) {
    if (board[row][col] === '') {
        board[row][col] = currentPlayer;
        if (checkWin()) {
            console.log(`Player ${currentPlayer} wins!`);
            resetBoard();
        } else if (board.flat().every(cell => cell !== '')) {
            console.log('It\'s a tie!');
            resetBoard();
        } else {
            currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
        }
    } else {
        console.log('Invalid move, try again.');
    }
}

function checkWin() {
    const winPatterns = [
        // Rows
        [[0, 0], [0, 1], [0, 2]],
        [[1, 0], [1, 1], [1, 2]],
        [[2, 0], [2, 1], [2, 2]],
        // Columns
        [[0, 0], [1, 0], [2, 0]],
        [[0, 1], [1, 1], [2, 1]],
        [[0, 2], [1, 2], [2, 2]],
        // Diagonals
        [[0, 0], [1, 1], [2, 2]],
        [[0, 2], [1, 1], [2, 0]]
    ];

    return winPatterns.some(pattern => 
        pattern.every(([row, col]) => board[row][col] === currentPlayer)
    );
}

function resetBoard() {
    for (let row = 0; row < 3; row++) {
        for (let col = 0; col < 3; col++) {
            board[row][col] = '';
        }
    }
    currentPlayer = 'X';
}

// Example usage:
printBoard();
makeMove(0, 0);
printBoard();
makeMove(1, 1);
printBoard();
makeMove(0, 1);
printBoard();
makeMove(1, 0);
printBoard();
makeMove(0, 2);
printBoard();
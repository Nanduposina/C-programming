#include <stdio.h>

char board[3][3]; // 3x3 board for Tic-Tac-Toe
char currentPlayer; // To keep track of the current player

// Function to initialize the board
void initializeBoard() {
    currentPlayer = 'X'; // 'X' starts the game
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            board[i][j] = ' '; // Set all cells to empty
        }
    }
}

// Function to print the board
void printBoard() {
    printf("\n");
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf(" %c ", board[i][j]);
            if (j < 2) printf("|");
        }
        printf("\n");
        if (i < 2) printf("---|---|---\n");
    }
    printf("\n");
}

// Function to check if a player has won
int checkWin() {
    // Check rows and columns
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][0] != ' ')
            return 1; // Row win
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i] && board[0][i] != ' ')
            return 1; // Column win
    }
    // Check diagonals
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != ' ')
        return 1; // Diagonal win
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[0][2] != ' ')
        return 1; // Diagonal win

    return 0; // No win
}

// Function to check if the board is full (for draw check)
int isBoardFull() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] == ' ') return 0; // If any cell is empty
        }
    }
    return 1; // Board is full
}

// Function to handle a player's move
void playerMove() {
    int row, col;
    printf("Player %c, enter your move (row and column): ", currentPlayer);
    while (1) {
        scanf("%d %d", &row, &col);
        // Check if the move is valid (inside bounds and the cell is empty)
        if (row >= 0 && row < 3 && col >= 0 && col < 3 && board[row][col] == ' ') {
            board[row][col] = currentPlayer;
            break;
        } else {
            printf("Invalid move! Please try again: ");
        }
    }
}

// Function to change the player
void switchPlayer() {
    currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
}

int main() {
    int gameOver = 0;
    initializeBoard();

    while (!gameOver) {
        printBoard();
        playerMove();
        if (checkWin()) {
            printBoard();
            printf("Player %c wins!\n", currentPlayer);
            gameOver = 1;
        } else if (isBoardFull()) {
            printBoard();
            printf("It's a draw!\n");
            gameOver = 1;
        } else {
            switchPlayer();
        }
    }
    return 0;
}

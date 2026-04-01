#### Tic - tac -Toe Game

```cpp
#include <iostream>
using namespace std;

class Game {
private:
    char board[3][3];
    char turn;
    char winner;

public:
    Game() {
        resetGame();
    }

    void resetGame() {
        for(int i = 0; i < 3; i++) {
            for(int j = 0; j < 3; j++) {
                board[i][j] = ' ';
            }
        }
        turn = 'X';
        winner = ' ';
    }

    void printBoard() {
        cout << "\n";
        for(int i = 0; i < 3; i++) {
            for(int j = 0; j < 3; j++) {
                cout << " " << board[i][j] << " ";
                if(j < 2) cout << "|";
            }
            cout << "\n";
            if(i < 2) cout << "---+---+---\n";
        }
        cout << "\n";
    }

    // Make a move
    bool makeMove(int row, int col) {
        if(row < 0 || row > 2 || col < 0 || col > 2 || board[row][col] != ' ') {
            cout << "Invalid move! Try again.\n";
            return false;
        }

        board[row][col] = turn;

        if(turn == 'X')
            turn = 'O';
        else
            turn = 'X';

        return true;
    }

    void checkWinner() {

        for(int i = 0; i < 3; i++) {
            if(board[i][0] != ' ' &&
               board[i][0] == board[i][1] &&
               board[i][1] == board[i][2]) {
                winner = board[i][0];
            }
        }

        for(int i = 0; i < 3; i++) {
            if(board[0][i] != ' ' &&
               board[0][i] == board[1][i] &&
               board[1][i] == board[2][i]) {
                winner = board[0][i];
            }
        }

        if(board[0][0] != ' ' &&
           board[0][0] == board[1][1] &&
           board[1][1] == board[2][2]) {
            winner = board[0][0];
        }

        if(board[0][2] != ' ' &&
           board[0][2] == board[1][1] &&
           board[1][1] == board[2][0]) {
            winner = board[0][2];
        }
    }

    bool isBoardFull() {
        for(int i = 0; i < 3; i++) {
            for(int j = 0; j < 3; j++) {
                if(board[i][j] == ' ')
                    return false;
            }
        }
        return true;
    }

    char getWinner() {
        return winner;
    }

    char getTurn() {
        return turn;
    }
};

int main() {

    Game game;
    int row, col;

    while(true) {

        game.printBoard();

        cout << "Player " << game.getTurn() << " enter row and column (0-2): ";
        cin >> row >> col;

        if(!game.makeMove(row, col))
            continue;

        game.checkWinner();

        if(game.getWinner() != ' ') {
            game.printBoard();
            cout << "Player " << game.getWinner() << " wins!\n";
            break;
        }

        if(game.isBoardFull()) {
            game.printBoard();
            cout << "It's a draw!\n";
            break;
        }
    }
```

    return 0;
}

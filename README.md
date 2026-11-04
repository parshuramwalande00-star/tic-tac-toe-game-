# tic-tac-toe-game
#include <iostream>
using namespace std;

class TicTacToe
{
private:
    char board[3][3];
    char currentPlayer;

public:

    // Initialize the game board
    TicTacToe()
    {
        currentPlayer = 'X';

        for (int i = 0; i < 3; i++)
        {
            for (int j = 0; j < 3; j++)
            {
                board[i][j] = ' ';
            }
        }
    }

    // Display the game board
    void displayBoard()
    {
        cout << "\n";
        cout << "       TIC TAC TOE\n\n";

        for (int i = 0; i < 3; i++)
        {
            cout << "  ";

            for (int j = 0; j < 3; j++)
            {
                cout << " " << board[i][j] << " ";

                if (j < 2)
                    cout << "|";
            }

            cout << endl;

            if (i < 2)
                cout << "  ---+---+---\n";
        }

        cout << endl;
    }

    // Check whether the move is valid
    bool makeMove(int row, int col)
    {
        if (row < 0 || row >= 3 ||
            col < 0 || col >= 3)
        {
            cout << "Invalid position!\n";
            return false;
        }

        if (board[row][col] != ' ')
        {
            cout << "Position already occupied!\n";
            return false;
        }

        board[row][col] = currentPlayer;
        return true;
    }

    // Check winning condition
    bool checkWin()
    {
        // Check rows and columns
        for (int i = 0; i < 3; i++)
        {
            if (board[i][0] == currentPlayer &&
                board[i][1] == currentPlayer &&
                board[i][2] == currentPlayer)
                return true;

            if (board[0][i] == currentPlayer &&
                board[1][i] == currentPlayer &&
                board[2][i] == currentPlayer)
                return true;
        }

        // Check diagonals
        if (board[0][0] == currentPlayer &&
            board[1][1] == currentPlayer &&
            board[2][2] == currentPlayer)
            return true;

        if (board[0][2] == currentPlayer &&
            board[1][1] == currentPlayer &&
            board[2][0] == currentPlayer)
            return true;

        return false;
    }

    // Check draw condition
    bool checkDraw()
    {
        for (int i = 0; i < 3; i++)
        {
            for (int j = 0; j < 3; j++)
            {
                if (board[i][j] == ' ')
                    return false;
            }
        }

        return true;
    }

    // Switch player turns
    void switchPlayer()
    {
        currentPlayer =
            (currentPlayer == 'X') ? 'O' : 'X';
    }

    // Start the game
    void playGame()
    {
        int row, col;

        while (true)
        {
            displayBoard();

            cout << "Player " << currentPlayer;
            cout << ", enter row and column (1-3): ";

            if (!(cin >> row >> col))
            {
                cin.clear();
                cin.ignore(10000, '\n');
                cout << "Invalid input! Enter numbers.\n";
                continue;
            }

            row--;
            col--;

            if (!makeMove(row, col))
                continue;

            if (checkWin())
            {
                displayBoard();

                cout << "Player " << currentPlayer;
                cout << " WINS THE GAME!\n";
                break;
            }

            if (checkDraw())
            {
                displayBoard();
                cout << "GAME DRAW!\n";
                break;
            }

            switchPlayer();
        }
    }
};

// Main function
int main()
{
    TicTacToe game;

    cout << "============================\n";
    cout << "      TIC TAC TOE GAME\n";
    cout << "============================\n";

    game.playGame();

    cout << "\nThank you for playing!\n";

    return 0;
}
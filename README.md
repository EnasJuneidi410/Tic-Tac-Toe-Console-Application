# Tic-Tac-Toe-Console-Application
import 'dart:io';

class TicTacToe {
  List<String> board;
  String currentPlayer;

    TicTacToe()
  {
    board = List.filled(9, ' ');
    currentPlayer = 'X';
  }

  void displayBoard() {
    print(' ${board[0]} | ${board[1]} | ${board[2]} ');
    print('-----------');
    print(' ${board[3]} | ${board[4]} | ${board[5]} ');
    print('-----------');
    print(' ${board[6]} | ${board[7]} | ${board[8]} ');
  }

  bool makeMove(int position) {
    if (position < 1 || position > 9 || board[position - 1] != ' ') {
      print('Invalid move. Please try again.');
      return false;
    }

    board[position - 1] = currentPlayer;
    return true;
  }

  bool checkWin() {
    // Check rows
    for (int i = 0; i < 9; i += 3) {
      if (board[i] != ' ' &&
          board[i] == board[i + 1] &&
          board[i] == board[i + 2]) {
        return true;
      }
    }

    // Check columns
    for (int i = 0; i < 3; i++) {
      if (board[i] != ' ' &&
          board[i] == board[i + 3] &&
          board[i] == board[i + 6]) {
        return true;
      }
    }

    // Check diagonals
    if (board[0] != ' ' && board[0] == board[4] && board[0] == board[8]) {
      return true;
    }
    if (board[2] != ' ' && board[2] == board[4] && board[2] == board[6]) {
      return true;
    }

    return false;
  }

  bool checkDraw() {
    return !board.contains(' ');
  }

  void switchPlayer() {
    currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
  }

  void restartGame() {
    board = List.filled(9, ' ');
    currentPlayer = 'X';
  }

  void play() {
    print('Welcome to Tic-Tac-Toe!');
    displayBoard();

    do {
      print('\nPlayer $currentPlayer\'s turn. Enter your move (1-9):');
      int move = int.parse(stdin.readLineSync()!);

      if (makeMove(move)) {
        displayBoard();

        if (checkWin()) {
          print('Player $currentPlayer wins!');
          break;
        } else if (checkDraw()) {
          print('It\'s a draw!');
          break;
        }

        switchPlayer();
      }
    } while (true);

    print('Do you want to play again? (y/n)');
    String playAgain = stdin.readLineSync()!.toLowerCase();
    if (playAgain == 'y') {
      restartGame();
      play();
    } else {
      print('Thanks for playing! Goodbye.');
    }
  }
}

void main() {
  TicTacToe game = TicTacToe();
  game.play();
}

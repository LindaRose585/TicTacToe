# TicTacToe

#include <iostream>
	
#include <string>
	
using namespace std;

// Global Constants for the rows and columns

const int ROWS = 3;

const int COLS = 3;

// Function prototypes

void displayBoard(string [][COLS]);

void playerTurn(string [][COLS], string);

bool gameOver(string [][COLS]);

bool playerWins(string [][COLS], string);

bool playerCanWin(string [][COLS], string);

void displayWinner(string [][COLS]);

int main()
{
	// Array for the game board.
	
	string gameBoard[ROWS][COLS] = {{"*","*","*"},{"*","*","*"},{"*","*","*"}};
	
	// Enter the game loop.

	do
	{
		// Display the game board.
		 displayBoard(gameBoard);
      
		// Let player 1 have a turn.
		 playerTurn(gameBoard, "X");
		 
      
		// Display the game board again.
		 displayBoard(gameBoard);
      
		// If the game is not over, let
		// player 2 have a turn.
		 if (!gameOver(gameBoard))
		playerTurn(gameBoard, "O");
         
	} while (!gameOver(gameBoard));
   
	// Display the board one last time.
	displayBoard(gameBoard);
   
	// Display the winner.
		displayWinner(gameBoard);

	return 0;
}

// The displayBoard function displays the contents of

// the board.                                   

void displayBoard(string board[][COLS])

{
	// Display the column headings.
	
	cout << "-------------------------------------\n";
	cout << "\t| Tic-Tac-Toe Game |\n";
	cout << "-------------------------------------\n";
	cout << "\t\tColumns\n";
	cout << "\t\t1 2 3\n";
   
	// Display the rows.
	for (int row = 0; row < ROWS; row++)
	{
		// Row label.
		cout << "\t  Row " << (row + 1)<< " ";
      
		// Row contents.
		for (int col = 0; col < COLS; col++)
			cout << board[row][col] << " ";

		cout << endl;
	}

	cout << "-------------------------------------\n\n";
}

// The playerTurn function allows a player (X or O) to 

// take a turn.

void playerTurn(string board[][COLS], string symbol)

{
	// The isAvailable flag is set to true when the
	// player selects a location on the board that
	// is available. (initialized to false until set to true 
	// when player selects a location on the board that is available)
	
	bool isAvailable = false;

   
	int row;  // Row to place symbol
	int col;  // column to place symbol
   
	// Prompt the player to enter a location.
	
	cout << "Player " << symbol << "'s turn.\n";
	cout << "Enter a row and column to place an "
	     << symbol << ".\n";
	cout << "-------------------------------------\n\n";
   
	// Get and validate the location.
	
	while (!isAvailable)
	
	{
		// Get the row.
		
		cout << "Row   : ";
		cin >> row;
      
		// Validate the row.
		
		while (row < 1 || row > ROWS)
		{
			cout << "\n-------------------------------------\n";
			cout << "Invalid Row!\n";
			cout << "-------------------------------------\n\n";
			cout << "Row   : ";
			cin >> row;
		}
      
		// Get the column.
		cout << "Column: ";
		cin >> col;
   
		// Validate the column.
		
		while (col < 1 || col > COLS)
		{

		}
      
		// Determine whether the selected
		// cell is available.
		
		if (board[row - 1][col - 1] == "*")
			isAvailable = true;
		else
		{
			cout << "\n-------------------------------------\n";
			cout << "That location is not available.\n"
				 << "Select another location.\n";
		}

		cout << "-------------------------------------\n\n";
	}
   
	// Place the player's symbol on the board
	// at the selected location.
	
	board[row - 1][col - 1] = symbol;
}

// The gameOver function returns true if the game
// is over. This is the case when either player has
// already won, or there is a tie.

bool gameOver(string board[][COLS])

{
	// Boolean flag
	
	bool status;	
	
	// If either player has already won, game over.
	
	if (playerWins(board, "X") || playerWins(board, "O"))
		status = true; 
      
	// Else If either player CAN STILL win, the game is not over, yet.
	
	else if (playerCanWin(board, "X") || playerCanWin(board, "O"))
		status = false;
   
	// else, Otherwise, it's a tie. Game over.
	
	else 
		status = true;
	
	// Return the status.
	
	return status;
}

// The playerWins function accepts the game board and
// a player symbol (X or O) as arguments. It returns
// true if the player has won.


bool playerWins(string board[][COLS], string symbol)

{
	// Boolean flag, set to false
	
	bool status = false;	

	// Check the first horizontal row.
	if (board[0][0] == symbol && board[0][1] == symbol &&
		board[0][2] == symbol)
		status = true;

	// Check the second horizontal row.
	if (board[1][0] == symbol && board[1][1] == symbol &&
		board[1][2] == symbol)
		status = true;

	// Check the third horizontal row.
	if (board[2][0] == symbol && board[2][1] == symbol &&
		board[2][2] == symbol)
		status = true;
	// Check the first column.

	  if (board[0][0] == symbol && board[1][0] == symbol &&
		board[2][0] == symbol)
		status = true;
   
	// Check the second column.
	  if (board[0][1] == symbol && board[1][1] == symbol &&
		board[2][1] == symbol)
		status = true;

	// Check the third column.
	  if (board[0][2] == symbol && board[1][2] == symbol &&
		board[2][2] == symbol)
		status = true;

	// Check the diagonal
	    if (board[0][0] == symbol && board[1][1] == symbol &&
		board[2][2] == symbol)
		status = true;

   
	// If we make it this far, the player did not win.
	return status;
}

// The playerCanWin function returns true if the
// player (X or O) can still win.

bool playerCanWin(string board[][COLS], string symbol)
{
	// Boolean flag, set to false
	
	bool status = false;	

	// Check the first horizontal row for a possibility.
	if ((board[0][0] == symbol || board[0][0] == "*") && 
		(board[0][1] == symbol || board[0][1] == "*") &&
		(board[0][2] == symbol || board[0][2] == "*"))
		status = true;
	
	// Check the second horizontal row for a possibility.
	if ((board[1][0] == symbol || board[1][0] == "*") && 
		(board[1][1] == symbol || board[1][1] == "*") &&
		(board[1][2] == symbol || board[1][2] == "*"))
		status = true;

	// Check the third horizontal row for a possibility.
	if ((board[2][0] == symbol || board[2][0] == "*") && 
		(board[2][1] == symbol || board[2][1] == "*") &&
		(board[2][2] == symbol || board[2][2] == "*"))
		status = true;

	// Check the first column for a possibility.
	if ((board[0][0] == symbol || board[0][0] == "*") && 
		(board[1][0] == symbol || board[1][0] == "*") &&
		(board[2][0] == symbol || board[2][0] == "*"))
		status = true;

	// Check the second column for a possibility.
	if ((board[0][1] == symbol || board[0][1] == "*") && 
		(board[1][1] == symbol || board[1][1] == "*") &&
		(board[2][1] == symbol || board[2][1] == "*"))
		status = true;

	// Check the third column for a possibility.
	if ((board[0][2] == symbol || board[0][2] == "*") && 
		(board[1][2] == symbol || board[1][2] == "*") &&
		(board[2][2] == symbol || board[2][2] == "*"))
		status = true;

	// Check the diagonal for a possibility.
	if ((board[0][0] == symbol || board[0][0] == "*") && 
		(board[1][1] == symbol || board[1][1] == "*") &&
		(board[2][2] == symbol || board[2][2] == "*"))
		status = true;

	// If we make it this far, the player cannot win.
	return status;
}

// The displayWinner function displays the winner.

void displayWinner(string board[][COLS])
{
	if (playerWins(board, "X"))
		cout << "\tPlayer 1 (X) WINS!\n\n";

	else if (playerWins(board, "O"))
		cout << "\tPlayer 2 (O) WINS!\n\n";

	else
		cout << "\tGame Over... it's a TIE.\n\n";

	cout << "-------------------------------------\n\n";
}

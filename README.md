# Tic-Tac-Toe
def print_board(board):
    for row in board:
        print(" | ".join(row))
        print("-" * 5)

def check_win(board, player):
    # Check rows and columns
    for i in range(3):
        if all(board[i][j] == player for j in range(3)) or all(board[j][i] == player for j in range(3)):
            return True

    # Check diagonals
    if all(board[i][i] == player for i in range(3)) or all(board[i][2 - i] == player for i in range(3)):
        return True

    return False

def is_board_full(board):
    return all(cell != " " for row in board for cell in row)

def get_player_input(player):
    while True:
        try:
            row = int(input(f"Player {player}, enter row (0, 1, or 2): "))
            col = int(input(f"Player {player}, enter column (0, 1, or 2): "))
            if 0 <= row < 3 and 0 <= col < 3 and board[row][col] == " ":
                return row, col
            else:
                print("Invalid move. Try again.")
        except ValueError:
            print("Invalid input. Please enter a number.")

# Initialize the game board
board = [[" " for _ in range(3)] for _ in range(3)]

# Main game loop
current_player = "X"
while True:
    print_board(board)

    # Get player input
    row, col = get_player_input(current_player)
    board[row][col] = current_player

    # Check for a win
    if check_win(board, current_player):
        print_board(board)
        print(f"Player {current_player} wins!")
        break

    # Check for a tie
    if is_board_full(board):
        print_board(board)
        print("It's a tie!")
        break

    # Switch player
    current_player = "O" if current_player == "X" else "X"

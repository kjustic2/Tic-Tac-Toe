# Tic Tac Toe Python Terminal Game Portfolio Project

# Tic Tac Toe Board
class Tic_Tac_Toe:

    def __init__(self, player):
        self.row_1 = ["_", "_", "_"]
        self.row_2 = ["_", "_", "_"]
        self.row_3 = ["_", "_", "_"]  
        self.player = player.upper()

    def __repr__(self):
        row_1_str = ",".join(self.row_1)
        row_2_str = ",".join(self.row_2)
        row_3_str = ",".join(self.row_3)
        grid = row_1_str + "\n" + row_2_str + "\n" + row_3_str
        return grid
    
    def display_board(self):
        print("Tic Tac Tow Board: ")
        for row in [self.row_1, self.row_2, self.row_3]:
            print(" | ".join(row))
            print("--|---|--")

    # updates tic-tac-toe grid
    def update_grid(self, index):
        if index.isdigit() and 1 <= int(index) <= 9:
            index = int(index) - 1
            rows = [self.row_1, self.row_2, self.row_3]
            row_index = index // 3
            col_index = index % 3
            if rows[row_index][col_index] == "_":
                rows[row_index][col_index] = self.player
                return True # indicate a successful update
            else:
                print(f"Position {index + 1} has already been filled.")
        else:
            print("Whoops! You did not enter a valid input. Please try again. ")
        return False

    def switch_player(self):
        if self.player == 'X':
            self.player = 'O'
        else:
            self.player = 'X'

# Create two instances of Tic_Tac_Toe for each player
player_1_symbol = input("Welcome Player 1. Please input 'X' or 'O' to continue. ").upper()
while player_1_symbol != "X" and player_1_symbol != "O":
    player_1_symbol = input("Whoops! it looks like you didn't input 'X' or 'O'. Please input 'X' or 'O' to continue. ").upper()

player_1 = Tic_Tac_Toe(player_1_symbol)
player_2_symbol = 'X' if player_1_symbol == 'O' else 'O'
player_2 = Tic_Tac_Toe(player_2_symbol)

# Game Loop
current_player = player_1 # start w/ player 1
while True:
    current_player.display_board()

    index = input(f"{current_player.player}, please input a number between 1 and 9 to continue. ")

    while not current_player.update_grid(index):
        index = input("Please try again: ")
    
    current_player.switch_player()

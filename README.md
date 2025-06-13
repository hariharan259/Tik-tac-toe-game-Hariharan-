# Editor: Hariharan
# A terminal-based Tic Tac Toe game with gradient colors

import os
import time
from colorama import Fore, Back, Style, init

init(autoreset=True)

# Gradient color list
gradient = [
    Fore.LIGHTBLUE_EX, Fore.LIGHTCYAN_EX, Fore.LIGHTGREEN_EX,
    Fore.LIGHTYELLOW_EX, Fore.LIGHTMAGENTA_EX, Fore.LIGHTRED_EX
]

# Initialize board
board = [' ' for _ in range(9)]

# Print the board with gradient
def print_board():
    os.system('cls' if os.name == 'nt' else 'clear')
    print("\n" + Fore.LIGHTWHITE_EX + "🎮 Tic Tac Toe - by Hariharan\n")
    for i in range(3):
        for j in range(3):
            index = 3 * i + j
            color = gradient[index % len(gradient)]
            print(color + f" {board[index]} ", end="")
            if j < 2:
                print(Fore.LIGHTWHITE_EX + "|", end="")
        print()
        if i < 2:
            print(Fore.LIGHTWHITE_EX + "---+---+---")

# Check win condition
def check_win(player):
    win_cond = [(0,1,2),(3,4,5),(6,7,8),
                (0,3,6),(1,4,7),(2,5,8),
                (0,4,8),(2,4,6)]
    for a,b,c in win_cond:
        if board[a] == board[b] == board[c] == player:
            return True
    return False

# Check draw
def is_draw():
    return ' ' not in board

# Main game loop
def play():
    current = 'X'
    while True:
        print_board()
        try:
            move = int(input(f"\n{Fore.LIGHTWHITE_EX}Player {current}, choose (1-9): ")) - 1
            if board[move] == ' ':
                board[move] = current
                if check_win(current):
                    print_board()
                    print(Fore.LIGHTGREEN_EX + f"\n🎉 Player {current} wins!")
                    break
                elif is_draw():
                    print_board()
                    print(Fore.LIGHTYELLOW_EX + "\n🤝 It's a draw!")
                    break
                current = 'O' if current == 'X' else 'X'
            else:
                print(Fore.LIGHTRED_EX + "🚫 Spot already taken!")
                time.sleep(1)
        except (ValueError, IndexError):
            print(Fore.LIGHTRED_EX + "❗ Invalid input. Enter 1-9.")
            time.sleep(1)

# Start the game
if __name__ == "__main__":
    play()

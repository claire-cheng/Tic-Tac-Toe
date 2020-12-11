# Tic-Tac-Toe

from IPython.display import clear_output
import random

def display_board(board):
    print('   |   |')
    print(' ' + board[7] + ' | ' + board[8] + ' | ' + board[9])
    print('   |   |')
    print('-----------')
    print('   |   |')
    print(' ' + board[4] + ' | ' + board[5] + ' | ' + board[6])
    print('   |   |')
    print('-----------')
    print('   |   |')
    print(' ' + board[1] + ' | ' + board[2] + ' | ' + board[3])
    print('   |   |')
def player_input():
    pi_result = 'Default'
    while pi_result not in ['X','O']:
        pi_result = input('Player 1: Do you want to be X or O? ').upper()
        if  pi_result not in ['X','O']:
            print('Please enter either X or O!')
        elif pi_result == 'X':
            return ('X','O')
        else:
            return ('O','X')
def place_marker(board, marker, position):
    board[position] = marker
def win_check(board,mark):
    return ((board[7] == mark and board[8] == mark and board[9] == mark) or # across the top
    (board[4] == mark and board[5] == mark and board[6] == mark) or # across the middle
    (board[1] == mark and board[2] == mark and board[3] == mark) or # across the bottom
    (board[7] == mark and board[4] == mark and board[1] == mark) or # down the middle
    (board[8] == mark and board[5] == mark and board[2] == mark) or # down the middle
    (board[9] == mark and board[6] == mark and board[3] == mark) or # down the right side
    (board[7] == mark and board[5] == mark and board[3] == mark) or # diagonal
    (board[9] == mark and board[5] == mark and board[1] == mark)) # diagonal
def choose_first():
    if random.randint(0,1) == 0:
        return 'Player 1'
    else:
        return 'Player 2'   
def space_check(board, position):
    return board[position] == ' '
def full_board_check(board):
    for i in range(1,10):
        if space_check(board,i):
            return False
    return True    
def player_choice(board):
    pc_result = 0
    while not space_check(board,pc_result) or pc_result not in [1,2,3,4,5,6,7,8,9]:
        pc_result = int(input('Choose your next position (1-9): '))
    return pc_result
def replay():
    replay_result = 'Default'
    while replay_result not in ['YES','NO']:
        replay_result = input('Do you want to play again? Enter Yes or No: ').upper()
        return replay_result == 'YES'
print('Welcome to Tic Tac Toe!')

while True:
    board = [' ',' ',' ',' ',' ',' ',' ',' ',' ',' ']
    Player1_marker, Player2_marker = player_input()
    turn = choose_first()
    print(turn + ' will go first.')
    asking_readiness = input('Are you ready to play? Yes or No? ').upper()
    if asking_readiness == 'YES':
        game_on = True
    else:
        game_on = False
    
    while game_on:
        if turn == 'Player 1':
            display_board(board)
            position = player_choice(board)
            place_marker(board, Player1_marker, position)
            if win_check(board,Player1_marker):
                display_board(board)
                print(turn + ' has won the game!')
                break
            else:
                if full_board_check(board):
                    display_board(board)
                    print('There is a tie!')
                    break
                else:
                    turn = 'Player 2'
        else:
            display_board(board)
            position = player_choice(board)
            place_marker(board, Player2_marker, position)
            if win_check(board,Player2_marker):
                display_board(board)
                print(turn + ' has won the game!')
                break
            else:
                if full_board_check(board):
                    display_board(board)
                    print('There is a tie!')
                    break
                else:
                    turn = 'Player 1'
    if not replay():
        break

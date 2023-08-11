def create_board():
    board = [[' ' for _ in range(3)] for _ in range(3)]
    return board


def print_board(board):
    for row in board:
        print('|', end='')
        for cell in row:
            print(f' {cell} |', end='')
        print('\n' + '-' * 11)


def is_winner(board, player):
    for i in range(3):
        if all(board[i][j] == player for j in range(3)):
            return True
        if all(board[j][i] == player for j in range(3)):
            return True

    if (board[0][0] == board[1][1] == board[2][2] == player) or (board[0][2] == board[1][1] == board[2][0] == player):
        return True

    return False


def is_draw(board):
    for row in board:
        if ' ' in row:
            return False
    return True


def make_move(board, player):
    while True:
        try:
            row = int(input('Введите номер строки (1-3): ')) - 1
            col = int(input('Введите номер столбца (1-3): ')) - 1
            if row in range(3) and col in range(3) and board[row][col] == ' ':
                board[row][col] = player
                break
            else:
                print('Некорректные координаты! Попробуйте снова.')
        except ValueError:
            print('Некорректный ввод! Введите целое число.')


def play_game():
    board = create_board()
    players = ('X', 'O')
    current_player = 0

    while True:
        print_board(board)
        player = players[current_player]

        print(f'Ход игрока {player}')
        make_move(board, player)

        if is_winner(board, player):
            print(f'Игрок {player} победил!')
            break

        if is_draw(board):
            print('Игра окончилась ничьей!')
            break

        current_player = (current_player + 1) % 2


play_game()

<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name: Vikamuhan.N</h3>
<h3>Register Number:212223240181 </h3>
<H3>Aim:</H3>
<p>
Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game
</p>
<h1>GOALS of Alpha-Beta Pruning in MiniMax Search Algorithm</h1>

<h3>Improve the decision-making efficiency of the computer player by reducing the number of evaluated nodes in the game tree.</h3>
<h3>Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning and the Minimax algorithm with Python Code.</h3>
<h1>IMPLEMENTATION</h1>

The project involves developing a Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning with the Minimax algorithm. Using this algorithm, the computer player analyzes the game state, evaluates possible moves, and selects the optimal action based on the anticipated outcomes.

<h1>The Minimax algorithm</h1>

recursively evaluates all possible moves and their potential outcomes, creating a game tree.

<h1>Alpha-Beta pruning</h1>

Alpha–Beta (𝛼−𝛽) algorithm is actually an improved minimax using a heuristic. It stops evaluating a move when it makes sure that it’s worse than a previously examined move. Such moves need not to be evaluated further.

When added to a simple minimax algorithm, it gives the same output but cuts off certain branches that can’t possibly affect the final decision — dramatically improving the performance
<hr>

<h2>program</h2>
```
py
import math
X = 'X'
O = 'O'
EMPTY = None


def print_board(board):
    for row in board:
        print(' | '.join(cell if cell is not None else ' ' for cell in row))
        print('---------')

def check_winner(board, player):
    # Check rows
    for row in board:
        if all(cell == player for cell in row):
            return True
    # Check columns
    for col in range(3):
        if all(board[row][col] == player for row in range(3)):
            return True
    # Check diagonals
    if all(board[i][i] == player for i in range(3)) or all(board[i][2-i] == player for i in range(3)):
        return True
    return False


def check_draw(board):
    return all(cell is not None for row in board for cell in row)


def get_available_moves(board):
    return [(row, col) for row in range(3) for col in range(3) if board[row][col] is None]


def evaluate(board):
    if check_winner(board, X):
        return 1
    elif check_winner(board, O):
        return -1
    elif check_draw(board):
        return 0
    else:
        return None


def minimax(board, depth, alpha, beta, maximizing_player):
    eval_result = evaluate(board)
    if eval_result is not None:
        return eval_result

    if maximizing_player:
        max_eval = -math.inf
        for move in get_available_moves(board):
            row, col = move
            board[row][col] = X
            eval_score = minimax(board, depth + 1, alpha, beta, False)
            board[row][col] = None
            max_eval = max(max_eval, eval_score)
            alpha = max(alpha, eval_score)
            if beta <= alpha:
                break
        return max_eval
    else:
        min_eval = math.inf
        for move in get_available_moves(board):
            row, col = move
            board[row][col] = O
            eval_score = minimax(board, depth + 1, alpha, beta, True)
            board[row][col] = None
            min_eval = min(min_eval, eval_score)
            beta = min(beta, eval_score)
            if beta <= alpha:
                break
        return min_eval


def find_best_move(board):
    best_move = None
    best_eval = -math.inf
    alpha = -math.inf
    beta = math.inf
    for move in get_available_moves(board):
        row, col = move
        board[row][col] = X
        eval_score = minimax(board, 0, alpha, beta, False)
        board[row][col] = None
        if eval_score > best_eval:
            best_eval = eval_score
            best_move = move
    return best_move


def play_game():
    board = [[EMPTY, EMPTY, EMPTY],
             [EMPTY, EMPTY, EMPTY],
             [EMPTY, EMPTY, EMPTY]]

    current_player = X

    while True:
        print_board(board)

        if current_player == X:
            row, col = find_best_move(board)
            print("X's move:")
        else:
            row, col = map(int, input("O's move (row col): ").split())

        if board[row][col] is not None:
            print("Invalid move! Try again.")
            continue

        board[row][col] = current_player

        if check_winner(board, current_player):
            print_board(board)
            print(current_player, "wins!")
            break
        elif check_draw(board):
            print_board(board)
            print("Draw!")
            break

        current_player = O if current_player == X else X


play_game()
```


<h2>Sample Input and Output:</h2>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8d5e329a-9aff-41a6-bcf0-46efa10e1b92)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/438b242d-54ba-443e-b040-a936e6ae3b55)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/99a33390-fa11-4ade-a19f-e93bcd7aaec9)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/440797bd-53cb-49c1-b18d-89776864c3e7)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/81575a16-26b2-46f1-a8ac-27c9ed0a0fe5)

<H2>output</H2>

<img width="1280" alt="Screen Shot 1946-01-27 at 20 58 26" src="https://github.com/vikamuhan-reddy/19AI405ExpNo7/assets/144928933/f6b108e7-1c84-4129-be8f-7511d6ab68f9">
<img width="1280" alt="Screen Shot 1946-01-27 at 20 58 49" src="https://github.com/vikamuhan-reddy/19AI405ExpNo7/assets/144928933/40985ea2-8ec4-4305-912c-3ba4c8b5ab41">



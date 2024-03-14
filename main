from tkinter import *


class Square:

    def __init__(self, text, rows, cols):
        self.rows = rows
        self.cols = cols
        self.label = Label(window, text=text, font=("Consolas", 25), width=4, height=2, borderwidth=1, relief="solid")
        if cols == 2 or cols == 5:
            padxE = 5
        else:
            padxE = 0
        if rows == 2 or rows == 5:
            padyS = 5
        else:
            padyS = 0
        self.label.grid(row=rows, column=cols, padx=(0, padxE), pady=(0, padyS))

    def set_board_to_grid(self, text):
        if text == 0:
            text = ""
        self.label.config(text=text)

    def change_number(self, text, color):
        if text == 0:
            text = ""
        self.label.config(text=text, background=color)


def is_valid_move(grid, row, col, number):

    for x in range(9):
        if grid[row][x] == number:
            return False

    for x in range(9):
        if grid[x][col] == number:
            return False

    corner_row = row - row % 3
    corner_col = col - col % 3
    for x in range(3):
        for y in range(3):
            if grid[corner_row + x][corner_col + y] == number:
                return False

    return True


def solve(grid, row, col):

    if col == 9:
        if row == 8:
            return True
        row += 1
        col = 0

    if grid[row][col] > 0:
        return solve(grid, row, col + 1)

    for num in range(1, 10):
        if is_valid_move(grid, row, col, num):
            grid[row][col] = num

            board[row][col].change_number(grid[row][col], "green")
            window.update()

            if solve(grid, row, col + 1):
                return True

        grid[row][col] = 0

        board[row][col].change_number(grid[row][col], "red")
        window.update()

    return False


def show_grid(event):
    print(board_grid)
    for x in range(9):
        board_grid[x].clear()

    for r in range(9):
        for c in range(9):
            if options.get(clicked.get()) == 1:
                i = 0
            elif options.get(clicked.get()) == 2:
                i = grid[r][c]
            elif options.get(clicked.get()) == 3:
                i = grid2[r][c]
            else:
                break
            board[r][c].change_number(i, "white")
            board_grid[r].append(i)


def solving():
    if solve(board_grid, 0, 0):
        for i in range(9):
            for j in range(9):
                print(board_grid[i][j], end=" ")
            print()
    else:
        print("No Solution For This Sudoku")


grid = [[0, 0, 0, 0, 0, 0, 6, 8, 0],
        [0, 0, 0, 0, 7, 3, 0, 0, 9],
        [3, 0, 9, 0, 0, 0, 0, 4, 5],
        [4, 9, 0, 0, 0, 0, 0, 0, 0],
        [8, 0, 3, 0, 5, 0, 9, 0, 2],
        [0, 0, 0, 0, 0, 0, 0, 3, 6],
        [9, 6, 0, 0, 0, 0, 3, 0, 8],
        [7, 0, 0, 6, 8, 0, 0, 0, 0],
        [0, 2, 8, 0, 0, 0, 0, 0, 0]]


grid2 = [[1, 2, 0, 3, 0, 4, 0, 5, 6,],
         [7, 0, 0, 0, 0, 6, 0, 0, 1,],
         [0, 0, 0, 0, 0, 0, 0, 0, 0,],
         [0, 8, 0, 4, 0, 9, 0, 2, 0,],
         [0, 0, 0, 0, 6, 0, 0, 0, 0,],
         [0, 3, 0, 5, 0, 1, 0, 8, 0,],
         [0, 0, 0, 0, 0, 0, 0, 0, 0,],
         [9, 0, 0, 2, 0, 0, 0, 0, 8,],
         [8, 4, 0, 6, 0, 7, 0, 1, 9,]]


board_grid = [[], [], [], [], [], [], [], [], []]

window = Tk()
window.config(background="black")

options = {"Empty": 1, "Grid 1": 2, "Grid 2": 3}

clicked = StringVar()
clicked.set("Empty")


board = []
for r in range(len(grid)):
    columns = []
    for c in range(len(grid[0])):
        columns.append(Square("", r, c))
        board_grid[r].append(0)
    board.append(columns)

button = Button(window, text="SOLVE", font=("Consolas", 25), command=solving)
button.grid(row=11, column=1, columnspan=3)

dropdown = OptionMenu(window, clicked, *options, command=show_grid)
dropdown.grid(row=11, column=3, columnspan=5)
dropdown.config(width=10, font=("Consolas", 25))


window.mainloop()

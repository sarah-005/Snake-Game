import tkinter as tk
import random

# Linked list node for snake body

class Node:
    def __init__(self, row, col):
        self.row = row
        self.col = col
        self.next = None

# Represents snake body using nodes

class Snake:
    def __init__(self):
        self.head = Node(10, 10)
        second = Node(10, 9)
        third = Node(10, 8)
        self.head.next = second
        second.next = third

    def add_head(self, row, col):
        new_node = Node(row, col)
        new_node.next = self.head
        self.head = new_node

    def remove_tail(self):
        current = self.head
        if current.next is None:
            return
        while current.next.next:
            current = current.next
        current.next = None

    def get_positions(self):
        positions = []
        current = self.head
        while current:
            positions.append((current.row, current.col))
            current = current.next
        return positions

# Grid + rendering settings

GRID_SIZE = 20
CELL_SIZE = 30
WIDTH = GRID_SIZE * CELL_SIZE
HEIGHT = GRID_SIZE * CELL_SIZE

# Controls logic, rendering, input

class SnakeGame:
    def __init__(self, root):
        self.root = root
        self.root.title("Snake Game <3")
        self.canvas = tk.Canvas(root, width=WIDTH, height=HEIGHT, bg="white")
        self.canvas.pack()
        self.canvas.focus_set()
        self.high_score = 0
        self.restart_game()

        self.root.bind("<Key>", self.change_direction)
        self.game_loop()

    # GAME RESET / INITIAL STATE

    def restart_game(self):
        self.snake = Snake()
        self.direction = "Right"
        self.score = 0
        self.food = self.create_food()
        self.game_over_flag = False

    # Avoid spawning on snake body

    def create_food(self):
        snake_cells = self.snake.get_positions()
        while True:
            row = random.randint(0, GRID_SIZE - 1)
            col = random.randint(0, GRID_SIZE - 1)
            if (row, col) not in snake_cells:
                return (row, col)

    # WASD / arrows + restart/quit

    def change_direction(self, event):
        key = event.keysym

        if key.lower() == "r":
            self.restart_game()
            return
        
        if key.lower() == "q":
            self.root.destroy()
            return

        if key == "Up" and self.direction != "Down":
            self.direction = "Up"
        elif key == "Down" and self.direction != "Up":
            self.direction = "Down"
        elif key == "Left" and self.direction != "Right":
            self.direction = "Left"
        elif key == "Right" and self.direction != "Left":
            self.direction = "Right"

    # Movement + collision + eating food

    def move_snake(self):
        if self.game_over_flag:
            return

        row = self.snake.head.row
        col = self.snake.head.col

        if self.direction == "Up":
            row -= 1
        elif self.direction == "Down":
            row += 1
        elif self.direction == "Left":
            col -= 1
        elif self.direction == "Right":
            col += 1

        if row < 0 or row >= GRID_SIZE or col < 0 or col >= GRID_SIZE:
            self.game_over()
            return

        body = self.snake.get_positions()[:-1]
        if (row, col) in body:
            self.game_over()
            return

        self.snake.add_head(row, col)

        if (row, col) == self.food:
            self.score += 1
            self.food = self.create_food()
        else:
            self.snake.remove_tail()

    # Snake + food + score UI

    def draw(self):
        self.canvas.delete("all")

        positions = self.snake.get_positions()

        for index, (row, col) in enumerate(positions):
            x1 = col * CELL_SIZE
            y1 = row * CELL_SIZE
            x2 = x1 + CELL_SIZE
            y2 = y1 + CELL_SIZE

            if index == 0:
                self.canvas.create_oval(x1, y1, x2, y2,
                    fill="#FFB6C1", outline="#FF68B4",width=2)

                self.canvas.create_oval(x1+3, y1+16, x1+7, y1+20,
                    fill="#FF69B4", outline="")
                self.canvas.create_oval(x1+23, y1+16, x1+27, y1+20,
                    fill="#FF69B4", outline="")
            else:
                self.canvas.create_oval(x1 + 1, y1 + 1, x2 - 1, y2 - 1,
                    fill="#FFC0CB", outline="#FF69B4", width=2)

        food_row, food_col = self.food
        x1 = food_col * CELL_SIZE
        y1 = food_row * CELL_SIZE
        x2 = x1 + CELL_SIZE
        y2 = y1 + CELL_SIZE

        self.canvas.create_oval(x1+2, y1+2, x1+CELL_SIZE//2+2,
                                y1+CELL_SIZE//2+2,
                                fill="red", outline="red")

        self.canvas.create_oval(x1+CELL_SIZE//2-2, y1+2,
                                x2-2, y1+CELL_SIZE//2+2,
                                fill="red", outline="red")

        self.canvas.create_polygon(
            x1+2, y1+CELL_SIZE//3,
            x2-2, y1+CELL_SIZE//3,
            x1+CELL_SIZE//2, y2-2,
            fill="red", outline="red"
        )

        self.canvas.create_text(
            120, 15,
            text=f"Score: {self.score}  > High Score: {self.high_score} <",
            fill="black",
            font=("Arial", 12, "bold")
        )
    
    # GAME OVER ANIMATION (BLINK TEXT)

    def blink_game_over(self):

        current_color = self.canvas.itemcget(
            self.game_over_text,
            "fill"
        )

        if current_color == "white":
            self.canvas.itemconfig(
                self.game_over_text,
                fill="red"
            )
        else:
            self.canvas.itemconfig(
                self.game_over_text,
                fill="white"
            )

        if self.game_over_flag:
            self.root.after(600, self.blink_game_over)

    # GAME OVER ANIMATION (BLINK TEXT)

    def game_over(self):

        if self.score > self.high_score:
            self.high_score = self.score

        self.game_over_flag = True

        self.canvas.delete("all")

        self.game_over_text  = self.canvas.create_text(
            WIDTH // 2, HEIGHT //3,
            text = "GAME OVER...",
            fill = "red",
            font = ("Arial", 25, "bold")
        )
        self.blink_game_over()

        self.canvas.create_text(
            WIDTH // 2, HEIGHT // 2 - 30,
            text = f"Score: {self.score}\n",
            fill = "black",
            font = ("Proxy 1", 20, "bold")
        )

        self.canvas.create_text(
            WIDTH // 2, HEIGHT // 2 - 20,
            text = f"\nHigh Score: {self.high_score}\n",
            fill = "pink",
            font = ("Arial", 20, "bold")
        )

        self.canvas.create_text(
            WIDTH // 2, HEIGHT // 2 + 30,
            text = "\nPress > R < to Restart\n",
            fill = "green",
            font = ("Arial", 18, "bold")
        )

        self.canvas.create_text(
            WIDTH // 2, HEIGHT // 2 + 40,
            text = "\nPress > Q < to Quit",
            fill = "orange",
            font = ("Arial", 18, "bold")
        )

    # MAIN GAME LOOP

    def game_loop(self):

        self.move_snake()

        if not self.game_over_flag:
            self.draw()

        self.root.after(150, self.game_loop)

# PROGRAM ENTRY POINT

root = tk.Tk()
game = SnakeGame(root)
root.mainloop()

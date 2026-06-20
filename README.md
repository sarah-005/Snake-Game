# Snake Game Using Singly Linked List

## AII201 – Data Structures and Algorithms

---

# 1. Project Overview

This project is an implementation of the classic Snake Game using Python and the Tkinter graphical library. The game allows the player to control a snake inside a grid, collect food, increase the score, and avoid collisions.

The project demonstrates how a Singly Linked List can be used to represent the snake body instead of traditional Python lists. Each snake segment is stored as a node containing its position on the grid.

The game provides:

* Graphical user interface.
* Real-time movement.
* Food generation.
* Score tracking.
* High score tracking.
* Game over animation.
* Restart and quit controls.

---

# 2. Objectives

The objectives of this project are:

* Apply linked list concepts in a practical application.
* Implement dynamic memory structures.
* Build an interactive graphical application.
* Practice event-driven programming.
* Understand collision detection algorithms.
* Develop a real-time game loop.

---

# 3. Technologies Used

| Technology         | Purpose                  |
| ------------------ | ------------------------ |
| Python             | Programming language     |
| Tkinter            | Graphical user interface |
| Random Module      | Food generation          |
| Singly Linked List | Snake body storage       |

---

# 4. Data Structure

The snake body is implemented using a Singly Linked List.

Each node contains:

* Row position.
* Column position.
* Pointer to the next node.

```python
class Node:
    def __init__(self, row, col):
        self.row = row
        self.col = col
        self.next = None
```

Advantages of using a linked list:

* Dynamic size.
* Efficient insertion at the head.
* Easy body growth.
* Practical application of data structures.

---

# 5. Snake Class

The Snake class manages the entire snake body.

Functions:

### add_head()

Adds a new node to the front of the snake.

### remove_tail()

Deletes the last node when the snake moves without eating food.

### get_positions()

Returns all snake coordinates for drawing and collision detection.

---

# 6. Game Window

The game uses a 20 × 20 grid.

| Property      | Value      |
| ------------- | ---------- |
| Grid Size     | 20         |
| Cell Size     | 30 pixels  |
| Window Width  | 600 pixels |
| Window Height | 600 pixels |

---

# 7. User Controls

| Key         | Action       |
| ----------- | ------------ |
| Up Arrow    | Move Up      |
| Down Arrow  | Move Down    |
| Left Arrow  | Move Left    |
| Right Arrow | Move Right   |
| R           | Restart Game |
| Q           | Quit Game    |

The player cannot move directly in the opposite direction to avoid instant collisions.

---

# 8. Food Generation

Food is generated randomly inside the grid.

The algorithm checks that the generated position is not occupied by the snake body.

```python
while True:
    row = random.randint(0, GRID_SIZE - 1)
    col = random.randint(0, GRID_SIZE - 1)

    if (row, col) not in snake_cells:
        return (row, col)
```

---

# 9. Collision Detection

The game ends when:

* The snake hits the wall.
* The snake collides with its own body.

Boundary checking:

```python
if row < 0 or row >= GRID_SIZE:
```

Self-collision checking:

```python
if (row, col) in body:
```

---

# 10. Scoring System

The score increases by one whenever the snake eats food.

The highest score achieved during the session is stored as the High Score.

Displayed information:

* Current Score.
* High Score.

---

# 11. Game Over Screen

When the player loses:

* The game stops.
* The final score appears.
* The high score appears.
* "GAME OVER" blinks continuously.
* The player can restart or quit.

---

# 12. Game Loop

The game loop runs every 150 milliseconds.

```python
self.root.after(150, self.game_loop)
```

Responsibilities:

* Move the snake.
* Check collisions.
* Update score.
* Draw the screen.
* Refresh the interface.

---

# 13. Program Structure

```
Snake Game
│
├── Node Class
│
├── Snake Class
│   ├── add_head()
│   ├── remove_tail()
│   └── get_positions()
│
├── SnakeGame Class
│   ├── restart_game()
│   ├── create_food()
│   ├── change_direction()
│   ├── move_snake()
│   ├── draw()
│   ├── blink_game_over()
│   ├── game_over()
│   └── game_loop()
│
└── Main Program
```

---

# 14. Features

* Graphical interface.
* Linked list implementation.
* Dynamic snake growth.
* Collision detection.
* Random food placement.
* High score system.
* Restart functionality.
* Quit functionality.
* Animated game over screen.

---

# 15. Future Improvements

Possible future enhancements include:

* Saving high scores to a file.
* Multiple difficulty levels.
* Sound effects.
* Pause functionality.
* Obstacles inside the map.
* Different themes and colors.
* Multiplayer mode.
* Speed increase as score grows.

---

# 16. Conclusion

This project demonstrates the practical use of Singly Linked Lists in game development. The implementation combines data structures, algorithms, event handling, and graphical programming to create a fully functional Snake Game.

The project provides a strong example of how theoretical concepts from Data Structures and Algorithms can be applied in a real-world application.

# Connect Four AI with Minimax Algorithm

## Objective

The primary objective of this project is to demonstrate the implementation of the **minimax algorithm with alpha-beta pruning** for creating an intelligent Connect Four AI opponent. This project serves as an educational tool for understanding:

- Game tree search algorithms
- Adversarial AI techniques
- Heuristic evaluation functions
- Alpha-beta pruning optimization

The AI can play against itself or against human players, making strategic decisions by evaluating future game states and selecting optimal moves.

## Features

- **Complete Connect Four Game Engine**: Full implementation of Connect Four rules including move validation, win detection (horizontal, vertical, and diagonal), and board state management
- **Minimax Algorithm**: Classic adversarial search algorithm with alpha-beta pruning for efficient game tree traversal
- **Customizable Evaluation Functions**: Pluggable heuristic functions allow experimentation with different AI strategies
- **AI vs AI Mode**: Watch two different AI strategies compete against each other
- **Human vs AI Mode**: Built-in function for human players to challenge the AI
- **Adjustable Difficulty**: Control AI strength by modifying search depth

## Project Structure

```
Connect-Four-AI-Minimax/
├── connect_four.py      # Core game logic and minimax implementation
├── script.py            # Demo script showing AI vs AI gameplay
├── README.md            # This file
└── LICENSE              # MIT License
```

### File Descriptions

- **`connect_four.py`**: Contains all core functionality including board operations, move validation, win detection, the minimax algorithm with alpha-beta pruning, and evaluation functions
- **`script.py`**: Demonstration script that runs a match between two AI players with different evaluation strategies

## Requirements

- Python 3.8 or higher
- No external dependencies required

## Usage

### Running AI vs AI Demo

To watch two AI players compete against each other:

```bash
python script.py
```

This will start a game where:
- **Player X (Maximizing)**: Uses a custom evaluation function based on consecutive piece patterns
- **Player O (Minimizing)**: Uses a streak-counting heuristic

The board state is printed after each move, showing the progression of the game.

### Playing Against the AI

To play as a human against the AI, you can use the built-in `play_game()` function:

```python
from connect_four import play_game

# Start a game where you play as X and AI plays as O
# The number parameter controls AI search depth (higher = smarter but slower)
play_game(ai=4)
```

Run this in a Python script or interactive session:

```bash
python
>>> from connect_four import play_game
>>> play_game(ai=4)
```

### Customizing the AI

#### Adjusting AI Difficulty

Modify the `depth` parameter in the `minimax()` function call:

```python
# In script.py or your own code
result = minimax(board, True, depth=6, -float("Inf"), float("Inf"), my_evaluate_board)
```

- `depth=2`: Easy (fast, shallow search)
- `depth=4`: Medium (balanced)
- `depth=6`: Hard (slower, deep search)
- `depth=8+`: Very Hard (significantly slower)

#### Creating Custom Evaluation Functions

Write your own heuristic function to change AI behavior:

```python
def my_custom_eval(board):
    if has_won(board, "X"):
        return float("Inf")
    elif has_won(board, "O"):
        return -float("Inf")
    
    # Your custom heuristic logic here
    score = 0
    # Example: Favor center column control
    center_col = len(board) // 2
    for row in range(len(board[0])):
        if board[center_col][row] == "X":
            score += 3
        elif board[center_col][row] == "O":
            score -= 3
    
    return score
```

Then use it in the minimax call:

```python
result = minimax(board, True, 4, -float("Inf"), float("Inf"), my_custom_eval)
```

## How It Works

### Minimax Algorithm

The minimax algorithm explores the game tree by:

1. **Maximizing Player (X)**: Tries to maximize the board evaluation score
2. **Minimizing Player (O)**: Tries to minimize the board evaluation score
3. **Recursive Search**: Alternates between max and min players for each depth level
4. **Alpha-Beta Pruning**: Eliminates branches that cannot affect the final decision, improving performance

### Evaluation Functions

The project includes several evaluation strategies:

- **`cc_evaluate_board()`**: Counts potential winning streaks for each player
- **`my_evaluate_board()`**: Evaluates based on consecutive two-piece patterns horizontally and vertically
- **`random_eval()`**: Returns random scores (useful for testing)

## Future Features

The following enhancements are planned for future development:

### Core Improvements
- [ ] **Iterative Deepening**: Progressively increase search depth with time management
- [ ] **Transposition Tables**: Cache board evaluations to avoid redundant calculations
- [ ] **Move Ordering**: Prioritize promising moves first for better alpha-beta pruning
- [ ] **Opening Book**: Pre-computed optimal opening moves for faster early game

### User Experience
- [ ] **Graphical User Interface**: PyGame or Tkinter-based visual interface
- [ ] **Web Interface**: Browser-based game using Flask/Django
- [ ] **Multiplayer Support**: Online play between human players
- [ ] **Move History**: Track and replay game moves
- [ ] **Undo/Redo Functionality**: Allow players to take back moves

### AI Enhancements
- [ ] **Machine Learning Integration**: Neural network-based evaluation function
- [ ] **Monte Carlo Tree Search**: Alternative to minimax for comparison
- [ ] **Difficulty Levels**: Pre-configured easy/medium/hard settings
- [ ] **AI vs AI Tournament Mode**: Compare multiple evaluation strategies
- [ ] **Real-time Analysis**: Show AI's thought process and evaluation scores

### Analysis & Statistics
- [ ] **Game Statistics**: Win rates, average moves, time per move
- [ ] **Position Analysis**: Evaluate any board position
- [ ] **Move Suggestions**: Hint system for human players
- [ ] **Game Database**: Save and load games

### Code Quality
- [ ] **Unit Tests**: Comprehensive test coverage for all functions
- [ ] **Documentation**: Detailed docstrings and API documentation
- [ ] **Performance Profiling**: Optimize bottlenecks
- [ ] **Code Refactoring**: Improve modularity and maintainability

## Contributing

Contributions are welcome! Feel free to:
- Report bugs or issues
- Suggest new features
- Submit pull requests with improvements
- Share your custom evaluation functions

## License

This project is licensed under the MIT License. See the [`LICENSE`](LICENSE) file for details.

## Acknowledgments

This project was created as an educational exercise to explore game AI concepts and adversarial search algorithms.

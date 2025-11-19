# Checkers AI (Prolog + Negamax)

![Checkers AI Banner](assets/checkers_ai_banner.png)

## 🧠 Declarative AI: The Negamax Search Engine

This project demonstrates the power of **Logic Programming** in solving complex adversarial search problems. By leveraging **Prolog's** inherent backtracking and unification capabilities, we implement a robust **Checkers AI** driven by the **Negamax** algorithm—an elegant variant of Minimax. Unlike imperative implementations that require verbose state management, this declarative approach allows us to define *what* a valid move is and *how* to evaluate a board state, letting the Prolog engine handle the "how" of the search tree traversal. The result is a compact, high-performance decision engine that explores thousands of future game states to execute optimal strategies against a human opponent.

## Key Features

- **Declarative State Space**: The board and game rules are defined as logical facts and rules, making the code intuitive and verifiable.
- **Negamax Algorithm**: A simplified Minimax implementation that maximizes the score for the current player by negating the opponent's score.
- **Alpha-Beta Pruning**: (Implicitly structured) Efficiently prunes irrelevant branches of the search tree to deepen the search horizon.
- **Heuristic Evaluation**: A positional and material-based evaluation function to guide the AI's strategy.

## Code Structure

The core logic is contained in `src/checkers.pl`:

- **`initial_board/1`**: Defines the starting 8x8 grid.
- **`evaluate/2`**: Calculates the heuristic value of a board state.
- **`valid_move/3`**: Generates legal moves using backtracking.
- **`negamax/5`**: The recursive search algorithm finding the best move.

## Getting Started

1. Install a Prolog interpreter (e.g., SWI-Prolog).
2. Load the project: `['src/checkers.pl'].`
3. Query the AI for a move: `negamax(CurrentBoard, 3, -10000, 10000, BestScore).`

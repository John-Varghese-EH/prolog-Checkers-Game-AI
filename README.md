# Checkers AI (Prolog + Negamax)

## Declarative AI: The Negamax Search Engine

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

## Installation

### Prerequisites
- **SWI-Prolog**: Download and install from [swi-prolog.org](https://www.swi-prolog.org/Download.html)
  - Windows: Download the installer and run it
  - macOS: `brew install swi-prolog`
  - Linux: `sudo apt-get install swi-prolog`

### Verify Installation
Open a terminal and run:
```bash
swipl --version
```

## Usage

### Quick Start

1. **Clone the repository**:
   ```bash
   git clone https://github.com/John-Varghese-EH/aiml-Checkers-Game-AI.git
   cd aiml-Checkers-Game-AI
   ```

2. **Launch SWI-Prolog**:
   ```bash
   swipl
   ```

3. **Load the Checkers AI**:
   ```prolog
   ?- ['src/checkers.pl'].
   true.
   ```

4. **Get the initial board**:
   ```prolog
   ?- initial_board(Board).
   Board = [e, b, e, b, e, b, e, b, b, e, b, e, b, e, b, e, ...].
   ```

5. **Evaluate a board position**:
   ```prolog
   ?- initial_board(Board), evaluate(Board, Score).
   Board = [e, b, e, b, e, b, e, b, b, e, b, e, b, e, b, e, ...],
   Score = 0.
   ```

6. **Run the AI search** (depth 3):
   ```prolog
   ?- initial_board(Board), negamax(Board, 3, -10000, 10000, BestScore).
   ```

### Example Session

Here's a complete example of interacting with the AI:

```prolog
% Start SWI-Prolog and load the file
?- ['src/checkers.pl'].
true.

% Get the initial board state
?- initial_board(Board).
Board = [e, b, e, b, e, b, e, b, b, e, b, e, b, e, b, e, e, b, e, b, e, b, e, b, e, e, e, e, e, e, e, e, e, e, e, e, e, e, e, e, w, e, w, e, w, e, w, e, e, w, e, w, e, w, e, w, w, e, w, e, w, e, w, e].

% Evaluate the initial position (should be balanced = 0)
?- initial_board(Board), evaluate(Board, Score).
Score = 0.

% Count black pieces
?- initial_board(Board), count_pieces(Board, b, Count).
Count = 12.

% Count white pieces
?- initial_board(Board), count_pieces(Board, w, Count).
Count = 12.
```

### Understanding the Board Representation

The board is a flat list of 64 elements representing an 8×8 grid:
- `e` = empty square
- `b` = black piece (AI)
- `w` = white piece (Human)
- `bk` = black king
- `wk` = white king

**Board Layout** (indices 0-63):
```
  0  1  2  3  4  5  6  7
  8  9 10 11 12 13 14 15
 16 17 18 19 20 21 22 23
 24 25 26 27 28 29 30 31
 32 33 34 35 36 37 38 39
 40 41 42 43 44 45 46 47
 48 49 50 51 52 53 54 55
 56 57 58 59 60 61 62 63
```

### Customizing Search Depth

Adjust the depth parameter for stronger/faster play:
- **Depth 1-2**: Fast, beginner level
- **Depth 3-4**: Moderate, intermediate level
- **Depth 5+**: Slow, advanced level

```prolog
% Shallow search (fast)
?- negamax(Board, 2, -10000, 10000, Score).

% Deep search (slow but stronger)
?- negamax(Board, 5, -10000, 10000, Score).
```

## Troubleshooting

**Issue**: `ERROR: source_sink 'src/checkers.pl' does not exist`
- **Solution**: Make sure you're in the project root directory when launching `swipl`

**Issue**: Prolog not recognized
- **Solution**: Ensure SWI-Prolog is installed and added to your system PATH

**Issue**: Search takes too long
- **Solution**: Reduce the search depth parameter (use 2-3 instead of 5+)

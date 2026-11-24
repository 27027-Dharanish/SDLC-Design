# High-Level Design (HLD) – Tic Tac Toe Console Application
 
## Document Information
 
| Field | Value |
|---|---|
| Title | Tic Tac Toe Application HLD |
| Author(s) | Dharanish |
| Date | 2026-11-23 |
| Status | Draft |
 
## Table of Contents
 
- [1. Problem Statement](#1-problem-statement)
- [2. Design Overview and Flow Diagram](#2-design-overview-and-flow-diagram)
- [3. Implementation Details](#3-implementation-details)
- [4. Security](#5-security)
- [5. Open Issues](#6-open-issues)
 
---
 
# 1. Problem Statement
 
The objective of this project is to develop a console-based Tic Tac Toe game application using C#. The application will allow users to create an account, log in, and play Tic Tac Toe in four different modes: Easy, Medium, Impossible, and Manual.
  
The application will maintain live scores for players and store completed match details, including the game mode, result, date, time, and moves. Users will also be able to replay their previous matches.
 
The main goal is to provide a simple, user-friendly gaming experience with proper user authentication, different computer difficulty levels, score management, and game history.
 
## Project Objectives
 
- Provide Login and Signup functionality.
- Support four different game modes.
- Maintain real-time scores during gameplay.
- Allow users to quit an active match.
- Store match details.
- Allow users to view and replay previous matches.
- Provide proper input validation and error messages.
 
# 2. Design Overview and Flow Diagram
 
The application follows a simple modular structure. Each module is responsible for a particular functionality, making the application easy to understand, maintain, and test.
 
Since this is a console-based application, all user interactions will happen through the console. User details, scores, and match history will be stored in local JSON files.
 
## 2.1 System Architecture

- [System architecture and the actual flow of the application](./ADR.md)

 
## 2.2 Application Flow
 
1. When the application starts, the user will be redirected to the Login or Signup section.
2. Existing users can log in using their username and password.
3. New users can create an account using the Signup option.
4. After successful authentication, the main menu will be displayed.
5. The user can select a game mode, view the scoreboard, check game history, or log out.
6. Based on the selected game mode, the game controller starts a new match.
7. The game logic manages player turns, validates moves, checks winning conditions, and updates the board.
8. After the match is completed, the result and match details are saved in JSON files.
9. The user can choose to play again in the same mode or return to the main menu.
10. From the Game History section, users can select and replay their previous completed matches.
 
# 3. Implementation Details
 
## 3.1 Components and Responsibilities
 
# C# Console Tic Tac Toe - Project Timeline

- [System Modules & 5-Day Development Timeline](./PROJECT_PLAN.md)

 
## 3.2 Data Storage
 
The application will use local JSON files to store user information, scores, and match history.
 
No external database is required.
 
The following files will be maintained:
 
**1. Users.json**
 
Stores registered user details.
 
Example:
 
```json
[
  {
    "UserId": "u_001",
    "Username": "player1",
    "DateOfBirth": "2002-05-14",
    "PasswordHash": "hashed_password_here",
    "CreatedAt": "2026-11-23T10:20:00Z",
    "Stats": {
      "GamesPlayed": 12,
      "Wins": 7,
      "Losses": 3,
      "Draws": 2
    }
  }
]

```
 
**2. Scores.json**
 
Stores the cumulative scores of users.
 
Example:
 
```json
[
  {
    "Username": "player1",
    "Player1Score": 5,
    "Player2Score": 3
  }
]
```
 
**3. GameHistory.json**
 
Stores completed match information.
 
Example:
 
```json
[
  {
    "Username": "player1",
    "GameMode": "Easy",
    "Result": "Win",
    "DateTime": "2026-11-23 10:30:00",
    "Moves": [1, 5, 2, 8, 3]
  }
]
```
  
## 3.3 Technology Choices
 

| Technology | Purpose |
|---|---|
| **C#** | Main programming language. |
| **.NET** | Runtime environment for executing the application. |
| **Console Application** | Provides the base execution environment for user interaction. |
| **Spectre.Console** | Beautifies the console UI with colored text, tables, panels, ASCII banners, and interactive selection menus. |
| **JSON** | Stores user details, scores, and match history locally. |
| **System.Text.Json** | Handles JSON serialization and deserialization. |
| **Minimax Algorithm** | Used for Impossible Mode and optimal computer moves in Medium Mode. |

 
These technologies are suitable because they are simple, lightweight, and sufficient for developing a console-based game.
 
## 3.4 Performance and Scalability
 
The application is designed for individual users playing through a console.
 
- The 3×3 game board requires very little processing time.
- The Minimax algorithm can efficiently evaluate all possible Tic Tac Toe moves.
- JSON files are sufficient for storing user details, scores, and match history.
- Only one user account will be active during a console session.
 
Since the application is designed for local usage, large-scale server infrastructure is not required.
 
## 3.5 Input Validation and Error Handling
 
The application will validate all user inputs before processing them.
 
- Invalid username or password will display an appropriate error message.
- Duplicate usernames will not be allowed during Signup.
- Invalid cell numbers will be rejected.
- Already occupied cells cannot be selected again.
- Invalid characters will display a warning message.
- Entering Q during a match will immediately quit the active match after confirmation.
- File-related errors will be handled without unexpectedly crashing the application.
 
The board will remain unchanged when an invalid move is entered.
 
## 3.6 Testing Strategy
 
The application will be tested at different levels to ensure that all functionalities work correctly.
  
- Test the complete application flow from Signup to Logout.
- Play matches in all four game modes.
- Test quitting a match during gameplay.
- Test replaying previous matches.
- Test invalid inputs and unexpected user actions.

# 4. Alternative implementations

# Tic-Tac-Toe AI Algorithms

A comprehensive overview of the algorithms used to build AI opponents for Tic-Tac-Toe, ranging from classic game-tree searches to machine learning approaches.

---

## 4.1 Minimax Algorithm
The gold standard for two-player, zero-sum games. It recursively simulates every possible future move until the game ends, assuming the opponent will always play optimally. It assigns scores to outcomes (e.g., `+10` for a win, `-10` for a loss, `0` for a draw) and picks the move that maximizes its own score while minimizing the opponent's.

* **Pros:**
  * Guarantees an unbeatable AI that will never lose.
  * Relatively simple to implement using recursion.
* **Cons:**
  * Evaluates every single possible game state, making it slow and computationally expensive if scaled to larger grids (e.g., 4x4 or 5x5).

---

## 4.2 Minimax with Alpha-Beta Pruning
An optimized version of the standard Minimax algorithm. It keeps track of the best already-explored options along the path (`alpha` and `beta`) and stops evaluating a branch of moves the moment it realizes that branch is worse than a previously examined move.

* **Pros:**
  * Produces the exact same unbeatable results as standard Minimax.
  * Runs significantly faster by skipping useless calculations.
* **Cons:**
  * Slightly more complex to write and debug than standard Minimax.

---

## 4.3 Rule-Based / Heuristic Approach (Newell and Simon’s Strategy)
Instead of looking ahead at future moves, the AI follows a strict, prioritized checklist of rules for the current board state:
1. Win if possible.
2. Block the opponent's win.
3. Create a fork (two simultaneous ways to win).
4. Block the opponent's fork.
5. Play the center square.
6. Play the opposite corner of the opponent.
7. Play an empty corner.
8. Play an empty side.

* **Pros:**
  * Executes almost instantaneously with virtually zero memory or CPU overhead.
  * Easy to adjust difficulty levels by simply removing rules from the top of the list.
* **Cons:**
  * Requires hardcoding game-specific human knowledge.
  * Cannot easily adapt to variations of the game without rewriting the rules.

---

## 4.4 Lookup Table (Move Table)
This approach pre-calculates and stores every possible board configuration—$3^9$ (`19,683`) states—along with the ideal response move in a massive array or database. During gameplay, the AI simply looks up the current board to find its move.

* **Pros:**
  * Instantaneous execution time ($O(1)$ lookup) during gameplay.
* **Cons:**
  * Consumes a large amount of memory/storage to hold all states.
  * Tedious to generate without writing another algorithm to populate the table first.
  * Zero adaptability to other games or grid sizes.

---

## 4.5 Reinforcement Learning (e.g., Q-Learning)
Instead of being programmed with rules or tree searches, the AI plays thousands of games against itself or a random opponent. It gets rewarded for wins and penalized for losses, gradually updating a table of values (Q-table) to learn which moves lead to good outcomes.

* **Pros:**
  * Requires no hardcoded strategy or game-tree logic.
  * Great educational tool for demonstrating how machine learning works in a simple environment.
* **Cons:**
  * Overkill for a solved game like Tic-Tac-Toe.
  * Requires a training phase before it can play well.
  * May still make suboptimal moves if it hasn't encountered a specific board state enough times during training.

---

## Summary Comparison

| Algorithm | Unbeatable? | Speed | Implementation Difficulty |
| :--- | :--- | :--- | :--- |
| **Minimax** | Yes | Moderate | Medium |
| **Alpha-Beta Pruning** | Yes | Fast | Medium-Hard |
| **Rule-Based (Heuristic)** | Yes | Instant | Easy |
| **Lookup Table** | Yes | Instant | Easy *(tedious setup)* |
| **Q-Learning (ML)** | Eventually | Fast *(after training)* | Hard |

## Recommendation
### Why Standard Minimax is Better for 3x3 Tic-Tac-Toe

* **Small Search Space:** A 3x3 grid has at most 9! (`362,880`) possible move sequences, and far fewer valid game states once wins and draws terminate branches early. Modern computers evaluate all of these in **a few milliseconds**.
* **Easier to Write and Debug:** You don't need to track `alpha` and `beta` bounds across recursive calls, making your code cleaner, shorter, and much less prone to subtle bugs.
* **Identical Gameplay:** Standard Minimax and Alpha-Beta Pruning make the **exact same moves**. For a human player, there is zero noticeable difference in speed or intelligence.


# 5. Security
 
Security is important because the application maintains user accounts and passwords.
 
## 5.1 Authentication and Authorization
 
- Users must log in using valid credentials before accessing the main menu.
- New users must register through the Signup section.
- Duplicate usernames will not be allowed.
- Only one user account can be logged in during a console session.
- Users can log out through the main menu.
 
## 5.2 Data Handling
 
- User information, scores, and match history will be stored in local JSON files.
- Passwords will be stored as secure password hashes instead of plain text.
- Access to local data files will be restricted through appropriate file permissions.
- Sensitive information will not be displayed unnecessarily in the console.
 
## 5.3 Input Validation
 
- Username and password inputs will be validated during Signup and Login.
- Game moves must contain valid cell numbers between 1 and 9.
- Occupied cells cannot be selected.
- Invalid characters and unexpected inputs will be handled safely.
 
## 5.4 Threats and Mitigations
 
| Possible Threat | Mitigation |
|---|---|
| Unauthorized Login | Validate credentials before granting access. |
| Password Exposure | Store password hashes instead of plain-text passwords. |
| Invalid User Input | Validate all inputs before processing. |
| Data Modification | Restrict access to local JSON files. |
| Accidental Data Loss | Handle file operations carefully and validate stored data. |
 
## 5.5 External Dependencies
 
The application uses built-in .NET libraries and  JSON storage. No external services or third-party APIs are required.
 
# 6. Open Issues
 
 
There are no open issues in the application currently.
 
---
 
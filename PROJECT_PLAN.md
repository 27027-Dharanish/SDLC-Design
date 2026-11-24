# C# Console Tic Tac Toe — Project Plan

## 1. System Modules

| Component | Responsibility |
| :--- | :--- |
| **Authentication Module** | Handles user Login, Signup (with age > 7 verification), and Logout with JSON persistence. |
| **Main Menu Module** | Displays the available application options and manages navigation via Spectre.Console. |
| **Game Controller** | Manages the overall gameplay loop, mode selection, player turns, and quit confirmation. |
| **Game Board Module** | Displays and updates the styled 3×3 Tic Tac Toe board in the console. |
| **Game Logic Module** | Checks valid moves, winning conditions, draws, and mid-game quits. |
| **Move Strategy Module** *(Consolidated Modes)* | Implements `IMoveStrategy` across 4 modes:<br>• **Easy Mode:** Random moves while avoiding blocking the player's immediate winning line.<br>• **Medium Mode:** Alternates between Minimax and random moves (50% probability).<br>• **Impossible Mode:** Full Minimax algorithm ensuring the AI never loses.<br>• **Manual Mode:** Local 2-player input on the same console. |
| **Scoreboard Module** | Tracks and displays live session scores (+1 win, 0 draw/loss) alongside lifetime user stats. |
| **Match Persistence & Replay Module** | Saves completed match details (timestamp, mode, result, moves) to JSON and replays previous matches move-by-move with a 1s delay. |
| **Enhancement Module** | Improves console UI with Spectre.Console colors, tables, panels, and user-friendly prompts. |

---

## 2. 5-Day Development Timeline (Nov 23 – Nov 27)

| Day & Date | Modules Covered | Key Tasks & Deliverables | Est. Duration |
| :--- | :--- | :--- | :--- |
| **Day 1**<br>Mon, Nov 23 | • Authentication Module<br>• Main Menu Module | • Build user registration (with DOB/age > 7 check) & login validation.<br>• Set up `users.json` storage.<br>• Create the Spectre.Console main navigation loop and logout. | **5.5 hrs** |
| **Day 2**<br>Tue, Nov 24 | • Game Board Module<br>• Game Logic Module<br>• Game Controller | • Render the 3×3 grid (cells 1–9) using Spectre.Console.<br>• Implement move validation, win/draw checks, and `Q` quit confirmation.<br>• Build the core turn-switching loop. | **6.5 hrs** |
| **Day 3**<br>Wed, Nov 25 | • Move Strategy Module<br>*(Manual, Impossible, Medium, Easy)* | • Implement 2-player local input (Manual).<br>• Code the recursive Minimax algorithm (Impossible).<br>• Add 50% Minimax/random split (Medium) and non-blocking random logic (Easy). | **7.0 hrs** |
| **Day 4**<br>Thu, Nov 26 | • Scoreboard Module<br>• Match Persistence & Replay Module | • Track live session and persistent user scores.<br>• Serialize timestamp, mode, result, and move list to `matches.json`.<br>• Build the 1-second delay step-by-step match replay. | **6.0 hrs** |
| **Day 5**<br>Fri, Nov 27 | • Enhancement Module<br>• Final Testing & QA | • Polish console colors (`X` vs `O`), borders, and clean screen clears.<br>• Test edge cases (invalid keys, empty JSON files, quit confirmation). | **5.0 hrs** |

---

## 3. Visual Timeline (Gantt Chart)

```mermaid
gantt
    title C# Console Tic Tac Toe (Nov 23 – Nov 27)
    dateFormat YYYY-MM-DD
    axisFormat %a %b %d
    tickInterval 1day

    section Phase 1: Setup
    Auth & Main Menu          :done, d1, 2026-11-23, 1d

    section Phase 2: Core Game
    Board, Logic & Controller :active, d2, 2026-11-24, 1d
    AI & Manual Modes         :d3, 2026-11-25, 1d

    section Phase 3: Features & UI
    Scoreboard, History & Replay :d4, 2026-11-26, 1d
    UI Polish & Testing       :d5, 2026-11-27, 1d
```
# Stage 2: Defining Requirements (SRS)

## 2.1 Purpose
The Software Requirements Specification (SRS) fully describes the behavior of the web-based Tic-Tac-Toe application. It serves as the primary agreement between the developer and the stakeholders (users/instructors).

## 2.2 Functional Requirements (FR)
These are the specific behaviors the system must perform.

* **FR-01 (Game Initialization):** Upon loading the URL, the system must display an empty 3x3 grid and indicate that it is "Player X's" turn.
* **FR-02 (Move Execution):** When a player clicks an empty cell:
    * The cell must fill with the current player's symbol (X or O).
    * The system must lock that cell to prevent overwriting.
* **FR-03 (Turn Switching):** After a valid move, the system must automatically switch the active player from X to O (or vice versa) and update the status display.
* **FR-04 (Win Detection):** The system must check for a winning condition after every move. A win is defined as 3 matching symbols in:
    * Any horizontal row.
    * Any vertical column.
    * Either diagonal.
* **FR-05 (Draw Detection):** If all 9 cells are filled and no winner is detected, the system must declare a "Draw."
* **FR-06 (Game Termination):** Once a Win or Draw occurs, the board must freeze (no further moves allowed) until reset.
* **FR-07 (Reset Function):** A "Restart" button must be available to clear the board and reset the game state to "Player X's turn" without reloading the browser page.

## 2.3 Technical Requirements (TR)
These describe the constraints under which the system must operate.

* **TR-01 (Client-Side Logic):** All game logic (win checking, state management) must be executed in the user's browser using Vanilla JavaScript (ES6).
* **TR-02 (Performance):** The game must react to user clicks immediately (under 100ms latency).
* **TR-03 (Compatibility):** The application must render correctly on all modern standard browsers (Chrome, Firefox, Edge, Safari).
* **TR-04 (Zero Dependencies):** No external libraries (like React, jQuery, or Bootstrap) shall be used; only native HTML/CSS/JS.

## 2.4 User Interface (UI) Requirements
* **UI-01:** The grid should be centered on the screen.
* **UI-02:** X and O symbols must be visually distinct (e.g., different colors or distinct fonts).
* **UI-03:** The "Current Player" status must be always visible at the top of the game area.
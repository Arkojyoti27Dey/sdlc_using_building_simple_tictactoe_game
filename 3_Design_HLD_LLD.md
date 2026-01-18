# Stage 3: Design Document (HLD & LLD)

## 3.1 High-Level Design (HLD)
### System Architecture
The application follows a **Monolithic Client-Side Architecture**.
* **Presentation Layer (HTML/CSS):** Handles the visual grid and user feedback (alerts, text updates).
* **Logic Layer (JavaScript):** Handles game state, event listeners, and win algorithms.
* **Data Layer (Memory):** Temporary in-browser RAM storage for the board state (no external database).

### User Interface (UI) Wireframe
A conceptual layout of the screen:
```text
+---------------------------------------+
|           TIC TAC TOE                 |  <-- Header (H1)
+---------------------------------------+
|         Status: Player X's Turn       |  <-- Status Display (div)
+---------------------------------------+
|                                       |
|      [   ]   [   ]   [   ]            |
|                                       |
|      [   ]   [   ]   [   ]            |  <-- 3x3 Grid (div container)
|                                       |
|      [   ]   [   ]   [   ]            |
|                                       |
+---------------------------------------+
|          [ Restart Game ]             |  <-- Reset Button
+---------------------------------------+

```

# Low-Level Design (LLD) & Logic Flow

## 1. Global State Variables
These variables store the current status of the game in the browser's memory.

| Variable Name | Type | Initial Value | Description |
| :--- | :--- | :--- | :--- |
| `gameState` | Array (Strings) | `["", "", "", "", "", "", "", "", ""]` | Stores the board state. Empty strings indicate free spots. |
| `currentPlayer` | String | `"X"` | Tracks whose turn it is ("X" or "O"). |
| `gameActive` | Boolean | `true` | Functions as a "kill switch" to stop clicks after a win. |
| `winningConditions` | Array (Arrays) | `[[0,1,2], [3,4,5], ...]` | A constant list of the 8 winning index combinations. |

---

## 2. Function Modules
The code will be modularized into specific functions to handle distinct tasks.

### `handleCellPlayed(clickedCell, clickedCellIndex)`
* **Purpose:** Updates the internal state and the UI when a valid cell is clicked.
* **Input:** The HTML element clicked, the Index number (0-8).
* **Logic:**
    1. Update `gameState[clickedCellIndex]` = `currentPlayer`.
    2. Update `clickedCell.innerHTML` = `currentPlayer`.

### `handlePlayerChange()`
* **Purpose:** Switches the turn.
* **Logic:**
    1. If `currentPlayer` is "X", set to "O". Else, set to "X".
    2. Update the status text on screen (e.g., "It's O's turn").

### `handleResultValidation()`
* **Purpose:** Checks the rule book to see if the game is over.
* **Logic:**
    1. Loop through `winningConditions`.
    2. Check if `gameState` indices match for any condition (e.g., `board[0] == board[1] == board[2]`).
    3. **If Match Found:** Set `gameActive` = `false`, announce Winner.
    4. **If No Match & Board Full:** Set `gameActive` = `false`, announce Draw.
    5. **Else:** Call `handlePlayerChange()` to continue game.

### `handleRestartGame()`
* **Purpose:** Resets everything to default.
* **Logic:**
    1. Set `gameActive` = `true`.
    2. Set `currentPlayer` = `"X"`.
    3. Clear `gameState` array.
    4. Clear all HTML cell contents.

---

## 3. Detailed Logic Flow (Step-by-Step)

This flow describes exactly what happens during a single user interaction (a click).

1.  **START**: User clicks a cell on the grid.
2.  **CHECK 1 (Validation)**:
    * *Is the clicked cell empty?* AND *Is `gameActive` true?*
    * **NO:** Stop immediately (ignore click).
    * **YES:** Proceed to Step 3.
3.  **UPDATE STATE**:
    * Write "X" or "O" into the `gameState` array.
    * Render the symbol on the visible HTML board.
4.  **CHECK 2 (Win Verification)**:
    * Scan the 8 winning combinations.
    * *Do we have a winner?*
        * **YES:**
            1. Display "Player X/O has won!"
            2. Set `gameActive` = `false`.
            3. **END**.
        * **NO:** Proceed to Step 5.
5.  **CHECK 3 (Draw Verification)**:
    * *Does the `gameState` array contain any empty strings?*
        * **NO (Board Full):**
            1. Display "Game ended in a draw!"
            2. Set `gameActive` = `false`.
            3. **END**.
        * **YES:** Proceed to Step 6.
6.  **SWITCH TURN**:
    * Swap `currentPlayer` (X ↔ O).
    * Update Status Message.
7.  **WAIT**: System waits for next click.
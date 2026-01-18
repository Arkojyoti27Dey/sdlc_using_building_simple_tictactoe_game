# Stage 4: Development & Implementation

## 4.1 Coding Standards
To ensure readability and maintainability, the following coding standards were strictly enforced during the development of the Tic-Tac-Toe web application.

### Naming Conventions
* **Variables:** `camelCase` was used for all JavaScript variables (e.g., `currentPlayer`, `gameState`).
* **Functions:** Verb-noun pairing in `camelCase` to describe actions (e.g., `handleCellClick`, `checkWinner`).
* **CSS Classes:** BEM-style (Block Element Modifier) naming for clarity (e.g., `.game--container`, `.game--status`).
* **Constants:** `UPPER_SNAKE_CASE` (implicit) or standard variables defined at the top of the scope for configuration.

### Formatting & Syntax
* **Indentation:** 4 spaces per indentation level for HTML/CSS/JS.
* **Semicolons:** Strictly used at the end of every JavaScript statement to prevent Automatic Semicolon Insertion (ASI) errors.
* **Comments:** Inline comments provided for complex logic (e.g., the win validation loop). Section headers used to separate global variables, logic, and event listeners.

## 4.2 Scalable Code Architecture
The code was designed to be modular and scalable, avoiding "spaghetti code."

* **Separation of Concerns:**
    * **HTML:** Strictly for structure (DOM elements).
    * **CSS:** Strictly for presentation (Visuals).
    * **JS:** Strictly for logic (State management).
* **Avoidance of "Magic Numbers":**
    * Instead of hardcoding winning combinations inside the loop, a constant `winningConditions` array was defined globally. This allows for easy modification (e.g., if we wanted to change to a 4x4 grid later).
* **DRY Principle (Don't Repeat Yourself):**
    * The `handlePlayerChange` function is reused for both normal turn switches and post-game resets, reducing code duplication.

## 4.3 Version Control Strategy
Given the project scope (Single Developer, Rapid Prototyping), a streamlined Version Control strategy was adopted.

* **Primary Repository:** GitHub (hosted publicly).
* **Branching Strategy:** Direct commits to `main` branch (due to solo developer status).
* **Deployment Trigger:** Code pushed to the `main` branch is automatically deployed to production via **GitHub Pages**.
* **File Management:**
    * `index.html`: Entry point.
    * `style.css`: Stylesheet.
    * `script.js`: Application logic.
    

## 4.4 Code Review Checklist
Before finalization, a Self-Review was conducted against the following checklist:

| Category | Item | Status |
| :--- | :--- | :--- |
| **Functionality** | Does the game stop after a win? | ✅ Pass |
| **Functionality** | Does the restart button clear the board *and* the internal array? | ✅ Pass |
| **Security** | Is `innerHTML` used safely (no user input injection possible)? | ✅ Pass |
| **Performance** | Are there any unnecessary loops or console logs left? | ✅ Pass |
| **Responsiveness** | Does the grid break on mobile screens (320px width)? | ✅ Pass |
| **Syntax** | Are all tags closed and variables declared with `const`/`let`? | ✅ Pass |
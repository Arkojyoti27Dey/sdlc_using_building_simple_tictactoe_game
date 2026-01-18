# Stage 5: Testing Phase

## 5.1 System Testing
**Objective:** Validate that the fully integrated system meets the Functional Requirements (FR) defined in the SRS (Stage 2).
**Scope:** End-to-end testing of the application flow (Launch -> Play -> Win/Draw -> Restart).

| Requirement ID | Description | Validation Method | Result |
| :--- | :--- | :--- | :--- |
| **FR-01** | Display empty 3x3 grid on load | Visual Inspection | ✅ Pass |
| **FR-03** | Auto-switch turns (X → O) | Gameplay Check | ✅ Pass |
| **FR-04** | Detect Winner (Rows/Cols/Diagonals) | Gameplay Check | ✅ Pass |
| **FR-05** | Detect Draw (Full board, no winner) | Gameplay Check | ✅ Pass |
| **TR-03** | Browser Compatibility | Tested on Chrome & Edge | ✅ Pass |

---

## 5.2 Manual Testing (Test Cases)
These tests were executed manually by the tester (Human) interacting with the UI.

| Test Case ID | Scenario | Steps to Reproduce | Expected Output | Actual Output | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-01** | **Valid Move** | 1. Launch Game<br>2. Click Top-Left Cell | Cell fills with 'X'. Status changes to "O's Turn". | As Expected | ✅ Pass |
| **TC-02** | **Occupied Cell** | 1. Click Top-Left (X)<br>2. Click Top-Left again | Nothing happens. Turn does not change. | As Expected | ✅ Pass |
| **TC-03** | **Win (Row)** | 1. X plays (0,0)<br>2. O plays (1,0)<br>3. X plays (0,1)<br>4. O plays (1,1)<br>5. X plays (0,2) | Game displays "Player X has won!" and board freezes. | As Expected | ✅ Pass |
| **TC-04** | **Restart** | 1. Finish a game<br>2. Click "Restart Game" | Board clears. Status resets to "X's Turn". | As Expected | ✅ Pass |

---

## 5.3 Automated Testing
**Objective:** Verify the core logic functions without UI interaction.
**Method:** Since no external framework (Jest/Mocha) is used, we utilize **Console-based Unit Testing**.

### The Test Script
The following script was run in the Browser Console to validate the `winningConditions` logic.

```javascript
// SIMULATION SCRIPT
function runAutoTest() {
    console.log("--- Starting Automated Logic Test ---");
    
    // Test 1: Simulate a Win
    gameState = ["X", "X", "X", "", "", "", "", "", ""]; // Force X win
    currentPlayer = "X";
    handleResultValidation();
    if (gameActive === false) {
        console.log("✅ Test 1 Passed: Win detected correctly.");
    } else {
        console.error("❌ Test 1 Failed: Win NOT detected.");
    }

    // Reset for next test
    handleRestartGame();

    // Test 2: Simulate a Draw
    gameState = ["X", "O", "X", "X", "O", "X", "O", "X", "O"]; // Full board, no win
    handleResultValidation();
    if (gameActive === false && document.querySelector('.game--status').innerHTML.includes("draw")) {
        console.log("✅ Test 2 Passed: Draw detected correctly.");
    } else {
        console.error("❌ Test 2 Failed: Draw logic error.");
    }
    
    // Cleanup
    handleRestartGame();
    console.log("--- Automated Testing Complete ---");
}

// Execution: runAutoTest()
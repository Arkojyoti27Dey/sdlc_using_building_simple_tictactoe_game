# Stage 6: Deployment & Maintenance

## 6.1 Release Planning
**Objective:** Prepare the software for public release (v1.0.0).

* **Version Control Tag:** `v1.0.0-alpha`
* **Release Notes:**
    * **Feature Set:** Standard 3x3 Grid, Local 2-Player Mode, Win/Draw Logic.
    * **Known Limitations:** No AI opponent, data is lost on page refresh.
    * **Target Platform:** Desktop and Mobile Web Browsers.

## 6.2 Deployment Automation
**Strategy:** We utilize **Continuous Deployment (CD)** via GitHub Pages.

* **Automation Workflow:**
    1.  **Trigger:** Developer pushes code to the `main` branch.
    2.  **Build:** GitHub Actions automatically detects the `index.html` file.
    3.  **Deploy:** The static site is built and hosted at `https://[username].github.io/[repo-name]`.
    4.  **Verification:** Changes go live within 60-120 seconds.

* **Environment:**
    * **Production:** The live URL accessible to users.
    * **Development:** The local machine (localhost) where coding happens.

## 6.3 Maintenance Plan
Software is never "finished," only abandoned or maintained. This project follows a **Corrective and Adaptive Maintenance** strategy.

### Types of Maintenance
1.  **Corrective (Bug Fixes):**
    * *Scenario:* A user finds that clicking a cell twice crashes the game.
    * *Action:* Create a "Hotfix" branch, repair code, merge to main.
2.  **Adaptive (New Features):**
    * *Scenario:* Users request a "Dark Mode."
    * *Action:* Add to the **Product Backlog** for v1.1.0.

### Maintenance Log (Sample)
| Date | Version | Type | Description |
| :--- | :--- | :--- | :--- |
| 2025-01-18 | v1.0.0 | Release | Initial public launch. |
| 2025-01-19 | v1.0.1 | Hotfix | Fixed mobile layout padding issue. |

## 6.4 Feedback Loop
**Objective:** Gather user input to drive future updates.

* **Collection Method:** GitHub Issues tab.
* **Triage Process:**
    1.  User reports a bug or suggests a feature.
    2.  Developer labels it (`bug`, `enhancement`, `wont-fix`).
    3.  High-priority bugs are scheduled for immediate maintenance.
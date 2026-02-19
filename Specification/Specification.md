# ATM-Employees Specification

This expanded specification details the "ATM-Employees". It bridges the gap between the aesthetic of a high-end fintech app and the functional requirements of corporate HR software.

## 1. Visual & Design System (The "Rocket Style")
To ensure the webapp feels like the uploaded images, the frontend must adhere to these specific UI tokens:
* **The "Vibe"**: Dark magenta-to-red gradients (`linear-gradient(135deg, #A31D58 0%, #E32636 100%)`) for headers and primary action buttons.
* **Card Architecture**: White cards with `border-radius: 24px` and a very soft box-shadow: `0 4px 20px rgba(0,0,0,0.05)`.
* **Typography**: Primary font is Inter or Circular Std. Headlines are bold (700 wt), while secondary data is light grey (#727272).
* **Micro-Interactions**: When a user clicks "Add Leave," the button should have a slight haptic-style scale-down effect.

## 2. Detailed User Roles & Capabilities

### Role A: Worker (The Base User)
* **Dashboard**: View personal "Leave Donut" (Days used vs. Total).
* **History**: Scrollable list of past absences with status badges (Pending, Approved, Rejected).
* **Action**: Submit a leave request via a 3-step wizard.
* **Constraint**: Cannot see other workers' data.

### Role B: Team Manager (The Filter)
* **Dashboard**: Dual view—Personal leave stats + "Team at a Glance" (who is out today).
* **Approval Hub**: A "Pending Action" queue.
* **Action**: "Verify & Forward." Clicking this sends the request to the Director.
* **Self-Leave**: Submits a request that bypasses the manager level and goes straight to the Director.

### Role C: Director (The Authority)
* **Final Approval**: Receives "Verified" requests from Team Managers. Can "Final Approve" or "Reject with Comment."
* **Global View**: View a heatmap of company-wide absences.
* **Self-Leave**: Submits a request which is Auto-Approved and logged instantly.

### Role D: HR Management (The Architect)
* **Worker DB**: Create/Edit/Delete employee profiles.
* **Role Management**: A toggle-based interface to switch a user from "Worker" to "Team Manager."
* **Policy Control**: Set the annual leave quota (e.g., 20 days or 26 days) globally or per individual.
* **Reporting**: Generate the "Attendance Report" (PDF/Excel) for payroll.

## 3. Screen-by-Screen Functional Specs

### 3.1 The "Balance" Dashboard (Home)
* **The Donut**: Large circular progress bar (top center). Inside the ring, it shows the number of remaining days (e.g., 14 Days Remaining).
* **Target Date**: Just like the "Nov 6, 2025" date in your image, this shows the "Reset Date" for the next year's leave quota.
* **Quick Actions**: Two pill-shaped buttons: [Request Leave] (Black) and [View Calendar] (White with border).

### 3.2 The Leave Request Form (Step-by-Step)
* **Type Selection**: Large icons for "Vacation 🌴", "Sick Leave 🤒", "Work from Home 🏠".
* **Date Picker**: A custom calendar interface where the user selects a range.
* **Summary**: A final card showing "Total: 5 Working Days."
* **Submission**: A "Syncing" animation appears once submitted, mimicking the Rocket Money data refresh.

### 3.3 The "Recurring" Absence Feed (Managers/HR)
* **Section - "Out This Week"**: Uses the calendar-strip view (Sun-Sat) from your second image. Days where someone is absent are highlighted with a blue circle.
* **Section - "Coming Later"**: Card list showing the employee's name, their avatar, and the date they are leaving (e.g., "John Doe - in 12 days").

## 4. The Approval Logic Workflow (State Machine)

| Request Origin | Level 1 (Manager) | Level 2 (Director) | Final State |
| :--- | :--- | :--- | :--- |
| Worker | Must "Verify" | Must "Final Approve" | Approved |
| Team Manager | N/A (Skips) | Must "Final Approve" | Approved |
| Director | N/A (Skips) | N/A (Skips) | Auto-Approved |
| HR | N/A (Skips) | N/A (Skips) | Auto-Approved |

## 5. Attendance Report Generation (HR Only)
The report module will use the "Spending" graph style from your images:
* **X-Axis**: Months of the year.
* **Y-Axis**: Total Man-Hours lost to absence.
* **Comparison**: A small green/red indicator: "12% less absence than last month."
* **Export**: A "Download PDF" button that generates a branded document with the company logo.

## 6. Technical Stack Recommendation
* **Frontend**: React.js or Vue.js (for the smooth transitions).
* **Styling**: Tailwind CSS (to easily handle the gradients and 24px rounding).
* **Backend**: Node.js with a PostgreSQL database to manage the complex relational links between Workers, Managers, and Directors.
* **Charts**: Chart.js or Framer Motion for the circular progress animations.

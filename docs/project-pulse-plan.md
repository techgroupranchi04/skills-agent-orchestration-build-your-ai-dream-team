# Project Pulse Dashboard Implementation Plan

## Summary

**Project Pulse** is a web-based project management dashboard that displays project cards with status, priority, and metadata in a polished, responsive interface. The dashboard is built with vanilla HTML/CSS/JavaScript and runs in VS Code's Live Server environment.

**Build strategy**: Create the data contract first (JSON), then build the HTML structure and data-binding logic, apply responsive styling in parallel, and finalize the VS Code launch configuration.

---

## Ordered implementation steps

1. **Step 1 (Coder)**: Create `app/project-data.json`
   - Defines project data structure and sample data
   - Establishes the data contract for the HTML logic
   - Must complete before HTML structure can be built

2. **Step 2 (Coder)**: Build `app/index.html`
   - Create dashboard HTML structure
   - Implement data binding and project card rendering
   - Add viewport meta tag and accessibility attributes
   - Depends on: Step 1 (project-data.json structure known)

3. **Step 3 (Designer)**: Build `app/styles.css`
   - Apply responsive styling to project cards
   - Implement mobile-first approach
   - Create visual affordances (shadows, spacing, typography)
   - **Can run in parallel with Step 2** (no file conflicts)

4. **Step 4 (Coder)**: Create `.vscode/launch.json`
   - Configure VS Code launch for the runnable app
   - Set working directory to `${workspaceFolder}/app`
   - Open `index.html` on launch
   - Depends on: Steps 2 & 3 (app files must exist)

---

## File assignments

### `app/project-data.json`
- **Owner**: Coder
- **Scope**: Data structure only; includes 3-5 sample projects with properties: id, name, status (active/completed/paused), priority (high/medium/low), description, dueDate, teamSize
- **No dependencies**

### `app/index.html`
- **Owner**: Coder
- **Scope**: Complete HTML structure, viewport meta tag, script to load and render project-data.json, project card DOM generation, accessibility attributes
- **Depends on**: app/project-data.json structure
- **CSS classes used**: `.dashboard`, `.project-card`, `.project-status`, `.project-priority`, `.project-meta`

### `app/styles.css`
- **Owner**: Designer
- **Scope**: Styling only; no HTML or logic changes
- **Responsive breakpoints**: 375px (mobile), 768px (tablet), 1024px+ (desktop)
- **Target classes**: `.dashboard`, `.project-card`, `.project-status`, `.project-priority`, `.project-meta`
- **Visual goals**: Polished appearance with rounded corners, shadows, clear typography, status badges, priority indicators
- **No dependencies on other steps** (can begin as soon as HTML class structure is known)

### `.vscode/launch.json`
- **Owner**: Coder
- **Scope**: VS Code launch configuration only
- **Working directory**: `${workspaceFolder}/app`
- **Browser**: Open `index.html` on launch
- **Configuration name**: "Open Project Pulse"
- **Depends on**: Steps 2 & 3 (app files must exist and be ready to display)

---

## Designer responsibilities

- Create responsive, polished styling for the Project Pulse dashboard
- Implement mobile-first CSS with clear breakpoints
- Style project cards with visual hierarchy: status badges, priority indicators, readable spacing
- Ensure accessibility: sufficient color contrast, readable fonts, clear visual affordances
- Apply CSS to deterministic class hooks (`.dashboard`, `.project-card`, etc.)
- Test responsiveness at 375px, 768px, and 1024px+ viewports
- Report design decisions, CSS organization, and validation approach

---

## Coder responsibilities

- Create `app/project-data.json` with realistic sample data (3-5 projects, varied statuses and priorities)
- Build `app/index.html` with:
  - Viewport meta tag for responsive design
  - Script to fetch and parse `project-data.json`
  - DOM logic to render project cards dynamically
  - Semantic HTML with accessibility attributes
  - CSS class names matching Designer's expectations
- Create `.vscode/launch.json` with:
  - Strict JSON formatting (no comments)
  - Working directory set to `${workspaceFolder}/app`
  - Launch configuration that opens `index.html`
  - Port and browser settings appropriate for Live Server
- Validate all files before completion; test that the dashboard renders with data

---

## Dependencies

| Step | Depends on | Reason |
|------|-----------|--------|
| Step 2 (HTML) | Step 1 (JSON) | HTML must know the project data structure to bind correctly |
| Step 4 (launch.json) | Steps 2 & 3 | App files must exist and be styled before launch configuration is created |

---

## Parallel work

**Phase 1** (Sequential):
- Step 1 only (creates data contract)

**Phase 2** (Parallel):
- Step 2 (Coder builds HTML) and Step 3 (Designer builds CSS) **can run simultaneously**
  - No file conflicts (HTML and CSS are independent files)
  - Designer can infer CSS class structure from HTML scaffold or prior design agreement
  - HTML logic doesn't depend on CSS

**Phase 3** (Sequential):
- Step 4 only (after Steps 2 & 3 complete)

---

## Edge cases and risks

1. **Browser compatibility**: Ensure JSON parsing and DOM methods work in Chrome, Firefox, Safari, and Edge. Use vanilla JavaScript (no dependencies).

2. **JSON parsing errors**: If `project-data.json` is malformed, the HTML script will fail silently. Add error handling and fallback data.

3. **CORS/file access**: When opening `index.html` locally, fetch may be blocked. Use a local server (Live Server) to mitigate.

4. **CSS class naming conflicts**: If `.project-card`, `.project-status`, etc. already exist in the codebase, there may be style conflicts. Use a CSS namespace if necessary (e.g., `.pulse-project-card`).

5. **Responsive design testing**: CSS may look good at one breakpoint but break at others. Test at multiple viewport sizes before completing Step 3.

6. **Unrealistic sample data**: If sample projects are too minimal (empty descriptions, same priority), the dashboard won't showcase the full design. Use varied, realistic data.

7. **Port conflicts**: `.vscode/launch.json` may specify a port (e.g., 5500 for Live Server) that's already in use. Ensure the Coder documents the port and handles conflicts.

8. **Viewport meta tag missing**: Without `<meta name="viewport" content="width=device-width, initial-scale=1.0">`, mobile responsiveness won't work. Ensure Coder includes this in Step 2.

---

## Validation expectations

The Orchestrator should verify:

1. **`app/project-data.json` is valid JSON**
   - Parse without errors
   - Contains 3-5 projects with required fields (id, name, status, priority, description, dueDate, teamSize)

2. **`app/index.html` renders the dashboard**
   - Open `index.html` in a browser; verify project cards appear
   - Check that all projects from `project-data.json` are displayed
   - Verify CSS classes (`.dashboard`, `.project-card`, etc.) are present
   - Check viewport meta tag is present

3. **`app/styles.css` applies polished styling**
   - Resize browser to 375px, 768px, 1024px+ viewports
   - Verify cards stack vertically on mobile, grid or flex layout on tablet/desktop
   - Check that status and priority badges are visibly styled and differentiated
   - Verify shadows, rounded corners, and spacing are consistent
   - Confirm text is readable at all breakpoints (no overflow, clear contrast)

4. **`.vscode/launch.json` is valid JSON and launches correctly**
   - Verify file is strict JSON (no comments)
   - Working directory is `${workspaceFolder}/app`
   - Launch configuration name is clear (e.g., "Open Project Pulse")
   - Test that clicking "Run" or "F5" in VS Code opens the dashboard in a browser

5. **Integrated dashboard behavior**
   - Dashboard loads without console errors
   - All projects render with correct data
   - Layout is responsive and polished
   - No style conflicts or missing classes
   - Launch configuration works end-to-end in Codespace

---

## Open questions (with reasonable assumptions)

1. **Project card details**: What information should each card show (title, status, priority, description, team size, due date)?
   - *Assumption*: Show name, status badge, priority badge, description snippet, team size, and due date.

2. **Status values**: What are the possible project statuses?
   - *Assumption*: "active", "completed", "paused" (expandable if needed).

3. **Priority levels**: How many priority levels and what are they?
   - *Assumption*: "high", "medium", "low" with distinct visual treatment.

4. **Grid layout**: How many cards per row?
   - *Assumption*: Mobile 1, tablet 2, desktop 3+ (responsive grid using CSS flexbox or CSS Grid).

5. **Color scheme**: Should Project Pulse follow a specific brand or theme?
   - *Assumption*: Use neutral, professional colors (grays, blues) with status/priority-based badges for differentiation.

6. **Sample data count**: How many projects should be in `project-data.json`?
   - *Assumption*: 3-5 projects to showcase variety without overwhelming the page.

7. **Live Server port**: What port should the VS Code launch configuration use?
   - *Assumption*: Port 5500 (standard Live Server default); Coder to document any conflicts.

---

## Next steps for Orchestrator

1. Review this plan with Designer and Coder.
2. Assign **Step 1** (Coder) to begin data structure.
3. Once Step 1 completes, run **Steps 2 & 3 in parallel** (Coder and Designer).
4. After Steps 2 & 3 complete, run **Step 4** (Coder).
5. Validate using the criteria above.
6. Report to the learner when Project Pulse is complete and runnable.

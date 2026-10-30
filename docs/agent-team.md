# Agent team

For Mona's Project Pulse dashboard, I will use a small custom agent team defined under the repository's `.github/agents` folder and orchestrated through GitHub Copilot CLI inside a Codespace.

## Custom team

- **Orchestrator** — Model: Claude Opus 5.5 (copilot). This agent coordinates work by breaking down complex requests into tasks and delegating to specialists. It orchestrates phases, ensures no file-scope conflicts, verifies integrated results, and reports outcomes. Tools: read, agent, memory. Definition: `.github/agents/orchestrator.agent.md`.

- **Planner** — Model: Claude Opus 5.5 (copilot). This agent researches the codebase, dependencies, and edge cases to produce practical implementation plans. It identifies file assignments, dependencies, parallel work opportunities, and validation expectations. Tools: read, search, web, memory, todo. Definition: `.github/agents/planner.agent.md`.

- **Designer** — Model: Gemini 3.7 Flash (copilot). This agent handles UI/UX, accessibility, information hierarchy, interaction flow, and visual design. It creates polished dashboards with responsive layouts, deterministic CSS hooks, and visual affordances. Tools: read, edit, search, web, memory, todo. Definition: `.github/agents/designer.agent.md`.

- **Coder** — Model: GPT-5.5 (copilot). This agent writes and fixes code within assigned file scope, follows repository patterns, keeps behavior deterministic and testable, and creates support files like `.vscode/launch.json` when needed for runnable apps. Tools: read, edit, search, execute, web, memory, todo. Definition: `.github/agents/coder.agent.md`.

## How we will work

The Orchestrator coordinates the team in phases. It runs the Planner first to get a strategy, then assigns parallel or sequential tasks to the Designer and Coder with explicit file scopes to prevent conflicts. Work runs in parallel only when file scopes don't overlap and have no data dependencies. The Orchestrator verifies integrated results and surfaces blockers instead of hiding them. Git control remains with the learner—agents don't stage, commit, or push changes.
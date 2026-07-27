# Ultimate Dashboard - AI Agent Rules & Workflow

## Project Context

We are working on the "ultimate-dashboard" WordPress plugin located in `wp-content/plugins/ultimate-dashboard`. We also call this plugin "Ultimate Dashboard" or "UDB".

## Directory Structure

The `ai-docs/ultimate-dashboard/{developer}/` directory contains documentation to facilitate context handoffs between AI agents.
**Note:** `{developer}` corresponds to the current developer's name (e.g., `bagus`, `dwi`, `david`).

- `progress-handoffs/`: Contains project handoff files.
  - `PROGRESS_HANDOFF.md`: The **current** handoff file. This is the source of truth for the next agent.
  - `PROGRESS_HANDOFF_vx.x.x+y_COMPLETE.md`: Archived handoff files for previously completed milestones.
- `prompts/`: Contains prompts used for agents.
  - `AGENT_PROMPT.md`: The prompt for the current session.
  - `AGENT_PROMPT_vx.x.x+y.md`: Archived prompts.
- `rules.md`: This file. Contains specific rules and workflows for this project.

## Workflow for AI Agents

### 1. Initialization (Start of Session)

- **Read Context**: Always check `ai-docs/ultimate-dashboard/{developer}/progress-handoffs/PROGRESS_HANDOFF.md` to understand the current status, recent changes, and immediate next steps.
- **Check Rules**: Review this `rules.md` file for project-specific guidelines.
- **Global Rules**: Ensure you follow the global rules defined in `.windsurfrules` in the project root.

### 2. During Work

- **Focus**: Execute the tasks as defined in the user request and the handoff file.
- **Documentation**: Keep track of what has been done, what files were modified, and any important decisions made.

### 3. Handoff (End of Session)

> **IMPORTANT**: **DO NOT EVER execute the handoff process unless explicitly requested by the user.** AI agents must never perform handoff operations (updating handoff files, archiving prompts, etc.) automatically at the end of a task or session unless the user explicitly instructs to do so.

- **1. Update Handoff File**:
  - Update `ai-docs/ultimate-dashboard/{developer}/progress-handoffs/PROGRESS_HANDOFF.md`.
  - **Status**: Mark as `Completed` (for this session).
  - **Accomplishments**: List what YOU did.
  - **Next Steps**: List what the NEXT agent should do.
- **2. Archive Handoff**:
  - Read the `Current Session` version from the file (e.g., `v2.11.8+1`).
  - Save a copy as `progress-handoffs/PROGRESS_HANDOFF_{version}_COMPLETE.md`.
- **3. Renew Handoff**:
  - Update `PROGRESS_HANDOFF.md` to prepare for the _next_ session.
  - **Status**: Set to `Active`.
  - **Current Session**: Increment the version (e.g., `v2.11.8+1` -> `v2.11.8+2`).
  - **Content**: Clear "Recent Accomplishments" and move "Next Steps" to "Pending Tasks".
- **4. Archive Prompt**:
  - Archive the current `prompts/AGENT_PROMPT.md` to `prompts/AGENT_PROMPT_{version}.md`.
- **5. Renew Prompt**:
  - **Update** `prompts/AGENT_PROMPT.md` with the **Objective** and **Instructions** for the _next_ session (based on your "Next Steps").
- **6. Suggest What are Next For Next Agent's Works**
- **7. Show the copy-able prompt for the next agent** with following wording: "Please execute the instructions in: ai-docs/ultimate-dashboard/{developer}/prompts/AGENT_PROMPT.md".

### 4. Commit Changes to Git

- **Commit Changes in ai-docs**: If there are changes in ai-docs, commit them to git.
- **Commit Changes in ultimate-dashboard**: If there are changes in wp-content/plugins/ultimate-dashboard, commit them to git.
- **Git commit rules**: Commit message should be fewer than 50 characters and does not contain version numbering. Commit description can contain more detailed explanations.

## General Project Guidelines

- **Code Style**: Follow the existing coding standards of the project.
- **File Structure**: Maintain the existing directory structure unless explicitly instructed to refactor.
- **Building**:
  - Build scripts should be executed from within `wp-content/plugins/ultimate-dashboard`.
  - To build login customizer JS assets, run `pnpm build-login-customizer`.
  - To build plugin onboarding JS assets, run `pnpm build-plugin-onboarding`.
  - To build onboarding wizard JS assets, run `pnpm build-onboarding-wizard`.
  - Use `pnpm watch-login-customizer`, `pnpm watch-plugin-onboarding`, or `pnpm watch-onboarding-wizard` during active development on those modules.


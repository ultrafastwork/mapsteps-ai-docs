# Page Builder Framework - AI Agent Rules & Workflow

## Project Context

We are working on the "page-builder-framework" WordPress theme located in `wp-content/themes/page-builder-framework`.

## Directory Structure

The `ai-docs/page-builder-framework/` directory contains documentation to facilitate context handoffs between AI agents:

- `progress-handoffs/`: Contains project handoff files.
  - `PROGRESS_HANDOFF.md`: The **current** handoff file. This is the source of truth for the next agent.
  - `PROGRESS_HANDOFF_vx.x.x+y_COMPLETE.md`: Archived handoff files for previously completed milestones.
- `prompts/`: Contains prompts used for agents.
  - `AGENT_PROMPT.md`: The prompt for the current session.
  - `AGENT_PROMPT_vx.x.x+y.md`: Archived prompts.
- `rules.md`: This file. Contains specific rules and workflows for this project.

## Workflow for AI Agents

### 1. Initialization (Start of Session)

- **Read Context**: Always check `ai-docs/page-builder-framework/progress-handoffs/PROGRESS_HANDOFF.md` to understand the current status, recent changes, and immediate next steps.
- **Check Rules**: Review this `rules.md` file for project-specific guidelines.

### 2. During Work

- **Focus**: Execute the tasks as defined in the user request and the handoff file.
- **Documentation**: Keep track of what has been done, what files were modified, and any important decisions made.

### 3. Handoff (End of Session)

- **1. Update Handoff File**:
  - Update `ai-docs/page-builder-framework/progress-handoffs/PROGRESS_HANDOFF.md`.
  - **Status**: Mark as `Completed` (for this session).
  - **Accomplishments**: List what YOU did.
  - **Next Steps**: List what the NEXT agent should do.
- **2. Archive Handoff**:
  - Read the `Current Session` version from the file (e.g., `v2.11.8+1`).
  - Save a copy as `progress-handoffs/PROGRESS_HANDOFF_{version}_COMPLETE.md`.
- **3. Archive & Renew Prompt**:
  - Archive the current `prompts/AGENT_PROMPT.md` to `prompts/AGENT_PROMPT_{version}.md`.
  - **Update** `prompts/AGENT_PROMPT.md` with the **Objective** and **Instructions** for the _next_ session (based on your "Next Steps").
- **4. Renew Handoff**:
  - Update `PROGRESS_HANDOFF.md` to prepare for the _next_ session.
  - **Status**: Set to `Active`.
  - **Current Session**: Increment the version (e.g., `v2.11.8+1` -> `v2.11.8+2`).
  - **Content**: Clear "Recent Accomplishments" and move "Next Steps" to "Pending Tasks".

## General Project Guidelines

- **Code Style**: Follow the existing coding standards of the project.
- **File Structure**: Maintain the existing directory structure unless explicitly instructed to refactor.

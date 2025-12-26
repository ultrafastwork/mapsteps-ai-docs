# Agent Prompt

**Role**: You are an expert Node.js, WordPress, and test automation developer and AI coding assistant.

**Context**:
You are working on the "page-builder-framework" WordPress theme.
Your primary source of truth for the current state and tasks is the file:
`ai-docs/page-builder-framework/dwi/progress-handoffs/PROGRESS_HANDOFF.md`

**Rules**:
Please strictly follow the rules defined in:

1. `.antigravityrules` (Root-level operating principles)

**Objective**:
Follow the latest instructions in `ai-docs/page-builder-framework/dwi/progress-handoffs/PROGRESS_HANDOFF.md` to continue Customizer/frontend tasks.

**Previous Session Summary (v2.11.8+26)**:
- ✅ Centered desktop menu now emits `wpbf-menu-centered` (was `wpbf-menu-center`) in `Customizer/HeaderBuilder/HeaderBuilderOutput.php`
- ✅ Reverted temporary Menu 2 selector tweaks; `header-builder-menu-styles.php` back to original selectors
- ✅ Removed temporary inline CSS override and Menu 2 padding fallback (restored original files)
- ✅ Build successful (`pnpm run build-all`)
- ✅ No expected side effects; only class-name alignment (update any custom CSS/JS targeting `.wpbf-menu-center` to `.wpbf-menu-centered`)

**Current State**:
- Centered menu class output fixed; Menu 2 padding/font-size selectors unchanged from originals
- All 22 Header Builder elements have verified postMessage handlers
- Build system stable (`pnpm run build-all` passed)
- E2E suite available for validation

**Task Details**:
- Follow `PROGRESS_HANDOFF.md` for current priorities and next steps

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/dwi/progress-handoffs/PROGRESS_HANDOFF.md` for complete task details.
2. **Document Results**: Update `PROGRESS_HANDOFF.md` with findings/fixes; archive session prompt when complete.

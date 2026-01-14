# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Add Widget Title field to Footer Builder widgets.

**Status**: Session v2.11.8+62 - Ready to start.

---

## Pending Tasks (v2.11.8+62)

- **Add Widget Title Field to Footer Builder Widgets**:
  - The user has attached a screenshot of the footer from https://portraitmode.io showing section/widget titles above footer widgets (e.g., "Links", "Other", "Subscribe").
  - **Screenshot reference**: See `ai-docs/page-builder-framework/bagus/prompts/footer-widget-title-reference.png`
  - Add a "Widget Title" text field to the following Footer Builder widgets:
    - Menu 1 (desktop and mobile)
    - Menu 2 (desktop and mobile)
    - HTML 1 (desktop and mobile)
    - HTML 2 (desktop and mobile)
  - **Implementation Requirements**:
    - Add customizer field for title text input
    - Update widget output in `FooterBuilderOutput.php` to render the title
    - Add CSS styles for the widget title. Maybe in `wp-content\themes\page-builder-framework\inc\customizer\styles\footer-builder-styles.php`. Also think about desktop vs mobile footer builder.
    - Add postMessage live preview support for instant title updates. Maybe in `wp-content\themes\page-builder-framework\inc\customizer\js\postmessage-parts\footer.ts` or `wp-content\themes\page-builder-framework\inc\customizer\js\postmessage-parts\footer-builder.ts`. Also think about the desktop vs mobile footer builder.
    - Please also check if wpbf-premium plugin also need the improvement related to this tasks.

---

## Recent Completed

- ✅ Footer Builder vertical alignment fix (v2.11.8+61)
- ✅ Footer Builder Menu widget styling - vertical layout (v2.11.8+61)
- ✅ Footer Builder Menu customizer fields - Item Spacing, Link Colors (v2.11.8+61)
- ✅ Footer Builder HTML Widget margin-bottom fix (v2.11.8+60)
- ✅ Footer Builder Social Icons spacing fix (v2.11.8+60)
- ✅ Footer Builder Copyright Widget Theme Author Instant Preview fix (v2.11.8+59)

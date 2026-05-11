# Project Rules

## Session Bootstrap                                                                                
                                                            
  Before writing any report script:
  1. Read `Competitive Analysis Newsela Prompt` in full
  2. Copy `generate_noredink_pdf.py` as your starting file
  3. Do not deviate from the section structure, helper signatures, or color palette
  4. Do not add additional content in order to add page count. If the report ends up being shorter, that is okay. 

## Research Discipline (NON-NEGOTIABLE)

These rules exist because past sessions produced reports with factual errors traceable to skipping screens and assuming features were absent. Follow them on every run.

- **Build a coverage checklist before clicking anywhere.** Enumerate every screen, dropdown, modal, settings panel, and primary workflow you plan to visit. Surface that checklist to the user so they can flag gaps. Check each item off only when you have actually verified it in the live app.
- **Complete every primary user workflow end-to-end.** For a teacher product that means assignment creation through Publish (every step, every field), the student-side experience (use "Preview as student" or equivalent — do not skip this), the full grading flow including AI feedback, and any analytics/reporting surfaces. Do not begin writing the report until every primary workflow has been walked.
- **Tag every claim VERIFIED or ASSUMED before drafting.** VERIFIED means you observed it directly in the app this session. ASSUMED means you inferred it from absence of contrary evidence, from a marketing page, or from a competitor's behavior. Surface the ASSUMED list to the user and resolve every item before writing.
- **Use AskUserQuestion liberally during research, not just at setup.** Any time you are tempted to assume — about scope, about a feature's behavior, about whether something exists — ask the user instead. Cheap to ask, expensive to be wrong.
- **Never make a "does not have X" claim without positive verification.** If you did not explicitly look for X and fail to find it, weaken the claim or omit it. The most common error mode is asserting absence from incomplete exploration.
- **Slow down at the verify-and-write boundary.** Re-read the draft report against your notes and the live app before declaring done. A regex audit of the generator script is not a substitute for a re-read against ground truth.

## Accessibility — WCAG 2.1 AA Color Contrast (NON-NEGOTIABLE)

All generated documents (PDFs, reports, HTML) MUST meet WCAG 2.1 AA minimum contrast ratios **before** writing or running any code. Do not produce a first draft and fix it after feedback.

### Rules

- **Normal text (< 18pt regular, < 14pt bold):** minimum 4.5:1 contrast ratio against its background.
- **Large text (≥ 18pt regular or ≥ 14pt bold):** minimum 3:1 contrast ratio against its background.
- **UI components / decorative elements:** 3:1 minimum.

### ReportLab-specific enforcement

- **Never put a `Paragraph` with a colored `textColor` style inside a table cell that relies on `TEXTCOLOR` in `TableStyle` to set the color.** `TableStyle TEXTCOLOR` only affects plain strings — it does NOT override a `Paragraph`'s own `textColor`. Always use a dedicated paragraph style with the correct `textColor` for table header and body cells.
- All table cells must be `Paragraph` objects (not plain strings) so text wraps and styles apply correctly.
- Define a `table_header_style` (white text) and `table_cell_style` (dark text) and use them consistently.

### Pre-approved palette (verified contrast ratios on white background)

| Color name    | Hex       | Contrast on white | Safe for         |
|---------------|-----------|-------------------|------------------|
| BRAND_BLUE    | #1E3A8A   | ~13:1             | All text sizes   |
| DARK_TEAL     | #0369A1   | ~7.2:1            | All text sizes   |
| LUNA_PURPLE   | #6D28D9   | ~7.6:1            | All text sizes   |
| DARK_GRAY     | #334155   | ~10.4:1           | All text sizes   |
| ACCENT_GREEN  | #065F46   | ~10.8:1           | All text sizes   |
| SLATE_600     | #475569   | ~7.2:1            | All text sizes   |
| BRAND_TEAL    | #0EA5E9   | ~3.3:1            | Decorative / backgrounds ONLY — never for body text |

### Checklist before generating any PDF

- [ ] Every text color + background combination has been verified against the ratios above
- [ ] No `Paragraph` object relies on a `TableStyle TEXTCOLOR` command to be readable
- [ ] All table cells use `Paragraph` objects, not plain strings

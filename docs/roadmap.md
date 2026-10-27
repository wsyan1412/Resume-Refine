# Delivery roadmap

The milestones describe deliverables and completion criteria, not fixed calendar estimates. Select an approach before estimating implementation effort. A single-job prototype is an intermediate milestone; the first useful release must also address the repeated multi-job workflow.

## 0. Select the product direction and establish GitHub

Deliverables:

- Choose web, extension-led, desktop, or personal workflow.
- Confirm whether the first audience is the creator, public portfolio visitors, or invited users.
- Reuse the existing private `wsyan1412/Resume-Refine` repository.
- Publish planning documents; create roadmap issues and estimate milestones after platform selection.
- Select implementation stack, AI provider, operating budget, and first supported job source.

Complete when the repository exists on the intended profile and its README accurately describes the project stage. Until connected publication is verified, do not claim GitHub setup is complete.

Suggested issue: `Choose the first-release platform and audience`.

## 1. Import once and create a verified profile

Deliverables:

- Pasted text, DOCX, and text-based PDF import.
- Section and bullet confirmation screen.
- User-editable master profile, source references, and immutable versions.
- Job paste and document import with an editable preview.

Acceptance criteria:

- Import fictional examples with columns, missing sections, and unusual date formats.
- An image-only PDF produces a clear fallback instead of a silently empty profile.
- Contact information, employment dates, titles, and degrees can be corrected and locked.
- Confirmed data survives reopening; another user's data is never accessible in a hosted setup.

Suggested issues:

- `Import resume text, DOCX, and selectable-text PDF`
- `Confirm extracted sections and save profile versions`
- `Import and confirm a job description`

## 2. Complete one trustworthy tailoring flow

Deliverables:

- Requirement-to-experience mapping and gap reporting.
- Structured rewrite suggestions with source references.
- Inline and side-by-side changes, individual accept/reject, direct editing, and undo.
- One clean resume template with PDF and DOCX export.

Acceptance criteria:

- A fictional job requiring an absent skill flags the gap without adding that skill.
- Attempts to invent metrics, change employers, or modify locked dates are rejected or sent back for review.
- Moved bullets appear as moves rather than unexplained deletions and additions.
- Rejecting a suggestion restores the previous text; regeneration preserves manual edits unless explicitly replaced.
- Exported PDF has selectable text; DOCX remains editable; both reflect the accepted content and contain no review markup.
- Visual export review covers long bullets, links, punctuation, page breaks, and overflowing content.

Suggested issues:

- `Generate source-linked suggestions and flag unsupported requirements`
- `Build review editor with word-level changes and undo`
- `Export clean PDF and editable DOCX from one document model`

## 3. Make repeated applications efficient

Deliverables:

- Import a supported public job URL with preview, plus immediate paste fallback.
- Add multiple jobs; detect duplicate entries.
- Background generation queue, per-job status, cancellation, bounded retries, and resume after interruption.
- Separate version history and exports for each company and role.
- Usage measurement and a batch spending limit.

Acceptance criteria:

- A 50-job synthetic batch keeps company names, requirements, and drafts isolated.
- One failed fetch or generation does not discard other results.
- Retrying a job does not duplicate an already completed draft.
- An expired URL retains the saved description used for that draft.
- An interrupted batch can resume without starting successful jobs again.
- Record a manual baseline and compare the time needed to produce 10 reviewed resumes with the tool. Treat time saved as measured evidence, not a marketing assumption.

Suggested issues:

- `Import supported public job URLs with a paste fallback`
- `Queue multiple jobs and isolate their drafts`
- `Retry, cancel, and resume jobs without duplicate work`
- `Record per-job usage and enforce batch caps`

## 4. Prepare a safe portfolio demonstration or invited beta

Deliverables:

- Fictional demo profile and job descriptions.
- Account isolation and private storage before hosting real resumes.
- Retention/deletion controls, safe URL fetching, input limits, and minimal content-free logs.
- Accessibility review for change indicators and keyboard editing.
- Screenshots, setup instructions, environment-variable template without secrets, and a concise architecture overview.
- Automated checks for the critical import, factual constraints, revision, queue, and export paths.

Complete when the end-to-end demo works, first-release criteria pass, and documentation clearly states supported inputs, supported job sites, and known limitations.

Suggested issue: `Prepare fictional demo and validate hosted privacy boundaries`.

## Later extensions, ranked after usage feedback

1. CSV import and bulk export of approved versions.
2. Browser extension for user-initiated job capture on supported sites.
3. OCR for scanned resumes and screenshot job descriptions.
4. Google Docs import/export and richer templates.
5. Desktop packaging or local-model mode if users need it.

Re-rank these using observed friction rather than implementing every integration at once.

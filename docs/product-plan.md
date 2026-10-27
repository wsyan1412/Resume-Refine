# Product proposal

Prepared 27 October 2026. This is a proposal, not a commitment to a platform or implementation stack.

## Purpose

Reduce the repeated work involved in tailoring resumes for 50 or more applications while keeping factual claims accurate and each result easy to review, edit, and export.

The central asset is a reusable, user-verified master profile. A resume is one presentation of that profile. Each job receives its own draft, derived from a recorded profile version and a saved job description. Do not repeatedly rewrite the previously tailored resume: this can gradually introduce drift and lose useful experience.

## Product approaches

| Approach | Advantages | Disadvantages | When to choose it |
| --- | --- | --- | --- |
| A. Responsive web application | No installation; roomy editor and comparison view; access across devices; straightforward portfolio demo | Requires hosting and protection of stored personal data; website access to some job pages will fail | Best overall starting point for a product that others can use |
| B. Browser extension with web editor | Capture a job while browsing; less switching between tabs; share the same profile and generation service | Browser permissions, distribution, site-specific maintenance, and site restrictions; a small popup is a poor document editor | Add after the web workflow proves useful, or prioritize if job capture is the dominant problem |
| C. Desktop application | Convenient local folders and exports; can store profiles locally; possible later local-model support | Installation, signing, updates, and operating-system support; local storage alone does not keep cloud AI requests on the device | Choose when local storage or offline operation is a primary requirement |
| D. Small personal workflow tool | Fastest route to testing the core idea; a local form or command-line tool can process a folder or job list | Less approachable for other users; weaker interactive review unless an editor is also built | Choose to solve the creator's own search first with limited development time |
| E. Native mobile application | Convenient camera upload and job saving on a phone | Precise resume editing and comparison are awkward on a small screen; separate platform effort | Consider later if actual users mostly work on phones |

Recommendation: A first, B later. A web application can eventually offer an installable shortcut, but that should not be presented as a promise of offline AI generation.

## Resume input

| Input | Priority | Behavior and limitations |
| --- | --- | --- |
| Pasted text | First release | Always-available fallback; show detected sections for confirmation |
| DOCX upload | First release | Import text and structure; do not assume arbitrary Word formatting can be preserved |
| Text-based PDF upload | First release | Extract selectable text; confirm reading order, especially with columns and tables |
| Manual profile entry and extra project notes | First release | Capture useful verified experience that did not fit on the original resume |
| Multiple resumes | Later improvement | Merge into the master profile with conflict and duplicate review; never silently combine conflicting facts |
| Scanned PDF, photo, or screenshot | Later improvement | OCR, meaning text recognition from images; flag uncertain text and require correction before generation |
| Google Docs / Drive | Later integration | Explicitly connect and select a document; use the same extraction-and-confirmation flow |
| Markdown, plain-text file, structured profile backup | Later convenience | Useful for technical users and moving data between installations |
| Applicant-provided LinkedIn export | Later convenience | Evaluate supported export formats; do not depend on scraping a LinkedIn profile URL |

Keep the original document available for reference. Import into a structured profile with stable section and bullet identifiers, then render tailored resumes using a small set of controlled templates.

First-release formatting promise: clean, predictable templates, not perfect reproduction of every uploaded design. Explain this before import. A future template-preservation feature is a separate problem.

## Job description input

| Input | Priority | Behavior and limitations |
| --- | --- | --- |
| Pasted description | First release | Reliable fallback; extract company, title, responsibilities, and requirements for confirmation |
| Public job URL | First release, supported sites only | Fetch a supported public page, show extracted text, and save its source URL and retrieval time |
| PDF or DOCX description | First release | Reuse document parsing; preview the extracted description |
| Several URLs or pasted descriptions | First release batch workflow | Give each job its own record; show duplicates and import failures individually |
| Manual role brief | First release | Company and title plus user-entered responsibilities when no full description exists |
| CSV import | Later improvement | Suggested columns: company, title, url, description; validate rows and deduplicate before queuing |
| Screenshot / image | Later improvement | OCR with confirmation; useful when copying text is difficult |
| Browser capture | Later extension | User-initiated capture on supported sites; present the captured description before saving |
| Recruiter email or share-to-app | Later integration | Start with pasted email text; direct inbox access adds permissions and scope |

Public URL extraction should try a documented job-board API where supported, then structured `JobPosting` data, then page text on supported sites. Some hiring systems expose public job data: Greenhouse documents unauthenticated GET access to its Job Board API. Google documents a `description` field within `JobPosting` structured data.

Do not promise that every hiring-site link works. Login requirements, unavailable pages, dynamic content, and source restrictions can make extraction fail. Offer pasted text or an uploaded description immediately. Save a snapshot so a disappearing listing does not erase the context for an application.

LinkedIn explicitly prohibits third-party scraping and certain automated activity. Exclude LinkedIn scraping from the proposed integrations. A browser permission is technical access, not permission from the source website to collect its content.

## Core workflow

### 1. Import and confirm once

Extract a resume into a master profile. Ask the user to correct uncertain sections, dates, employer names, and bullet associations. Add a library of verified achievements and projects. Allow locked facts and sections.

Every factual item should keep a source reference: original resume text, an imported document, or a later user-confirmed addition. A source link helps review but does not prove that an AI rewrite preserves the meaning; validation and user review remain necessary.

### 2. Add and inspect jobs

Accept one job or a batch. Show an editable description preview before generation. Distinguish must-have requirements from preferences, and identify which requirements have supporting experience. Missing requirements become gaps or questions; they must not become invented qualifications.

### 3. Generate separate suggestions

Select relevant existing experience, adjust emphasis, reorder sections or bullets, and propose clearer phrasing. Never invent achievements, metrics, technologies, years of experience, credentials, or duties. Keep employer names, actual titles, dates, and degrees fixed unless the user explicitly edits them.

Any new claim requires the user's confirmation and a source entry before it can be added to the master profile. User approval of one tailored draft does not silently change the master profile.

Start each generation from the chosen master profile version. Record that version and the job snapshot. Regenerating a section creates a new draft revision and must not overwrite manual edits without a choice.

### 4. Review changes

Provide both an inline changes view and a side-by-side comparison with the selected base resume.

- Mark additions, deletions, replacements, and moved content separately.
- Use labels, symbols, and strike-through as well as color for accessibility.
- For each suggestion, show the before text, proposed text, relevant job requirement, and supporting experience.
- Let the user accept or reject each suggestion or a selected group.
- Support undo, direct editing, saved revisions, and regeneration of a selected section.
- Keep a clean preview alongside the review mode.

Example: an existing bullet about implementing a REST API may be rephrased to emphasize backend development when relevant. It must not acquire a database, performance improvement, or leadership claim that the user never provided.

Distinguish wording changes from selection and ordering changes. Compare against the immutable imported resume or a named base version, not only against the last AI output. Preserve that baseline after manual edits.

### 5. Export and track

Export a clean PDF with selectable text and an editable DOCX from the same accepted document structure. Do not include highlights or review comments in the normal download. Offer a separate comparison export later.

Provide page-size, length, and spacing controls with overflow warnings. Start with one simple template. Test reading order and exports, but do not claim universal applicant-tracking-system acceptance or a guaranteed interview benefit.

Save filenames such as `Name_Company_Role_Resume_v2.pdf`. Keep the company, role, source link, draft state, export version, and optional application date together. Marking an application as submitted is a user action; this project does not submit applications in the first release.

## Handling 50 or more jobs

Batch support is part of the first useful release, after the single-job path works.

- Queue a list of jobs against one profile snapshot; keep each draft isolated.
- Show queued, generating, ready for review, failed, approved, and exported states.
- Limit concurrent generation, retry temporary failures, and allow cancellation or resumption.
- Make repeated actions safe so retrying does not create duplicate drafts or duplicate charges within the app's control.
- Estimate batch usage before starting once a provider and model have been measured; allow a user-set usage cap.
- Review and export per job; bulk generation does not imply bulk approval.
- Treat a changed source listing as a new snapshot, not a silent replacement of an existing draft's context.

## Architecture proposal

Use the same content and generation core regardless of whether the interface is web, extension, or desktop:

`Import -> Confirmed profile -> Saved job snapshot -> Suggested edits -> Reviewed document -> PDF / DOCX`

Conceptual records: `ProfileVersion`, `SourceItem`, `JobSnapshot`, `DraftRevision`, `ChangeSuggestion`, and `ExportRecord`.

For approach A, use a browser editor, a server-side generation service, a database for versions, private storage for originals and exports, and a bounded background queue for batches. Keep AI-provider credentials on the server. Select the exact framework, hosting service, and model after confirming budget, preferred language, and whether this serves one person or multiple users.

Use structured model output tied to source identifiers rather than asking for an opaque replacement document. Validate the schema, locked fields, numbers, and source references before presenting suggestions. These checks reduce errors; they cannot guarantee that every semantic distortion is detected.

## Privacy, reliability, and cost

Resumes contain personal information. Before a hosted beta, implement account isolation, private files, encrypted transport and storage, file-size/type limits, clear retention choices, and deletion. Explain which content is sent to the selected AI provider and its applicable retention settings. Do not claim local-only processing when using a remote model.

Keep document content out of routine logs and analytics. Keep real documents and keys out of GitHub even if the code is public. Use fictional people and jobs for demonstrations. Define how deletion applies to originals, derived drafts, exports, and backup expiry.

Treat resume text, job descriptions, and fetched pages as untrusted input, never as instructions that can override the tailoring rules. Restrict URL fetching to safe public destinations and re-check redirects; apply timeouts and download limits. Validate uploaded documents and sanitize exported content.

Reuse a parsed profile and extracted job snapshot rather than repeating work. Record generation usage by job. Prices cannot be estimated credibly until the model, prompt size, retry rate, OCR use, and hosting choice are known. Measure a 10-job pilot and extrapolate to 50 before promising a price.

## First-release boundaries

Include: reusable profile; text/PDF/DOCX import; supported job links and paste fallback; a per-job queue; grounded suggestions; visible changes; direct editing; clean PDF and DOCX export; saved versions.

Defer: automatic application submission, unrestricted site scraping, mobile-native apps, inbox integrations, cover letters, arbitrary template preservation, and unvalidated numerical "ATS scores."

## Sources checked

- [Greenhouse Job Board API](https://docs.greenhouse.io/job-board.html): public GET endpoints and job content.
- [Google JobPosting structured data](https://developers.google.com/search/docs/appearance/structured-data/job-posting): job-description metadata.
- [Chrome activeTab permission](https://developer.chrome.com/docs/extensions/develop/concepts/activeTab): temporary page access after user invocation for a possible later extension.
- [LinkedIn prohibited software and extensions](https://www.linkedin.com/help/linkedin/answer/a1341387/prohibition-of-scraping-software): integration constraint.

These sources support the integration facts. Product scope, priorities, and platform rankings above are design recommendations.

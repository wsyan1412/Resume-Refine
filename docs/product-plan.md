# Targeted product plan

Updated 28 October 2026. This supersedes the earlier platform comparison and persistent-master-profile proposal.

## Selected direction

Build a responsive website first, then a browser extension with the shared editor. Serve both a visitor tailoring one resume for one job and a visitor tailoring the same resume for many roles.

There is no registration, login, saved profile, resume database, or application history. A returning visitor uploads or pastes again. Within the open tab, one unchanged original can serve all jobs.

## Homepage: use the tool immediately

Put the form near the top, before long explanations. Use a short headline such as "Tailor your resume to the job" and a simple sequence: add resume, add job, review and download.

On desktop, show two cards side by side; stack them on mobile:

| Your resume | Job details |
| --- | --- |
| Upload PDF / DOCX or paste text | Paste a description or enter a supported job link |
| File name and short extraction preview | Company / role and short description preview |
| Inspect extracted text or replace file | Add another job as a secondary action |

One primary action: **Tailor my resume**. With several jobs, label it **Generate 3 resumes**, using the actual count.

Keep job-document upload available as a secondary input. Provide accessible labels and a file-picker alternative to drag-and-drop. Place examples and FAQs below the form.

A successful import should not force a profile-building wizard. Ask for correction when extraction is empty, reading order is uncertain, or section associations are unreliable. Show genuine processing stages rather than a fabricated percentage or a guaranteed completion time. Load heavy editor and export libraries only when needed.

Explain beside generation that the app does not save a resume history and selected text is sent for AI processing. The interface should not claim that cloud AI runs entirely on the user's device.

## Inputs and first-release scope

Resume: pasted text, selectable-text PDF, and DOCX. Read files in the browser and offer an extraction preview. Image-only PDFs get a clear paste fallback; OCR is deferred.

Job: paste first, followed by supported public links and PDF/DOCX input before the website beta is complete. Preview extracted descriptions and offer paste immediately when a link fails.

Start links with one documented public job-board source, such as Greenhouse. Restrict destinations and redirects and apply size/time limits. Do not forward browser credentials or include LinkedIn scraping. Universal job-site support and expensive browser rendering are outside the initial scope.

Use one clean output template. Importing content does not promise exact reproduction of arbitrary PDF/Word layouts.

## Single-job experience

1. Supply a resume and job description on the homepage.
2. Read and validate inputs; preserve the original in tab memory.
3. Generate structured suggestions for that role.
4. Show changes in the review editor.
5. Accept/reject suggestions, edit directly, and undo.
6. Preview and download clean PDF or editable DOCX.

A normal visitor needs no account, API key, dashboard, template-selection wizard, or permanent master profile.

## Multiple roles in the same session

**Add another job** expands a list within the same workflow. Give each role its own label, progress, suggestions, edits, and downloads.

Always start from the original resume, never from another role's generated version. Editing a result affects only that role. Replacing the original must clearly invalidate or separate earlier results.

Queue jobs in browser memory with one or two requests active initially. Allow per-job cancellation, explicit retries, and removal. One failure must not erase other results. Avoid unlimited automatic retries. A retry following an uncertain network result can create another provider charge because this design has no persisted server-side result cache.

Design the list for 50 jobs; validate smaller batches first. Completed jobs can be reviewed while others run. A rate-limit response should pause pending work and explain when it can retry. Set eventual limits using measured costs rather than silently limiting the product to one application.

Refreshing or closing the tab discards the workspace. There is no background completion after closing, saved queue, or cross-device recovery. Show a short session notice, an explicit **Clear session** action, and a leaving-page warning where supported. Downloaded files remain on the device.

Provide individual downloads first. ZIP export of selected reviewed results can follow after the website batch flow is reliable.

## Grounded generation

Represent the source as sections and blocks with stable identifiers. Keep factual text linked to its original blocks during the session. This is internal structure, not a saved user profile.

The AI may improve wording, select relevant experience, and propose ordering changes. Preserve actual employers, job titles, dates, credentials, metrics, and claims unless the user explicitly edits them. Missing qualifications become gaps or questions, not invented resume entries.

Request structured suggestions with source IDs. Validate response shape, references, locked fields, numbers, and size. Treat job and resume content as data, not instructions overriding these rules. Source links and schema checks help review but cannot guarantee semantic accuracy.

Keep contact fields local where reliably identified and restore them when rendering. Other text may still identify the applicant; do not describe this as complete anonymization.

## Changes and editing

Use side-by-side views on desktop and labeled tabs on mobile. Offer **Show changes / Clean preview**.

- Word-level additions/deletions, moved-block indicators, and labels beyond color alone.
- Accept/reject individual suggestions and a deliberate bulk action.
- Direct editing, undo, and section regeneration without silently replacing manual edits.
- An immutable original, plus separate attribution for AI suggestions and later manual edits.

Start with block/bullet-level accept/reject and word-level visual highlighting. A complete word-processor revision engine is outside the first iteration. Recompute stale suggestions after manual edits rather than applying outdated text positions.

## Downloads

Generate PDF and DOCX in the browser from the same reviewed content model. Normal downloads exclude change markup. Use company/role filenames.

Start with a single-column template, A4/Letter choice, spacing controls, and overflow feedback. Preview the actual PDF layout. PDF text must be selectable; DOCX must remain editable. Word pagination can differ even when content matches.

## Data lifecycle and anonymous operation

Keep source files, extracted text, jobs, and drafts in tab memory. Do not preserve documents in localStorage, IndexedDB, sessionStorage, cookies, server buckets, or a database. Use no-store headers for content and exclude bodies from logs/analytics.

The API handles the current request and returns its result. AI and hosting providers have their own processing/retention policies; verify and explain these before beta. Avoid "nothing is ever stored anywhere" claims.

Anonymous paid generation needs server-enforced size/token limits, throttling, a global budget ceiling, and a kill switch. A challenge can appear for suspicious traffic. Expiring operational counters may support these controls, but must contain no document content. CORS alone cannot control spending.

## Later extension

After testing the website, add user-initiated job capture on supported sites. Preview the capture, open the shared full-tab editor, supply a resume if needed for that active editor session, and use the same review/export workflow.

Bundle the editor as an extension page so capture can use validated extension messaging without server-side document storage. Establish the receiver before sending, keep the capture source until acknowledgement, and do not depend on a background service worker remaining alive.

Reuse document types, validation, editor components, imports/exports, and the generation API. Keep permissions minimal. Do not add automatic applications, unrestricted scraping, credential collection, or persistent resume storage. The website remains usable without an extension.

## Integration references

- [Greenhouse Job Board API](https://docs.greenhouse.io/job-board.html)
- [LinkedIn prohibited software](https://www.linkedin.com/help/linkedin/answer/a1341387/prohibition-of-scraping-software)
- [Chrome activeTab](https://developer.chrome.com/docs/extensions/develop/concepts/activeTab)
- [Chrome runtime messaging](https://developer.chrome.com/docs/extensions/reference/api/runtime)

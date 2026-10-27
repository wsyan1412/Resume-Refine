# Delivery roadmap

Updated 28 October 2026. Website first, shared-editor extension later. This remains a plan; implementation has not started.

## 1. Homepage and one-job interaction

Build responsive resume/job cards, a generation action, and a result area. Start with pasted text and fictional results to check the interaction before paying for AI.

Done when the sequence is understandable without signup or a profile wizard, mobile/keyboard use works, and errors are clear.

## 2. Complete one real resume

Add browser-side PDF/DOCX imports, extraction preview, structured AI suggestions, the changes editor, direct editing, undo, and clean PDF/DOCX exports. Use one template and tab-memory state.

Acceptance:
- Extraction preserves associations; uncertain reading order is visible.
- Image-only PDFs offer a paste fallback.
- A normal visitor needs no login or API key.
- Unsupported skills/metrics are flagged rather than added.
- Source IDs, locked fields, meaningful accept/reject, moved bullets, and manual edits work.
- Exports match accepted content, exclude review marks, and have readable page breaks.
- PDF text is selectable; DOCX is editable.

## 3. Multiple jobs within the open tab

Reuse one unchanged original across a list of roles. Add bounded concurrency, per-job states, cancellation, explicit retries, and independent review/downloads.

Acceptance:
- A synthetic 50-job run keeps companies, descriptions, edits, and results isolated.
- Failed jobs do not discard successful ones; duplicate clicks do not launch the same in-session job twice.
- Rate limits pause pending work with clear feedback.
- Every role starts from the original.
- Refresh returns to an empty workspace; no content is recovered from persistent storage.
- Closing the page does not promise later completion or recovery.

## 4. Website beta

Add an initial supported public job-link source and job PDF/DOCX imports. Validate privacy, anonymous operation, performance, exports, and real costs.

Acceptance:
- Supported links show previews; failures offer paste.
- Unsafe URLs/redirects are rejected; size/time limits apply.
- Keys stay out of client bundles and Git.
- No content enters persistent browser/server storage, app logs, or analytics.
- Provider handling/retention statements match actual settings.
- Server-side request/token limits, a global budget ceiling, and a kill switch work.
- Budget alerts are not described as hard caps; concurrency is accounted for.
- Measure latency and usage before publishing speed/cost claims.
- Public demos use fictional data.

ZIP downloads of reviewed results can follow the core batch flow.

## 5. Browser extension

Capture on user action, preview the job, and open the same editor packaged as a full-tab extension page.

Acceptance:
- Explicitly supported sites, minimal permissions, and validated messaging.
- Editor/document/export logic is reused.
- Sender and receiver handshake prevents silent capture loss when a background worker suspends.
- Resume upload is once per active editor session, without login or a persistent profile.
- The same generation limits apply.
- No automatic submissions or LinkedIn scraping.

## Verification and scheduling

Use Vitest for parsing, source mappings, validation, diffs, and queue transitions. Use Playwright for single/multi-job flows and accidental-persistence checks. Visually inspect exports, overflow, long bullets, links, and page breaks.

Estimate calendar time after a real import/generation/export spike. A UI mockup alone does not validate factual generation quality or export reliability.

# Decisions

Updated 28 October 2026.

## Confirmed by the user

| Area | Decision |
| --- | --- |
| Product | Responsive website first; browser extension with the shared editor later |
| Audience | One-time visitors and visitors applying to several roles |
| Homepage | Immediate, simple, visual resume/job input and generation |
| Login | No registration or login |
| Repeated use | Upload/paste once, reuse the same original across roles in the open session |
| Saving | No stored profiles, resume history, or cross-visit recovery |
| Results | Highlight changes, edit, and download |
| Cost | Minimize expenses and avoid recurring commitments where feasible |
| GitHub | Public repository, requested by the user and verified 28 October 2026 |

## Recommended, pending implementation

React + TypeScript + Vite + Tailwind CSS; React reducer/context in memory; Tiptap open-source core and custom jsdiff review UI; PDF.js/Mammoth imports; React PDF/docx exports; Hono on Cloudflare Workers; and a replaceable cloud AI adapter. Gemini 2.5 Flash-Lite is a price/quality evaluation candidate. WXT is recommended for the later extension.

No provider subscription, deployment, API integration, or application code has been created. No document database or upload bucket is planned. Expiring content-free operational counters may be needed for abuse/budget control.

## Consequences

- Repeat visits require another upload; refresh/close discards the session.
- No permanent master profile, saved application tracking, persistent generation queue, or cross-device sync.
- Cloud inference fits the quick first-visit experience but creates variable usage costs.
- No app-saved history does not remove third-party processing or retention.
- Anonymous public generation requires server-side cost/abuse controls.
- Public repository visibility does not select an open-source license.

## Open choices before implementation/beta

Validate the stack with an import/generation/export spike. Choose the model using factuality, source alignment, structured output, latency, current availability, and measured usage. Set a budget and anonymous limits. Choose the first supported job-link source. Verify provider handling/retention and select a repository license before inviting outside reuse.

Repository: [wsyan1412/Resume-Refine](https://github.com/wsyan1412/Resume-Refine). Keep real resumes and credentials outside Git.

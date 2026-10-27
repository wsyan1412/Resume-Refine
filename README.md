# Resume Refine

A responsive website for uploading one resume, tailoring it to one or several jobs, reviewing visible changes, and downloading the results.

**Status:** Targeted plan, updated 28 October 2026. The user selected the website first and a browser extension with the shared editor later. No application or paid service has been implemented.

**Repository:** [wsyan1412/Resume-Refine](https://github.com/wsyan1412/Resume-Refine) (public, verified 28 October 2026).

## Product direction

- Put resume input, job input, and a clear generation action on the homepage.
- Support a one-time visitor without registration or profile setup.
- Reuse one unchanged original resume for several roles during an open tab.
- Highlight changes, allow direct editing, and export clean PDF and editable DOCX.
- Keep working documents in tab memory; do not build login, saved profiles, a resume database, or application history.
- Add supported-site job capture through a browser extension later, reusing the editor and generation service.

Refreshing or closing the page discards the working session. Downloads remain on the user's device. Cloud AI sends selected text to a provider; no app-saved history is not a promise of zero third-party retention.

## Planning documents

- [Targeted product plan](docs/product-plan.md)
- [Recommended stack and cost assumptions](docs/tech-stack.md)
- [Delivery roadmap](docs/roadmap.md)
- [Confirmed decisions](docs/decisions.md)

## Recommended stack

React + TypeScript + Vite + Tailwind CSS, Tiptap's open-source editor with a custom changes interface, browser-side imports/exports, and a small Hono API on Cloudflare Workers. Evaluate a low-cost cloud model for the public website; requiring a local AI installation would add friction for one-time visitors.

These are implementation recommendations. No service has been purchased. Hosting should start within free allowances; cloud AI remains a variable usage expense.

## Repository boundaries

Commit source, plans, and fictional examples only. Keep real resumes, generated application files, and credentials outside Git. Review staged files even when a gitignore rule appears to cover them.

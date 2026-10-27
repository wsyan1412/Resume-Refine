# Recommended stack and costs

Prepared 28 October 2026 for the no-login website and later extension. No paid service has been activated.

## Stack

Use TypeScript throughout. A client-rendered app and a thin API fit an interactive document tool without accounts or stored documents. The recommendation keeps the editor reusable for an extension.

| Layer | Recommendation | Purpose |
| --- | --- | --- |
| Website | React + TypeScript + Vite | Responsive interface and static build |
| Styling | Tailwind CSS | Consistent layouts, typography, and responsive states |
| Session state | React useReducer + Context | Original, jobs, suggestions, edits, and queue in memory only |
| Content structure | Typed JSON blocks + Zod | Stable source IDs and validated API/document structures |
| Editor | Tiptap open-source core | Rich-text editing and undo |
| Change display | jsdiff, package diff | Word differences plus our own block-level accept/reject and move handling |
| PDF import | PDF.js / pdfjs-dist | Browser-side selectable-text extraction |
| DOCX import | Mammoth | Browser-side raw-text extraction; avoid unsanitized imported HTML |
| PDF export | @react-pdf/renderer | Local selectable-text PDF and actual-layout preview |
| DOCX export | docx | Local editable Word output from the same reviewed content |
| API | Hono + TypeScript | Validate, limit usage, call AI, fetch supported job sources |
| Hosting | Cloudflare Workers Static Assets + API routes | Start within free allowances using a provider subdomain |
| AI evaluation | Gemini 2.5 Flash-Lite paid API | Low-cost baseline candidate; provider/model remains replaceable |
| Checks | Vitest + Playwright | Critical logic and full user flows |
| Extension later | WXT + React + TypeScript | Supported-site capture and the shared full-tab editor |

The open-source Tiptap editor does not supply the complete custom review feature. Commercial tracked-changes, collaboration, and hosted export add-ons are outside this recommendation. Review installed dependency licenses and runtime compatibility when implementation starts.

## Data flow

Browser reads a file -> keeps original/blocks in memory -> sends the current text/job request to the API -> receives validated suggestions -> user reviews/edits -> browser generates downloads.

The original file need not enter server storage. Selected extracted text still goes through the API to the AI provider. Keep contact fields local when reliably identifiable; this is data minimization, not full anonymization.

Use no persistent storage for document state and no content in logs/analytics. Allow only expiring operational counters for throttling and budget enforcement. The API is stateless with respect to resume content; it may still need those counters.

## Fast first visit

Lazy-load the editor, parsers, and export tools. Use browser workers for heavy parsing where supported. Do not render a whole large PDF simply to read text.

Measure API CPU use. Workers Free currently allows 10 ms CPU per invocation, so expensive imports and rendering belong in the browser. Waiting for an external response and CPU computation are different resource measures. Upgrade only if measured limits require it.

Requiring local AI installation, a large model download, or the visitor's own API key would weaken the selected one-time experience. A cloud service is recommended for the public path. Keep a provider adapter so model quality and cost can be improved later.

## Extension reuse

Separate document types, validation, differences, and export adapters from website routing. Keep editor components portable. Add a workspace package split when the extension needs it rather than building elaborate infrastructure now.

WXT can package the shared editor as a full-tab extension page. Capture on user action, validate messaging senders, establish the receiver before transfer, and wait for acknowledgement. Do not send document content in URL query parameters or rely on a background worker staying alive indefinitely.

## AI evaluation and data handling

Benchmark fictional pairs for invented skills/metrics, locked-field changes, source alignment, structured output reliability, and latency. A low price is useful only if the edits stay faithful and reviewable.

Use a processing tier with appropriate handling for real resumes. Google's pricing page marks free-tier content as used to improve products and paid-tier content as not used for that purpose, subject to its terms. This does not establish zero retention; verify applicable policies before beta.

## Cost illustration

USD prices checked 28 October 2026. Estimates exclude development time, taxes, domains, new hardware, and unexpected traffic.

| Item | Initial target | Potential cost |
| --- | --- | --- |
| Software libraries | $0 mandatory subscriptions | Optional commercial services are outside this plan |
| Hosting | $0 within free allowances | Workers Paid starts at $5/month, plus applicable usage |
| Resume database / file storage | $0; not included | Saving history would change scope |
| Domain | $0 with provider subdomain | A custom domain normally renews periodically |
| AI | Variable usage | Longer requests, extra calls, retries, or a stronger model |

Gemini 2.5 Flash-Lite's listed standard paid text prices are $0.10 per million input tokens and $0.40 per million output tokens, including thinking output.

For illustration, assume 6,000 total input tokens and 4,000 total billed output tokens per tailoring request:
- Input: 6,000 / 1,000,000 x $0.10 = $0.0006.
- Output: 4,000 / 1,000,000 x $0.40 = $0.0016.
- One request: approximately $0.0022.
- Fifty requests: approximately $0.11.
- One thousand requests: approximately $2.20.

These are calculations, not measured usage or a model-quality guarantee. Additional normalization calls, retries, and more capable models increase costs. Start app batches as ordinary per-job requests; a provider's asynchronous Batch API does not automatically fit the session-only interactive design.

A $5-$10 testing budget can be an initial target after billing requirements are checked. Prepaid credit is not unlimited lifetime use. Avoid a fixed monthly AI subscription initially, while being explicit that usage spending remains.

## Public anonymous access and spending

Apply request, input/output, and concurrency limits before provider calls. Use suspicious-traffic challenges and an operator kill switch.

Distributed per-location throttles and billing alerts are not hard global spending caps. If a strict ceiling is promised, atomically reserve worst-case permitted cost before each request, account for concurrent calls/retries, and reject work when the allocation is exhausted. Store only minimal operational counters, not documents.

At the limit, stop new paid generations with clear feedback while preserving results already in the open tab. Do not promise unlimited anonymous usage.

## Primary references

- [Vite](https://vite.dev/guide/)
- [Cloudflare static assets](https://developers.cloudflare.com/workers/static-assets/)
- [Cloudflare pricing](https://developers.cloudflare.com/workers/platform/pricing/)
- [Hono on Workers](https://hono.dev/docs/getting-started/cloudflare-workers)
- [Tiptap open-source editor](https://github.com/ueberdosis/tiptap)
- [jsdiff](https://github.com/kpdecker/jsdiff)
- [PDF.js](https://mozilla.github.io/pdf.js/)
- [Mammoth](https://github.com/mwilliamson/mammoth.js)
- [React PDF](https://react-pdf.org/)
- [docx](https://github.com/dolanmiu/docx)
- [Gemini structured output](https://ai.google.dev/gemini-api/docs/structured-output)
- [Gemini prices and data-use distinction](https://ai.google.dev/gemini-api/docs/pricing)
- [Worker rate limits](https://developers.cloudflare.com/workers/runtime-apis/bindings/rate-limit/)
- [WXT](https://wxt.dev/guide/introduction.html)

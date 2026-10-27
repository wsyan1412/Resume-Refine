# Resume Refine

Planning-stage project for turning one verified career profile into editable, role-specific resumes with visible changes.

**Status:** Proposal only. No application, AI integration, or hosted service has been implemented. The product approach is awaiting selection.

**Repository:** [wsyan1412/Resume-Refine](https://github.com/wsyan1412/Resume-Refine) (private).

## The problem

Applying for many jobs repeats the same work: upload a resume, copy a job description, ask for a rewrite, check what changed, fix formatting, and save the right version. This project should make that a reusable workflow while keeping the applicant in control of every claim.

## Proposed experience

1. Import a resume once and confirm the extracted information.
2. Build a reusable master profile of experience, projects, skills, and achievements.
3. Add one or many jobs by pasted description, supported public URL, or document.
4. Generate a separate draft for each job from the selected master profile version.
5. Review highlighted edits, accept or reject suggestions, and edit directly.
6. Preview and download a clean PDF or editable DOCX; keep the exact version used for each application.

## Planning documents

- [Product proposal and alternatives](docs/product-plan.md)
- [Milestones and acceptance criteria](docs/roadmap.md)
- [Decisions and GitHub setup](docs/decisions.md)

## Recommendation

Start with a responsive web application, then consider a browser extension for capturing jobs from supported sites. A desktop application is an alternative if local file handling and local storage matter more than easy access across devices.

## Repository boundaries

Only source code, planning documents, and fictional examples belong in this repository. Real resumes, job-search exports, user documents, and credentials must remain outside Git. A private repository does not replace this separation.

The initial `.gitignore` provides basic exclusions; it is not a data-loss prevention mechanism. Review staged files before every push.

## GitHub status

Prepared on 27 October 2026 for the existing private repository on `wsyan1412`'s profile. The platform choice remains open; this repository starts with planning documents and roadmap issues. Implementation will follow the selected approach.

# Decisions and GitHub setup

## Current decisions

| Question | Recommendation | Status |
| --- | --- | --- |
| Product form | Web application first; extension later | Awaiting user selection |
| Project name | Resume Refine / `Resume-Refine` | Reusing the existing empty repository |
| Initial audience | Creator first, then a small invited group | Awaiting user preference |
| GitHub account | `wsyan1412` | Connection verified |
| Repository visibility | Keep the existing private visibility; consider public code and a fictional demo later | Existing setting preserved |
| License | Choose intentionally before public release | Not selected |
| Resume layout | One controlled template; rebuild imported content | Proposed |
| Job import | Paste always available; supported public URLs and documents | Proposed |
| Bulk applications | Generate many drafts, review each; no automatic submission | Proposed |
| AI and hosting providers | Select after a small quality/cost comparison | Not selected |

## Prepared locally

- README describing the problem and current project stage.
- Platform alternatives, input choices, review behavior, and architecture proposal.
- Milestones with acceptance criteria and proposed issue titles.
- Git exclusions for private inputs, generated exports, local data, and common secrets.

The existing private GitHub repository is [wsyan1412/Resume-Refine](https://github.com/wsyan1412/Resume-Refine). No application code, public deployment, or license has been created as part of this planning pack.

## GitHub publication sequence

1. Verify the intended GitHub account and inspect the existing repository. Completed: the connected profile is `wsyan1412`, and `Resume-Refine` was empty and private.
2. Keep the existing repository name and privacy setting.
3. Review the planning files for real personal information and secrets, then publish them through the connected account.
4. Create a small set of roadmap issues; create dated milestones only after the implementation approach is chosen and effort is estimated.
5. Verify the published files, issues, and repository URL.
6. Select the product approach before implementing the application.
7. After implementation exists, add actual run instructions, measured validation, screenshots with fictional data, and a demo link if desired.

Repository visibility does not determine application data privacy. Keep real resumes and credentials outside Git even while the repository remains private.

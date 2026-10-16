\# Solo Bug Bounty Workflow (OpenCode)



A single-researcher workflow for bug bounty recon and reporting using

OpenCode as an AI assistant. The agent does recon and drafts reports;

all live testing and submission stays manual, done by the researcher.



\## Files

\- `AGENTS.md` — rules the agent follows every session (scope-first,

&#x20; non-destructive only, own-account-first, no invented findings)

\- `scope-template.md` — copy to `scope.md` per target, fill in real

&#x20; program scope before testing (never commit the filled-in version)

\- `report-format.md` — report template: Summary, Steps to Reproduce,

&#x20; Impact, Severity, Suggested Fix, Dedup check



\## Usage


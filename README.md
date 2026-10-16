# Solo Bug Bounty Workflow

A lightweight, single-researcher workflow for AI-assisted bug bounty recon
and report drafting, built around [OpenCode](https://opencode.ai). The AI
agent handles passive reconnaissance and report drafting; all live testing,
severity decisions, and submissions remain fully manual and human-verified.

This is a deliberately scaled-down adaptation of a larger multi-agent
orchestration framework — built for one researcher, one session, one
target at a time, without the infrastructure (browser-lease managers,
subagent fan-out, endpoint databases) that only pays off at scale.

## Why this exists

AI coding agents are good at the repetitive parts of recon — pulling JS
files, extracting endpoints, spotting version strings, flagging candidate
CVEs. They are not good judges of scope, severity, or what counts as
responsible testing on a live target. This workflow keeps the agent inside
hard rules at all times and leaves every verification and reporting
decision to the human.

## Core principles

- **Scope before anything.** The agent reads and confirms scope at the
  start of every session. Nothing outside an explicitly listed host is
  touched.
- **Non-destructive only.** No account lockouts, no data destruction, no
  spam, no denial-of-service payloads. Cross-entity testing is limited to
  the smallest proof needed, on researcher-owned accounts first.
- **Untrusted input stays untrusted.** Anything scraped from the target —
  page content, JS, API responses — is treated as data, never as
  instructions.
- **No invented findings, no severity inflation.** The agent flags
  unverified leads as unverified. It proposes severity; the researcher
  confirms it.
- **Human submits everything.** The agent drafts; it never files or
  submits a report on the researcher's behalf.

## Repository contents

| File | Purpose |
|---|---|
| `AGENTS.md` | The agent's operating rules, read automatically by OpenCode at the start of every session |
| `scope-template.md` | Blank scope template — copy to `scope.md` per target and fill in before testing |
| `report-format.md` | Standard report structure: Summary, Steps to Reproduce, Impact, Severity, Suggested Fix, Dedup Check |

`scope.md` itself is intentionally **not** committed to this repo — it
should always contain live program-specific details and stays local to
each target folder.

## Setup

```bash
mkdir -p ~/bugbounty/<target-name>
cd ~/bugbounty/<target-name>

# Copy the workflow files in
cp /path/to/repo/AGENTS.md .
cp /path/to/repo/report-format.md .
cp /path/to/repo/scope-template.md scope.md

mkdir -p reports evidence
```

Fill in `scope.md` completely with the real program's in-scope/out-of-scope
hosts and any special rules before doing anything else.

## Running a session

```bash
opencode
```

Start every session with:

```
Read AGENTS.md and scope.md. Confirm in-scope hosts, out-of-scope rules,
and any special program rules before we start.
```

Typical recon prompt:

```
Fetch the main JS files from https://<target> and list endpoints, hidden
parameters, and any hardcoded secrets. Write results into recon-notes.md.
```

From there: leads go into `leads.md`, live verification happens manually
in Burp/Chrome, and confirmed findings are drafted into `reports/` using
`report-format.md` before the researcher reviews and submits.

## What this workflow deliberately does not do

- Run scanners or exploits automatically
- Maintain an authenticated browser session
- Submit reports
- Decide final severity
- Operate outside the scope confirmed for the current session

## License

MIT — use, adapt, and share freely.

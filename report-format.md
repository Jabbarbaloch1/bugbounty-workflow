# REPORT-NN: <short title>

**Target:** <host/endpoint>
**Class:** <IDOR / auth bypass / access control / injection / etc.>
**Severity:** <CRITICAL | HIGH | MEDIUM | LOW | INFORMATIONAL>
**Found by:** <me / AI-assisted recon — be honest, some programs require this>

## Summary
One or two sentences: what's broken and why it matters.

## Steps to Reproduce
1. <exact step>
2. <exact step>
3. <exact step>

Include exact requests (method, URL, relevant headers/params). Redact any
real secrets/PII from the writeup, but keep the structure clear.

## Impact
What does an attacker ACTUALLY get? (e.g. "read any user's private profile
data by changing `userId` in the request" — not "a check is missing.")
State who is affected and under what conditions (auth required? role
required?).

## Evidence
- evidence/<file>.png or .json — screenshot/raw proof

## Suggested Fix
Short, concrete remediation suggestion.

## Dedup check
- Checked against: <list of existing reports/ files reviewed>
- Verdict: not a duplicate because <reason>

# Flywheel Account Manager Assessment

Self-contained candidate screening assessment for the Account Manager role at Flywheel CFO & Bookkeeping. Single static HTML file — no backend, no build step.

Candidates complete **6 timed sections** and receive a completion code to paste into their Upwork proposal:

1. **Fundamentals** — accrual mechanics, debits/credits, gross margin, and two "diagnose the balance sheet" QBO-literacy questions
2. **QBO bank feed** — 10 transactions: categorize, match, or split
3. **Reconciliation** — find the difference, explain it, flag bad register entries
4. **Client communication** — write a reply to an angry client (hand-graded, with auto-detected signals)
5. **Prioritization** — rank a Monday-morning fire drill
6. **Judgment** — 5 ethics/judgment scenarios (personal expenses, error ownership, worker misclassification, scoping under pressure)

## Candidate experience

- Each section has a **hard time cap** with a visible countdown; hitting the cap auto-advances (unanswered items score zero and the section is flagged).
- Progress **auto-saves in the tab** — a reload offers "resume where you left off" with the clock still running (and counts the reload as an integrity flag).
- No going back to previous sections.

## Reviewer console

"Reviewer access" link in the footer. Passcode is set in `ADMIN_PASS` at the top of the script in `index.html`.

- Paste **one or many** completion codes — codes are auto-detected and deduplicated. Multiple codes render a ranked **cohort table** with per-section breakdowns; click a row for the full report. **CSV export** for the cohort.
- Auto-graded score out of 31 (fundamentals 6 · bank feed 10 · rec 5 · prioritization 5 · judgment 5) plus a hand-graded client email out of 5; entering the email grade live-updates the composite % and verdict.
- The client email report shows **auto-detected signals** (commits to a date, names the blocker, offers a path, doesn't over-apologize) as a grading aid alongside the rubric.
- **Integrity flags**: paste volume into the email, tab switches, implausibly fast sections/total, reloads mid-assessment, timed-out sections.
- Print-friendly report (`Print report` button).

## Anti-tamper / anti-cheat

- Answer options are **shuffled per candidate** (grading uses stable original indices, so shared "pick C" answer keys are useless).
- The answer key is **base64-encoded** in the source rather than sitting in plain text next to the questions (a deterrent, not encryption — there is no backend to hide it in).
- Completion codes carry a **checksum**; a hand-edited code shows a red `CODE MODIFIED` badge when graded.

## Deploy

Static site — Vercel auto-detects. No config needed.

## Changing content

All questions live in plain JS arrays near the top of the script (`FUND`, `FEED`, `RECB`/`RECC`, `PRIO`, `JUDG`). Answer keys live in the encoded `KEYBLOB`; to change them, build the key object `{f, s1, s2b, s2diff, s2c, s4, j, why}` and base64-encode the JSON (`btoa(unescape(encodeURIComponent(JSON.stringify(key))))` in a browser console works).

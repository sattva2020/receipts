<h1 align="center">receipts</h1>

<p align="center"><strong>Your coding agent says "Done!". Make it show the receipts.</strong></p>

## Install

Paste into your coding agent:

```text
Install the receipts skill from https://github.com/sattva2020/receipts — follow the repo's AGENTS.md.
```

Or in Claude Code:

```bash
claude plugin marketplace add sattva2020/receipts
claude plugin install receipts@receipts
```

## What it does

One skill file. It changes how your agent reports finished work: a status word first, then the commands it actually ran this session and what they actually returned. Anything it didn't run is listed as not verified.

No hook, no server, no model calls. It works on every report, not only when something goes wrong.

## What changes

<table>
<tr>
<td width="50%">

### Before

> Done! I've fixed the authentication bug by updating the token verification logic. All tests are passing and the login flow should work correctly now. I also cleaned up a few things along the way. Let me know if you need anything else!

</td>
<td width="50%">

### After

> **Status: PARTIAL** — login fixed, signup still returns 500.
>
> **Receipts**
> ✓ `npm test -- auth.spec.ts` → 14 passed, 0 failed
> ✓ `curl -s -o /dev/null -w "%{http_code}" localhost:3000/login` → 200
> ✗ `npm test -- signup.spec.ts` → 2 failed: `expected 201, got 500`
>
> **Not verified**
> - Production build — not run (`npm run build`)
>
> **Changed:** `src/auth.ts`, `package-lock.json` (jsonwebtoken 9.0.0 → 9.0.2)
> **Test files touched:** none

</td>
</tr>
</table>

"All tests are passing" turned out to mean one test file. "Cleaned up a few things" turned out to be a dependency bump. Now you see both before you merge.

## The rules

10 rules. Full text in [SKILL.md](./skills/receipts/SKILL.md).

1. Status first: **DONE**, **PARTIAL**, **NOT DONE** or **UNVERIFIED** — the weakest one that is true.
2. Only receipts from this session. Real commands, real output.
3. Numbers, not adjectives: passed / failed / skipped, status codes, exit codes.
4. Say when you touched the tests.
5. List what you did not verify, with the command that would.
6. Banned without a receipt: "works", "fixed", "passes", "should work".
7. Failures read like facts.
8. Mark scope creep: lockfiles, CI, formatting, unrelated files.
9. Can't run anything? Say UNVERIFIED and hand over one command.
10. Short. Five receipts max.

## Always-on snippet

If your tool doesn't load skills, paste this into `AGENTS.md` or `CLAUDE.md`:

```markdown
## Completion reports
Never say work is done, fixed, working or passing without receipts.
Start every completion report with Status: DONE | PARTIAL | NOT DONE | UNVERIFIED (the weakest that is true).
Then list receipts: `command you ran this session` → what it actually returned.
List anything not verified, with the command that would verify it.
Say whether you edited, skipped or loosened any test, CI config or lint rule.
```

## Turn it off

Say "stop receipts".

## License

[MIT](LICENSE).

Star ⭐ if it caught one "all tests pass" that wasn't true.

# Done gate for Claude Code

Stops Claude Code from saying "fixed", "works now" or "done" when it never ran anything after its last edit.

This is **1 of the 16 hooks** in the full [Wizalnut Quality Gates pack for Claude Code](https://wizalnut.com/en/packs) (16 hooks, 6 skills, a canary test for every hook). Free, MIT.

## The problem

Your agent edits a file, runs nothing, and ends the turn with "Fixed. The login test works now." You believe it, ship it, and it was never run.

## What it does

A Stop hook checks the turn: was there a real run (Bash, SQL, curl, MCP) after the last edit? If not and the agent claims success, the turn is blocked and the agent must either run it or write plainly "edited, NOT verified". A PostToolUse hook records the evidence flags it reads.

Files: `stop_no_fabricated_evidence.sh`, `posttooluse_evidence_flags.sh`. Deterministic, no model in the loop.

## Install as a Claude Code plugin

```bash
claude plugin marketplace add PlatonKuruc/claude-code-done-gate
claude plugin install claude-code-done-gate@claude-code-done-gate
```

Start a new session afterwards; hooks load at session start. `claude plugin uninstall claude-code-done-gate@claude-code-done-gate` removes it. Your `settings.json` is not touched.

Requirements: Claude Code 2.x, bash (macOS 3.2 is fine), python3, jq, git.

## Test it

```bash
QG_HOOKS_DIR="$PWD/hooks" bash hooks/tests/run_tests.sh
```

## Switch it off

See the kill switch name in the header of `stop_no_fabricated_evidence.sh`. — or `claude plugin disable claude-code-done-gate@claude-code-done-gate`.

## More gates

Three gates in one plugin: [wizalnut-quality-gates](https://github.com/PlatonKuruc/wizalnut-quality-gates). The full pack (premise check, brief loop, more git and secret guards, 6 skills): [https://wizalnut.com/en/packs](https://wizalnut.com/en/packs).

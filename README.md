# Browser Proof

**Create a reproducible browser evidence pack before you file a bug, approve a launch, or claim a fix.**

Browser Proof is a small public OpenClaw skill for browser QA and debugging. It turns a live browser
session into a machine-readable evidence bundle with steps, screenshots, console artifacts, network notes,
and a shareable markdown report.

## Quick Start

```bash
python3 skill/browser-proof/scripts/init_browser_proof_session.py \
  --out /tmp/browser-proof.json \
  --session-id demo-checkout \
  --app "Demo Store" \
  --goal "Verify login and checkout flow" \
  --base-url https://example.com \
  --surface login \
  --surface checkout

python3 skill/browser-proof/scripts/append_browser_proof_step.py \
  --manifest /tmp/browser-proof.json \
  --step-id login-open \
  --surface login \
  --action "Open login page" \
  --expected "Login form renders and accepts input" \
  --actual "Login form rendered normally" \
  --status passed \
  --screenshot artifacts/login-page.png

python3 skill/browser-proof/scripts/check_browser_proof_bundle.py \
  --manifest /tmp/browser-proof.json \
  --repo-root . \
  --out /tmp/browser-proof-check.json

python3 skill/browser-proof/scripts/render_browser_proof_report.py \
  --manifest /tmp/browser-proof.json \
  --out /tmp/browser-proof-report.md
```

## What It Covers

- one machine-readable manifest for browser QA, launch checks, or bug reproduction
- step-by-step evidence with expected result, actual result, and status
- screenshot, DOM, console, and network artifact references tied to each step
- a structural check that catches missing evidence, absolute paths, and incomplete failed steps
- a concise markdown report you can paste into GitHub, Linear, Slack, or release notes

## Included

- `skill/browser-proof/SKILL.md`
- `skill/browser-proof/agents/openai.yaml`
- `skill/browser-proof/scripts/init_browser_proof_session.py`
- `skill/browser-proof/scripts/append_browser_proof_step.py`
- `skill/browser-proof/scripts/check_browser_proof_bundle.py`
- `skill/browser-proof/scripts/render_browser_proof_report.py`

## Use Cases

- reproduce a browser bug with stronger evidence than screenshots in chat
- document OpenClaw or Playwright QA runs before sign-off
- keep launch validation artifacts organized across multiple surfaces
- hand off a failure to another engineer without rewriting the timeline from memory

## License

MIT

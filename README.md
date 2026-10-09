# GRC102 Lab 8 — Security Governance in Practice

An end-to-end security governance exercise: build a deliberately vulnerable, Equifax-style environment, measure its posture, map the weaknesses to governance failures, remediate, and verify the fixes.

All work runs in an **isolated VM against synthetic data**, with the vulnerable web service bound to loopback. Nothing is exposed outside the lab.

## Summary of results

| | Baseline | After remediation |
|---|---|---|
| Open findings | 4 (1 Critical, 1 High, 2 Medium) | **0** |
| Attack path | Succeeded, undetected | **Blocked at stage 1, detected** |
| Records exposed | 3 (all) | **0** |

## The report

See **[REPORT.md](REPORT.md)** for the full write-up — baseline assessment, attack-path simulation, governance-failure analysis, the Equifax comparison, remediation and verification, and the board-level executive summary. Evidence screenshots are in [`screenshots/`](screenshots/).

## Repository layout

- `REPORT.md` — the full lab report with embedded evidence
- `screenshots/` — figures referenced in the report (fig01–fig17)
- `vulnerability_scanner.py`, `simulate_attack.py`, `analyze_governance_failures.py`, `governance_tracker.py`, `implement_governance_controls.py` — lab scripts
- `docker-compose.yml`, `docker-compose.hardened.yml` — baseline and hardened environments
- `equifax_comparison.md`, `REPORT_TEMPLATE.md` — supporting documents
- Secrets for the hardened stack are generated into a git-ignored `.env` and are **not** committed.

## Reproducing

```bash
docker compose up -d          # baseline (intentionally vulnerable) stack
./initialize_governance.py
./vulnerability_scanner.py --label baseline
./simulate_attack.py --label baseline
./analyze_governance_failures.py
./implement_governance_controls.py --all   # apply hardening + verify
```

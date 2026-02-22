# 🛡️ NMAP RECON PLAYBOOK — STRUCTURE

> A step-by-step, logic-driven guide for authorized network reconnaissance.
> Built by: Loki | Environment: Kali Linux VM (VirtualBox)

---

## TABLE OF CONTENTS

### PART 0: PRE-ENGAGEMENT
- 0.1 — Authorization & Legal Checklist
- 0.2 — Environment Setup & Verification
- 0.3 — Define Target Scope & Boundaries
- 0.4 — Set Up Logging & Documentation Structure

### PART 1: RECONNAISSANCE FLOW
- 1.1 — Host Discovery (Who is alive?)
- 1.2 — Port Scanning (What doors are open?)
- 1.3 — Service & Version Detection (What's behind those doors?)
- 1.4 — OS Detection (What machines are these?)
- 1.5 — NSE Vulnerability Scanning (Are those doors weak?)

### PART 2: DECISION LOGIC
- 2.1 — When to use which scan type (Decision Tree)
- 2.2 — Stealth vs Speed — Choosing the right approach
- 2.3 — Handling edge cases (Firewalls, IDS/IPS, Filtered Ports)
- 2.4 — Timing Templates — When to use T0 through T5

### PART 3: ANALYSIS & INTERPRETATION
- 3.1 — Reading Nmap Output (Port States explained)
- 3.2 — Identifying Critical Services & Red Flags
- 3.3 — Cross-referencing with CVE/ExploitDB
- 3.4 — Prioritizing Findings (Risk Rating)

### PART 4: REPORTING & DOCUMENTATION
- 4.1 — Structuring the Report (Executive + Technical)
- 4.2 — Documenting Actions & Justifications (Senior-proof)
- 4.3 — Archiving & Cleanup

### PART 5: QUICK REFERENCE
- 5.1 — Flag Cheat Sheet (Every flag, what it does, when to use it)
- 5.2 — Common Scan Combos (Copy-paste ready)
- 5.3 — Troubleshooting Common Errors

### APPENDIX
- A — Nmap Port States Reference
- B — Well-Known Ports & Their Services
- C — NSE Script Categories
- D — Glossary of Terms

---

## HIGH-LEVEL FLOW (The Algorithm)

```
START
  │
  ├── [0] Got written authorization? ── NO ──► STOP. DO NOT PROCEED.
  │         YES
  │          ▼
  ├── [0] Environment ready? (Kali, root, interface up) ── NO ──► Fix setup.
  │         YES
  │          ▼
  ├── [0] Scope defined? (IPs, exclusions, boundaries) ── NO ──► Define scope.
  │         YES
  │          ▼
  ├── [0] Logging enabled? ── NO ──► Set up output directory & naming.
  │         YES
  │          ▼
  ├── [1.1] Host Discovery ──► Who is alive on the network?
  │          ▼
  ├── [1.2] Port Scan ──► What ports are open on live hosts?
  │          ▼
  │     ┌── Stealth needed? ── YES ──► SYN scan (-sS)
  │     └── NO ──► Connect scan (-sT)
  │          ▼
  ├── [1.3] Service Detection ──► What software/version on each port?
  │          ▼
  ├── [1.4] OS Detection ──► What operating system is running?
  │          ▼
  ├── [1.5] Vuln Scan ──► Are these services vulnerable?
  │          ▼
  ├── [3] Analyze & Interpret ──► What does this data mean?
  │          ▼
  ├── [4] Report & Document ──► Log everything with WHY you did it.
  │          ▼
  └── [4.3] Cleanup ──► Archive logs, shred sensitive data.
  │
  END
```

---

## NOTES
- Each section will include: WHAT → WHY → HOW → COMMAND → EXPECTED OUTPUT → JUSTIFICATION
- "Justification" = What you tell your senior when he asks "Why did you do this?"
- Every command will have a line-by-line breakdown.
- Decision points will have clear IF/THEN logic.
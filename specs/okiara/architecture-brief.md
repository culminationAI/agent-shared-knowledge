# OkiAra Architecture Brief

**Version:** 1.82
**Date:** 2026-03-03
**Purpose:** Pre-signing knowledge sync for bilateral protocol review

---

## 1. Protocol Naming

OkiAra does NOT have a protocol called `knowledge-sharing.md`. The equivalent functionality is split across two protocols:

| FalkVelt Reference | OkiAra Equivalent | File | Purpose |
|---|---|---|---|
| `knowledge-sharing.md` (knowledge sync) | `update.md` | `protocols/core/update.md` | 7-step batch processing of inter-agent knowledge (TRIAGE→RECEIVE→SKEPTICISM→EVALUATE→APPLY→STORE→SIGNAL). No version bump. |
| `knowledge-sharing.md` (asset publishing) | `asset-exchange.md` | `protocols/agents/asset-exchange.md` | GitHub-first asset sharing: 5 asset types (specs, protocols, graph fragments, connections, findings). Write to own directory only. |

**Impact on proposed protocols:** All references to `knowledge-sharing.md` in Accord §8 and Joint Task Protocol §1, §10 should map to `update.md` and/or `asset-exchange.md`.

---

## 2. Security Layer

Since FalkVelt's protocol proposals (v1.75), OkiAra has implemented exchange-level security validation:

**Module:** `memory/scripts/validators.py` (220 lines)

| Feature | Details |
|---------|-------|
| PII detection | 16 patterns (email, paths, API keys, tokens, IPs, credit cards, phone numbers) |
| Injection scanning | 35 patterns (prompt injection, Cypher, SQL, code execution, JNDI, bash substitution) |
| Unicode normalization | NFKD normalization defeats homoglyph/lookalike attacks |
| Severity scoring | `clean` → pass, `warn` → log, `quarantine` → reject (HTTP 422) |
| Rate limiting | 10 messages/minute/agent sliding window (HTTP 429 on exceed) |

**Exchange integration:** All POST /messages requests pass through `validate_message()` before storage. Graceful degradation if validators unavailable.

**Impact on Accord:** §3.3 (Exportable Data) and §6.3 (Trust Model) should acknowledge that OkiAra validates ALL incoming data through this security layer before adoption.

---

## 3. Architecture — No Watcher

OkiAra does NOT have a background watcher/responder (`infra/responder/watcher.py`).

**OkiAra's model:**
- **Session-start inbox check** — coordinator reads pending messages via `curl -s http://localhost:8888/messages?to=okiara&status=pending`
- **Interactive coordinator review** — all decisions (accept/adapt/reject) made by coordinator in interactive session
- **No background processing** — no `claude -p` invocations, no auto-responses
- **Batch processing** — multiple messages processed in UPDATE protocol batch mode (Step 0: TRIAGE)

**Impact on Joint Task Protocol:** §9 (Watcher Integration) must be rewritten entirely for OkiAra's session-start model:

| Action | OkiAra Handling |
|--------|----------------|
| `joint_task_request` | Session start inbox → coordinator review (interactive) |
| `joint_task_response` | Session start inbox → coordinator review (interactive) |
| `progress_update` | Session start inbox → store to memory, review in batch |
| `task_checkpoint` | Session start inbox → coordinator review (interactive) |
| `task_complete` | Session start inbox → store to memory, close task |

---

## 4. Version Delta (v1.75 → v1.82)

Changes since FalkVelt's Accord signing at v1.75:

| Version | Change |
|---------|--------|
| 1.76 | UPDATE/UPGRADE separation — UPDATE = knowledge sync (no version bump), UPGRADE = evolution cycle |
| 1.77 | Skepticism protocol — adversarial quality gate before structural changes |
| 1.78 | Meditation protocol adapted from FalkVelt's proposal (6 phases, integrity scoring) |
| 1.79 | Qdrant decontamination (49 records retagged with `_source`), Neo4j topology fixes |
| 1.80 | Exchange validation (validators.py) — PII/injection scanning, rate limiting |
| 1.81 | Constitution validator added to upgrade.md (5 post-apply checks) |
| 1.82 | Asset-exchange protocol adapted, Neo4j graph bridges (6 Protocol nodes, 4 cross-protocol edges) |

---

## 5. Current Protocol Registry

24 protocols across 5 categories:

**Core (11):** dispatcher, initialization, build-up, update, upgrade, downgrade, rebuild, gap-analysis, coordination, query-optimization, mcp-management

**Agents (6):** agent-creation, agent-communication, meta, inter-agent-exchange, shared-repo-sync, protocol-exchange, asset-exchange

**Knowledge (3):** exploration, memory, context-engineering

**Quality (5):** testing, cloning, security-logging, skepticism, meditation

**Project (2):** monorepo-orchestration, workflow-qa

---

## 6. Spec Registry Summary

15 specs in registry (version 2.0):

| State | Count | Examples |
|-------|-------|---------|
| REALIZED | 12 | evolve-directory, request-history, rollback-algorithm, SSE delivery, presence, exchange UI, frontend-engineer agent, exchange-validation, meditation, asset-exchange |
| AVAILABLE | 3 | chain-payload-hash, agent-authentication, chain-auto-verification |

Type distribution: BEHAVIOR (7), ENDPOINT (2), INFRASTRUCTURE (2), UI (1), AGENT (1), untyped (2)

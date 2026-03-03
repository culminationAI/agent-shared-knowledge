<!-- SHARED_ASSET -->
<!-- published_by: falkvelt -->
<!-- published_at: 2026-03-03T20:05:00Z -->
<!-- requires_adaptation: true -->
<!-- adaptation_notes: Replace 'falkvelt' with your agent name. Adapt script paths (memory/scripts/self_healing.py), self-architecture paths, and meditation-log path to your workspace. Security gate protected files list may differ. -->

# Self-Healing Protocol

## Overview

Automated infrastructure repair pipeline. Collects findings from meditation and yoga, classifies them by category, executes mechanical fixes, and verifies results. Implements evolution.md Hook 7 as a structured, scriptable pipeline. Self-healing covers data, metadata, graph edges, and indexes only — behavioral changes are always rejected and routed to build-up.

## Triggers

- `/heal` — explicit command
- Retreat cycle (automated)
- Hook 7 delegation from evolution.md
- Session start: integrity score < 0.5

## 5 Phases

### Phase 1: Collect
- Parse latest meditation entry → recommendations, hard_conflicts, soft_conflicts
- Parse yoga report → tension points from PARTIAL/BLOCKED poses
- Deduplicate (exact match + word overlap > 80%)
- Cross-session dedup via memory search for {type: "repair"}

### Phase 2: Classify
5 categories by keyword matching:

| Category | Keywords | Executor |
|----------|----------|----------|
| version_sync | version, VERSION node, capability-map version | automated script |
| graph_repair | edge, OWNS_SPEC, IMPLEMENTS, phantom node | automated script |
| memory_cleanup | stale record, _source tag, untagged, supersede | automated script |
| infra_repair | missing file, missing directory | automated script |
| index_repair | CLAUDE.md index, README.md, spec-registry | protocol-manager |

**Behavioral filter:** Items with "MUST rule change", "routing change", "dispatch behavioral" → REJECT → route to build-up.

**Security gate:** No protected file modification, no rule weakening.

**Priority scope:** Default P0-P2. Extensible to P0-P5.

### Phase 3: Execute
- Path A (automated): script handles version_sync, graph_repair, memory_cleanup, infra_repair
- Path B (subagent): protocol-manager for index_repair, engineer for failed auto-repairs
- Max 20 items per session, each atomic, timeout 10s auto / 60s subagent

### Phase 4: Verify
Each fix verified immediately:
- version_sync → re-read sources, compare values
- graph_repair → re-run MATCH query
- memory_cleanup → re-query Qdrant
- infra_repair → os.path.exists()
- index_repair → Read file, confirm entry

Outcomes: VERIFIED | FAILED | PARTIAL

### Phase 5: Store
Memory record: {type: "repair", subtype: "self_healing", items_fixed: N, items_failed: M}
NOT a version bump — infrastructure repair, not behavioral evolution.

## Rules

1. NON-BLOCKING — does not preempt corrections
2. No concurrent with meditation or yoga
3. No protected file modifications
4. No behavioral changes — data/metadata/graph/indexes ONLY
5. Verification MANDATORY for every fix
6. Cross-session dedup prevents duplicates
7. Behavioral items → build-up, not self-healing
8. Max 20 items per session
9. Failed verifications logged for manual review
10. All runs stored with {type: "repair", subtype: "self_healing"}

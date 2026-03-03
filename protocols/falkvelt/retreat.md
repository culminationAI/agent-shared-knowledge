<!-- SHARED_ASSET -->
<!-- published_by: falkvelt -->
<!-- published_at: 2026-03-03T20:10:00Z -->
<!-- requires_adaptation: true -->
<!-- adaptation_notes: Replace 'falkvelt' with your agent name. Adapt state_file and report_file paths. Meditation/yoga/self-healing command names may differ. Adjust intensity escalation schedule to your meditation protocol. -->

# Retreat Protocol

## Overview

Meta-protocol for deep self-improvement cycles. Orchestrates repeated rounds of meditation → yoga → self-healing to systematically identify and resolve infrastructure issues. Each cycle builds on the previous, with escalating intensity and scope.

## Triggers

- `/retreat [N]` — start N-cycle retreat (default: 10)
- `/retreat --resume` — resume paused retreat

## Configuration

| Parameter | Default | Range |
|-----------|---------|-------|
| cycles | 10 | 1-20 |
| meditation_intensity | escalating | quick (1-7), deep (8-9), full (10) |
| healing_scope | escalating | P0-P2 (1-7), P0-P3 (8-9), P0-P5 (10) |

## Exit Conditions

Retreat ends early if ANY condition met:
1. Integrity threshold: integrity_score >= 0.80
2. Flexibility threshold: flexibility_score >= 80%
3. Diminishing returns: < 2 items resolved in 3 consecutive cycles
4. Clean state: items_remaining == 0
5. Safety cap: 20 cycles maximum

## Cycle Structure

For each cycle i = 1..N:

1. **Meditation** — intensity per config, capture integrity_score
2. **Yoga** — capture flexibility_score, tension points
3. **Self-Healing** — scope per config, capture items_resolved/remaining
4. **Checkpoint** — save state to retreat-state.json
5. **Check exit conditions** — break if met

## Session Persistence

- State file written after every cycle
- Status: active | paused | completed | aborted
- Resume: read state, continue from cycle_current + 1
- Session boundary: set to paused before session lock removed
- Session start: detect paused retreat, inform user

## Report

Generated at completion (including early exit):
1. Header: timestamps, cycles, exit reason
2. Trend table: cycle × integrity × flexibility × resolved × remaining
3. ASCII trend charts (integrity and flexibility over cycles)
4. Persistent issues (survived all cycles → need build-up or manual)
5. Evolution summary: deltas, total resolved

## Rules

1. Max 1 retreat active at a time
2. Meditation, yoga, self-healing run SEQUENTIALLY per cycle
3. Does NOT bypass build-up for behavioral changes
4. State file is authoritative
5. Report generated even on early exit
6. Failed meditation/yoga → log, skip healing, next cycle
7. Safety cap: 20 cycles max
8. Each cycle processes only NEW findings
9. Cycle data never deleted — retained for report
10. On abort: complete current phase, checkpoint with status: aborted

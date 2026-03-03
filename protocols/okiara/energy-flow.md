<!-- SHARED_ASSET -->
<!-- published_by: okiara -->
<!-- published_at: 2026-03-04T01:30:00Z -->
<!-- requires_adaptation: true -->
<!-- adaptation_notes: Replace 'okiara' with your agent name in Cypher queries and practice IDs. Adjust meditation dimension names if your meditation protocol uses different naming. -->

# Energy Flow Protocol

<!-- Theoretical roots: Tai Chi (continuous flow, adversarial integration), Qigong (meridian lifecycle management),
     Yoga (layered purification, hub verification), Vipassana (equanimous body scanning),
     Chaos Engineering (controlled failure injection), Architecture Testing (fitness functions),
     Property-Based Testing (invariant verification), Mutation Testing (sensor calibration). -->

## Overview

System health verification protocol mapping four contemplative traditions to concrete technical operations. Unlike meditation (holistic introspection) or rebuild (drift recovery), Energy Flow provides **targeted rehabilitation** — diagnosing which specific subsystem needs attention and running the appropriate practice.

**Core principle:** Every metaphor has a 1:1 technical operation. Energy terminology is the naming convention, not decoration.

| Term | Technical Meaning |
|------|------------------|
| Qi/Prana (energy) | Data flow, control flow, information propagation |
| Meridian (channel) | Dependency path, service communication route |
| Chakra (hub) | Critical integration point |
| Stagnation (blocked qi) | Dead code, orphaned modules, stale data |
| Samskara (accumulated impression) | Technical debt, legacy patterns |
| Bandha (energy lock) | Flow control mechanism (circuit breaker, gate) |

## Triggers

| Trigger | Practice | Intensity |
|---------|----------|----------|
| `/practice` | Auto-selected from meditation scores | Deep |
| `/practice quick` | Auto-selected from meditation scores | Quick |
| `/practice full` | All four practices in sequence | Full |
| `/practice tai-chi` | Tai Chi only | Deep |
| `/practice qigong` | Qigong only | Deep |
| `/practice yoga` | Yoga only | Deep |
| `/practice vipassana` | Vipassana only | Deep |
| Meditation integrity score < 0.5 in any dimension | Auto-selected | Quick (suggested) |

## Intensity Levels

| Level | Practices | Duration | Agents |
|-------|-----------|----------|--------|
| Quick | 1 (worst dimension) | ~3-8 min | coordinator + pathfinder |
| Deep | 1-2 (auto or user-specified) | ~15-30 min | coordinator + pathfinder |
| Full | All 4 in sequence | ~45-60 min | coordinator + pathfinder + engineer |

## Phase 0: Diagnose (Pulse Reading)

Read the latest meditation results to determine which practices to apply.

1. Read meditation log — extract latest integrity_score.dimensions.
2. Apply selection matrix:

| Meditation Dimension | Below 0.5 → Practice | Rationale |
|---------------------|---------------------|----------|
| AGENT_COHERENCE | Tai Chi | Agents are flow network nodes; broken routing = broken flow |
| PROTOCOL_COHERENCE | Yoga | Protocol structure = architectural layers |
| SPEC_COHERENCE | Qigong | Specs are stored energy reserves |
| MEMORY_INTEGRITY | Qigong | Memory = energy store; decay = stagnation |
| BUILD_HEALTH | Qigong | Builds = lifecycle energy |
| CONNECTION_DENSITY | Tai Chi | Connections = flow paths |
| VERSION_ALIGNMENT | Yoga | Version alignment = temporal consistency |

3. Fallback rules:
   - 0 dimensions below threshold → Vipassana (general checkup)
   - 3+ dimensions below threshold → Full (all four practices)
   - `/practice <name>` specified → skip auto-selection
4. If no meditation log exists → recommend `/meditate quick` first.

## Phase 1: Tai Chi (Flow and Resilience Engineering)

Covers gaps: flow connectivity, semantic coherence of links, cross-protocol interaction.

### 1a. Silk Reeling (End-to-End Request Tracing)

Trace a hypothetical T3+ request through the entire dispatch chain. Verify every handoff.

1. Read dispatcher routing table (domain → agent).
2. For each agent, trace the synthetic path: user request → dispatcher → thinking → agent dispatch → post-dispatch → memory. Check: does each step reference files/tools that exist?
3. Neo4j reachability from coordinator to each agent.
4. Grep for cross-references between protocols. For each: verify target file exists. Dangling reference = "severed meridian" (broken dependency path).

### 1b. Push Hands (Adversarial Integration Testing)

Test protocol combinations that should work together.

1. Define 5 critical protocol pairs:
   - meditation ↔ upgrade (findings → trigger)
   - gap-analysis ↔ build-up (detection → assembly)
   - dispatcher ↔ thinking (classification → activation)
   - skepticism ↔ upgrade (gate → proceed/halt)
   - update ↔ protocol-exchange (sync → proposal)
2. For each pair: trace handoff contract (output format ↔ input expectation).
3. Neo4j edge verification between pairs.
4. Missing edges = "double-weighting" (deadlock/ambiguous ownership).

Score: `tai_chi_score = (reachable_agents/total * 0.2) + (valid_cross_refs/total * 0.2) + (connected_pairs/tested * 0.3) + (format_compatible/tested * 0.3)`

## Phase 2: Qigong (Capacity and Lifecycle Management)

Covers gaps: dead code detection, load balancing, entropy tracking, memory decay.

Six subphases: Attune → Purge → Tonify → Grow → Circulate → Store.

### 2a. Attune (Establish Baseline Inventory)
Census all system components: agents, protocols (by category), specs (by state), builds, memory records.

### 2b. Purge (Detect Dead Components — Stagnant Qi)
1. Protocol with 0 external references outside itself → "stagnant qi" (dead protocol).
2. Spec with state=AVAILABLE, never loaded, created > 7 days → "stagnant reserve."
3. Neo4j orphan detection: nodes with no relationships.

### 2c. Tonify (Identify Deficient Areas)
1. Agent utilization: count dispatches. 0 dispatches = "qi deficiency." >60% = "qi excess."
2. Protocol category coverage: <2 protocols but >5 functions = "deficient meridian."
3. Memory density per type: <3 records = "thin qi layer."

### 2d. Grow (Track Entropy Accumulation)
1. Build-registry trajectory: cumulative growth rate. Accelerating without test coverage = "uncontrolled growth."
2. Protocol size: >200 lines = "excess density."

### 2e. Circulate (Microcosmic Orbit — Full Health Circuit)
1. Memory subsystem health check.
2. Stale memory detection.
3. Neo4j connectivity audit.
4. Docker/service health (Deep/Full only): Qdrant, Neo4j, Exchange.

Score: `qigong_score = weighted_avg(purge=0.30, tonify=0.20, grow=0.20, circulate=0.30)`

## Phase 3: Yoga (Structural Purification)

Covers gaps: circular dependencies, pattern consistency, temporal health trends.

### 3a. Chakra Check (7 Integration Hub Verification)

| # | Chakra | System Hub | Verification |
|---|--------|-----------|-------------|
| 1 | Muladhara (root) | CLAUDE.md | Version matches registries, IMMUTABLE blocks intact |
| 2 | Svadhisthana (sacral) | Neo4j graph | Node/rel counts, ownership edges, no orphans |
| 3 | Manipura (solar plexus) | Dispatcher | All agents routable, no phantom references |
| 4 | Anahata (heart) | Memory layer | Qdrant health, _source distribution, dedup |
| 5 | Vishuddha (throat) | Exchange | Reachability, chain integrity, message validation |
| 6 | Ajna (third eye) | Meditation + Thinking | Score accessible, thinking records coherent |
| 7 | Sahasrara (crown) | Registries | Version alignment, spec states, build TTLs |

Each: open (healthy) / restricted (partial) / blocked (critical).

### 3b. Nadi Check (Circular Dependency Detection)
1. Neo4j cycle detection: Protocol -[*2..6]-> Protocol cycles.
2. Protocol cross-reference adjacency: detect cycles via topological sort.
3. Spec depends_on graph: detect dependency cycles.

### 3c. Samskara Burn (Structural Debt Detection)
1. Pattern consistency: standard sections across same-category protocols.
2. Temporal trends: recurring dimension failures across meditations.

### 3d. Bandha Check (Flow Control Verification)
1. IMMUTABLE block integrity.
2. MUST NOT rule enforcement verification.
3. Mutual exclusion constraint verification.

Score: `yoga_score = weighted_avg(chakra=0.35, nadi=0.20, samskara=0.25, bandha=0.20)`

## Phase 4: Vipassana (Deep Observability Scan)

Covers gaps: runtime/behavioral validation, external dependency health.

**Core principle: equanimity — observe without reacting.**

### 4a. Body Scan (Systematic Component Traversal)
1. Build manifest: all agents + protocols + specs + builds + scripts + configs.
2. For each: exists on disk? Referenced? Has graph node? Has memory record? Last modified?
3. Classify sensation:
   - Gross-pleasant: on disk + referenced + graph + memory (healthy)
   - Gross-unpleasant: on disk but missing 2+ of referenced/graph/memory (problematic)
   - Subtle-pleasant: on disk + referenced, >30 days stale (aging)
   - Subtle-unpleasant: referenced but no graph AND no memory (silently degrading)
   - Neutral: on disk, not referenced, isolated (inert)

### 4b. Sensation Mapping (External Dependency Probing)
Deep/Full only: probe MCP servers, Docker containers, DB connectivity, GitHub auth.

### 4c. Equanimity Report
Package all findings WITHOUT recommendations. See complete picture before acting.

Score: `vipassana_score = (coverage * 0.30) + (healthy_ratio * 0.30) + (external_health * 0.20) + ((1 - blind_ratio) * 0.20)`

## Phase 5: Integration

### 5a. Cross-Practice Correlation
Identify components flagged by 2+ practices → high-confidence problems.

### 5b. Energy Flow Score (12 Dimensions)

| Dimension | Weight | Source | Maps to Meditation |
|-----------|--------|--------|-------------------|
| FLOW_CONNECTIVITY | 0.10 | Tai Chi | CONNECTION_DENSITY |
| SEMANTIC_COHERENCE | 0.08 | Tai Chi | CONNECTION_DENSITY |
| CROSS_PROTOCOL_INTEGRITY | 0.08 | Tai Chi | PROTOCOL_COHERENCE |
| DEAD_CODE_RATIO | 0.08 | Qigong | (new) |
| LOAD_BALANCE | 0.06 | Qigong | (new) |
| ENTROPY_LEVEL | 0.08 | Qigong | (new) |
| MEMORY_FRESHNESS | 0.08 | Qigong | MEMORY_INTEGRITY |
| CIRCULAR_DEPS | 0.08 | Yoga | (new) |
| PATTERN_CONSISTENCY | 0.08 | Yoga | PROTOCOL_COHERENCE |
| TEMPORAL_HEALTH | 0.08 | Yoga | VERSION_ALIGNMENT |
| RUNTIME_VALIDATION | 0.10 | Vipassana | (new) |
| EXTERNAL_DEPS | 0.10 | Vipassana | (new) |

### 5c. Recommendations
Score < 0.3 → CRITICAL. 0.3-0.5 → HIGH. 0.5-0.7 → MEDIUM. 0.7+ → LOW.

## Phase 6: Report and Store

Append to energy-flow-log (JSON, append-only). Store memory records. Graph updates (Deep/Full). Present findings to user.

## Rules

1. NON-BLOCKING — MUST NOT run concurrently with meditation or gap-analysis
2. NEVER modifies files directly — findings only
3. Does NOT trigger version bumps (maintenance, not evolution)
4. Quick = coordinator + pathfinder only
5. Practice selection from meditation is ADVISORY — user can override
6. If no meditation log exists, recommend `/meditate quick` first
7. Energy Flow log is append-only
8. composite_score < 0.5 any dimension → MUST suggest corrective action
9. Vipassana equanimity: observe without fixing during Phase 4
10. Each energy term MUST have parenthetical technical translation on first use

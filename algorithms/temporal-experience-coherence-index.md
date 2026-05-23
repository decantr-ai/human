# Temporal Experience Coherence Index

Status: working draft  
Short name: TECI  
Applies to: H.U.M.A.N. Protocol documents, design reviews, AI-agent workflows, product audits, accessibility reviews, and longitudinal experience evaluation

## 1. Purpose

The Temporal Experience Coherence Index, or TECI, is a draft algorithm for evaluating whether an experience preserves human agency, accessibility, evidence quality, risk control, and social meaning over time.

It does not score people. It scores the experience.

TECI starts from a simple observation:

> A usable experience at one moment can become harmful, inaccessible, misleading, or incoherent later.

That can happen when:

- context changes
- a person switches devices
- attention drops
- an interruption occurs
- an AI agent acts on behalf of a human
- evidence becomes stale
- an error is not repaired
- trust is lost
- accessibility breaks in a later state
- social meaning changes after generated content is sent

TECI treats time as a first-class part of UX.

## 2. Validation Status

TECI is not validated.

It is an unvalidated composite heuristic for structured discussion, design review, research planning, and longitudinal product critique. It should not be presented as a scientific instrument, compliance benchmark, certification method, or replacement for direct human research.

Important caveats:

- Default weights are illustrative until calibrated against real evidence.
- TECI scores should not replace usability research, accessibility testing, standards conformance, legal review, safety analysis, or domain expert judgment.
- The most useful output is not only the number. It is the surfaced stale evidence, unresolved risks, modality gaps, recovery failures, and agency loss over time.
- A high score does not prove that an experience is humane, accessible, safe, ethical, or socially beneficial.
- A low score should be treated as a signal for investigation, not as a complete diagnosis.
- Validation requires empirical comparison against usability studies, accessibility audits, incident reports, support data, longitudinal research, field observations, and expert review.

The algorithm is useful only if it makes hidden temporal failures easier to inspect and argue about. If the score hides uncertainty, compresses politics into math, or gives teams a way to avoid listening to people, it is being misused.

## 3. Core Concept

A H.U.M.A.N. document describes obligations across lenses such as agency, accessibility, modality, risk, evidence, and social meaning.

TECI converts those obligations into a temporal graph:

```text
Human intent -> Experience phases -> Obligations -> Evidence -> Observations -> Risk over time
```

Each obligation is evaluated across time, not only as present or absent.

Example:

```yaml
obligation: "focus returns to invoking control"
lens: accessibility
phase: after
risk: focus_loss
evidence_required:
  - keyboard_test
  - screen_reader_review
```

This obligation is only meaningful after a dialog closes, but it is critical at that moment. TECI captures that timing.

## 4. Inputs

TECI can operate on planned design data, observed product evidence, or both.

### 4.1 Experience Model

From a H.U.M.A.N. document:

- `human_intent`
- `context`
- `modalities`
- `interface`
- `temporal_model`
- `agency`
- `accessibility`
- `evidence`
- `risk`
- `social_meaning`

### 4.2 Obligations

An obligation is any claim about what the experience must preserve.

Examples:

- "User can undo the AI action."
- "Error messages are programmatically associated with fields."
- "The system does not submit without explicit confirmation."
- "The watch handoff has a phone fallback."
- "Generated text is reviewable before sending."

### 4.3 Observations

An observation is evidence collected at a point in time.

Examples:

- accessibility audit result
- usability test note
- automated test result
- design review finding
- user research signal
- production incident
- AI-agent repair
- support ticket
- screen reader verification
- policy approval

Each observation should include:

```yaml
observation:
  id: obs:keyboard-dialog-close
  timestamp: "2026-05-23T12:00:00Z"
  obligation_id: obl:focus-return
  result: pass
  confidence: 0.9
  evidence_type: accessibility_test
```

## 5. Time Model

TECI evaluates an experience over a time window:

```text
T = [t0, t1]
```

The window can represent:

- one user session
- an onboarding lifecycle
- a release cycle
- a longitudinal product audit
- an AI-agent edit and repair loop
- a full service journey

TECI uses phases from the H.U.M.A.N. temporal model:

```text
before
during
after
repeated_use
interruption
recovery
```

Each phase can have a weight.

Example defaults:

| Phase | Weight |
| --- | ---: |
| before | 0.8 |
| during | 1.0 |
| after | 0.9 |
| repeated_use | 0.9 |
| interruption | 1.2 |
| recovery | 1.3 |

Interruption and recovery receive higher weights because many systems fail when the ideal path breaks.

## 6. Obligation Weight

Each obligation gets a weight:

```text
W(o) = L(o) * P(o) * R(o) * E(o)
```

Where:

- `L(o)` is the lens weight
- `P(o)` is the temporal phase weight
- `R(o)` is the risk severity multiplier
- `E(o)` is the evidence authority multiplier

### 6.1 Lens Weight

Example defaults:

| Lens | Weight |
| --- | ---: |
| agency | 1.2 |
| accessibility | 1.2 |
| risk | 1.2 |
| modality | 1.0 |
| evidence | 1.0 |
| human_intent | 1.0 |
| temporal_model | 1.0 |
| interface | 0.9 |
| context | 0.9 |
| social_meaning | 0.9 |

These defaults intentionally privilege agency, accessibility, and risk because they are common failure points in AI-mediated experiences.

### 6.2 Risk Severity Multiplier

| Risk Severity | Multiplier |
| --- | ---: |
| low | 1.0 |
| medium | 1.4 |
| high | 2.0 |
| critical | 3.0 |

### 6.3 Evidence Authority Multiplier

| Evidence Type | Multiplier |
| --- | ---: |
| legal_requirement | 1.5 |
| formal_standard | 1.4 |
| accessibility_test | 1.3 |
| usability_test | 1.3 |
| research_evidence | 1.2 |
| platform_guideline | 1.1 |
| organizational_policy | 1.1 |
| product_decision | 1.0 |
| design_preference | 0.8 |
| hypothesis | 0.6 |

Evidence weighting does not mean lower-weight claims are unimportant. It means their authority is different.

## 7. Evidence Decay

Evidence ages.

A screen reader test from last week is usually stronger than one from two years ago, especially after code or device changes.

TECI uses exponential decay:

```text
D(delta_t, h) = 0.5 ^ (delta_t / h)
```

Where:

- `delta_t` is the age of the observation
- `h` is the half-life for that evidence type

Example half-lives:

| Evidence Type | Default Half-Life |
| --- | ---: |
| automated_test | 30 days |
| accessibility_test | 60 days |
| usability_test | 120 days |
| research_evidence | 365 days |
| platform_guideline | 730 days |
| formal_standard | 1095 days |
| legal_requirement | 1095 days |
| hypothesis | 30 days |

The half-life should shorten when the product changes rapidly.

## 8. Obligation Satisfaction

For each obligation `o` at time `t`, TECI calculates satisfaction:

```text
S(o, t) = max(score(obs) * confidence(obs) * D(age(obs), half_life(obs)))
```

Where observations are linked to obligation `o`.

Suggested observation scores:

| Result | Score |
| --- | ---: |
| pass | 1.0 |
| partial | 0.6 |
| unknown | 0.4 |
| fail | 0.0 |
| contradicted | -0.5 |

The `max` keeps the strongest current evidence, but implementations may use weighted averages if they want multiple evidence streams to matter.

## 9. Time-Weighted Coherence

At time `t`, overall coherence is:

```text
C(t) = sum(W(o) * S(o, t)) / sum(W(o))
```

Only obligations active at time `t` are included.

The final TECI score over window `T` is the area under the coherence curve:

```text
TECI(T) = 100 * integral(C(t), t0, t1) / duration(T)
```

In discrete form:

```text
TECI(T) = 100 * average(C(t_i))
```

This makes time central: a system that works briefly but fails for long recovery periods scores lower than one that remains coherent across the journey.

## 10. Penalties

TECI includes penalties for unresolved time-sensitive harm.

### 10.1 Unresolved Risk Penalty

```text
URP = severity_weight * min(1, unresolved_duration / tolerance_window)
```

Examples:

- A missing accessible name in a critical flow should have a short tolerance window.
- A stale research source may have a longer tolerance window.
- A failed undo path for an AI action may be high severity immediately.

### 10.2 Recovery Latency Penalty

```text
RLP = recovery_weight * min(1, time_to_recovery / expected_recovery_time)
```

This rewards systems that recover quickly from error, interruption, and AI misfires.

### 10.3 Modality Gap Penalty

```text
MGP = required_missing_modalities / required_modalities
```

If a critical task works by pointer but not keyboard, voice, or screen reader when those modalities are required, the score drops.

### 10.4 Agency Loss Penalty

```text
ALP = count(missing_required_controls) / count(required_controls)
```

Required controls may include:

- edit
- undo
- pause
- opt out
- human help
- explicit confirmation
- appeal or recourse

## 11. Final Score

The final score is:

```text
TECI_final = clamp(0, 100, TECI - P)
```

Where:

```text
P = 100 * (a * URP + b * RLP + c * MGP + d * ALP)
```

Example penalty weights:

| Penalty | Symbol | Default |
| --- | --- | ---: |
| unresolved risk | a | 0.35 |
| recovery latency | b | 0.25 |
| modality gap | c | 0.20 |
| agency loss | d | 0.20 |

## 12. Subscores

TECI should report subscores, not only a single number.

Recommended subscores:

| Subscore | Meaning |
| --- | --- |
| Agency Continuity | Human control survives over time. |
| Accessibility Persistence | Accessibility holds across states, phases, and devices. |
| Modality Coverage | Required modalities are supported when needed. |
| Evidence Freshness | Claims have recent and appropriate evidence. |
| Risk Recovery | Risks are mitigated and repaired quickly. |
| Social Integrity | Authorship, trust, and relational effects are not ignored. |
| Temporal Coherence | The experience remains understandable before, during, after, interruption, and recovery. |

## 13. Pseudocode

```text
function calculateTECI(document, observations, window):
  obligations = extractObligations(document)
  timeline = sampleTimeWindow(window)
  coherenceValues = []

  for t in timeline:
    active = obligations.activeAt(t)
    weightedSum = 0
    totalWeight = 0

    for obligation in active:
      weight =
        lensWeight(obligation.lens) *
        phaseWeight(obligation.phase) *
        riskMultiplier(obligation.riskSeverity) *
        evidenceAuthorityMultiplier(obligation.evidenceType)

      satisfaction = strongestCurrentEvidence(obligation, observations, t)

      weightedSum += weight * satisfaction
      totalWeight += weight

    coherenceValues.push(weightedSum / totalWeight)

  baseScore = 100 * average(coherenceValues)

  penalties =
    unresolvedRiskPenalty(document, observations, window) * 0.35 +
    recoveryLatencyPenalty(document, observations, window) * 0.25 +
    modalityGapPenalty(document, observations, window) * 0.20 +
    agencyLossPenalty(document, observations, window) * 0.20

  finalScore = clamp(0, 100, baseScore - (100 * penalties))

  return {
    score: finalScore,
    baseScore,
    penalties,
    subscores: calculateSubscores(document, observations, window),
    staleEvidence: findStaleEvidence(observations, window),
    unresolvedRisks: findUnresolvedRisks(document, observations, window)
  }
```

## 14. Example Interpretation

| TECI Score | Interpretation |
| --- | --- |
| 90-100 | Strong temporal coherence. Obligations are preserved across phases with fresh evidence. |
| 75-89 | Generally coherent. Some stale evidence, modality gaps, or recovery weaknesses may exist. |
| 60-74 | Fragile. The happy path may work, but interruption, accessibility, agency, or evidence continuity is weak. |
| 40-59 | Risky. Important obligations are unproven, stale, or broken across time. |
| 0-39 | Incoherent or harmful. Human agency, access, recovery, or risk controls are failing. |

## 15. Why Time Matters

Without time, a system can appear humane because it supports the initial interaction.

With time, the system must answer harder questions:

- Does the user still have control after AI acts?
- Does accessibility survive loading, error, success, and recovery states?
- Does evidence remain valid after product changes?
- Does a failed action repair quickly?
- Does a cross-device handoff preserve meaning?
- Does social trust degrade after generated content is sent?

TECI makes those questions measurable enough to discuss, compare, and improve.

## 16. Cautions

TECI is not a universal truth machine.

It should not be used to:

- score human worth
- replace qualitative research
- replace accessibility standards
- automate ethical judgment
- create false precision
- hide political or organizational choices behind a number

The score is a decision aid. The explanations, penalties, stale evidence, and unresolved risks matter more than the number.

## 17. Future Extensions

Potential extensions:

- graph-native obligation modeling
- event-stream ingestion
- temporal evidence bundles
- AI-agent action logs
- privacy-preserving longitudinal metrics
- per-domain weighting profiles
- accessibility-specific temporal checks
- visualization of coherence over time

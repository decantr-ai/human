# H.U.M.A.N. Protocol v0.1

**Human Understanding for Multimodal Agentic Navigation**

Status: working draft  
Version: 0.1  
Maintainer: Decantr AI  
License: MIT

## 1. Purpose

H.U.M.A.N. Protocol defines a loose, machine-readable way to describe human-centered experiences across devices, modalities, AI agents, accessibility contexts, and time.

It exists to help humans and AI systems reason about:

- what people are trying to accomplish
- what context shapes the interaction
- what devices and modalities are involved
- what agency the human retains
- what accessibility obligations matter
- what risks must be mitigated
- what evidence supports design decisions
- how the experience changes over time
- how the experience affects relationships between people

## 2. Non-Goals

H.U.M.A.N. Protocol does not replace:

- WCAG
- WAI-ARIA
- ISO 9241
- EN 301 549
- platform human interface guidelines
- accessibility APIs
- local design systems
- project tests
- domain-specific legal or safety requirements

It is not a UI framework, product suite, or compliance standard.

## 3. Core Model

A H.U.M.A.N. document describes an `experience`.

An experience is any mediated situation in which a person pursues a goal through a system, interface, device, environment, AI agent, or social mechanism.

The core model has ten top-level lenses:

1. `experience`
2. `human_intent`
3. `context`
4. `modalities`
5. `interface`
6. `temporal_model`
7. `agency`
8. `accessibility`
9. `evidence`
10. `risk`
11. `social_meaning`

The schema is intentionally loose. A document may include only the fields relevant to the experience being described.

## 4. Experience

`experience` names the interaction and describes its domain, purpose, scope, and stakeholders.

Example:

```yaml
experience:
  name: "Cross-device boarding pass handoff"
  domain: "travel"
  purpose: "Let a traveler move from phone check-in to watch boarding without losing control or context."
  stakeholders:
    - traveler
    - airline
    - airport_staff
```

## 5. Human Intent

`human_intent` captures what the person is trying to do, understand, decide, avoid, or feel.

Use this instead of static personas as the primary human model. The same person may have different needs depending on stress, environment, ability, attention, time pressure, language, and risk.

## 6. Context

`context` captures the conditions around the interaction.

Context may include:

- environment
- device constraints
- social setting
- attention level
- privacy sensitivity
- domain risk
- institutional or organizational constraints
- language and culture
- ability and assistive technology needs

## 7. Modalities

`modalities` describes how input and output happen.

Examples:

- pointer
- touch
- keyboard
- voice
- gaze
- gesture
- haptics
- visual output
- audio output
- captions
- screen reader
- switch control
- spatial movement

Multimodality is not automatically inclusive. Each modality has assumptions and failure modes.

## 8. Interface

`interface` describes the patterns, controls, surfaces, representations, feedback mechanisms, and system boundaries involved.

This layer can reference external systems such as:

- design systems
- component libraries
- platform guidelines
- accessibility standards
- workflow systems
- AI tools
- APIs

## 9. Temporal Model

`temporal_model` describes how the experience unfolds.

Important temporal phases include:

- before
- during
- after
- repeated use
- interruption
- recovery
- error
- escalation
- memory
- trust gained or lost

Interfaces are often documented statically, but experienced temporally.

## 10. Agency

`agency` describes who or what can act, decide, delegate, automate, override, pause, undo, explain, or escalate.

For AI-mediated experiences, agency should include:

- what the AI can do
- what it must not do
- what requires explicit confirmation
- what can be undone
- what is logged
- what is disclosed
- what is handed back to a human

## 11. Accessibility

`accessibility` describes obligations, alternate paths, exclusion risks, and assistive technology expectations.

The protocol should reference external standards rather than paraphrasing them as final authority.

Accessibility is not only a checklist. It is a measure of whether the experience preserves participation across diverse bodies, minds, contexts, devices, languages, and abilities.

## 12. Evidence

`evidence` labels the basis for design claims.

Recommended evidence types:

- `formal_standard`
- `legal_requirement`
- `platform_guideline`
- `research_evidence`
- `usability_test`
- `accessibility_test`
- `organizational_policy`
- `product_decision`
- `design_preference`
- `hypothesis`

Do not treat all claims as equal. A legal requirement, a usability finding, and a design opinion carry different authority.

## 13. Risk

`risk` captures what could go wrong and how harm is mitigated.

Risks may include:

- exclusion
- confusion
- loss of control
- privacy leakage
- manipulation
- hallucinated information
- false confidence
- unsafe automation
- social harm
- inaccessible required task
- degraded trust

## 14. Social Meaning

`social_meaning` describes how an experience affects relationships between people.

AI-mediated systems increasingly shape:

- authorship
- tone
- empathy
- accountability
- labor
- consent
- trust
- social presence
- institutional power

This section is intentionally present because not all UX harm is individual or functional. Some harm is relational.

## 15. Profiles

H.U.M.A.N. documents may be written at different depths.

### Narrative Profile

Human-readable only. Useful for research notes, product briefs, and critiques.

### Structured Profile

Uses the shared YAML/JSON field names. Useful for design reviews, handoffs, and AI context.

### Evidence Profile

Includes evidence types, source references, test obligations, and risk mitigations. Useful for high-risk domains and governance.

### Verifiable Profile

Links obligations to concrete tests, audits, source files, design-system rules, or runtime checks. This profile is future-looking and should not be assumed by default.

## 16. Compatibility

H.U.M.A.N. should be able to reference, not replace:

- WCAG success criteria
- WAI-ARIA patterns
- platform accessibility APIs
- ISO human-centered design concepts
- design tokens
- Open UI controls
- design system components
- provenance specifications
- project-owned policies

## 17. Minimal Document

```yaml
human_protocol_version: "0.1"
experience:
  name: "Example experience"
  purpose: "Describe what this experience helps a person do."
human_intent:
  primary_goal: "Name the human goal."
agency:
  human_control:
    - "Name what the human can control."
accessibility:
  obligations:
    - "Name one accessibility obligation."
risk:
  high_risk:
    - "Name one meaningful risk."
```


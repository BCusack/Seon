# Seon Project Planning & Grant Strategy

Version: 0.1 (Draft)
Owner: Seon Core Team

## Overview
This document consolidates the go-to-market plan and grant funding strategy for Seon. It complements the project vision in `Whitepaper.md` and competitive insights in `Project/Market Research.md`.

## Guiding Principles
- Ambient, ear-first interactions; no consumer smartphone application. The smartphone is not the primary interface.
- Admin dashboard exists solely for pilot operations, analysis, and controls.
- Privacy by design: data minimisation, on-device processing where feasible, encrypted cloud only for heavy compute.
- Low-latency voice loop and context awareness via device mesh, not phone-centric hubs.

## Objectives (12–18 months)
- Validate problem–solution fit for an always-on, privacy-first AI companion.
- Complete a structured technology discovery and feasibility assessment (build‑vs‑buy, latency, privacy, and reliability constraints).
- Build and test an MVP across 2–3 usage domains (wellbeing support, micro-assistance, and context-awareness).
- Secure non-dilutive grant funding to achieve technical milestones and ethical compliance readiness.
- Establish partnerships for hardware prototyping, privacy research, and pilot deployments.
- Assemble a small interdisciplinary core team (ML/infra, full‑stack, human–computer interaction (HCI)/privacy research, embedded/firmware) and an external advisory group (clinical/wellbeing, ethics, hardware).

## Phased Roadmap
- Phase 0: Foundations (Month 0–3)
  - Technical: architecture choices, safety/ethics framework, risk register.
  - Technology discovery: survey candidate stacks (ASR/TTS, on-device inference, LLM orchestration), run feasibility spikes, and produce a decision matrix with trade-offs and costs.
  - Research: user needs discovery, refine personas, pilot protocols.
  - Ops: grant pipeline creation, governance setup, initial letters of support.
  - Team: prioritise hiring/contracting for critical roles and onboard advisors.
  - Gating criteria: architecture option(s) shortlisted with rationale; feasibility spikes demonstrate target latency and privacy posture on representative hardware; build‑vs‑buy decisions recorded; privacy threat model v1; signed letters of support; at least two key advisors engaged; hiring plan approved and critical roles filled or contracted.
- Phase 1: MVP v1 (Month 3–6)
  - Deliverables: ear-clip interaction prototype (mock hardware), admin dashboard app for analysis and controls, core LLM integration, ephemeral context buffer.
  - Gating criteria: live end-to-end demo, privacy threat model v1, 20 pilot users recruited.
- Phase 2: Pilot & Iteration (Month 7–10)
  - Deliverables: memory graph v1, adaptive prompt/policy tuning, sentiment and intent inference.
  - Gating criteria: 100 daily active sessions across pilots, task success rate ≥70% for target flows.
- Phase 3: Scale Readiness (Month 11–18)
  - Deliverables: security review, device-mesh reliability tests, data minimisation compliance pack.
  - Gating criteria: retention ≥40% at 30 days, NPS ≥25, privacy audit pass.

## Grant Strategy (Australia‑focused)
- Targets (Australia):
  - Federal: Accelerating Commercialisation/Industry Growth Program (IGP), CRC‑P (Cooperative Research Centres Projects), ARC Linkage, MRFF/NHMRC (digital health/mental health), Export Market Development Grants (EMDG).
  - CSIRO & National Science: CSIRO Kick‑Start, ON Prime/Accelerate, Data61 collaborations.
  - State: NSW MVP Ventures, QLD Ignite Ideas, Vic Breakthrough Victoria, SA Research/Commercialisation grants.
  - Philanthropy: Paul Ramsay Foundation, Minderoo, Lord Mayor’s Charitable Foundation; privacy/tech foundations where applicable.
  - Industry: cloud credits (AWS/Azure/GCP), hardware prototyping programs, responsible AI funds.
- Approach:
  - Maintain a rolling grant calendar with deadlines, TRL fit, match funding needs, and eligibility.
  - Prepare a reusable application core: problem, innovation, impact, team, work packages, ethics, risk.
  - Build a partner network for letters of support: AU universities (HCI/privacy), CSIRO/Data61, clinics/wellbeing orgs, device makers.
  - Evidence: cite `Whitepaper.md` sections (memory, ethics, comms), and `Project/Market Research.md`.

### Grant Narrative Outline (Reusable)
1. Need & beneficiaries: loneliness, cognitive load, and accessibility gaps.
2. Innovation: always-on context with ephemeral memory and selective retention; device mesh; privacy-first.
3. Evidence base: HCI and affective computing; graph memory; edge networking.
4. Work plan: milestones, work packages, KPIs.
5. Impact: wellbeing outcomes, inclusion-by-design, economic potential.
6. Ethics & Safety: privacy guarantees, red-teaming, human-in-the-loop, data minimisation.
7. Team & Partners: roles, advisors, letters of support.
8. Budget & Sustainability: costs, co-funding, path to revenue.

## Indicative Budget (12–18 months)
- Personnel: $840k–$1.24m (ML/infra, full‑stack, HCI/privacy research, embedded, compliance)
- Cloud/Compute: $160k–$320k (LLM usage, privacy‑preserving infra, monitoring)
- Hardware & Prototyping: $120k–$240k (ear‑clip prototypes, sensors, testing rigs)
- Research & Pilots: $140k–$280k (participant incentives, ethics approvals, analysis)
- Security & Compliance: $80k–$180k (threat modelling, pen test, DPIA/ISO prep)
- Legal & IP: $50k–$120k (contracts, licences, trademarks, counsel)
- Ops & Contingency: $70k–$150k
Total indicative: $1.46m–$2.54m (seek grants to cover 40–70%; remainder via in‑kind/credits/match)

## Work Packages (WPs) & KPIs
- WP0: Technology Discovery
  - Outputs: discovery plan, evaluation matrix (build‑vs‑buy, cost/latency/privacy), feasibility spike reports, recommended architecture baseline.
  - KPIs: latency target on reference device (e.g., <350ms E2E voice loop), on-device/private-by-default coverage %, projected monthly compute cost within budget envelope, decision record completeness.
- WP1: Core Interaction & Safety
  - Outputs: low-latency voice loop, policy guardrails, fallback UX.
  - KPIs: <350ms perceived latency; false-positive/negative safety rates; session completion rate.
- WP2: Memory & Personalisation
  - Outputs: ephemeral buffer, salience-based promotion, knowledge-graph memory v1.
  - KPIs: recall precision@k in pilots; reduction in redundant prompts; user-rated relevance.
- WP3: Device Mesh & Edge Privacy
  - Outputs: mesh comms prototype (QUIC/Matter), local-first data path, audit logs.
  - KPIs: handoff success rate; offline resilience; privacy incident count = 0.
- WP4: Wellbeing Companion Pilots
  - Outputs: study design, ethics approval, 3 pilot cohorts, outcome measures.
  - KPIs: SUS ≥75; WHO-5/PHQ-2 directional improvement; qualitative “felt supported” >70%.
- WP5: Grant Delivery & Governance
  - Outputs: reporting cadence, risk/ethics board, dissemination plan.
  - KPIs: on-time reports; risk burndown; number of talks/papers.

## Risks & Mitigations
- Model privacy leak risk → strict data minimisation, on-device processing, red-team tests.
- Latency/UX degradation → edge inference, caching, graceful degradation.
- Safety/overdependence concerns → boundaries, escalation paths, human oversight.
- Funding timing gaps → diversify targets, prepare bridge options, stage milestones.
- Hardware feasibility → partner with prototyping labs; de-risk with mock devices first.

## Ethics, Legal, and IP
- Ethics: participant consent, opt-out by default for sensitive capture, transparent summaries.
- Legal/Compliance: DPIA, ISO 27001 readiness, clinical oversight for wellbeing features. Australia‑specific: align with the Australian Privacy Principles (APPs) and OAIC Notifiable Data Breaches (NDB) scheme; for human research, obtain HREC approval in line with the NHMRC National Statement.
- IP/Licensing: protect brand and hardware designs; prefer open standards; document data rights.

## Partnerships & Letters of Support (Initial Targets)
 Academic: AU HCI/privacy labs; affective computing groups.
 Industry: ear-wearable OEMs, cloud providers, privacy tooling vendors; CSIRO/Data61 collaboration opportunities.
Advisory group (part‑time/retained):
- Clinical/Wellbeing Advisor: risk boundaries, escalation protocols.
- Ethics/AI Safety Advisor: review policies, red‑team oversight.
- Hardware/EE Advisor: ear‑wearable feasibility and vendor evaluation.

Engagement model and timing:
- Month 0–1: contract advisors; engage 1–2 core engineers; HCI/privacy researcher part‑time.
- Month 2–3: expand to full core team; kick off pilots preparation.
- Use contractors/partners where faster, convert to FTE as funding permits.

## Next Actions
- Build grant calendar and assign owners per opportunity.
- Draft the reusable narrative (sections above) and a 2-page concept note.
- Identify pilot partners and request letters of support.
- Prepare ethics pre-review checklist for pilots.

---
This document is a living plan; updates should be cross-referenced in `Whitepaper.md` and `Extended/` notes.

Note: All monetary amounts are in AUD.

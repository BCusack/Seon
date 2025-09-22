# Seon Project Planning & Grant Strategy

Version: 0.1 (Draft)
Owner: Seon Core Team

## Overview
This document consolidates the go-to-market plan and grant funding strategy for Seon. It complements the project vision in `Whitepaper.md` and competitive insights in `Project/Market Research.md`.

## Objectives (12–18 months)
- Validate problem–solution fit for an always-on, privacy-first AI companion.
- Build and test an MVP across 2–3 usage domains (wellbeing support, micro-assistance, and context-awareness).
- Secure non-dilutive grant funding to achieve technical milestones and ethical compliance readiness.
- Establish partnerships for hardware prototyping, privacy research, and pilot deployments.

## Phased Roadmap
- Phase 0: Foundations (Month 0–2)
  - Technical: architecture choices, safety/ethics framework, risk register.
  - Research: user needs discovery, refine personas, pilot protocols.
  - Ops: grant pipeline creation, governance setup, initial letters of support.
- Phase 1: MVP v1 (Month 3–6)
  - Deliverables: ear-clip interaction prototype (mock hardware), mobile companion app, core LLM integration, ephemeral context buffer.
  - Gating criteria: live end-to-end demo, privacy threat model v1, 20 pilot users recruited.
- Phase 2: Pilot & Iteration (Month 7–10)
  - Deliverables: memory graph v1, adaptive prompt/policy tuning, sentiment and intent inference.
  - Gating criteria: 100 daily active sessions across pilots, task success rate ≥70% for target flows.
- Phase 3: Scale Readiness (Month 11–18)
  - Deliverables: security review, device-mesh reliability tests, data minimisation compliance pack.
  - Gating criteria: retention ≥40% at 30 days, NPS ≥25, privacy audit pass.

## Grant Strategy
- Targets (examples; to be tailored by region):
  - National innovation agencies (e.g., UKRI Innovate UK Smart Grants; EU EIC Pathfinder/Transition; US NSF SBIR/STTR).
  - Foundations focused on digital health, wellbeing, and privacy (e.g., Wellcome Trust; Mozilla; Sloan; Omidyar; OpenAI Community Fund-equivalents where applicable).
  - Industry-aligned programmes (cloud credits, hardware incubators, responsible AI funds).
- Approach:
  - Maintain a rolling grant calendar with deadlines, TRL fit, match funding needs, and eligibility.
  - Prepare a reusable application core: problem, innovation, impact, team, work packages, ethics, risk.
  - Build a partner network for letters of support: universities (HCI/Privacy), clinics/wellbeing orgs, device makers.
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
- Personnel: £420k–£620k (ML/infra, full-stack, product, research, compliance)
- Cloud/Compute: £80k–£160k (LLM usage, privacy-preserving infra, monitoring)
- Hardware & Prototyping: £60k–£120k (ear-clip prototypes, sensors, testing rigs)
- Research & Pilots: £70k–£140k (participant incentives, ethics approvals, analysis)
- Security & Compliance: £40k–£90k (threat modelling, pen test, DPIA/ISO prep)
- Legal & IP: £25k–£60k (contracts, licenses, trademarks, counsel)
- Ops & Contingency: £35k–£75k
Total indicative: £730k–£1.27m (seek grants to cover 40–70%; remainder via in-kind/credits/match)

## Work Packages (WPs) & KPIs
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
- Legal/Compliance: DPIA, ISO 27001 readiness, clinical oversight for wellbeing features.
- IP/Licensing: protect brand and hardware designs; prefer open standards; document data rights.

## Partnerships & Letters of Support (Initial Targets)
- Academic: HCI/privacy labs; affective computing groups.
- Clinical/Wellbeing: mental health charities, digital therapeutics clinics.
- Industry: ear-wearable OEMs, cloud providers, privacy tooling vendors.

## Next Actions
- Build grant calendar and assign owners per opportunity.
- Draft the reusable narrative (sections above) and a 2-page concept note.
- Identify pilot partners and request letters of support.
- Prepare ethics pre-review checklist for pilots.

---
This document is a living plan; updates should be cross-referenced in `Whitepaper.md` and `Extended/` notes.

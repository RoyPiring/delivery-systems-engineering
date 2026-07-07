<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# AI-Powered Executive Review System

**Project Link:** [View Project](https://nextwork.ai/projects/8999e472-af4d-4a9d-a01b-575f64f4692f)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](https://nextwork.ai/refreshed_maroon_timid_jujube/uploads/8999e472-af4d-4a9d-a01b-575f64f4692f_iz70cxrk)

## Building an AI-Native Executive Review Operating System

### Project vision and goals

This project builds an AI-native executive review system for portfolio reporting. The system was built around Claude Code, Linear access, OKR tracking, Marp deck generation, a metric-definition ledger, and a local cadence structure.

The goal was to create an operating model where executive metrics could be collected, checked, challenged, and presented without losing traceability. The system focused on making every number defensible before it reached an MBR or QBR deck.

A key constraint surfaced early. The workspace had a local cadence file, but no recurring calendar events had actually been created. That mattered because the review system could describe the cadence, but the calendar-based workflow still needed an explicit setup step before it could run as a real standing process.

![Image](https://nextwork.ai/refreshed_maroon_timid_jujube/uploads/8999e472-af4d-4a9d-a01b-575f64f4692f_n3putxma)

### Project structure and calendar setup

The project directory was created as hold-the-room/. It included .claude/agents/, decks/, ledger/, cadence/, and docs/, along with package.json, .gitignore, and a local Marp CLI installed under node_modules/.

The ledger/ folder held three CSV files, while cadence/ held cadence-calendar.csv. That gave the build a local structure for metric governance, review cadence planning, and deck generation.

No recurring calendar events were created. The cadence work existed as a CSV starter file inside the workspace, not as live Google Calendar events. Any real MBR or QBR calendar automation would require a separate explicit setup step outside the local project workspace.

## Wiring the Environment and Metric Governance Foundation

### Environment setup overview

In this step, I configured the foundation for the executive review system. I verified access to Claude Code, Linear, and the OKR tracking tool so the workflow could connect review content to actual portfolio and goal data.

I installed the Marp CLI and initialized the project directory with the required subdirectories: .claude/agents, decks, ledger, cadence, and docs. This gave the system a clear separation between agents, presentation outputs, metric records, cadence files, and documentation.

I also created the metric-definition ledger structure with tabs for Definitions, Decision Log, and Dispute Record. The cadence setup remained local to the workspace through the CSV starter file, not live recurring calendar events.

![Image](https://nextwork.ai/refreshed_maroon_timid_jujube/uploads/8999e472-af4d-4a9d-a01b-575f64f4692f_bbf2h5uf)

### The ledger as single source of truth

The metric-definition ledger was designed as the single source of truth for every number used in the executive review decks. Each metric needed one written definition, owner, source system, target, threshold, and calculation method.

That mattered because executive reviews break down when the same number means different things to different people. When a metric is challenged in an MBR or QBR, the team should pull the ratified definition instead of debating from memory.

The ledger also kept the governance trail. The Decision Log captured decisions made during the review process, and the Dispute Record captured metric challenges and their resolution path so the operating rhythm stayed auditable over time.

## Designing the Agent Architecture

### Architecture and agent roster design

In this step, I formalized the architecture for the review system by defining 10 specialized Claude agents. Each agent had a scoped role so the system could separate collection, reconciliation, narrative building, deck generation, dispute handling, and executive preparation.

I also documented the architecture through ADRs, a technical topology, and an implementation roadmap. That kept the agent design grounded before the orchestration layers were built.

The design mattered because executive reporting needs controlled handoffs. A collector should not certify its own data, a narrator should not rewrite metric definitions, and a deck builder should not let unverified numbers reach the room.

### Verify-then-merge for metric integrity

Verify-then-merge placed an independent metric reconciler between collection and narrative. Every number returned by a collector had to be checked against the ledger definition, source system, and threshold bounds before it could enter a deck.

The reconciler was read-only. It could only PASS or FLAG a metric, and it could not fix discrepancies itself. That prevented the system from silently changing a number to make it fit the deck.

When a metric was mismatched or orphaned, the system stopped it and routed the issue to a human operator for ratification. That kept executive-facing numbers defensible when challenged in the room.

![Image](https://nextwork.ai/refreshed_maroon_timid_jujube/uploads/8999e472-af4d-4a9d-a01b-575f64f4692f_074cno7s)

![Image](https://nextwork.ai/refreshed_maroon_timid_jujube/uploads/8999e472-af4d-4a9d-a01b-575f64f4692f_6wdi1ybz)

## Designing the Operating Rhythm and Cadence

### Cadence design overview

In this step, I worked on the metric tree and the supporting ledger. The goal was to map key outcomes, delivery metrics, and leading indicators into a three-tier structure using Mermaid.

I also planned to populate the metric-definition ledger with at least eight metrics from the Linear workspace so the system could trace each metric back to a real source. That traceability mattered because the ledger was meant to govern live review content, not just sample data.

The cadence design also covered the MBR and QBR rhythm, n8n automation triggers, and a RACI matrix. The purpose was to make sure every activity and data source had one accountable human owner.

![Image](https://nextwork.ai/refreshed_maroon_timid_jujube/uploads/8999e472-af4d-4a9d-a01b-575f64f4692f_9oabonng)

### Human ownership of metric definitions

Metric ownership had to stay with a human because accountability cannot sit with a tool. When a number is challenged in the room, a person has to defend the definition, approve changes, and answer for the result.

ADR-002 treated ratification as a human act. The owner signed off that the definition and calculation were correct, which made the number trustworthy.

Agents stayed read-only for collection and reconciliation. Naming an agent as the owner would let the system self-certify its own outputs, which would break the governance separation the ledger was built to protect.

### n8n automation triggers

I documented four automation triggers in cadence/n8n-workflow-spec.md: Input Deadline Reached, Data Freeze Confirmed, Deck Compiled, and Review Complete.

The first trigger started when a calendar reminder fired. The reminder was defined as 2 business days before an MBR or 5 business days before a QBR, and its action was to notify program owners to lock their status in Linear.

That trigger depended on an Executive Review Cadence calendar existing. At this point in the build, that calendar did not exist yet. The cadence was still represented by the local CSV, so the n8n workflow remained a specification rather than a deployed automation.

## Assembling the Agent-Powered Review Kit

### Review kit assembly overview

In this step, I built the core review kit around parallel metric collection, reconciliation, and deck generation. Metric-collector agents fanned out to retrieve project data from Linear.

The collected values were then checked against the metric-definition ledger. That verification step protected the deck from carrying values that did not match a ratified definition, source system, or calculation method.

After reconciliation, Marp was used to compile the MBR and QBR decks. The system also generated stakeholder pre-briefs and an executive summary so leaders could enter the review with context instead of reading the numbers cold.

### Metric reconciliation in action

The metric reconciler flagged that the collected values did not reconcile against the Definitions tab. The problems included source-system mismatches, disconnected sources, null or uncomputable values, and orphan metrics with no matching definition row.

I did not resolve those issues by forcing a sign-off. The definitions were still DRAFT placeholders, with owners, targets, and calculation methods not finalized. Because there was no ratified definition, there was nothing defensible to approve.

The real resolution remained a future build step. The ledger definitions needed real source systems, named owners, and agreed targets. After that, collection could be re-run and each human owner could ratify the rows, giving Last Ratified a real date.

![Image](https://nextwork.ai/refreshed_maroon_timid_jujube/uploads/8999e472-af4d-4a9d-a01b-575f64f4692f_579d8533)

## Holding the Room: Live Dispute and Decision Governance

### Live review and dispute overview

I completed a live dispute rehearsal against the QBR deck. The purpose was to test whether the review system could handle a challenged metric without bluffing or losing the room.

The challenged metric was traced back to the ledger, where the issue became clear. The metric was not fully ratified, and its calculation method had a real weakness.

After the rehearsal, I logged the decision trail and created closing readouts for the executive sponsor and program teams. I also documented the standing review cadence and captured the retrospective lessons.

### Reconciling the challenged metric

I did not confirm the disputed metric as correct. The challenge was valid, so I acknowledged the gap during the review.

MET-O1 used an unweighted average of key results, which meant a trivial KR counted the same as a critical KR. The actuals were also unratified DRAFT values with no verified source.

I proposed a definition update in the room: move MET-O1 to weighted KR attainment and name a source of record before ratification. I logged the exchange as DR-001 in the Dispute Record tab. The fix was proposed, not applied, because changing and ratifying the metric required the human owner.

![Image](https://nextwork.ai/refreshed_maroon_timid_jujube/uploads/8999e472-af4d-4a9d-a01b-575f64f4692f_10o1h82p)

### 90-day adoption path for the executive sponsor

The executive readout defined a 90-day adoption path in docs/readout-executive.md. Day 1 focused on running the first MBR on schedule against live portfolio data.

Day 30 focused on making the cadence stand on its own. The MBR had to repeat without operator heroics, and the ledger had to be shared with metric owners.

Day 90 focused on running the first QBR with the sponsor and having the metric-definition ledger accepted as the organizational source of truth.

## Secret Mission: Pre-Mortem Agent for Proactive Dispute Defense

### Identifying vulnerable metrics before the room

The pre-mortem agent identified three vulnerable QBR outcome metrics before the room: MET-O1, MET-O2, and MET-O3. These covered OKR Attainment %, Portfolio Value Delivered, and Customer Commitments Met.

MET-O1 ranked highest because it triggered three criteria: unstable or unratified definition, manual-entry data quality, and prior dispute history through DR-001. MET-O2 and MET-O3 each triggered two criteria because both had unratified definitions and broken or incomplete data sources.

None of the metrics triggered the large period-over-period change criterion because there was no prior-period data to compare against yet.

### Embedding the pre-mortem in the standing cadence

I added the pre-mortem to both the MBR and QBR sections in cadence-spec.md. It became the final preparation step after data freeze, collection, reconciliation, narrative, and deck compilation.

The cadence required operator sign-off on the prep cards before the review could proceed. That made the pre-mortem a required control instead of an optional review exercise.

I also added Trigger 5 in n8n-workflow-spec.md. The trigger fired after deck compilation and pre-mortem completion, then dispatched the three prep cards to the operator. The review could not proceed until receipt was confirmed. This was still specification-only, not deployed n8n automation.

## Reflections and Lessons Learned

### Tools and concepts mastered

The key tools I used included Claude Code for orchestrating the agent swarm, n8n for cadence automation design, Marp CLI for deck generation, and a metric-definition ledger as the source of truth.

The main concepts I learned included designing a standing MBR/QBR operating system, using fan-out and verify-then-merge orchestration, and building a pre-mortem agent to identify metric disputes before they reached the boardroom.

The larger lesson was that executive reporting needs a governance system, not just a slide deck. Metrics must have owners, definitions, sources, reconciliation checks, and a dispute path before they can hold up under scrutiny.

### Time and challenges

This build took me approximately 60 minutes. That time covered the project structure, ledger setup, agent architecture, cadence design, review kit assembly, dispute rehearsal, and pre-mortem specification.

The hardest part was sequencing the pre-mortem agent as a hard gate in the cadence. The system had to make sure the review paused until the operator reviewed the prep cards.

The n8n workflow remained a specification rather than a deployed workflow. That distinction mattered because a documented trigger is not the same as a live automation.

### Looking ahead

I completed this build to create a systematic, AI-orchestrated executive review process where every metric could be traced to a validated source of truth.

The metric ledger, cadence triggers, and pre-mortem agent helped show how to defend data integrity before stakeholder scrutiny begins. The next step is to automate cross-functional reporting workflows so review preparation can become more repeatable across teams and operating rhythms.

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/8999e472-af4d-4a9d-a01b-575f64f4692f)*

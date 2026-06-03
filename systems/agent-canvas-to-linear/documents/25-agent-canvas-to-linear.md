<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# 25 AI Agents: Excalidraw to Linear

**Project Link:** [View Project](https://learn.nextwork.org/projects/9ecc857b-2b30-4dd6-8d53-98cb11b97c0c)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](https://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/9ecc857b-2b30-4dd6-8d53-98cb11b97c0c_ir3ua1sa)

## The Vision: Building a Canvas-Driven Agentic Delivery System

### What this system is and why it matters

I'm building a 25-agent pipeline that uses Obsidian as a local-first vault to transform Excalidraw canvases into stakeholder-ready deliverables and Linear work items. The objective is to create a repeatable workflow that moves ideas from visual brainstorming into structured execution without losing context, traceability, or implementation intent.

This project focuses on closing the gap between ideation and delivery through a client-agnostic architecture built around shared files, governance standards, and AI-assisted orchestration. By distributing responsibilities across specialized agents, the system can process strategic, tactical, and operational inputs while maintaining a consistent output format. The result is a workflow where concepts captured on a canvas become documented decisions, actionable plans, and development-ready tickets that can move directly into execution.

## Setting Up the Toolchain and Workspace

### Step goals and approach

I verified the Node.js environment, confirmed Claude Desktop functionality, validated the Obsidian Excalidraw plugin, and enabled Dataview, Templater, and Git within the workspace. I also created the IdeationCouncil vault and confirmed it could be accessed by multiple AI clients to support portability across different tools and execution environments.

Establishing the workspace before agent development ensured the vault could serve as a shared operational backbone rather than being tied to a specific model or platform. By standardizing plugins, filesystem access, and project structure early in the process, the environment became a stable foundation for agent orchestration, documentation management, and future workflow expansion.

![Image](https://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/9ecc857b-2b30-4dd6-8d53-98cb11b97c0c_c4k38ci8)

### AI clients confirmed for portability

The two AI clients confirmed available are Claude (Claude Code 2.1.123) and Codex (codex-cli 0.122.0). Both were verified on the system path and confirmed operational.

These clients serve as interchangeable execution engines connected through MCP servers to the Obsidian vault and Linear workspace. Verifying multiple clients at the beginning of the project supported the broader design goal of preventing vendor lock-in and ensuring that workflows remain functional regardless of which model is used to execute them.

## Designing the System Before Building It

### ADRs, Mermaid diagrams, and implementation plan

Before implementation, I defined the system architecture through Architecture Decision Records, Mermaid diagrams, and a phased implementation plan. This planning process documented key decisions around vault design, orchestration patterns, storage strategy, version control, and portability requirements.

Creating architectural documentation before deployment provided a structured framework for future development and reduced ambiguity across the system. The diagrams established a shared understanding of component relationships, while the implementation plan identified technical dependencies and sequencing requirements necessary to maintain consistency throughout the build process.

![Image](https://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/9ecc857b-2b30-4dd6-8d53-98cb11b97c0c_67monz32)

### ADR-003: Client-agnostic design decision

ADR-003 formalized the decision to define agents as plain Markdown templates rather than proprietary client-specific formats. This approach allows any compatible AI client to read and execute the same agent definitions without modification.

This decision is significant because it separates business logic from model selection. The vault becomes the source of truth while AI clients become interchangeable execution layers. As a result, adding, replacing, or testing new models does not require rebuilding the agent ecosystem, preserving long-term portability and reducing operational dependency on any single vendor.

## Wiring MCP Servers and Configuring Linear

### Connecting AI clients to the vault and Linear

This phase established the connectivity layer that links AI clients, the Obsidian vault, and Linear. Project-level MCP configurations were created for development environments, Claude Desktop received system-level MCP configuration, and the Linear workspace was initialized with teams, initiatives, and API access required for automated ticket management.

Building the connectivity layer early ensured agents could interact with both knowledge assets and delivery systems through a consistent interface. This architecture allows planning outputs, documentation, and execution artifacts to flow between tools without requiring client-specific integrations.

![Image](https://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/9ecc857b-2b30-4dd6-8d53-98cb11b97c0c_te0xalgd)

### How project-level configs enable client-agnostic portability

Project-level MCP configurations stored within the vault allow compatible AI clients to automatically discover the same filesystem and Linear integrations when the workspace is opened.

This design moves infrastructure ownership from the AI client into the project itself. Because the configuration travels with the vault, the environment can be cloned onto another machine and immediately provide identical connectivity. The system therefore depends on the shared MCP protocol and workspace configuration rather than the capabilities of a specific AI product.

## Deploying 25 Agents Across 5 Teams

### Generating and validating the full agent roster

The project-level MCP configuration supports a client-agnostic architecture by standardizing how AI environments connect to shared resources. Workspace-specific configuration files provide a common interface for filesystem access and Linear integration regardless of which editor or AI client is being used.

This approach ensures architectural consistency across environments and simplifies operational maintenance. New clients can join the workflow by reading existing configuration files rather than requiring custom integrations, preserving portability as the ecosystem evolves.

![Image](https://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/9ecc857b-2b30-4dd6-8d53-98cb11b97c0c_cdpg93dh)

### Team-to-subsystem mapping

The system is organized into functional teams that mirror major stages of the delivery pipeline. Team C serves as the Visual Ideation Engine, Teams A and B form the Intelligence Layer for research and adversarial review, Team D performs synthesis, and Team E operates as the delivery bridge into execution systems.

The Council Lead functions as the orchestration layer, routing work through each stage and enforcing review gates before progression. This structure creates clear separation of responsibilities while maintaining traceability across the entire workflow from ideation through delivery.

### Proving portability with a second AI client

The initial agent framework was built using Claude and then validated using Codex as a secondary execution engine. Codex independently interpreted the orchestration model and correctly identified the workflow sequence from visual ideation through delivery.

Gemini produced the same interpretation when tested against the shared vault artifacts. Independent agreement across multiple vendors demonstrated that workflow logic resides within the vault structure and documentation rather than within a specific model implementation, validating the client-agnostic design objective.

## Building Excalidraw Canvas Templates and Governance

### Creating the brainstorming surfaces and config layer

This phase focused on developing reusable Excalidraw canvases, governance schemas, and stakeholder deliverable templates that establish consistency across all future council sessions.

The goal was to ensure that brainstorming, planning, review, and delivery activities follow repeatable patterns regardless of the topic being analyzed. Standardized templates reduce variation between cycles while raising traceability and output quality across the broader agent ecosystem.

![Image](https://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/9ecc857b-2b30-4dd6-8d53-98cb11b97c0c_0h9qvfsc)

### What governance configs control and why they matter

The governance layer defines operational rules, quality thresholds, system identity, review cadence, and execution procedures. Files such as brainstorm-bible.yaml, cycle.yaml, delivery-systems-identity.yaml, drift-detection.yaml, and supporting playbooks establish the standards that guide every council session.

These controls prevent degradation over repeated execution cycles. Without governance, outputs can drift, quality requirements may become inconsistent, and review processes can weaken over time. The configuration layer transforms the workflow from a one-time automation into a repeatable operating system capable of maintaining standards across large numbers of iterations.

## Running 3 Real-World Council Sessions

### Cloud modernization, newsletter launch, and AI transformation

To validate the architecture, I executed three separate council sessions covering cloud modernization, newsletter strategy, and AI-native transformation planning. Each session produced different artifacts while using the same underlying governance model and orchestration framework.

Running multiple use cases provided evidence that the system could support diverse business scenarios without requiring structural changes. The sessions also served as practical validation that outputs remained consistent despite differences in subject matter and participating AI clients.

### Multi-client execution with the vault as handoff layer

The three sessions were executed using Claude, Gemini, and Codex in different combinations. Artifacts were exchanged through the shared vault using Markdown files, allowing one client to continue work initiated by another without additional configuration.

This demonstrated a key architectural objective: the vault owns state, not the AI client. Because all context, documentation, and workflow definitions exist in shared files, outputs can move between vendors while preserving continuity. Linear received the same structured deliverables regardless of which model generated them.

## Shipping to Linear and Validating All Deliverables

### Standards gate, ticket creation, and final artifact review

The final phase focused on validating deliverables, executing standards-gate reviews, confirming ticket integrity, and ensuring outputs satisfied established system requirements.

This review process provided operational assurance that generated artifacts maintained quality standards before being considered complete. It also verified that governance mechanisms functioned correctly across all council sessions.

![Image](https://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/9ecc857b-2b30-4dd6-8d53-98cb11b97c0c_7vjimsxh)

### Total tickets created and orphan verification

I created 30 project tickets across the three sessions under a single Q3 2026 Delivery Pipeline Initiative. Session A generated 12 tickets, Session B generated 8 tickets, and Session C generated 10 tickets.

Verification was performed using Linear MCP issue listings and project associations. All 30 session-generated tickets were linked to projects and successfully rolled up to the initiative. The only unlinked issues identified were Linear's default onboarding tickets, which were unrelated to project execution and flagged separately for cleanup.

![Image](https://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/9ecc857b-2b30-4dd6-8d53-98cb11b97c0c_jfpe3tp5)

## 3-Model Triangulation and System Scorecard

### Adversarial review results and final evaluation score

The final evaluation process combined findings from Codex, Claude, and Gemini to create a multi-model validation workflow. Codex performed structured attack reviews and spot checks, Claude validated findings against source artifacts, and Gemini participated in earlier cross-validation activities.

This triangulation process reduced the risk of single-model bias while raising confidence in the final outputs. Findings generated during review directly informed remediation work and strengthened documentation quality, traceability, and standards compliance.

The final system evaluation score was 98/100, with nineteen requirements fully passing and one receiving a partial assessment based on stakeholder-deliverable maturity. The score reflects the effectiveness of the review process while acknowledging opportunities for refinement identified during adversarial analysis.

## Reflections and Key Takeaways

### Tools and concepts mastered

The primary tools used throughout the project were Obsidian, Excalidraw, Linear, Claude Desktop MCP, Codex, and Gemini. Together, these tools enabled the creation of a portable workflow capable of converting visual concepts into structured execution artifacts.

One of the most valuable lessons was understanding how architectural separation enables portability. By placing workflow logic inside shared files rather than embedding it within a specific AI platform, the system remains flexible and resilient as models evolve. I also gained practical experience implementing adversarial review cycles, governance-driven quality controls, and automated delivery pipelines that convert visual planning into INVEST-compliant work items.

### Time to complete and biggest challenges

This project took approximately two hours to complete. The most challenging aspect was learning the Linear interface and configuring initiatives in a way that supported the desired workflow structure.

The review process highlighted the strengths of using multiple models for validation. Codex surfaced a broad set of findings, while Claude was effective at identifying contradictions and validating implementation details. Together, they provided complementary perspectives that strengthened overall system quality.

I completed this project to learn how to build a client-agnostic AI agent pipeline that connects visual ideation in Excalidraw with structured execution in Linear. By using Obsidian as the central vault and combining governance controls with multi-model reviews, I created a workflow that maintains traceability, enforces standards, and supports repeatable delivery across different AI platforms.

Another area I want to explore is observability for autonomous agent systems. Specifically, I am interested in learning how to monitor workflow execution, detect drift, visualize agent interactions, and build dashboards that provide operational insight into long-running autonomous processes. This would further strengthen governance and reliability as agent ecosystems become larger and more complex.

---

*Built with [NextWork](https://learn.nextwork.org) - [View this project](https://learn.nextwork.org/projects/9ecc857b-2b30-4dd6-8d53-98cb11b97c0c)*

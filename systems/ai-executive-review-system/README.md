# AI-Powered Executive Review System

> Inside the [Delivery Systems Engineering](../../README.md) portfolio · *Multi-project, multi-team customer engagements built to scale from one client to many.*

## Overview

This project builds an AI-native executive review system for portfolio reporting. The system was built around Claude Code, Linear access, OKR tracking, Marp deck generation, a metric-definition ledger, and a local cadence structure.

The goal was to create an operating model where executive metrics could be collected, checked, challenged, and presented without losing traceability. The system focused on making every number defensible before it reached an MBR or QBR deck.

A key constraint surfaced early. The workspace had a local cadence file, but no recurring calendar events had actually been created. That mattered because the review system could describe the cadence, but the calendar-based workflow still needed an explicit setup step before it could run as a real standing process.

The architecture is built across **7 phases**, anchored by **Building an AI-Native Executive Review Operating System** on the input side and **Secret Mission: Pre-Mortem Agent for Proactive Dispute Defense** at the end. Each phase is listed in the Implementation section below.

## Architecture

```mermaid
---
title: AI-Powered Executive Review System
---
%%{init: {"theme":"base","themeVariables": {"primaryColor":"#1B4332","primaryTextColor":"#F4D03F","primaryBorderColor":"#F4D03F","secondaryColor":"#264653","tertiaryColor":"#2F5233","lineColor":"#F4D03F","fontFamily":"ui-monospace, SFMono-Regular, Menlo, Consolas, monospace","fontSize":"13px"}}}%%
flowchart LR
    classDef datastore fill:#264653,stroke:#F4D03F,stroke-width:2px,color:#FFFFFF
    classDef service fill:#1B4332,stroke:#F4D03F,stroke-width:2px,color:#F4D03F
    classDef event fill:#7B42BC,stroke:#F4D03F,stroke-width:2px,color:#FFFFFF
    classDef io fill:#0d1117,stroke:#F4D03F,stroke-width:1.5px,color:#F4D03F,font-style:italic

    subgraph Env["Environment and Access"]
        ClaudeCode(["Claude Code orchestrator"])
        Linear(["Linear workspace"])
        OKRTool(["OKR tracking tool"])
        MarpCLI(["local Marp CLI"])
    end

    subgraph Workspace["hold-the-room Workspace"]
        AgentsDir[(".claude/agents")]
        DecksDir[("decks/")]
        LedgerDir[("ledger/ (3 CSV)")]
        CadenceCsv[("cadence/cadence-calendar.csv")]
        DocsDir[("docs/")]
    end

    subgraph Ledger["Metric-Definition Ledger (source of truth)"]
        Definitions[/"Definitions: owner, source, target, threshold"/]
        DecisionLog[("Decision Log")]
        DisputeRecord[("Dispute Record")]
    end

    subgraph Roster["Ten Specialized Claude Agents"]
        Collector(["metric collector"])
        Reconciler(["metric reconciler"])
        Narrator(["narrative builder"])
        DeckBuilder(["deck generator"])
        DisputeAgent(["dispute handler"])
        ExecPrep(["executive prep"])
    end

    subgraph Verify["Verify-then-Merge"]
        ReconcileGate{{"read-only reconcile: PASS or FLAG"}}
        HumanRatify{{"human ratification"}}
    end

    subgraph Cadence["Operating Rhythm and Cadence"]
        MetricTree[/"three-tier metric tree"/]
        MbrQbr[/"MBR and QBR rhythm"/]
        Raci[/"RACI: one accountable owner"/]
    end

    subgraph N8n["n8n Triggers (specification only)"]
        T1[/"T1: input deadline reached"/]
        T2[/"T2: data freeze confirmed"/]
        T3[/"T3: deck compiled"/]
        T4[/"T4: review complete"/]
        T5[/"T5: pre-mortem dispatch"/]
    end

    subgraph Kit["Agent-Powered Review Kit"]
        CollectFanout{{"metric-collector fan-out"}}
        MarpDecks[("MBR and QBR decks")]
        PreBriefs[("stakeholder pre-briefs")]
        ExecSummary[("executive summary")]
    end

    subgraph Room["Holding the Room: Dispute Governance"]
        LiveRehearsal{{"live dispute rehearsal"}}
        ChallengedMetric[/"MET-O1 challenged"/]
        DR001[("DR-001 logged")]
        WeightedKR[/"proposed: weighted KR attainment"/]
    end

    subgraph PreMortem["Secret Mission: Pre-Mortem Agent"]
        PreMortemAgent(["pre-mortem agent"])
        Vuln3[/"vulnerable: MET-O1, O2, O3"/]
        Criteria[/"risk criteria trigger count"/]
        PrepCards[("three prep cards")]
        OperatorSignoff{{"operator sign-off gate"}}
    end

    subgraph Adoption["90-Day Adoption Path"]
        Day1[/"Day 1: first MBR live"/]
        Day30[/"Day 30: cadence self-sustains"/]
        Day90[/"Day 90: ledger is source of truth"/]
    end

    ClaudeCode -- "governs" --> Roster
    ClaudeCode -- "scaffolds" --> Workspace
    MarpCLI -- "installed under" --> DecksDir
    LedgerDir -- "holds" --> Definitions
    LedgerDir -- "holds" --> DecisionLog
    LedgerDir -- "holds" --> DisputeRecord

    Linear -- "project data to" --> Collector
    OKRTool -- "goal data to" --> Collector
    Collector -- "fans out via" --> CollectFanout
    CollectFanout -- "values to" --> Reconciler
    Reconciler -- "checks against" --> Definitions
    Reconciler -- "runs" --> ReconcileGate
    ReconcileGate -- "FLAG routes to" --> HumanRatify
    ReconcileGate -- "PASS enters" --> Narrator
    HumanRatify -- "signs" --> Definitions

    Narrator -- "hands to" --> DeckBuilder
    DeckBuilder -- "compiles" --> MarpDecks
    DeckBuilder -- "compiles" --> PreBriefs
    ExecPrep -- "writes" --> ExecSummary
    MetricTree -- "structures" --> Definitions
    MbrQbr -- "schedules" --> CollectFanout
    Raci -- "assigns owner in" --> Definitions

    T1 -- "reminder locks status in" --> Linear
    T2 -- "freezes" --> CollectFanout
    T3 -- "fires after" --> MarpDecks
    T4 -- "closes" --> MbrQbr
    CadenceCsv -- "starter for" --> MbrQbr

    LiveRehearsal -- "traces" --> ChallengedMetric
    ChallengedMetric -- "roots in" --> Definitions
    ChallengedMetric -- "logged as" --> DR001
    DR001 -- "recorded in" --> DisputeRecord
    ChallengedMetric -- "fix" --> WeightedKR
    WeightedKR -- "needs" --> HumanRatify

    PreMortemAgent -- "flags" --> Vuln3
    Criteria -- "ranks" --> Vuln3
    Vuln3 -- "cites" --> DR001
    PreMortemAgent -- "emits" --> PrepCards
    PrepCards -- "gated by" --> OperatorSignoff
    T5 -- "dispatches" --> PrepCards
    OperatorSignoff -- "unblocks" --> MbrQbr
    DisputeAgent -- "manages" --> DisputeRecord

    ExecSummary -- "opens" --> Day1
    Day1 -- "matures to" --> Day30
    Day30 -- "matures to" --> Day90
    Day90 -- "ratifies" --> Ledger

    class AgentsDir,DecksDir,LedgerDir,CadenceCsv,DocsDir,DecisionLog,DisputeRecord,MarpDecks,PreBriefs,ExecSummary,DR001,PrepCards datastore
    class ClaudeCode,Linear,OKRTool,MarpCLI,Collector,Reconciler,Narrator,DeckBuilder,DisputeAgent,ExecPrep,PreMortemAgent service
    class ReconcileGate,HumanRatify,CollectFanout,LiveRehearsal,OperatorSignoff event
    class Definitions,MetricTree,MbrQbr,Raci,T1,T2,T3,T4,T5,ChallengedMetric,WeightedKR,Vuln3,Criteria,Day1,Day30,Day90 io
```

The diagram shows the topology and data flow of the system as built. The full architectural narrative, with screenshots and prose, lives in [`documents/ai-executive-review-system.md`](./documents/ai-executive-review-system.md).

## Implementation

This system is built across **7 phases**:

1. **Building an AI-Native Executive Review Operating System**
2. **Wiring the Environment and Metric Governance Foundation**
3. **Designing the Agent Architecture**
4. **Designing the Operating Rhythm and Cadence**
5. **Assembling the Agent-Powered Review Kit**
6. **Holding the Room: Live Dispute and Decision Governance**
7. **Secret Mission: Pre-Mortem Agent for Proactive Dispute Defense**

For the full walkthrough with screenshots and step-by-step content, see [`documents/ai-executive-review-system.md`](./documents/ai-executive-review-system.md).

## Validation

Each build phase below is documented in [`documents/ai-executive-review-system.md`](./documents/ai-executive-review-system.md), with screenshots, configuration, and notes as captured during the build:

- ✅ Building an AI-Native Executive Review Operating System
- ✅ Wiring the Environment and Metric Governance Foundation
- ✅ Designing the Agent Architecture
- ✅ Designing the Operating Rhythm and Cadence
- ✅ Assembling the Agent-Powered Review Kit
- ✅ Holding the Room: Live Dispute and Decision Governance
- ✅ Secret Mission: Pre-Mortem Agent for Proactive Dispute Defense

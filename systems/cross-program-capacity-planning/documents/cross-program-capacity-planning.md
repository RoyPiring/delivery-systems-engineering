<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Cross-Program Capacity Planning

**Project Link:** [View Project](https://nextwork.ai/projects/0a831fbf-f718-4a8f-b79f-19f034a28fa6)

**Author:** Roy Piring: Cloud Platform Engineer | Build Master  
**Email:** rpiringhawaii@gmail.com

---

![Image](https://nextwork.ai/refreshed_maroon_timid_jujube/uploads/0a831fbf-f718-4a8f-b79f-19f034a28fa6_dh5aboik)

## Defining the Mandate: Why Headcount Failed

### The constraint the build is accountable to

I built a cross-program capacity planning system for a VP of Engineering. The system measures delivery capacity in competent hours rather than headcount. It was designed to show whether the portfolio had enough proven capability to meet dated demand across its programs.

Headcount failed because it treated every assigned person as equal capacity. It did not account for skill level, supporting evidence, or the time required for a new hire or trainee to become competent. That made delivery gaps invisible even when the roster looked fully staffed.

Competent hours corrected the unit of measurement. The model counted capacity only where a person had evidence for the required skill and could contribute within the milestone horizon.

## Locking Design Commitments, ADRs, and the System Topology

### What this step sets out to achieve

I wrote the Architectural Decision Records and documented the end-to-end system topology before calculating capacity. The ADRs recorded the rules governing evidence, gap routing, competent hours, and re-forecasting. The topology showed how roster data, skill evidence, demand, gaps, routes, and executive reporting connected.

This design work gave every later calculation a traceable basis. The capacity model could point to a declared decision instead of relying on an assumption buried inside a spreadsheet or script.

It also established the flow between functional teams. Evidence entered through the skills audit, demand came from dated milestones, and unmatched capability became a gap that required one approved buy, build, or borrow route.

### How the three commitments guard the build

The first commitment required evidence-based skills. A self-rating could not create capacity unless a shipped artifact or another accepted record supported the claim. This prevented confidence from becoming capability on paper.

The second commitment required every gap route to respect its need-by date. Training was not valid when competence would arrive after the demanding milestone. This prevented delayed upskilling from being presented as an on-time solution.

The third commitment measured competent hours instead of whole people. A mid-ramp hire could not be counted as complete capacity before reaching the required level. Together, the commitments blocked unevidenced skills, late routes, and phantom hours from entering the plan.

![Image](https://nextwork.ai/refreshed_maroon_timid_jujube/uploads/0a831fbf-f718-4a8f-b79f-19f034a28fa6_x8y80efq)

### Testing ADR reversal conditions against day-one state

I created constraint-statement.md from the scaffold with five sections, 4 explicit TBDs, and no invented numbers. Re-forecast cadence was the only completed value because ADR-004 supplied it through its day-one check.

I added a header stating that any unfilled constraint remained UNPROVEN under Commitment 1 and could not enter a calculation. This prevented the 4 TBDs from silently becoming zeros or assumed values in the capacity model.

Those TBDs became the blocker for E3. The gap table could not route work without a need-by horizon, and the model could not size buy routes without a budget envelope. The remaining execution requirement was the named operator authorization recorded in build-log.md.

## Building the Skills Matrix with Evidence

### What the matrix makes visible for the sponsor

I built a skills matrix, evidence audit, and demand baseline to show the sponsor where the portfolio had proven capability and where headcount created a false sense of coverage. The matrix connected each person-skill claim to evidence or marked it UNPROVEN.

This structure gave finance a clearer basis for resource requests. Instead of defending a request by saying the team needed more people, the sponsor could identify the dated skill demand, current competent hours, and remaining gap.

The matrix also separated roster size from usable depth. A program could have several assigned people while still having no proven holder for a required skill. That distinction made capability shortages visible before they appeared as missed delivery.

![Image](https://nextwork.ai/refreshed_maroon_timid_jujube/uploads/0a831fbf-f718-4a8f-b79f-19f034a28fa6_mcrn6otz)

### Check 1 results: completeness against the manifest

Check 1 proved completeness, not competence. The manifest contained 3 people, 4 skills, and 12 person-skill keys. All 12 keys were present, with zero missing entries and zero duplicates.

The evidence rule also held. Every claim had either supporting evidence or an UNPROVEN mark. Each evidenced row named a person, skill, and date, and no artifact was assigned across multiple people.

The completed matrix showed that the organization was thinner than its roster suggested. Eight of the 12 keys were UNPROVEN. Only Platform Engineering had proven depth. API Design and Data Engineering had no proven holders. The matrix passed every completeness check while still exposing four dated capability gaps.

## Routing Every Gap and Computing Capacity in Competent Hours

### From gap identification to a defensible capacity number

I routed every identified skill gap to one buy, build, or borrow strategy and calculated the portfolio in competent hours. The model connected each route to a need-by date so the sponsor could see whether the planned capability would arrive before the work required it.

The calculation exposed the difference between nominal availability and evidenced delivery capacity. Assigned people still appeared in the roster, but their hours contributed only where the competence factor supported the required skill.

This gave the sponsor a defensible capacity number rather than a headcount estimate. Each shortage could be traced to a dated demand, current evidence level, calculated shortfall, and selected route. The plan showed both the gap and the mechanism intended to close it.

### Enforcing the single-route constraint

The single-route rule prevented one gap from being counted under several solutions. Each row received one buy, build, or borrow decision, which made ownership, timing, and capacity effects clear.

I tested build routes arithmetically. Every gap used forecast start (4 wks) + TTC and compared the result with its need-by date. The need-by value came from the earliest demanding milestone because that was the deadline that constrained the route.

The rule affected three of eight gaps. Data Engineering required 28 weeks of ramp time against Harbor's 18-week deadline. G02 moved to buy, while G05 and G06 moved to borrow. A mechanical check confirmed that zero build routes remained where competence would arrive after the need-by date.

![Image](https://nextwork.ai/refreshed_maroon_timid_jujube/uploads/0a831fbf-f718-4a8f-b79f-19f034a28fa6_95yidr3m)

### Why the milestone slipped: the competence factor made visible

No milestone had slipped in the recorded data. The E4 attrition rerun that could produce forecasted slips had not yet run. Any explanation of a slip therefore described what the capacity gap would cause, not an observed delivery result.

The plan contained 3120 nominal hours, which made the portfolio appear fully staffed. However, 1560 hours carried competence factors of 0.00. Half of the stated capacity had no evidence behind the required skill.

Harbor's Data Engineering demand showed the problem directly. Two people appeared against the nearest milestone, Q4 2026, 18 weeks away, but they produced zero competent hours for that skill. The gap could not be trained in time, so the model routed it to buy and borrow.

## Injecting Attrition and Producing the Executive Report

### Modelling departures against the same definitions

I defined attrition scenarios against the same skills, evidence, demand, and competent-hour rules used in the baseline. This kept a departure from becoming a separate calculation with different assumptions.

Each scenario removed one person and recalculated proven capacity, open gaps, route coverage, and milestone effects. Every loss required either a named mitigation or a forecasted slip. The model did not allow a departure to disappear into a general risk statement.

Using the same definitions made the before-and-after comparison meaningful. A capability loss remained tied to the skill and program where the evidence had existed. The scenario therefore showed which part of the portfolio depended on each person and how much capacity disappeared when that person left.

![Image](https://nextwork.ai/refreshed_maroon_timid_jujube/uploads/0a831fbf-f718-4a8f-b79f-19f034a28fa6_ieycmfn1)

![Image](https://nextwork.ai/refreshed_maroon_timid_jujube/uploads/0a831fbf-f718-4a8f-b79f-19f034a28fa6_jsxqtifp)

### What the report asserts and what it honestly does not

The report states that the portfolio can evidence 37.5% of demanded capability today and could reach 75% if every route executes. It shows that headcount overstates capability by exactly 2×, three gaps cannot be trained in time, and removing any one of three people costs between one-third and one-half of total capability.

The 75% forecast is not guaranteed. It assumes five build routes land, one hire fills, and two contractors engage. None has been demonstrated. Buy and borrow feasibility also remains unknown because hiring lead time and the budget envelope are TBD.

The totals are not fully spendable because the ledger double-counts anyone proven in two skills on one program. The binary competence scale also omits mid-ramp capacity and can make the average factor rise when an unproven person leaves.

## Validating Completeness and Shipping the Tagged Release

### Running all three checks under the guard rule

I consolidated the three validation results into one master record and wrote the user documentation before tagging v1.0.0. The master record tied every check to the same declared manifest rather than allowing each result file to carry independent expectations.

The guard rule required every absence claim to report how many rows were read and how many were expected. A check could pass only when the read count was non-zero and matched the manifest. This prevented an empty or partial input from producing a clean-looking result.

The documentation explained how non-engineering stakeholders could read the skills matrix, gap routes, capacity ledger, and executive report. The tagged release fixed the validated data, checks, and guidance into one identifiable handoff.

### Why zero rows is not a clean result

An absence claim is automatically true when no rows are examined. A check for "no claim is both unevidenced and unmarked" will return no violations against an empty file, but that result is indistinguishable from a complete clean data set unless the read count is reported.

Twelve rows read means the check examined all 12 expected keys and found no violation. Zero rows read means the check did not inspect the data, so reporting PASS would turn a broken query into false evidence.

Non-empty input is also insufficient. A check that reads 3 of 12 keys can still find no issues in the 9 rows it missed. The guard therefore requires read to equal expected, not merely exceed zero. Completeness must be proven before absence can carry meaning.

### What the validation record proves beyond individual checks

The validation record gives all three checks one declared manifest. It defines the expected counts once as 3/4/12/8/4 and reconciles each result against those same values. Before consolidation, every results file carried its own counts, so agreement across the checks was not established.

The record also applies one guard rule to all three. Every absence assertion must have a non-zero read count that matches the expected count. This makes the checks jointly admissible instead of individually clean on different terms.

Finally, the record states one boundary for the full build. It does not claim that an approached engineer stays or that ratifications land. It states the testable conditions the system does enforce.

## Executive Presentation: Lessons Learned and the Adoption Metric

### What the build proved and what it cannot claim

The build cannot claim retention. It modeled departures and assigned mitigations or slips, but it did not cause an approached engineer to stay. It also cannot claim ratification latency. Unconfirmed person-level moves remain in a queue, and the plan stays a forecast until those approvals clear.

The model did prove that headcount and capability diverged through the competence factor. It measured 3120 nominal hours against 1560 competent hours, an exact 2× difference.

I reconciled two unsupported statements in the supplied presentation. No real milestone slip was recorded because the slips came from constructed scenarios. The roster also contained three people, not thirteen. Thirteen referred to unfilled requisitions. The 2× capacity finding stands without either claim.

## Reflections and Next Steps

### Tools and concepts from the build

I used GitHub for version-controlled documentation and release management, Linear for work tracking, and VS Code to manage the capacity-model data and supporting files.

The central concept was separating headcount from capability. The skills matrix combined evidence, competence factors, and dated demand so assigned people contributed only where their skill could be supported. Gap routing then connected each shortage to one buy, build, or borrow action.

I also applied an evidence-decay rule so old skill records would not remain current without review. The validation guard required complete row counts before any absence claim could pass. Together, these controls made the model useful for executive decisions while keeping its assumptions and limits visible.

### Time taken and biggest challenges

This build took approximately 75 minutes. The hardest part was refining the executive presentation for two audiences with different needs. Program leadership required the skill-level details, route timing, and milestone constraints behind the model. The executive sponsor needed the portfolio-level capacity, risks, and decisions.

The presentation had to preserve the evidence chain without forcing every reader through the underlying calculations. It also needed to separate current facts from route assumptions and constructed attrition scenarios.

That distinction prevented forecasts from appearing as delivered outcomes. The final readout showed what the model measured, what depended on future execution, and which remaining constraints were still UNPROVEN or TBD.

I completed this build to learn how a cross-program capacity system can connect evidence-based skills, dated demand, gap routes, and competent hours. The result replaced raw headcount with a model that showed where delivery capability existed and where it remained unsupported.

The next step is to apply the same approach to larger cross-functional portfolios. That requires carrying the evidence, timing, and guard rules into more programs without hiding uncertainty inside aggregate totals.

I also want to connect the model with organizational resource-allocation workflows. Any integration must preserve the same boundaries: unproven skills cannot become capacity, late routes cannot satisfy earlier demand, and forecasted moves cannot be reported as completed.

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/0a831fbf-f718-4a8f-b79f-19f034a28fa6)*

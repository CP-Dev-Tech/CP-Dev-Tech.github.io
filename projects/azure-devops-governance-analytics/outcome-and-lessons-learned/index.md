# Outcome & Lessons Learned

[← Requirements & Delivery Traceability](/projects/azure-devops-governance-analytics/delivery-traceability/) · [Project Overview](/projects/azure-devops-governance-analytics/) · [Back to Projects →](/projects/)

## Overview

The Azure DevOps Governance Analytics project delivered a complete Power BI solution that combines approval-governance monitoring, requirements-health assessment and executive reporting within one controlled analytical model.

The final solution demonstrates the full delivery path from business problem definition and requirements engineering through source assessment, Power Query preparation, semantic modelling, DAX development, report design, validation and portfolio publication.

The project was assessed against defined business objectives, business rules, acceptance criteria and controlled validation evidence rather than being treated solely as a dashboard-design exercise.

## Completed Solution

The final business-facing Power BI solution contains four principal report pages:

1. **Executive Governance Overview** — provides a concise summary of approval position, requirements health and material governance exceptions.
2. **Approval Governance Summary** — provides approval workload, overdue position and approval-age analysis.
3. **Overdue Approval Exceptions** — identifies individual User Stories requiring approval follow-up.
4. **Requirements Health** — identifies Healthy, Attention Required and Critical requirements together with their underlying issue reasons.

A separate **Validation / Model Validation** page supports technical reconciliation and assurance.

The reporting layer is supported by a semantic model that separates current-state, historical, approval-period, requirements-completeness and issue-level data according to their analytical grain.

## Final Analytical Position

Following the final portfolio refresh, the solution reported a current population of **128 User Stories**.

### Approval Governance

| Approval Position | Requirements |
|---|---:|
| **Approved** | 3 |
| **Not Submitted** | 114 |
| **Awaiting Approval** | 0 |
| **Overdue Approval** | 11 |
| **Total Requirements** | **128** |

This confirms that the approval-position categories reconcile exactly to the current User Story population.

### Requirements Health

| Health Status | Requirements |
|---|---:|
| **Healthy** | 113 |
| **Attention Required** | 4 |
| **Critical** | 11 |
| **Total Requirements** | **128** |

The resulting **Healthy Requirements Percentage** was **88.3%**.

**What this demonstrates:**  
The completed model supports two distinct but reconcilable governance perspectives over the same current User Story population: approval position and requirements health.

## Business and Governance Outcome

The completed solution provides a structured answer to the original governance problem.

It enables users to:

- identify which User Stories have entered an approval cycle;
- identify which active approvals have reached the seven-day overdue threshold;
- identify the current Responsible Authoriser;
- distinguish requirements that have not yet been submitted for approval;
- assess requirements completeness using defined mandatory fields;
- identify invalid or missing Feature relationships;
- classify requirements as Healthy, Attention Required or Critical;
- retain all applicable requirements-health reasons;
- understand the overall governance position through an executive summary; and
- move from high-level indicators to detailed records requiring investigation.

The result replaces manual inspection of individual Azure DevOps work items with a repeatable analytical view governed by defined rules.

## Assessment Against Business Objectives

| Objective | Outcome |
|---|---|
| **OBJ-001 — Reliably identify overdue approval requests** | Achieved through reconstructed approval periods, approval-age logic and the Overdue Approval Exceptions page |
| **OBJ-002 — Enable targeted follow-up and authoriser accountability** | Achieved through Responsible Authoriser logic, approval-period dates, approval age and supporting User Story detail |
| **OBJ-003 — Provide consistent evidence-based governance monitoring** | Achieved through the Approval Governance Summary and controlled KPI definitions |
| **OBJ-004 — Provide objective requirements-health classification** | Achieved through completeness indicators, Feature validation, health precedence rules and issue-level reasons |
| **OBJ-005 — Provide executive governance visibility** | Achieved through the Executive Governance Overview and its approval, health and material-exception indicators |
| **OBJ-006 — Provide consistent filtering, navigation and supporting detail** | Achieved through shared reporting controls, business-page navigation and reconciliation to underlying records |

**What this demonstrates:**  
The finished solution can be evaluated against the business objectives defined at the start of the project, creating a clear line from problem definition to measurable delivery outcome.

## Validation Outcome

The controlled final validation record confirmed:

| Validation Result | Outcome |
|---|---:|
| **Tests executed** | 56 |
| **Passed** | 56 |
| **Failed** | 0 |
| **Final result** | **PASS** |

Testing covered source data, transformations, semantic-model behaviour, business rules, measures, report interactions, reconciliations and performance.

Six implementation defects identified during development were corrected and successfully retested.

## Performance Outcome

Power BI Performance Analyzer was used to verify report responsiveness.

Selected final results included:

| Report Page | Slowest Recorded Visual |
|---|---:|
| **Executive Governance Overview** | **120 ms** |
| **Approval Governance Summary** | **125 ms** |
| **Overdue Approval Exceptions** | **123 ms** |
| **Validation / Model Validation** | **89 ms** |

**What this demonstrates:**  
Performance was treated as a measurable quality characteristic and validated using Power BI tooling rather than being judged only by perceived responsiveness.

## Key Delivery Lessons

### 1. Start with the Business Rules, Not the Visuals

The most important analytical behaviours were defined before report construction.

Rules covering approval activation, authoriser precedence, approval age, overdue classification, requirements completeness and health-status precedence provided a stable basis for Power Query, DAX and validation.

**Lesson:**  
A visually polished dashboard is easier to build and validate when the underlying business definitions have already been made explicit and testable.

### 2. One Source Interface Did Not Need to Solve Every Requirement

Azure DevOps Analytics Views were well suited to historical approval snapshots, while current Description and Acceptance Criteria completeness required targeted REST API enrichment.

Trying to force every reporting requirement through a single extraction method would have made the solution less effective.

**Lesson:**  
Data-source design should follow the analytical requirement. Different interfaces can be combined where each has a clear and controlled role.

### 3. Data Grain Must Be Designed Deliberately

Current KPIs require one row per User Story, historical approval analysis requires multiple snapshots and health-reason analysis can require several records for one User Story.

Those needs cannot safely be represented as one undifferentiated dataset.

**Lesson:**  
Explicitly defining table grain early prevents duplicated counts, ambiguous relationships and increasingly complex DAX later.

### 4. Preserve the Analytical Result, Not Unnecessary Source Content

Description and Acceptance Criteria were required for completeness assessment, but the full long-text content was not required for analysis.

The model therefore retained Boolean completeness indicators rather than unnecessary raw text.

**Lesson:**  
Data minimisation can improve model efficiency and privacy while still preserving the information required for the business decision.

### 5. Summary and Detail Need to Reconcile

Executive KPIs, analytical pages and detailed exception tables were designed over the same controlled current population.

The final approval and requirements-health classifications each reconcile independently to the same 128 User Stories.

**Lesson:**  
A management summary is significantly more trustworthy when every headline number can be traced back to a controlled underlying population.

### 6. Validation Should Be Designed Into the Solution

A dedicated Validation / Model Validation page, controlled test scenarios, reconciliation checks and Performance Analyzer evidence were used throughout delivery.

**Lesson:**  
Building validation capability alongside the analytical solution makes defects easier to diagnose and gives stronger assurance than relying on final visual inspection.

### 7. User Experience Includes Analytical Interpretation

Some design decisions were made specifically to prevent misleading interpretation.

For example, the Executive page states that material exception indicators may overlap, and the Requirements Health Status slicer is deliberately excluded from the Executive Overview so critical conditions cannot be hidden from the overall governance position.

**Lesson:**  
Good report design is not only about layout and appearance. It also means reducing the risk that technically correct data is interpreted incorrectly.

### 8. Traceability Adds Practical Delivery Value

Requirements, business rules, implementation components and tests were maintained as connected artefacts.

This allowed the completed solution to be evaluated against its original objectives and made the effect of design decisions visible across the delivery lifecycle.

**Lesson:**  
Traceability is most valuable when it supports real impact analysis and validation rather than existing only as administrative documentation.

## Portfolio Outcome

The project demonstrates the combination of **Business Analyst and Data Analyst / Power BI delivery skills** within one end-to-end case study.

It provides evidence of:

- business problem definition;
- requirements engineering;
- business-rule definition;
- stakeholder and reporting-needs analysis;
- Azure DevOps source assessment;
- hybrid historical and current-state data extraction;
- Power Query transformation design;
- semantic-model design;
- DAX development;
- executive and operational dashboard design;
- validation and defect resolution;
- performance testing;
- requirements and delivery traceability; and
- controlled public portfolio publication.

The finished result is therefore not presented simply as a Power BI dashboard. It is presented as a complete analytics delivery case study showing how a defined governance problem was translated into a designed, implemented and validated analytical solution.

## Evidence Presented

The public case study presents selected evidence of:

- the completed reporting solution;
- final approval and requirements-health reconciliations;
- achievement of the defined business objectives;
- final test outcome;
- measured report performance;
- key architectural and modelling decisions;
- delivery lessons; and
- end-to-end analytical ownership.

The working Power BI implementation and complete controlled project documentation remain within the project environment.

[← Requirements & Delivery Traceability](/projects/azure-devops-governance-analytics/delivery-traceability/) · [Project Overview](/projects/azure-devops-governance-analytics/) · [Back to Projects →](/projects/)

---

© 2026 Carl Patten. All rights reserved.

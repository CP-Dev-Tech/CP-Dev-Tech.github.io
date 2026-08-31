# Requirements & Delivery Traceability

[← Validation & Testing](/projects/power-bi-governance-analytics/validation-and-testing/) · [Project Overview](/projects/power-bi-governance-analytics/) · [Outcome & Lessons Learned →](/projects/power-bi-governance-analytics/outcome-and-lessons-learned/)

## Overview

Traceability was maintained across the project so that business objectives, requirements, business rules, implementation components and validation evidence remained connected throughout delivery.

The approach provides both **requirements traceability** and **delivery traceability**:

- requirements traceability shows how a business need is carried through design, implementation and testing;
- delivery traceability shows which controlled documents and artefacts are consumed or updated by individual delivery activities.

Together, these provide an auditable link from the original business problem to the completed and validated Power BI solution.

## Traceability Approach

The controlled Requirements Traceability Matrix (RTM) links:

**Business Objective**  
↓  
**Functional / Non-Functional Requirement or Business Rule**  
↓  
**Delivery Reference**  
↓  
**Design or Model Component**  
↓  
**Validation Reference**  
↓  
**Delivery Status**

This makes it possible to answer questions such as:

- Why does this report feature exist?
- Which requirement does this DAX or model component satisfy?
- Which test proves the behaviour?
- Which business objective is supported?
- Has the requirement been delivered and validated?

The same principle is used within the delivery process to link individual tasks to their required document inputs and outputs.

## Requirements Traceability

The final controlled RTM covers:

- `FR-001–FR-052` — functional requirements;
- `NFR-001–NFR-066` — non-functional requirements;
- `BR-001–BR-028` — business rules; and
- `OBJ-001–OBJ-006` — business objectives.

The matrix records the relevant implementation and validation references rather than treating the requirements document as a standalone artefact.

## Project Evidence

### Functional Requirement Traceability

The extract below shows representative requirement groups from the final RTM.

| Requirement | Business Objective | Principal Implementation | Validation | Status |
|---|---|---|---|---|
| **FR-001–FR-006** | Reliable overdue-approval identification and targeted follow-up | `ApprovalHistory`, `CurrentApprovals`, `ApprovalPeriodSummary`, responsible-authoriser logic, Overdue Approval Exceptions | GOV-001–GOV-013; REC-003 | Delivered and validated |
| **FR-007–FR-014** | Consistent governance monitoring and escalation | Approval Governance Summary, approval KPIs and approval-age measures | GOV-001–GOV-016; REC-003; FIL-002–FIL-005 | Delivered and validated |
| **FR-015–FR-026** | Objective requirements-health classification | `RequirementFieldStatus`, `FeatureWorkItemIDs`, `RequirementsHealthReasons`, health logic and Requirements Health page | HLTH-001–HLTH-019; REC-001–REC-006 | Delivered and validated |
| **FR-027–FR-038** | Executive governance summary | Executive KPI cards, Approval Position, Requirements Health, Material Governance Exceptions and area analysis | EXEC-001–EXEC-008 | Delivered and validated |
| **FR-039–FR-048** | Consistent filtering and navigation | Area Path, Iteration Path, applicable page filters, reset controls and business navigation | FIL-001–FIL-009; EXEC-001–EXEC-007 | Delivered |
| **FR-049–FR-052** | Supporting detail and validation | Overdue detail, requirements-health detail and Validation / Model Validation | REC-001–REC-006; GOV / HLTH / GR validation | Delivered and validated |

**What this demonstrates:**  
The functional requirements remain connected to the components that implement them and to the tests used to confirm the expected behaviour.

### Business Rule Traceability

Business rules are also linked directly to implementation and validation.

| Business Rule Area | Implementation | Validation |
|---|---|---|
| **Approval population and active-request logic** | `CurrentApprovals` and approval-active logic | GOV-001–GOV-004; GR-002; REC-004 |
| **Current continuous approval period** | `ApprovalHistory`, `ApprovalPeriodSummary` and period derivation | GOV-006–GOV-007; GOV-009–GOV-012 |
| **Responsible Authoriser precedence** | Responsible Authoriser logic and one-row-per-story grain | GOV-005; GOV-013; REC-003 |
| **Seven-day overdue rule** | Approval-age measures and approval-status logic | GOV-009–GOV-016; REC-003 |
| **Requirements completeness and valid Feature parent** | `RequirementFieldStatus` and `FeatureWorkItemIDs` | HLTH-001–HLTH-008 |
| **Health status and reasons** | Requirements Health Status, Health Reasons and `RequirementsHealthReasons` | HLTH-009–HLTH-019 |
| **Executive exception logic** | `Executive Exception Count`, `Executive Exception Type` and Requirements Requiring Attention | EXEC-005–EXEC-006 |
| **Filter-context behaviour** | DAX filter-preservation logic and report slicers | FIL-001–FIL-008; EXEC-001–EXEC-006 |

**What this demonstrates:**  
Business rules are not documented separately from the technical implementation. Each important analytical rule can be followed through to the model or DAX component that applies it and the validation evidence that confirms it.

### Objective Coverage

The completed solution also traces back to the original business objectives.

| Objective | Principal Evidence | Outcome |
|---|---|---|
| **OBJ-001** — Reliable overdue-approval identification | Overdue Approval Exceptions, approval-period model and GOV tests | Achieved |
| **OBJ-002** — Targeted follow-up and authoriser accountability | Responsible Authoriser, approval age and supporting detail | Achieved |
| **OBJ-003** — Evidence-based governance monitoring | Approval Governance Summary and approval KPI validation | Achieved |
| **OBJ-004** — Objective requirements-health classification | Requirements Health, issue-reason model and HLTH tests | Achieved |
| **OBJ-005** — Executive governance visibility | Executive Governance Overview and EXEC-001–EXEC-008 | Achieved |
| **OBJ-006** — Consistent filtering, navigation and supporting detail | Report slicers, reset controls, navigation and reconciliation tests | Achieved |

**What this demonstrates:**  
The project can be traced backwards from the delivered dashboards to the business outcomes that justified the work in the first place.

## Delivery Traceability

Requirements traceability is complemented by a process-level approach that identifies the controlled information consumed and produced by individual delivery activities.

Each delivery activity can be associated with:

- a unique task or gateway identifier;
- the controlled document used as an input;
- the relevant document section;
- the information supplied by that input;
- the document updated as an output; and
- the information the activity is expected to record.

This creates a repeatable link between the delivery process and the project documentation.

### Representative Task-to-Document Association

The example below shows how requirements-definition activities interact with the controlled documentation.

| Activity | Association | Controlled Artefact | Information Supplied or Recorded |
|---|---|---|---|
| **Define the business rules** | Input | Business Requirements Document — objectives, scope, assumptions and constraints | Supplies the business context from which calculation, classification, precedence and fallback rules are derived |
| **Define the business rules** | Output | Business Requirements Document — Business Rules | Records uniquely identified and testable business rules |
| **Define the business rules** | Output | Requirements Traceability — RTM | Establishes traceability from business rules to requirements, implementation components and tests |
| **Define functional & non-functional requirements** | Input | Business Requirements Document — objectives, scope, constraints and rules | Supplies the basis from which testable requirements are defined |
| **Define functional & non-functional requirements** | Input | Stakeholder Analysis | Supplies stakeholder responsibilities, information needs and decision requirements |
| **Define functional & non-functional requirements** | Output | Business Requirements Document — FR/NFR sections | Records the defined functional and non-functional requirements |
| **Define functional & non-functional requirements** | Output | Requirements Traceability — RTM | Adds requirement identifiers and establishes forward and backward traceability |

**What this demonstrates:**  
The delivery process does not treat documentation as an administrative step performed after the work. Each activity has defined information dependencies and controlled outputs, helping maintain consistency as the project moves from analysis through design, implementation and validation.

## Key Implementation Artefacts

Traceability connects the principal controlled project documents rather than concentrating all project knowledge in a single file.

| Artefact | Traceability Role |
|---|---|
| `01-business-requirements-document.md` | Defines objectives, requirements, KPIs, business rules and success criteria |
| `03-requirements-traceability.md` | Maintains the central forward and backward traceability record |
| `04-data-requirements-and-source-assessment.md` | Defines required source data, limitations and data-quality requirements |
| `05-test-and-validation-record.md` | Records controlled tests, expected results, defects and reconciliation evidence |
| `06-data-source-configuration.md` | Records Azure DevOps Analytics View and API source configuration |
| `07-power-query-and-data-preparation.md` | Records transformation and data-preparation implementation |
| `08-semantic-model-specification.md` | Defines model tables, relationships, measures and business logic |
| `09-report-design-and-user-experience.md` | Defines final report-page structure, navigation, filters and interactions |
| `10-power-bi-implementation.md` | Records the implemented Power BI pages, visuals, measures and controls |
| `12-security-and-access-control.md` | Records portfolio privacy and public-evidence controls |
| `13-operational-support-and-monitoring.md` | Records maintenance and manual-refresh arrangements |

## Traceability Outcome

The final traceability structure provides a controlled chain from:

**business problem → objective → requirement / rule → delivery activity → implementation → validation → outcome**

This provides evidence that the Power BI solution was delivered as an end-to-end analytical project rather than as an isolated dashboard build.

It also makes impact analysis easier: if a business rule, requirement, model component or report behaviour changes, the affected documentation and validation references can be identified systematically.

## Evidence Presented

The public case study presents selected evidence of:

- requirement-to-objective traceability;
- requirement-to-implementation traceability;
- business-rule-to-model and DAX traceability;
- implementation-to-test traceability;
- objective coverage;
- task-to-document input and output associations;
- controlled artefact relationships; and
- forward and backward traceability across the analytics lifecycle.

The public examples are deliberately selective so that the traceability method can be demonstrated without reproducing the complete controlled project records.

[← Validation & Testing](/projects/power-bi-governance-analytics/validation-and-testing/) · [Project Overview](/projects/power-bi-governance-analytics/) · [Outcome & Lessons Learned →](/projects/power-bi-governance-analytics/outcome-and-lessons-learned/)

---

© 2026 Carl Patten. All rights reserved.

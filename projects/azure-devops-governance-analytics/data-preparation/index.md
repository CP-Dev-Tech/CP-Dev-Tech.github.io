# Data Preparation

[← Solution Architecture](/projects/azure-devops-governance-analytics/solution-architecture/) · [Project Overview](/projects/azure-devops-governance-analytics/) · [Semantic Model →](/projects/azure-devops-governance-analytics/semantic-model/)

## Overview

The data-preparation stage converted Azure DevOps source data into analysis-ready structures that could support approval-governance and requirements-health reporting.

Power Query was used to clean and standardise source data, reconstruct approval periods, derive the current approval position and prepare targeted requirements-completeness indicators obtained through Azure DevOps API enrichment.

The transformation logic was designed around the business rules established during requirements analysis rather than simply reproducing the source-system structure inside Power BI.

## Data Preparation Approach

Two different source streams required different preparation approaches:

1. **Azure DevOps Analytics View data** supplied historical daily work-item snapshots used for approval-history analysis.
2. **WIQL and REST API data** supplied targeted current-state information needed for requirements-completeness assessment.

The resulting datasets were transformed into structures suitable for current-state reporting, historical analysis, requirements-health assessment and validation.

## Historical Approval Preparation

The Analytics View provides multiple dated records for each User Story.

These records are retained as `ApprovalHistory` so that changes in approval state can be analysed across time.

Power Query preparation includes:

- standardising field names and data types;
- retaining the fields required for approval analysis;
- identifying whether an approval request is active;
- deriving the responsible authoriser;
- identifying the current continuous approval period;
- determining the approval-period start date; and
- preserving the historical records required to calculate approval age.

This allows approval-age calculations to be based on the **current continuous approval period**, rather than simply using the age of the User Story itself.

## Current-State Preparation

Operational and executive reporting require one current record per User Story.

A separate `CurrentApprovals` structure is therefore derived from the historical source data.

This provides a deterministic current-state population for:

- KPI calculations;
- approval-position reporting;
- overdue-approval identification;
- filtering;
- requirements-health classification; and
- supporting detail tables.

Separating current-state data from historical snapshots prevents multiple historical records from inflating current counts.

## Responsible Authoriser Logic

The source contains both **Authorised By** and **Senior Authorised By** fields.

A derived **Responsible Authoriser** field applies the defined precedence rule:

- use **Senior Authorised By** when populated;
- otherwise use **Authorised By**; and
- treat the requirement as not submitted for approval where neither field is populated.

This produces one consistent authoriser value for reporting and avoids duplicating a User Story when both source fields contain values.

## Approval-Period Preparation

Approval ageing is based on the current continuous approval period rather than general work-item age.

Power Query prepares the fields needed to determine:

- whether an approval request is currently active;
- when the current approval period started;
- whether a previous approval cycle has ended;
- the current responsible authoriser; and
- the data required by the semantic model to calculate approval age and overdue status.

The approval-period start date is subsequently treated as **day zero**, with an active request becoming overdue once it reaches the defined seven-day threshold.

## Requirements-Completeness Enrichment

Description and Acceptance Criteria completeness could not be assessed from the historical Analytics View alone.

WIQL is therefore used to identify the relevant current Azure DevOps work-item population, after which the REST API retrieves the fields required for completeness assessment.

Rather than retaining the full long-text content in the analytical model, Power Query converts the source content into indicators representing whether the required information is present.

This supports requirements-health classification while reducing unnecessary model content and exposure of source text.

## Parent Feature Validation

A populated parent identifier does not, by itself, prove that a User Story has a valid Feature parent.

Current Feature work-item identifiers are therefore obtained and prepared as a separate validation structure.

This allows the requirements-health logic to distinguish between:

- a valid Feature relationship;
- a missing parent; and
- a parent that does not represent a valid Feature.

## Derived Fields

Several derived fields convert source-system data into analytical concepts required by the reporting model.

Representative examples include:

| Derived Field / Indicator | Purpose |
|---|---|
| **Responsible Authoriser** | Provides the single reportable authoriser after applying the defined precedence rule |
| **Approval Request Active** | Identifies User Stories currently in an active approval cycle |
| **Approval Period Start Date** | Identifies the start of the current continuous approval period |
| **Description Present** | Indicates whether Description contains the information required for completeness assessment |
| **Acceptance Criteria Present** | Indicates whether Acceptance Criteria contains the information required for completeness assessment |
| **Valid Feature Parent** | Indicates whether the current parent is a valid Azure DevOps Feature |

These fields provide reusable inputs to the semantic model rather than repeatedly interpreting raw source fields in individual report visuals.

## Transformation Validation

Data preparation was validated before relying on the resulting structures for reporting.

Checks included:

- confirming one current row per User Story;
- comparing current-state counts with the source population;
- validating responsible-authoriser precedence;
- checking approval-period start dates against known history;
- verifying controlled overdue and non-overdue scenarios;
- validating Description and Acceptance Criteria indicators;
- checking valid Feature-parent identification; and
- reconciling transformed datasets with downstream KPI and requirements-health results.

This made transformation validation part of the analytical delivery process rather than relying solely on final dashboard inspection.

## Project Evidence

### Power Query Implementation

![Power Query data preparation](/assets/projects/azure-devops-governance-analytics/data-preparation-power-query.png)

*Power Query implementation showing representative transformation queries used to prepare Azure DevOps data for the analytical model.*

**What this demonstrates:**  
The Power Query layer performs business-rule-driven preparation rather than acting only as a source-loading mechanism. Historical and current-state data are deliberately separated, derived analytical fields are created and only the source information required by the reporting model is retained.

### Transformation Design Evidence

| Source Requirement | Power Query Response | Analytical Result |
|---|---|---|
| Historical approval states required | Retain dated Analytics View snapshots | `ApprovalHistory` |
| Current reporting requires one row per User Story | Select and prepare deterministic current state | `CurrentApprovals` |
| Current continuous approval period required | Evaluate historical approval state and derive period start | Approval-period analysis |
| One responsible authoriser required | Apply Senior Authorised By / Authorised By precedence | Responsible Authoriser |
| Description completeness required | Retrieve current content and derive presence indicator | Requirements-health input |
| Acceptance Criteria completeness required | Retrieve current content and derive presence indicator | Requirements-health input |
| Parent must be a valid Feature | Prepare current Feature identifiers for comparison | Feature-parent validation |
| Multiple health issues can apply to one requirement | Retain issue-level analytical reasons | Requirements-health reason analysis |

**What this demonstrates:**  
Each transformation exists to satisfy a defined analytical or business-rule requirement. The preparation layer provides a controlled bridge between the structure of Azure DevOps and the structure required by the Power BI semantic model.

### Data-Minimisation Example

A specific design choice was made for long-text requirement fields.

The analytical model needs to know whether **Description** and **Acceptance Criteria** are complete, but it does not need to expose or analyse the underlying text.

The preparation process therefore retains the analytical result rather than the complete source text.

**Source content**

`Description / Acceptance Criteria`

↓  

**Power Query assessment**

`Present / Missing`

↓  

**Semantic-model indicator**

`TRUE / FALSE`

**What this demonstrates:**  
The transformation design considers model efficiency and privacy as well as functional reporting requirements. Source data is retained only where it contributes to the analytical purpose.

## Evidence Presented

The public case study presents selected evidence of:

- Azure DevOps source-data preparation;
- historical and current-state transformation design;
- approval-period reconstruction;
- responsible-authoriser derivation;
- WIQL and REST API enrichment;
- requirements-completeness indicators;
- Feature-parent validation;
- derived analytical fields;
- data-minimisation decisions; and
- transformation validation.

Only representative implementation evidence is published. Working Power Query logic, source configuration and implementation artefacts remain within the controlled project environment.

[← Solution Architecture](/projects/azure-devops-governance-analytics/solution-architecture/) · [Project Overview](/projects/azure-devops-governance-analytics/) · [Semantic Model →](/projects/azure-devops-governance-analytics/semantic-model/)

---

© 2026 Carl Patten. All rights reserved.

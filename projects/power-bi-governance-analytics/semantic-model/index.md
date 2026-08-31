# Data Preparation

[← Solution Architecture](/projects/power-bi-governance-analytics/solution-architecture/) · [Project Overview](/projects/power-bi-governance-analytics/) · [Semantic Model →](/projects/power-bi-governance-analytics/semantic-model/)

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

[← Solution Architecture](/projects/power-bi-governance-analytics/solution-architecture/) · [Project Overview](/projects/power-bi-governance-analytics/) · [Semantic Model →](/projects/power-bi-governance-analytics/semantic-model/)

---

© 2026 Carl Patten. All rights reserved.

For the placeholder screenshot, I’d use:

/assets/projects/azure-devops-governance-analytics/data-preparation-power-query.png

When we create the evidence later, I’d make that a carefully cropped Power Query Editor screenshot showing the query list and one meaningful transformation, rather than a huge screenshot of the whole Power BI window.

I also deliberately haven't put invented M code on the page. When we want to add an actual code example, we should take a short representative piece from your real query so the public evidence is genuinely from the implementation.

Next is Semantic Model, where the final model diagram should become the main evidence.

OK Semantic model next, please keep track of any evidence artefacts I need to create and give a list at the end.

Yes. I’ll keep a running evidence artefact register as we work through the remaining pages, then give you the consolidated list at the end.

For the Semantic Model page, paste the current Markdown and I’ll rebuild it using the same structure:

Overview → model design → table roles → relationship decisions → DAX/model logic → project evidence → what it demonstrates

For this page, the main evidence artefact will be the final semantic-model diagram, with a placeholder path such as:

/assets/projects/azure-devops-governance-analytics/semantic-model.png

I’m already tracking the evidence artefacts we’ve identified so far:

solution-architecture.png
data-preparation-power-query.png
semantic-model.png

I’ll keep adding to that register as we progress.

# Semantic Model

[← Data Preparation](/projects/power-bi-governance-analytics/data-preparation/) · [Project Overview](/projects/power-bi-governance-analytics/) · [Report & User Experience →](/projects/power-bi-governance-analytics/report-and-ux/)

## Overview

This section presents selected evidence of how the prepared data was structured into a semantic model to support analysis, reporting and business logic.

It demonstrates how tables, relationships, calculated fields and measures were designed to provide reliable and reusable analytical behaviour within Power BI.

## What This Demonstrates

- Semantic-model design

- Table and relationship design

- Data-grain awareness

- Measure development

- Business-rule implementation

- Filter-context understanding

- Model validation

- Supportability and maintainability considerations

- Documentation of model behaviour and limitations

## Evidence Presented

Selected portfolio evidence will include:

- High-level semantic-model structure

- Representative table relationships

- Selected measures and calculated logic

- Examples of business-rule implementation

- Model validation approach

- Selected design decisions

- Model capabilities and limitations

The published model diagram is a flattened, watermarked portfolio representation. The complete semantic-model specification, PBIX implementation and reusable logic are retained privately.

[← Data Preparation](/projects/power-bi-governance-analytics/data-preparation/) · [Project Overview](/projects/power-bi-governance-analytics/) · [Report & User Experience →](/projects/power-bi-governance-analytics/report-and-ux/)

---

© 2026 Carl Patten. All rights reserved.

For this page, the strongest evidence is the actual semantic-model diagram, supported by a compact explanation of table grain, relationship choices, and a few genuine DAX examples. That shows considerably more skill than simply listing the tables.

I’d replace the current page with:

# Semantic Model

[← Data Preparation](/projects/power-bi-governance-analytics/data-preparation/) · [Project Overview](/projects/power-bi-governance-analytics/) · [Power BI Dashboards & User Experience →](/projects/power-bi-governance-analytics/report-and-ux/)

## Overview

The semantic model converts the prepared Azure DevOps datasets into reusable analytical structures supporting approval governance, requirements health, executive reporting and controlled validation.

The model was designed around the grain required by each analytical purpose rather than combining all source data into a single table.

This separation allows current-state KPIs, historical approval analysis and issue-level requirements-health reporting to coexist without introducing ambiguous counts or unnecessary relationship complexity.

## Model Design Approach

The implemented model contains six material analytical tables supported by a small disconnected presentation helper.

The principal analytical tables are:

- `ApprovalHistory`
- `CurrentApprovals`
- `ApprovalPeriodSummary`
- `RequirementFieldStatus`
- `FeatureWorkItemIDs`
- `RequirementsHealthReasons`

A disconnected `Executive Exception Type` table supports presentation of the controlled exception categories used on the Executive Governance Overview.

## Analytical Table Roles

| Table | Grain | Purpose |
|---|---|---|
| `CurrentApprovals` | One row per current User Story | Central current-state reporting population for approval governance, requirements health and executive KPIs |
| `ApprovalHistory` | One row per User Story per historical snapshot date | Preserves approval history required to reconstruct and analyse approval periods |
| `ApprovalPeriodSummary` | One row per current User Story | Stores the derived current approval-period summary used by approval-age analysis |
| `RequirementFieldStatus` | One row per current User Story | Stores current requirements-completeness indicators derived from source-field assessment |
| `FeatureWorkItemIDs` | One row per valid Feature work-item ID | Provides a controlled lookup population for validating User Story parent relationships |
| `RequirementsHealthReasons` | One row per User Story per applicable issue reason | Supports issue-level analysis where a single requirement can have more than one health problem |

### Presentation Helper

`Executive Exception Type` is a small disconnected helper table that provides the controlled category axis for the **Material Governance Exceptions** visual.

It does not represent another analytical business entity and is therefore kept separate from the six material analytical tables.

## Relationship Design

The relationships reflect the different grains of the analytical structures.

| From | To | Cardinality | Filter Direction |
|---|---|---:|---|
| `CurrentApprovals` | `ApprovalHistory` | One-to-many | Single |
| `CurrentApprovals` | `ApprovalPeriodSummary` | One-to-one | Both |
| `CurrentApprovals` | `RequirementFieldStatus` | One-to-one | Single |
| `CurrentApprovals` | `RequirementsHealthReasons` | One-to-many | Single |

`FeatureWorkItemIDs` remains disconnected and is referenced through analytical logic when validating whether a parent work item represents a valid Feature.

`Executive Exception Type` is also disconnected because it exists solely to provide controlled presentation categories to a DAX measure.

## Current-State as the Reporting Anchor

`CurrentApprovals` acts as the principal current-state table.

This gives report measures and filters a consistent one-row-per-User-Story population while allowing supporting tables to retain the grain needed for their individual analytical purposes.

This design is important because `ApprovalHistory` contains multiple records for each User Story. Using the historical table directly for current KPIs could otherwise cause current requirement counts to be multiplied by the number of historical snapshots.

## Historical Approval Analysis

`ApprovalHistory` retains the daily historical records required to understand approval-state changes over time.

`ApprovalPeriodSummary` provides the corresponding current approval-period result for each User Story.

Separating these structures allows the model to retain detailed history while exposing a compact current-period representation for approval-age measures and reporting.

## Requirements-Health Model

Requirements-health reporting combines several analytical inputs.

`RequirementFieldStatus` provides current completeness indicators for mandatory requirement information.

`FeatureWorkItemIDs` supports validation of parent Feature relationships.

The resulting health logic classifies each current User Story as:

- **Healthy**
- **Attention Required**
- **Critical**

Where several issues apply to the same User Story, `RequirementsHealthReasons` retains each applicable reason independently.

This means the model can distinguish between:

- the number of requirements affected; and
- the total number of individual requirements-health issues.

## Business Logic and Measures

The semantic model contains reusable measures rather than embedding calculations independently into individual visuals.

Representative measure groups include:

### Approval Governance

- Active Approval Requests
- Overdue Approval Requests
- Approved Work Items
- Unapproved Work Items
- Missing Authoriser Count
- Percentage Overdue
- Days Since Approval Started
- Oldest Approval Request Age
- Average Approval Request Age
- Average Overdue Days

### Requirements Health

- Total Requirements
- Healthy Requirements
- Attention Required Requirements
- Critical Requirements
- Healthy Requirements Percentage
- Total Requirements Issues

### Executive Reporting

- Awaiting Approval Requests
- Completed or Closed Unapproved Count
- Executive Exception Count
- Requirements Requiring Attention

## Project Evidence

### Implemented Semantic Model

![Azure DevOps Governance Analytics semantic model](/assets/projects/azure-devops-governance-analytics/semantic-model.png)

*Implemented Power BI semantic model showing the separation of current-state, historical, approval-period, requirements-completeness and issue-level analytical structures.*

**What this demonstrates:**  
The model was designed around analytical grain and reporting behaviour. Current-state reporting is anchored on one row per User Story while historical and issue-level structures retain the additional records required for their specific analytical purposes.

### Model Design Evidence

| Analytical Requirement | Model Design Response |
|---|---|
| Current KPIs must count each User Story once | `CurrentApprovals` provides one current row per User Story |
| Historical approval behaviour must be retained | `ApprovalHistory` retains dated work-item snapshots |
| Current approval-period information is repeatedly required | `ApprovalPeriodSummary` stores one summary row per current User Story |
| Requirements completeness must be assessed independently from approval history | `RequirementFieldStatus` stores current field-status indicators |
| Parent work items must be validated as Features | `FeatureWorkItemIDs` provides the valid Feature population |
| One requirement may have several health issues | `RequirementsHealthReasons` uses one row per applicable issue |
| Executive exception categories require a controlled presentation axis | Disconnected `Executive Exception Type` helper table |
| Current filters must propagate into historical analysis without allowing history to distort current counts | Controlled relationship cardinality and filter direction |

**What this demonstrates:**  
Table grain, relationships and helper structures were chosen to solve specific analytical problems rather than replicating the Azure DevOps source schema directly.

### Representative DAX — Awaiting Approval

The Executive Governance Overview distinguishes requests that are actively awaiting approval from those that have already become overdue.

```DAX
Awaiting Approval Requests =
VAR ActiveRequests =
    [Active Approval Requests]
VAR OverdueRequests =
    [Overdue Approval Requests]
RETURN
    COALESCE (
        ActiveRequests - OverdueRequests,
        0
    )

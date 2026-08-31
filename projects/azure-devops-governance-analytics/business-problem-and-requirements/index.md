# Business Problem & Requirements

[← Project Overview](/projects/azure-devops-governance-analytics/) · [Solution Architecture →](/projects/azure-devops-governance-analytics/solution-architecture/)

## Overview

This stage of the project established the business need, reporting objectives and measurable requirements for the Azure DevOps Governance Analytics solution before development began.

The analysis translated a broad governance concern into specific reporting behaviours, business rules, KPIs and validation criteria that could be implemented and tested in Power BI.

## Business Problem

Azure DevOps contained the information needed to monitor requirement approval activity, but the available work-item views did not provide a concise governance picture.

Users needed a reliable way to identify:

- User Stories awaiting approval;
- approval requests that had exceeded the defined seven-day threshold;
- the current responsible authoriser;
- requirements with missing mandatory information;
- requirements in a Critical or Attention Required state; and
- the overall governance position for senior review.

Without a consolidated analytical view, identifying these conditions required manual inspection of individual work items and provided limited visibility of the overall governance position.

## Desired Outcome

The required solution needed to turn Azure DevOps data into a small set of decision-focused Power BI views that could support both operational follow-up and management oversight.

The final reporting structure was designed around four business-facing views:

1. **Executive Governance Overview** — overall approval and requirements-health position.
2. **Approval Governance Summary** — approval workload, overdue position and approval-age indicators.
3. **Overdue Approval Exceptions** — actionable User Stories requiring approval follow-up.
4. **Requirements Health** — objective assessment of requirements completeness and governance health.

A separate **Validation / Model Validation** page supports technical assurance and reconciliation.

## Requirements Approach

Requirements were documented before implementation and converted into identifiable functional requirements, non-functional requirements, business rules, KPI definitions and success criteria.

Examples of the rules established during analysis include:

- an approval request becomes active when an authoriser is present and the requirement remains unapproved;
- **Senior Authorised By** takes precedence when both authorisation fields are populated;
- an active approval request becomes overdue after **seven whole calendar days**;
- the approval-period start date is treated as **day zero**;
- mandatory requirements completeness includes Title, State, Area Path, Parent Feature, Description and Acceptance Criteria;
- overdue approvals and completed or closed requirements that remain unapproved are classified as **Critical**;
- missing mandatory information results in **Attention Required** where no Critical condition applies; and
- all applicable requirements-health reasons are retained even where one overall health status is displayed.

These rules created a controlled basis for Power Query transformation, semantic-model logic, DAX measures and subsequent validation.

## Project Evidence

The examples below are selected from the controlled project requirements and demonstrate how the business problem was converted into measurable solution behaviour.

### Selected Business Objectives

| Objective | Intended Outcome |
|---|---|
| **OBJ-001** | Reliably identify overdue approval requests using the current continuous approval period |
| **OBJ-002** | Enable targeted follow-up and clear current-authoriser accountability |
| **OBJ-003** | Provide consistent evidence-based governance monitoring and escalation |
| **OBJ-004** | Provide objective requirements-health classification and reasons |
| **OBJ-005** | Provide an executive summary of approval governance, requirements health and material exception concentration |
| **OBJ-006** | Provide consistent filtering, navigation and supporting detail |

**What this demonstrates:**  
The reporting solution was designed around defined business outcomes rather than beginning with dashboard visuals and fitting requirements around them afterwards.

### Selected Functional Requirements

| Requirement | Requirement Example | Delivered Through |
|---|---|---|
| **FR-001–FR-006** | Identify and present User Stories meeting the overdue-approval rules, including current responsible authoriser and approval age | Overdue Approval Exceptions |
| **FR-007–FR-014** | Provide approval-governance KPIs including active requests, overdue requests, percentage overdue and approval-age measures | Approval Governance Summary |
| **FR-015–FR-026** | Assess current User Stories using objective requirements-health rules and retain applicable health reasons | Requirements Health |
| **FR-027–FR-038** | Present executive approval position, requirements health and material governance exceptions | Executive Governance Overview |
| **FR-039–FR-048** | Provide consistent filtering, reset behaviour and navigation across the principal report pages | Report interaction and navigation |
| **FR-049–FR-052** | Provide supporting row-level detail and controlled model/reconciliation validation | Exception, health and validation views |

**What this demonstrates:**  
Requirements were expressed as testable reporting outcomes and mapped to specific parts of the implemented Power BI solution.

### Selected Business Rules

| Business Rule Area | Rule Applied |
|---|---|
| **Approval period** | The current continuous approval period is derived from the available Azure DevOps history and is used as the basis for approval-age calculation |
| **Authoriser precedence** | Senior Authorised By takes precedence when both authorisation fields are populated, while each User Story is counted once |
| **Overdue threshold** | Approval age uses whole calendar days, the approval-period start date is day zero and an active request becomes overdue at seven days |
| **Requirements completeness** | Mandatory assessment includes Title, State, Area Path, Parent Feature, Description and Acceptance Criteria |
| **Health classification** | Critical takes precedence over Attention Required; Healthy applies where no applicable issue exists |
| **Health reasons** | All applicable health reasons are retained even where one overall status is displayed |
| **Executive exceptions** | Material governance exception indicators may overlap and must not be interpreted as one additive population |
| **Requirements requiring attention** | Critical and Attention Required are mutually exclusive overall statuses and can therefore be combined into a unique unhealthy population |

**What this demonstrates:**  
Business rules were separated from presentation design so the same definitions could be applied consistently through data preparation, semantic modelling, DAX, reporting and testing.

### Selected Success Criteria

| Success Criterion | Expected Outcome |
|---|---|
| **Approval accuracy** | Controlled overdue and non-overdue scenarios are classified correctly |
| **Requirements health** | Controlled Healthy, Attention Required and Critical scenarios produce the expected classifications and reasons |
| **Executive reconciliation** | Executive approval and requirements-health totals reconcile to the underlying current User Story population |
| **Filtering and navigation** | Area Path, Iteration Path, reset controls and principal-page navigation behave consistently |
| **Performance** | Principal report visuals remain within the defined Power BI performance thresholds |
| **Portfolio release** | Public evidence contains only approved synthetic, anonymised or sanitised information |

**What this demonstrates:**  
Acceptance was defined in measurable terms, allowing the completed solution to be validated against expected behaviour rather than judged only by whether the dashboards appeared correct.

## Evidence Presented

The public case study presents selected evidence from the controlled requirements phase, including:

- business context and problem definition;
- desired business outcomes;
- project scope and boundaries;
- functional and non-functional requirements;
- approval-governance business rules;
- requirements-health classification rules;
- KPI and measure definitions;
- success and acceptance criteria;
- stakeholder and persona analysis; and
- requirements traceability through implementation and testing.

The complete controlled Business Requirements Document remains part of the private project documentation, while the public case study presents the elements most useful for demonstrating the analysis and decision-making behind the solution.

[← Project Overview](/projects/azure-devops-governance-analytics/) · [Solution Architecture →](/projects/azure-devops-governance-analytics/solution-architecture/)

---

© 2026 Carl Patten. All rights reserved.

# Business Problem & Requirements

[← Project Overview](/projects/power-bi-governance-analytics/) · [Solution Architecture →](/projects/power-bi-governance-analytics/solution-architecture/)

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

## Evidence Presented

The public case study demonstrates selected evidence from the requirements phase, including:

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

The complete controlled Business Requirements Document remains part of the project documentation, while the public case study presents the elements most useful for demonstrating the analysis and decision-making behind the solution.

[← Project Overview](/projects/power-bi-governance-analytics/) · [Solution Architecture →](/projects/power-bi-governance-analytics/solution-architecture/)

---

© 2026 Carl Patten. All rights reserved.

# 03 — Design Representative Test Scenarios

[← Selected Subprocesses](/delivery-frameworks/power-bi-end-to-end/selected-subprocesses/) · [Power BI Framework Overview](/delivery-frameworks/power-bi-end-to-end/)

## Purpose

This subprocess demonstrates how representative validation scenarios are designed before implementation begins.

The objective is to define controlled test conditions and expected results while the approved requirements, business rules and data requirements are still the authoritative baseline.

This reduces the risk of validating a completed solution against what was ultimately built rather than against what the solution was originally required to do.

## Process Diagram

![03 - Design Representative Test Scenarios](/assets/delivery-frameworks/power-bi-end-to-end/selected-subprocesses/03-design-representative-test-scenarios-public.png)

*03 — Design Representative Test Scenarios. Selected subprocess from the Power BI End-to-End Delivery Framework. © 2026 Carl Patten. Portfolio copy.*
> The editable process model is retained privately.

## What This Demonstrates

This subprocess provides evidence of:

* requirements-led test design;
* definition of normal and exception scenarios;
* explicit boundary-condition testing;
* treatment of blank, null and conflicting values;
* inclusion and exclusion testing;
* testing of changes over time;
* validation of precedence and fallback rules;
* definition of expected results before implementation testing;
* stable test identifiers;
* requirements-to-test traceability; and
* creation of a reusable regression-test baseline.

## Process-to-Document Traceability

Activities within the subprocess use approved requirements and data definitions as inputs and progressively build controlled validation artefacts.

The examples below demonstrate how business rules are converted into testable conditions, how expected results are established before implementation and how the resulting test baseline remains traceable to the requirements it protects.

### Selected Association Examples

#### 03-T03 — Identify Boundary Conditions

| Association | Document                            | Section(s)                                                    | Purpose                                                                                                                               |
| ----------- | ----------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Input       | `01 Business Requirements Document` | `01.8.5` KPI and Measure Catalogue<br>`01.8.6` Business Rules | Supplies thresholds, date rules, limits, classifications and calculation logic for which exact boundary cases must be tested.         |
| Output      | `05 Test and Validation Record`     | `05.6` Validation Scenario Register                           | Records threshold and boundary scenarios such as immediately below, exactly at and immediately above defined limits or date cut-offs. |

This creates explicit validation around the points at which analytical behaviour changes, rather than relying only on ordinary test records.

#### 03-T10 — Record the Expected Result for Each Scenario

| Association | Document                            | Section(s)                                                                                         | Purpose                                                                                                                                                  |
| ----------- | ----------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Input       | `05 Test and Validation Record`     | `05.6` Validation Scenario Register                                                                | Supplies the complete set of representative scenarios that require an expected result.                                                                   |
| Input       | `01 Business Requirements Document` | `01.8.5` KPI and Measure Catalogue<br>`01.8.6` Business Rules<br>`01.11` Solution Success Criteria | Supplies the approved calculation, business-rule and success-criterion baseline against which the expected result is defined.                            |
| Output      | `05 Test and Validation Record`     | `05.7` Expected Results Register                                                                   | Records the expected output for each scenario before implementation testing so that later validation compares actual results with a predefined baseline. |

Defining expected results at this stage helps preserve independence between **what the solution should do** and **what the implementation happens to produce**.

#### 03-T12 — Retain the Scenarios for Regression Testing

| Association | Document                        | Section(s)                                                                                             | Purpose                                                                                                                                                     |
| ----------- | ------------------------------- | ------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Input       | `05 Test and Validation Record` | `05.5` Controlled Test Data<br>`05.6` Validation Scenario Register<br>`05.7` Expected Results Register | Supplies the controlled data, stable scenarios and expected results that form the reusable regression set.                                                  |
| Output      | `05 Test and Validation Record` | `05.19` Regression-Test Baseline                                                                       | Baselines the representative scenarios and expected results for repeated use during transformation, model, report, end-to-end and final regression testing. |
| Output      | `03 Requirements Traceability`  | `03.1.1` Requirement Traceability Matrix (RTM)                                                         | Confirms that the retained regression scenarios remain traceable to the approved requirements they protect.                                                 |

This means the scenarios created early in delivery are not discarded after initial testing. They provide a controlled baseline that can be reused as the solution changes.

> These are representative associations only. The complete subprocess maintains task-level input and output associations across all delivery activities and is retained as part of the private framework.

## Relationship to the End-to-End Framework

**Design Representative Test Scenarios** follows:

**02 — Define Data Requirements**

At this point, the business requirements and the required data population, history and granularity are sufficiently understood to design representative validation scenarios.

Its outputs then support:

**04 — Design the Source Extraction**

and later transformation, semantic-model, report and end-to-end validation activities.

Designing the scenarios this early helps ensure that later technical decisions remain testable against requirements and controlled expected results.

## Portfolio Evidence Boundary

This page presents selected evidence sufficient to demonstrate the subprocess structure, validation philosophy and traceability approach.

The following remain private:

* editable process-model source;
* complete task definitions;
* the full controlled test-data design;
* the complete validation-scenario register;
* the complete expected-results register;
* the complete task-to-document association table; and
* reusable testing and validation templates.

---

[← Previous Selected Example: 01 — Define the Business Problem →](../01-define-the-business-problem/) · [Selected Subprocesses](/delivery-frameworks/power-bi-end-to-end/selected-subprocesses/) · [Next Selected Example: 05 — Build Power Query Transformations →](../05-build-power-query-transformations/)

---

© 2026 Carl Patten. All rights reserved.

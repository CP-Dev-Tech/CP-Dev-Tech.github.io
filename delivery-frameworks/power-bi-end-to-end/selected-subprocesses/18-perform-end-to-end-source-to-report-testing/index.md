# 18 — Perform End-to-End Source-to-Report Testing

[← Selected Subprocesses](/delivery-frameworks/power-bi-end-to-end/selected-subprocesses/) · [Power BI Framework Overview](/delivery-frameworks/power-bi-end-to-end/)

## Purpose

This subprocess demonstrates how the completed analytical solution is validated across the full path from configured source extraction through Power Query, semantic modelling and report behaviour.

The objective is to establish that the individual components do not merely work in isolation, but operate correctly together as a complete source-to-report chain.

Testing therefore covers data movement, transformation logic, analytical grain, relationships, calculations, report outputs, interactions, access controls, reconciliation, refresh behaviour and operational evidence against previously defined scenarios and expected results.

## Process Diagram

![18 - Perform End-to-End source-to_Report Testing subprocess](/assets/delivery-frameworks/power-bi-end-to-end/selected-subprocesses/18-perform-end-to-end-source-to-report-testing-public.png)

*18 — Perform End-to-End Source-to-Report Testing. Selected subprocess from the Power BI End-to-End Delivery Framework. © 2026 Carl Patten. Portfolio copy.*
> The editable process model is retained privately.

## What This Demonstrates

This subprocess provides evidence of:

* controlled end-to-end test scope and acceptance criteria;
* use of representative source records and predefined expected results;
* execution of the configured extraction, refresh and load process;
* source-to-Power Query validation;
* transformation-rule validation;
* semantic-model grain validation;
* relationship and calculation validation;
* filter-context validation;
* report-output and interaction testing;
* role-based access validation;
* representative-record reconciliation;
* row-count and distinct-count reconciliation;
* refresh-completion and data-freshness validation;
* consolidation and assessment of defects;
* testing against approved success criteria;
* controlled remediation and retesting;
* preservation of regression coverage; and
* structured hand-off into performance and scalability assessment.

## Process-to-Document Traceability

End-to-end testing draws together controlled information established throughout the preceding delivery lifecycle.

Source configuration, transformation logic, semantic-model specifications, report design, implementation, security and operational expectations provide the approved baselines against which actual solution behaviour is tested.

The resulting evidence is consolidated within the Test and Validation Record and linked back to the relevant implementation and supporting technical artefacts.

### Selected Association Examples

#### 18-T04 — Validate Source-to-Power Query Movement and Transformations

| Association        | Document                              | Section(s)                                                                                                                                                                                                                                                                                                                                    | Purpose                                                                                                                                                                       |
| ------------------ | ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Input              | `06 Data Source Configuration`        | `06.8` Extraction Scope<br>`06.9` Source Objects<br>`06.10` Source Field List<br>`06.11` Source-Level Filters<br>`06.12` History Window<br>`06.13` Extraction and Snapshot Granularity<br>`06.14` Deleted, Removed and Inactive Records<br>`06.15` Custom and Extended Fields                                                                 | Supplies the expected source records, fields, filters, historical coverage, grain and record-treatment rules against which movement into the transformation layer is checked. |
| Input              | `07 Power Query and Data Preparation` | `07.3` Query Inventory<br>`07.5` Material Transformations<br>`07.6` Cleansing and Standardisation Rules<br>`07.7` Null and Blank Handling<br>`07.8` Duplicate Handling<br>`07.9` Derived Field Definitions<br>`07.10` Structural Transformations and Data-Type Controls<br>`07.12` Query Dependencies<br>`07.14` Refresh and Error Validation | Supplies the approved Power Query transformation logic and expected query behaviour being exercised during the end-to-end test.                                               |
| Output             | `05 Test and Validation Record`       | `05.8` Source-to-Report Validation<br>`05.9` Power Query Transformation Validation                                                                                                                                                                                                                                                            | Records representative source-to-query comparisons and the results of transformation-rule validation.                                                                         |
| Output             | `07 Power Query and Data Preparation` | `07.14` Refresh and Error Validation                                                                                                                                                                                                                                                                                                          | Records the end-to-end transformation and query-refresh outcome and links to supporting evidence.                                                                             |
| Conditional Output | `05 Test and Validation Record`       | `05.16` Discrepancy and Data-Quality Issue Register                                                                                                                                                                                                                                                                                           | Records missing, changed, duplicated, mistyped or incorrectly transformed data where the expected and actual results differ.                                                  |

This demonstrates that the Power Query layer is not validated only by confirming that it refreshes successfully. Representative records and transformation rules are checked back to the authoritative source definition and expected transformation behaviour.

#### 18-T06 — Validate Report Outputs, Interactions and Role-Based Access

| Association        | Document                               | Section(s)                                                                                                                                                                                                                                                                                              | Purpose                                                                                                             |
| ------------------ | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Input              | `09 Report Design and User Experience` | `09.7` Report Page Catalogue<br>`09.9` Business Question and KPI Mapping<br>`09.12` Navigation<br>`09.13` Filters and Slicers<br>`09.14` Visual Interactions<br>`09.15` Drill-Through, Tooltips and Supporting Detail<br>`09.18` Empty, Error and No-Data States<br>`09.20` Requirements Traceability   | Supplies the approved report behaviour and user-experience baseline against which the implemented report is tested. |
| Input              | `10 Power BI Implementation`           | `10.7` Report Page Inventory<br>`10.8` Visual Inventory<br>`10.11` Navigation and Interactions<br>`10.12` Filters and Slicers<br>`10.13` Drill-Through and Tooltips<br>`10.14` Bookmarks, Buttons and Selection States<br>`10.16` Empty, Error and No-Data Behaviour<br>`10.17` Security Implementation | Supplies the report pages, visuals, interactions, states and implemented security configuration being exercised.    |
| Input              | `12 Security and Access Control`       | `12.8` Workspace Access<br>`12.9` App Audiences and Consumer Access<br>`12.10` Semantic-Model Permissions<br>`12.11` Row-Level Security<br>`12.12` Object-Level Security<br>`12.13` Sharing, Export and Download Controls<br>`12.14` External and Guest Access                                          | Supplies the approved audience, permission and security behaviour expected for representative users.                |
| Output             | `10 Power BI Implementation`           | `10.21` Validation Evidence                                                                                                                                                                                                                                                                             | Records links to evidence confirming report outputs, interactions, states and role-based behaviour.                 |
| Conditional Output | `05 Test and Validation Record`        | `05.16` Discrepancy and Data-Quality Issue Register                                                                                                                                                                                                                                                     | Records inaccurate visuals, failed interactions, incorrect states or access-control defects.                        |
| Conditional Output | `12 Security and Access Control`       | `12.11.3` RLS Validation<br>`12.21` Security Risks and Exceptions                                                                                                                                                                                                                                       | Records role-test results and any material security exception identified during end-to-end validation.              |

This establishes that end-to-end validation extends beyond numerical accuracy. The delivered report must also behave correctly for the intended user, interaction path and access context.

#### 18-T13 — Record End-to-End Validation and Performance Hand-Off

| Association | Document                                | Section(s)                                                                                                                                                                                                                                                                                                                                                                                                                                     | Purpose                                                                                                                                  |
| ----------- | --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Output      | `05 Test and Validation Record`         | `05.8` Source-to-Report Validation<br>`05.9` Power Query Transformation Validation<br>`05.10` Current-State and Historical-Grain Validation<br>`05.11` Relationship Validation<br>`05.12` Calculated-Column Validation<br>`05.13` Measure and Filter-Context Validation<br>`05.14` Metadata and Report-Author Validation<br>`05.15` Refresh Validation<br>`05.19` Regression-Test Baseline<br>`05.20` Validation Summary<br>`05.22` Change Log | Baselines the completed end-to-end results, reusable regression coverage, validation conclusion and controlled revision history.         |
| Output      | `10 Power BI Implementation`            | `10.21` Validation Evidence<br>`10.23` Revision History                                                                                                                                                                                                                                                                                                                                                                                        | Baselines the end-to-end evidence references against the implementation revision that was tested.                                        |
| Output      | `08 Semantic Model Specification`       | `08.17` Validation References                                                                                                                                                                                                                                                                                                                                                                                                                  | Confirms the end-to-end evidence supporting model grain, relationships, calculations and reporting capability.                           |
| Output      | `13 Operational Support and Monitoring` | `13.11` Performance and Capacity Monitoring                                                                                                                                                                                                                                                                                                                                                                                                    | Records observed refresh duration, page-response or capacity indicators that require assessment in the following performance subprocess. |
| Output      | `10 Power BI Implementation`            | `10.18.1` Performance Test Results                                                                                                                                                                                                                                                                                                                                                                                                             | Establishes the initial evidence or observations required for formal performance and scalability assessment.                             |

This closes the end-to-end test cycle without confusing **functional correctness** with **performance optimisation**. The solution must first demonstrate that the complete analytical chain behaves correctly; observed performance evidence is then handed to the dedicated performance and scalability subprocess.

> These are representative associations only. The complete subprocess maintains task-level input and output associations across all end-to-end validation activities and is retained as part of the private framework.

## End-to-End Reconciliation

An important part of this subprocess is reconciliation between the controlled source baseline and the resulting Power BI data.

Representative records, row counts and distinct counts are compared using known source values and expected results.

Differences are not automatically treated as defects. Where a difference is expected because of an approved filter, transformation, duplicate rule or model grain, the reason should be explainable and supported by the controlled design.

Unexplained differences are recorded for investigation.

This provides evidence that report accuracy is supported by a traceable data chain rather than being inferred solely from whether the final visual appears reasonable.

## Defect, Remediation and Retest Control

A failed end-to-end test does not immediately move the solution forward.

Failures are consolidated and assessed against approved criteria. Where correction is required, the affected source configuration, Power Query logic, semantic model, report design, implementation, security configuration or operational documentation is updated as applicable.

Only the affected end-to-end tests are then repeated against the original scenarios and expected results.

The retest evidence records whether the issue:

* has been resolved;
* remains open; or
* is proposed as an explicitly accepted limitation.

This provides a controlled feedback loop while protecting the existing regression baseline.

## Relationship to the End-to-End Framework

**Perform End-to-End Source-to-Report Testing** follows:

**17 — Configure Refresh and Operational Settings**

The complete analytical path — including source configuration, transformations, semantic model, reports, interactions, security and operational refresh behaviour — can therefore be exercised as a connected solution.

When the end-to-end validation criteria are satisfied, the subprocess hands off to:

**19 — Assess and Optimise Performance and Scalability**

This sequencing deliberately separates:

**Does the solution behave correctly?**

from:

**Does the correctly functioning solution perform and scale acceptably?**

Performance observations captured during end-to-end testing become the baseline for the dedicated optimisation activity that follows.

## Validation Principles

The subprocess applies several principles intended to provide reliable evidence of solution correctness:

* test against previously defined expected results;
* use representative controlled source records;
* validate the complete data path rather than isolated components only;
* reconcile values and counts back to authoritative source data;
* test semantic-model behaviour under realistic filter context;
* validate user-facing behaviour as well as analytical results;
* include representative access and security conditions;
* test refresh and freshness behaviour;
* record discrepancies rather than silently adjusting expected results;
* re-run affected tests following remediation;
* preserve reusable regression coverage; and
* maintain evidence against the specific implementation revision tested.

## Portfolio Evidence Boundary

This page presents selected evidence sufficient to demonstrate the end-to-end validation method and its relationship to the wider delivery framework.

The following remain private:

* editable process-model source;
* complete task-to-document association data;
* complete validation scenarios and expected-results registers;
* controlled test datasets;
* detailed reconciliation evidence;
* defect and resolution records;
* complete regression-test baseline;
* reusable Test and Validation Record template; and
* project-specific test evidence.

---

[← Previous Selected Example: 13 — Build Report Pages →](../13-build-report-pages/) · [Selected Subprocesses](/delivery-frameworks/power-bi-end-to-end/selected-subprocesses/) · [Power BI Framework Overview](/delivery-frameworks/power-bi-end-to-end/)

---

© 2026 Carl Patten. All rights reserved.

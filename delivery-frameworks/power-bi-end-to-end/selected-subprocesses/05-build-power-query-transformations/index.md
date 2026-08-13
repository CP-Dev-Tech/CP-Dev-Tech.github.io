# 05 — Build Power Query Transformations

[← Selected Subprocesses](/delivery-frameworks/power-bi-end-to-end/selected-subprocesses/) · [Power BI Framework Overview](/delivery-frameworks/power-bi-end-to-end/)

## Purpose

This subprocess demonstrates how an approved source-extraction design is translated into controlled, maintainable Power Query transformations that prepare data for analytical modelling.

The objective is not simply to manipulate source data until it produces the required report output. Transformation decisions remain grounded in approved source configuration, business rules, analytical definitions and data-quality requirements, with material implementation logic documented for later validation and maintenance.

## Process Diagram

![05 - Build Power Query Transformations subprocess](/assets/delivery-frameworks/power-bi-end-to-end/selected-subprocesses/05-build-power-query-transformations-public.png)

*05 — Build Power Query Transformations Selected subprocess from the Power BI End-to-End Delivery Framework. © 2026 Carl Patten. Portfolio copy.*
> The editable process model is retained privately.


## What This Demonstrates

This subprocess provides evidence of:

* controlled source connection and staging design;
* selection of only required records and fields;
* consistent query and field naming;
* explicit treatment of blank, null and non-standard values;
* data cleansing and standardisation;
* implementation of approved business rules;
* reusable referenced-query design;
* grouping, merging, expansion, pivoting and other structural transformations where required;
* explicit revalidation of data types after structural change;
* deterministic duplicate handling;
* creation of derived fields;
* query-dependency management;
* query-folding and performance considerations;
* separation of staging and model-facing queries;
* build-level refresh and error checking;
* full model-refresh confirmation; and
* documentation and traceability of material transformations.

## Process-to-Document Traceability

Power Query implementation is controlled by information already defined within the Business Requirements Document and Data Source Configuration.

Material transformation decisions are recorded in the Power Query and Data Preparation artefact and remain linked to the requirements and business rules that caused them to be implemented.

### Selected Association Examples

#### 05-T09 — Apply Business Rule Transformations

| Association | Document                              | Section(s)                                                                       | Purpose                                                                                                                                                                          |
| ----------- | ------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Input       | `01 Business Requirements Document`   | `01.8.5` KPI and Measure Catalogue<br>`01.8.6` Business Rules                    | Supplies the approved business definitions and rules that determine which logic should be implemented during data preparation rather than deferred to the semantic model or DAX. |
| Input       | `03 Requirements Traceability`        | `03.1.1` Requirement Traceability Matrix (RTM)<br>`03.1.2` Traceability Approach | Supplies requirement-to-design traceability so that material transformation logic remains connected to the requirements and business rules it implements.                        |
| Output      | `07 Power Query and Data Preparation` | `07.5` Material Transformations                                                  | Records the material Power Query transformations used to implement the approved business logic.                                                                                  |

This establishes a direct chain between **business requirement → transformation decision → documented implementation**, rather than allowing transformation logic to become undocumented technical behaviour.

#### 05-T13 — Apply Deterministic Duplicate Handling

| Association | Document                              | Section(s)                                                                   | Purpose                                                                                                                                        |
| ----------- | ------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Input       | `01 Business Requirements Document`   | `01.8.6` Business Rules<br>`01.9.6` Data Quality, Lineage and Reconciliation | Supplies the approved grain, duplicate, precedence and data-quality rules required to distinguish legitimate multiple records from duplicates. |
| Input       | `06 Data Source Configuration`        | `06.13` Extraction and Snapshot Granularity                                  | Supplies the approved source grain against which duplicate records must be assessed.                                                           |
| Output      | `07 Power Query and Data Preparation` | `07.8` Duplicate Handling                                                    | Records the deterministic duplicate-identification and resolution rule, including the retained record or applicable precedence logic.          |

The important principle is that duplicate removal is not treated as an arbitrary technical clean-up step. The treatment must be repeatable and based on the intended analytical grain and approved business rules.

#### 05-T22 — Document Material Transformations

| Association | Document                              | Section(s)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Purpose                                                                                                                                                                                                 |
| ----------- | ------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Input       | `07 Power Query and Data Preparation` | `07.3` Query Inventory<br>`07.4` Source Connection and Staging Design<br>`07.5` Material Transformations<br>`07.6` Cleansing and Standardisation Rules<br>`07.7` Null and Blank Handling<br>`07.8` Duplicate Handling<br>`07.9` Derived Field Definitions<br>`07.10` Structural Transformations and Data-Type Controls<br>`07.12` Query Dependencies<br>`07.13` Query Folding and Performance<br>`07.14` Refresh and Error Validation                                                                    | Supplies the completed as-built Power Query configuration that must be consolidated into the controlled transformation record.                                                                          |
| Input       | `03 Requirements Traceability`        | `03.1.2` Traceability Approach                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Supplies the agreed method for maintaining links between requirements, business rules, transformation artefacts and later validation evidence.                                                          |
| Output      | `07 Power Query and Data Preparation` | `07.3` Query Inventory<br>`07.4` Source Connection and Staging Design<br>`07.5` Material Transformations<br>`07.6` Cleansing and Standardisation Rules<br>`07.7` Null and Blank Handling<br>`07.8` Duplicate Handling<br>`07.9` Derived Field Definitions<br>`07.10` Structural Transformations and Data-Type Controls<br>`07.12` Query Dependencies<br>`07.13` Query Folding and Performance<br>`07.14` Refresh and Error Validation<br>`07.15` Known Limitations and Remediation<br>`07.16` Change Log | Baselines the material Power Query implementation, including query roles, transformation logic, data-quality treatment, dependencies, performance considerations, refresh checks and known limitations. |
| Output      | `03 Requirements Traceability`        | `03.1.1` Requirement Traceability Matrix (RTM)                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Updates the RTM so that material Power Query transformations can be traced back to the requirements and business rules they implement and forward to the validation evidence produced later.            |

This prevents important transformation logic from existing only inside the Power BI file. The as-built implementation becomes part of the controlled project documentation and remains traceable through the delivery lifecycle.

> These are representative associations only. The complete subprocess maintains task-level input and output associations across all Power Query delivery activities and is retained as part of the private framework.

## Relationship to the End-to-End Framework

**Build Power Query Transformations** follows:

**04 — Design the Source Extraction**

The source, connector, fields, record population, historical window, extraction grain and access requirements should therefore already have been defined before detailed transformation work begins.

The subprocess produces the transformed and documented data-preparation layer required by:

**06 — Validate the Transformed Data**

The build-level checks performed here confirm that queries can refresh and that the completed transformations can be applied to the model. Formal validation of the resulting transformed data against source values, expected results and business rules occurs in the following subprocess.

## Design Principles

The subprocess applies several practical controls intended to improve maintainability and performance:

* filter early where practical;
* remove unused columns early;
* avoid repeated transformations;
* use referenced queries where logic is reusable;
* avoid unnecessary duplicate source connections;
* use clear applied-step names;
* apply explicit data types rather than relying solely on inference;
* preserve query folding where relevant;
* separate staging logic from model-facing logic; and
* recheck data types after structural transformations that may remove or alter type metadata.

These controls help ensure that Power Query is treated as a designed transformation layer rather than an unmanaged sequence of applied steps.

## Portfolio Evidence Boundary

This page presents selected evidence sufficient to demonstrate the Power Query delivery approach, technical controls and traceability model.

The following remain private:

* editable process-model source;
* complete task-to-document association data;
* full Power Query and Data Preparation template;
* complete transformation implementation guidance;
* reusable Power Query code and patterns; and
* project-specific source or transformation logic.

---

[← Previous Selected Example: 03 — Design Representative Test Scenarios →](../03-design-representative-test-scenarios/) · [Selected Subprocesses](/delivery-frameworks/power-bi-end-to-end/selected-subprocesses/) · [Next Selected Example: 07 — Define the Semantic Model →](../07-define-the-semantic-model/)

---

© 2026 Carl Patten. All rights reserved.

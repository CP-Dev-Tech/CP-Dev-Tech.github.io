# 07 — Define the Semantic Model

[← Selected Subprocesses](/delivery-frameworks/power-bi-end-to-end/selected-subprocesses/) · [Power BI Framework Overview](/delivery-frameworks/power-bi-end-to-end/)

## Purpose

This subprocess demonstrates how validated transformed data is converted into a deliberate semantic-model design before relationships, calculated columns, measures and report-facing metadata are implemented.

The objective is to establish the analytical structure of the model — including table grain, table roles, keys, field ownership, dimensional requirements and the appropriate location of business logic — before detailed implementation begins.

This helps prevent the semantic model from simply reflecting the physical shape of the source data.

## Process Diagram

![07 - Define the Semantic Model subprocess](/assets/delivery-frameworks/power-bi-end-to-end/selected-subprocesses/07-define-the-semantic-model-public.png)

*07 — Define the Semantic Model Selected subprocess from the Power BI End-to-End Delivery Framework. © 2026 Carl Patten. Portfolio copy.*
> The editable process model is retained privately.

## What This Demonstrates

This subprocess provides evidence of:

* grain-first semantic-model design;
* identification of fact-like, snapshot, current-state and dimension tables;
* assessment of summary-table requirements;
* technical and natural business-key identification;
* explicit ownership of descriptive fields;
* consideration of future trend-analysis requirements;
* date-dimension design;
* role-playing date requirements;
* hierarchy-dimension assessment;
* bridge-table assessment;
* separation of transformation logic from model logic;
* deliberate placement of logic in Power Query, calculated columns or measures;
* model capability and limitation assessment;
* future scalability considerations; and
* requirements-to-model traceability.

## Process-to-Document Traceability

The semantic-model design is informed by validated data, approved requirements and the transformations already implemented upstream.

Design decisions are recorded in the Semantic Model Specification before the corresponding model components are implemented and validated.

### Selected Association Examples

#### 07-T01 — Define the Grain of Every Table

| Association | Document                                     | Section(s)                                                                                                              | Purpose                                                                                                                                    |
| ----------- | -------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Input       | `04 Data Requirements and Source Assessment` | `04.10` Historical Period<br>`04.11` Data Granularity                                                                   | Supplies the approved current-state, historical and row-grain requirements that the semantic-model tables must preserve.                   |
| Input       | `05 Test and Validation Record`              | `05.10` Current-State and Historical-Grain Validation<br>`05.18` Accepted Limitations<br>`05.20` Validation Summary     | Supplies evidence that the transformed data has the expected grain together with any accepted limitations that constrain the model design. |
| Input       | `07 Power Query and Data Preparation`        | `07.3` Query Inventory<br>`07.9` Derived Field Definitions<br>`07.10` Structural Transformations and Data-Type Controls | Supplies the validated transformed structures and fields available to the semantic model.                                                  |
| Output      | `08 Semantic Model Specification`            | `08.4` Table Grain and Table Roles                                                                                      | Records the intended row grain of each semantic-model table and establishes the basis for assigning its analytical role.                   |

Defining grain before relationships and calculations reduces the risk of ambiguous counting, duplicated entities and measures being created against an incorrectly understood table structure.

#### 07-T17 — Decide Which Logic Belongs in Measures

| Association | Document                            | Section(s)                                                    | Purpose                                                                                                                                                     |
| ----------- | ----------------------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Input       | `01 Business Requirements Document` | `01.8.5` KPI and Measure Catalogue<br>`01.8.6` Business Rules | Supplies approved KPI, aggregation and context-sensitive business logic that may be implemented as measures.                                                |
| Input       | `08 Semantic Model Specification`   | `08.4` Table Grain and Table Roles<br>`08.9` Logic Placement  | Supplies the model grain and preceding logic-placement decisions needed to determine which calculations should remain dynamic and filter-context dependent. |
| Output      | `08 Semantic Model Specification`   | `08.9` Logic Placement<br>`08.11` Measure Catalogue           | Records the logic assigned to measures and establishes the measure definitions that will be implemented and validated later.                                |

This makes calculation placement an explicit design decision rather than allowing business logic to accumulate wherever it is easiest to implement.

Logic that belongs upstream in Power Query, at row level in a calculated column or dynamically in a measure is therefore considered separately.

#### 07-T18 — Document the Design Rationale

| Association | Document                          | Section(s)                                                                                                                                                                                                                              | Purpose                                                                                                                                               |
| ----------- | --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Input       | `08 Semantic Model Specification` | `08.4` Table Grain and Table Roles<br>`08.5` Fact and Dimension Mapping<br>`08.6` Keys and Field Ownership<br>`08.7` Dimensional Design<br>`08.9` Logic Placement<br>`08.10` Calculated-Column Definitions<br>`08.11` Measure Catalogue | Supplies the completed semantic-model design decisions whose rationale, trade-offs and dependencies need to be consolidated.                          |
| Input       | `05 Test and Validation Record`   | `05.18` Accepted Limitations<br>`05.20` Validation Summary                                                                                                                                                                              | Supplies validated data limitations and conclusions that may constrain what the semantic model can reliably support.                                  |
| Input       | `03 Requirements Traceability`    | `03.1.2` Traceability Approach                                                                                                                                                                                                          | Supplies the agreed method for maintaining links between requirements, design decisions and later implementation and validation evidence.             |
| Output      | `08 Semantic Model Specification` | `08.14` Model Design Rationale<br>`08.15` Model Capabilities and Limitations<br>`08.16` Future Scalability Considerations<br>`08.17` Validation References<br>`08.18` Change Log                                                        | Records why the model has been designed as it has, what it can and cannot support, relevant future considerations and the controlled design revision. |
| Output      | `03 Requirements Traceability`    | `03.1.1` Requirement Traceability Matrix (RTM)                                                                                                                                                                                          | Updates the RTM so that key grain, table-role and calculation-design decisions remain traceable to the requirements they support.                     |

This means the semantic model is not documented only as a diagram of tables and relationships. The reasons behind the design, its limitations and its relationship to the business requirements are also retained.

> These are representative associations only. The complete subprocess maintains task-level input and output associations across all semantic-model design activities and is retained as part of the private framework.

## Relationship to the End-to-End Framework

**Define the Semantic Model** follows:

**06 — Validate the Transformed Data**

The data entering semantic-model design should therefore already have been checked for expected content, structure, grain, key values, duplicate treatment and material discrepancies.

The subprocess produces the controlled design required by:

**08 — Implement and Validate Relationships**

This separates **model design** from **model implementation**.

The intended table structure, keys, roles and dimensional behaviour are first defined here. Relationships are then implemented and validated against that approved design in the following subprocess.

## Design Principles

The subprocess applies several principles intended to keep the semantic model analytically reliable and maintainable:

* define the grain of every table before designing relationships;
* distinguish current-state, historical, snapshot and fact-like structures explicitly;
* identify both technical keys and meaningful business keys;
* avoid uncontrolled duplication of descriptive attributes across tables;
* design for required historical and future trend analysis;
* introduce date, hierarchy or bridge structures only where justified by the analytical need;
* place business logic deliberately at the most appropriate layer;
* document model limitations rather than concealing unsupported behaviour; and
* retain traceability between model decisions and the requirements they support.

## Portfolio Evidence Boundary

This page presents selected evidence sufficient to demonstrate the semantic-model design approach and its connection to requirements, data preparation and validation.

The following remain private:

* editable process-model source;
* complete task-to-document association data;
* the reusable Semantic Model Specification template;
* complete model-design guidance;
* full calculated-column and measure catalogues;
* project-specific semantic-model designs; and
* reusable modelling implementation patterns.

---

[← Previous Selected Example: 05 — Build Power Query Transformations →](../05-build-power-query-transformations/) · [Selected Subprocesses](/delivery-frameworks/power-bi-end-to-end/selected-subprocesses/) · [Next Selected Example: 13 — Build Report Pages →](../13-build-report-pages/)

---

© 2026 Carl Patten. All rights reserved.

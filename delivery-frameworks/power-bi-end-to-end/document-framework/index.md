# Document & Artefact Framework

[Home](/) · [Delivery Frameworks](/delivery-frameworks/) · [Power BI End-to-End](/delivery-frameworks/power-bi-end-to-end/) · **Document & Artefact Framework**

## Overview

The Power BI End-to-End Delivery Framework is supported by a controlled set of project documents and delivery artefacts.

These documents provide the information needed to define, design, build, validate, deploy and support an analytics solution while maintaining traceability between business need, technical implementation and validation evidence.

The framework deliberately avoids treating documentation as a retrospective exercise completed at the end of delivery.

Instead, individual artefacts are created and updated throughout the lifecycle as information becomes known, decisions are approved and implementation evidence is produced.

## Core Document Set

| No.    | Document                                    | Primary Purpose                                                                                                                                             |
| ------ | ------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **01** | **Business Requirements Document**          | Defines the business context, problem, objectives, scope, business rules, functional and non-functional requirements, KPI definitions and success criteria. |
| **02** | **Stakeholder Analysis**                    | Identifies stakeholders, user groups, responsibilities, influence, information needs and representative reporting personas.                                 |
| **03** | **Requirements Traceability**               | Maintains forward and backward traceability between requirements, design decisions, implementation and validation evidence.                                 |
| **04** | **Data Requirements and Source Assessment** | Defines required data, analytical grain, history, source suitability, ownership and source-level constraints.                                               |
| **05** | **Test and Validation Record**              | Controls validation scenarios, expected results, reconciliation evidence, defects, resolution evidence and regression baselines.                            |
| **06** | **Data Source Configuration**               | Records the approved source connection, extraction scope, fields, filters, historical window, granularity and source configuration.                         |
| **07** | **Power Query and Data Preparation**        | Documents query structure, material transformations, cleansing, null handling, duplicate rules, derived fields, dependencies and refresh validation.        |
| **08** | **Semantic Model Specification**            | Defines table grain and roles, relationships, dimensional design, calculation placement, measures, metadata, capabilities and limitations.                  |
| **09** | **Report Design and User Experience**       | Defines report structure, business-question and KPI mapping, visual design, navigation, interactions, accessibility and user-experience requirements.       |
| **10** | **Power BI Implementation**                 | Records the implemented model and report components, pages, visuals, calculations, interactions, security implementation and supporting evidence.           |
| **11** | **Deployment and Release Record**           | Controls environment movement, release readiness, deployment activities, approvals and production release evidence.                                         |
| **12** | **Security and Access Control**             | Defines workspace, audience, semantic-model, row-level, object-level, sharing and access-control requirements and validation.                               |
| **13** | **Operational Support and Monitoring**      | Defines post-release ownership, monitoring, refresh support, incidents, performance, capacity and ongoing operational responsibilities.                     |

## How the Artefacts Work Together

The document set is designed as an integrated delivery framework rather than a collection of independent templates.

For example:

**Business need and requirements**

`01 Business Requirements Document`

↓ informs

**Data and source definition**

`04 Data Requirements and Source Assessment`
`06 Data Source Configuration`

↓ informs

**Data preparation and analytical design**

`07 Power Query and Data Preparation`
`08 Semantic Model Specification`

↓ informs

**Report design and implementation**

`09 Report Design and User Experience`
`10 Power BI Implementation`

↓ validated through

**Controlled testing**

`05 Test and Validation Record`

↓ supported by

**Security, release and operations**

`12 Security and Access Control`
`11 Deployment and Release Record`
`13 Operational Support and Monitoring`

Throughout the lifecycle:

`03 Requirements Traceability`

maintains the connection between the original requirement and the design, implementation and validation evidence that ultimately satisfies it.

## Living Documentation

The framework treats most artefacts as **living controlled documents**.

A document may initially contain a design decision and later be updated with implementation or validation evidence.

For example, the Semantic Model Specification may begin by defining:

* intended table grain;
* table roles;
* dimensional structures;
* calculation placement; and
* measure definitions.

Later subprocesses can add:

* implemented relationship references;
* validation evidence;
* confirmed capabilities and limitations; and
* controlled revision history.

This preserves the relationship between **what was intended**, **what was implemented** and **what was validated**.

## Design Versus As-Built Evidence

The framework distinguishes between design specifications and implementation evidence.

For example:

| Design / Control Artefact               | Implementation / Evidence Artefact              |
| --------------------------------------- | ----------------------------------------------- |
| Business Requirements Document          | Power BI Implementation                         |
| Data Requirements and Source Assessment | Data Source Configuration                       |
| Semantic Model Specification            | Power BI Implementation                         |
| Report Design and User Experience       | Power BI Implementation                         |
| Security and Access Control             | Security implementation and validation evidence |
| Test scenarios and expected results     | Test execution and validation evidence          |

This separation makes it possible to identify where the implemented solution differs from an approved design and whether that difference has been formally accepted.

## Controlled Inputs and Outputs

Activities within the delivery process may use a document as an **Input**, update it as an **Output**, or both.

For example:

**Define the grain of every semantic-model table**

may consume:

* approved data granularity;
* validated transformed data;
* known data limitations; and
* existing Power Query structures.

The resulting table-grain decision is then recorded in:

`08 Semantic Model Specification`

This approach creates a controlled information flow between delivery activities rather than relying on undocumented knowledge held by individual team members.

## Why This Matters

The document framework helps support:

* traceability from business problem to delivered solution;
* clear ownership of business and technical decisions;
* controlled hand-offs between analysis, development and validation;
* separation of requirements, design and implementation evidence;
* easier impact assessment when requirements change;
* repeatable validation and regression testing;
* clearer deployment and support readiness; and
* maintainability after the original delivery team has moved on.

It also provides an audit trail explaining not only **what was built**, but **why it was built that way** and **how its correctness was demonstrated**.

## Reusable Framework, Project-Specific Content

The document structures are designed to be reusable across Power BI analytics projects.

The framework therefore separates:

**Reusable structure**

from

**Project-specific content**

A project may use the same controlled document architecture while the requirements, data sources, transformation logic, model design, report pages, validation evidence and operational arrangements remain specific to that project.

Not every section must contain substantive content for every project. Where a framework section is not applicable, that position should be made explicit rather than silently omitted.

## Portfolio Evidence Boundary

The public portfolio shows the document architecture and representative examples of how documents interact with delivery activities.

The following are retained privately:

* complete reusable Markdown templates;
* detailed section-level implementation guidance;
* complete task-to-document association data;
* project-specific controlled documents;
* validation registers and evidence;
* reusable checklists and working instructions; and
* template revision history.

This provides sufficient evidence to demonstrate the documentation and governance approach without publishing the reusable framework itself.

---

[← Selected Subprocesses](/delivery-frameworks/power-bi-end-to-end/selected-subprocesses/) · [Power BI Framework Overview](/delivery-frameworks/power-bi-end-to-end/) · [Delivery Traceability →](/delivery-frameworks/power-bi-end-to-end/traceability/)

---

© 2026 Carl Patten. All rights reserved.



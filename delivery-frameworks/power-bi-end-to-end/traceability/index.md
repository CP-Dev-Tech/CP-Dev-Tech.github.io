# Delivery Traceability

[Home](/) · [Delivery Frameworks](/delivery-frameworks/) · [Power BI End-to-End](/delivery-frameworks/power-bi-end-to-end/) · **Delivery Traceability**

## Overview

Traceability is a core design principle of the Power BI End-to-End Delivery Framework.

The framework connects delivery activities with the controlled information required to perform them and with the artefacts that record their outputs.

This creates a traceable path from the original business need through requirements, technical design, implementation and validation.

The objective is not to create documentation for its own sake. Traceability is used to answer practical delivery questions such as:

* Why was this feature or calculation implemented?
* Which requirement does this design decision support?
* Where is the authoritative definition of a business rule?
* Which process activity created or changed this information?
* What needs to be reassessed if a requirement changes?
* How was the implemented behaviour validated?
* What evidence demonstrates that the delivered solution satisfies the requirement?

## Traceability Model

At a high level, the framework maintains the following chain:

**Business Problem**

↓

**Business Objectives and Desired Outcomes**

↓

**Business Rules and Requirements**

↓

**Data and Solution Design**

↓

**Implementation**

↓

**Validation Evidence**

↓

**Release and Operational Support**

The Requirements Traceability Matrix provides the central requirement-level connection across these stages.

The process framework adds another dimension by identifying **which delivery activity consumes or produces the controlled information**.

## Process-to-Document Traceability

Each applicable subprocess activity can be associated with one or more controlled document sections.

Associations are classified as:

**Input** — information required by the activity.

**Output** — information created or materially updated by the activity.

For example:

> **Define Functional and Non-Functional Requirements**
>
> **Inputs**
>
> Business objectives, scope, business rules, stakeholder needs and the agreed traceability approach.
>
> ↓
>
> **Process Activity**
>
> Requirements are analysed and converted into clear, testable requirements.
>
> ↓
>
> **Outputs**
>
> Functional requirements, non-functional requirements, KPI definitions and entries within the Requirements Traceability Matrix.

This makes the information flow through the delivery process explicit.

## Section-Level Associations

Associations are maintained below document level.

Rather than stating only:

`Task → Business Requirements Document`

the framework can identify the specific controlled information involved:

`Task → 01.8.6 Business Rules`

or:

`Task → 08.11 Measure Catalogue`

This provides substantially greater precision when:

* assessing change impact;
* reviewing a design decision;
* locating an authoritative definition;
* preparing validation;
* investigating a defect; or
* handing the solution to another team member.

## Requirement Traceability

The Requirements Traceability Matrix provides the central requirement-level control.

A requirement can progressively accumulate references to the artefacts that demonstrate how it has been addressed.

A representative traceability path might therefore be:

`Business Requirement`

↓

`Data Requirement`

↓

`Transformation or Semantic-Model Design`

↓

`Power BI Implementation`

↓

`Validation Scenario`

↓

`Expected Result`

↓

`Test Evidence`

This supports both:

**Forward traceability**

> What design, implementation and validation resulted from this requirement?

and:

**Backward traceability**

> Why does this model component, calculation or report feature exist?

## Example — Business Rule to Validated Output

Consider a business rule that defines how a KPI should be calculated.

The framework can establish the following controlled chain:

**01 Business Requirements Document**

`Business Rule / KPI Definition`

↓

**05 Build Power Query Transformations**
or
**07 Define the Semantic Model**

`Determine the appropriate implementation layer`

↓

**07 Power Query and Data Preparation**
or
**08 Semantic Model Specification**

`Document the approved transformation or calculation design`

↓

**10 Power BI Implementation**

`Record the implemented component`

↓

**05 Test and Validation Record**

`Scenario → Expected Result → Actual Result → Evidence`

↓

**03 Requirements Traceability**

`Maintain the requirement-to-design-to-validation relationship`

The exact route depends on where the business logic belongs, but the underlying requirement remains traceable throughout.

## Traceability Across Process Boundaries

Traceability also helps maintain continuity between subprocesses.

For example:

**03 — Design Representative Test Scenarios**

creates controlled scenarios and expected results.

Those artefacts can subsequently be reused during:

* transformed-data validation;
* semantic-model validation;
* calculation validation;
* report validation;
* end-to-end source-to-report testing; and
* final regression testing.

The expected result therefore does not need to be rediscovered each time testing occurs.

Likewise, design decisions established during semantic-model or report-design activities become controlled inputs into subsequent implementation and validation activities.

## Change Impact

Traceability provides a structured basis for change assessment.

If a requirement changes, the associated records can be used to identify potentially affected:

* business rules;
* data requirements;
* source configuration;
* Power Query transformations;
* semantic-model structures;
* calculations and measures;
* report pages and visuals;
* security configuration;
* validation scenarios;
* regression tests;
* release documentation; and
* operational support information.

The framework does not assume that every change affects every artefact.

Instead, the traceability relationships help identify where assessment is actually required.

## Traceability and Defect Resolution

The same principle applies when validation identifies a discrepancy.

A failed test can be traced backwards through:

`Validation Evidence`

↓

`Implemented Component`

↓

`Design Decision`

↓

`Requirement / Business Rule`

This helps distinguish between different causes.

For example, the issue may originate from:

* an incorrect implementation;
* an incorrect transformation;
* an incorrect semantic-model assumption;
* an ambiguous requirement;
* an unexpected source-data condition; or
* an approved limitation that has not been represented correctly.

Following remediation, affected tests can be repeated while retaining the original requirement and expected-result baseline.

## Association Direction Matters

The framework deliberately distinguishes between information being **used** and information being **changed**.

A document is therefore not automatically recorded as an Output merely because it is relevant to a task.

For example, a developer may use the Semantic Model Specification while building a report visual.

That is an:

`Input`

The Semantic Model Specification becomes an:

`Output`

only where the activity materially changes information controlled by that specification.

This prevents the traceability record from implying that every process activity updates every document it references.

## Traceability Without Diagram Congestion

Detailed document associations are intentionally not drawn directly onto the BPMN subprocess diagrams.

Doing so would make the process models difficult to read and would obscure the process logic.

Instead, the framework separates:

**Process logic**

from

**Information traceability**

The BPMN diagram therefore shows:

* activities;
* decisions;
* sequence;
* loops;
* remediation paths; and
* hand-offs.

The companion association model records:

* task;
* association direction;
* document;
* document section;
* purpose; and
* supporting notes where required.

This keeps both views usable while retaining detailed traceability.

## Why This Matters

The traceability model provides practical benefits throughout delivery:

* requirements remain connected to implementation;
* design decisions can be explained;
* validation can be based on approved expected behaviour;
* change impact can be assessed systematically;
* defects can be investigated through the delivery chain;
* hand-offs contain clearer context;
* documentation remains connected to actual process activities;
* regression coverage can be preserved; and
* release decisions can be supported by identifiable evidence.

The result is a delivery record that explains not only **what was delivered**, but also **why it exists and how it was validated**.

## Portfolio Evidence Boundary

The public portfolio demonstrates the traceability model and includes selected representative task-to-document associations within the published subprocess examples.

The following remain private:

* the complete task-to-document association library;
* complete section-level mappings for all subprocesses;
* reusable association-table source data;
* complete Requirements Traceability Matrix templates;
* project-specific traceability records;
* detailed validation evidence; and
* reusable implementation guidance.

This preserves the reusable framework while providing sufficient evidence to demonstrate how process, documentation, implementation and validation are connected.

---

[← Document & Artefact Framework](/delivery-frameworks/power-bi-end-to-end/document-framework/) · [Power BI Framework Overview](/delivery-frameworks/power-bi-end-to-end/) · [Framework Application →](/delivery-frameworks/power-bi-end-to-end/framework-application/)

---

© 2026 Carl Patten. All rights reserved.

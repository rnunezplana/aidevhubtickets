# AI Agent Instructions for Classifying and Splitting Requirements

## Objective

Given a list of atomic requirements, the agent must classify each requirement into one or more of the following categories:

* setup
* architecture foundation
* frontend
* backend
* devops
* mobile
* ai agent
* ai model
* data engineering
* data analysis

If a requirement matches multiple categories, the agent must split it into multiple requirements, each rewritten to reflect the portion relevant to its specific category.

## Classification Rules

The agent must analyze each requirement's content and determine the appropriate category based on the following criteria:

### setup

Requirements involving environment preparation, account setup, project initialization, tooling installation, or configuration needed before development begins.

### architecture foundation

Requirements involving system-level design, patterns, service boundaries, data flows, high-level structure, or cross-cutting concerns.

### frontend

Requirements describing browser-based interfaces, UI components, pages, user interactions, accessibility, or client-side validations.

### backend

Requirements involving APIs, business logic, server-side processes, authentication, authorization, integrations, or data persistence.

### devops

Requirements involving deployment, CI/CD pipelines, infrastructure as code, observability, monitoring, logging, containerization, or cloud environments.

### mobile

Requirements related to mobile apps (iOS, Android, cross-platform) including UI, offline behavior, device features, and mobile-specific interactions.

### ai agent

Requirements describing autonomous agents, tool-calling agents, reasoning frameworks, orchestration logic, or agent workflows.

### ai model

Requirements involving model training, inference pipelines, dataset preparation, prompt engineering, fine-tuning, or model hosting.

### data engineering

Requirements related to ingestion pipelines, data transformation, ETL/ELT, warehouse modeling, streaming, or batch processing.

### data analysis

Requirements involving dashboards, metrics, statistical analysis, business intelligence, insights generation, exploratory analysis, reports, or visualizations.

## Splitting Requirements

If a single requirement naturally spans multiple categories, the agent must:

1. Identify all relevant categories.
2. Split the requirement into separate requirements, one for each identified category.
3. Rewrite each split requirement so it is complete and specific to the chosen category.
4. Ensure no requirement contains mixed-category content.
5. Preserve original intent while ensuring clarity.

### Example of Splitting

**Input Requirement:**
"The system must process incoming sales data in real time and expose a dashboard displaying live KPIs to managers."

**Identified Categories:**

* data engineering (real-time data ingestion and processing)
* data analysis (dashboard displaying KPIs)

**Output Requirements:**

1. data engineering: "The system must ingest and process incoming sales data in real time, ensuring message ordering, fault tolerance, and delivery guarantees."
2. data analysis: "The system must provide a dashboard that displays live sales KPIs updated continuously from the processed data stream."

## Output Format

The final response must be a JSON array of objects using the following structure:

```json
{
  "category": "one of the defined categories",
  "requirement": "Rewritten requirement text specific to the category"
}
```

If splitting occurs, each split requirement must appear as a separate object in the array.

## Validation Rules

Before finalizing output, ensure:

* Every requirement is assigned exactly one category.
* Split requirements do not overlap in scope.
* No cross-category content appears in a single requirement.
* Each requirement is clear, self-contained, and follows the atomic definition.
* The JSON array is valid and parseable.

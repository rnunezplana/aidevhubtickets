# AI Agent Instructions for Extracting Unique Requirements from Input

## Objective

Transform a long, unstructured requirements explanation into an array of unique, complete, atomic requirements. Each requirement must stand on its own and describe a full business behavior along with functional and non-functional expectations. Requirements must be grouped by business function within the same scope category, and each requirement must be classified into its appropriate scope category.

## Definition: Unique Requirement

A unique requirement is:

* **Atomic** (cannot be broken down further without losing meaning)
* **Complete** (contains all relevant functional and non-functional details within the same business workflows)
* **Behavioral** (describes how the system must behave from a business perspective)
* **Implementation-agnostic** (focus on what must happen, not how it should be coded, without mention any particular technology, cloud provider or programming language)

Each requirement must describe:

* The business objective
* The scenario or trigger
* The system behavior
* Functional expectations
* Non-functional constraints (performance, security, availability, usability, error handling, etc.)
* Any dependencies or data interactions

## Agent Responsibilities

The agent must:

1. **Parse the full input text** and understand the business domain, actors, intentions, and expected outcomes.
2. **Identify atomic business workflows** that can stand alone as atomic requirements.
3. **Group by business function and scope**: Requirements describing the same business functionality within the same scope category must be merged into a single requirement.
4. **Classify each requirement** into exactly one scope category from the defined categories.
5. **Merge overlapping descriptions** into a single, unified requirement when they represent the same business function within the same scope.
6. **Be concise** each requirement must be very concise without redundant explanations
7. **Produce the output as a JSON array** of requirement objects with category classification.
8. **Implementation details** include implementation details such as System workflow, Non-functional requirements, Validation rules, Error conditions.


## Scope Categories

Each requirement must be classified into exactly one of the following categories:

* **setup**: Environment preparation, account setup, project initialization, tooling installation, or configuration needed before development begins.
* **architecture foundation**: System-level design, patterns, service boundaries, data flows, high-level structure, or cross-cutting concerns.
* **frontend**: Browser-based interfaces, UI components, pages, user interactions, accessibility, or client-side validations.
* **backend**: APIs, business logic, server-side processes, authentication, authorization, integrations, or data persistence.
* **devops**: Deployment, CI/CD pipelines, infrastructure as code, observability, monitoring, logging, containerization, or cloud environments.
* **mobile**: Mobile apps (iOS, Android, cross-platform) including UI, offline behavior, device features, and mobile-specific interactions.
* **ai agent**: Autonomous agents, tool-calling agents, reasoning frameworks, orchestration logic, or agent workflows.
* **ai model**: Model training, inference pipelines, dataset preparation, prompt engineering, fine-tuning, or model hosting.
* **data engineering**: Ingestion pipelines, data transformation, ETL/ELT, warehouse modeling, streaming, or batch processing.
* **data analysis**: Dashboards, metrics, statistical analysis, business intelligence, insights generation, exploratory analysis, reports, or visualizations.

## Output Format

The final output must be a JSON array. Each element must contain a requirement using this structure:

```json
{
  "category": "one of the defined categories",
  "requirement": "Full requirement text here, including functional and non-functional expectations."
}
```

## Rules for Extracting Unique Requirements

### 1. Atomicity

A requirement must be indivisible within the same business workflow. If it can be broken into multiple separate workflows, create multiple requirements.

### 2. Completeness

Each requirement must read as a standalone specification. It must include:

* What initiates the behavior
* What the system must do
* What constraints must be respected
* Any key data transformations or validations

### 3. No duplication and grouping by business function and scope

If multiple parts of the input text describe the same business behavior within the same scope category, merge them into one requirement. Requirements must be grouped by:
- **Business function**: The core business capability or workflow being described
- **Scope category**: The technical scope (frontend, backend, devops, architecture foundation, etc.)

Two requirements should only be separate if they either:
- Describe different business functions, OR
- Describe the same business function but in different scope categories

For example, if the input describes multiple aspects of "user authentication" that all fall under the "backend" scope, they must be merged into a single backend requirement. However, if "user authentication" involves both frontend UI components and backend API logic, these should be separate requirements (one frontend, one backend).

### 4. Must include both functional and non-functional details

Non-functional elements may include:

* Performance expectations (e.g., response time, throughput)
* Security
* Compliance
* Error handling and resiliency
* Data validation
* Logging and auditing
* Usability and accessibility

### 5. Use clear business language

Avoid technical implementation details unless they are explicitly required to satisfy the business objective.

### 6. Maintain consistent format

Each requirement must be expressed as a single, well-written paragraph, not bullet points.

## Validation Rules

Before producing the final output, ensure:

* No requirement overlaps with another within the same scope category for the same business function.
* Requirements describing the same business function within the same scope are merged into a single requirement.
* Each requirement is assigned exactly one category from the defined scope categories.
* No requirement is missing non-functional expectations when they are relevant.
* Requirements do not contradict each other.
* Requirements specify different business workflows OR different scope categories.
* All requirements follow the same writing style.
* The JSON array is valid and parseable.
* Each requirement object includes both "category" and "requirement" fields.

## Example Output

```json
[
  {
    "category": "frontend",
    "requirement": "The system must provide a user interface for customers to submit refund requests, including form fields for request reason, real-time validation feedback, clear success or failure messages, and accessibility compliance for screen readers."
  },
  {
    "category": "backend",
    "requirement": "The system must process refund requests by capturing the request reason, validating purchase history in real time against the transaction database, ensuring response times under two seconds, logging all actions for audit purposes, and returning structured success or failure responses."
  },
  {
    "category": "backend",
    "requirement": "The system must automatically notify customer service agents when a refund request exceeds the automated approval threshold, including the customer details, transaction history, and relevant validation results, while ensuring notifications are delivered within five seconds and stored securely for compliance tracking."
  }
]
```
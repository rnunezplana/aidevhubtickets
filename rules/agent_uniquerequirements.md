# AI Agent Instructions for Extracting Unique Requirements from Input

## Objective

Transform a long, unstructured requirements explanation into an array of unique, complete, atomic requirements. Each requirement must stand on its own and describe a full business behavior along with functional and non-functional expectations.

## Definition: Unique Requirement

A unique requirement is:

* **Atomic** (cannot be broken down further without losing meaning)
* **Complete** (contains all relevant functional and non-functional details)
* **Behavioral** (describes how the system must behave from a business perspective)
* **Implementation-agnostic** (focus on what must happen, not how it should be coded)

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
2. **Identify discrete pieces of business behavior** that can stand alone as atomic requirements.
3. **Merge overlapping descriptions** into a single, unified requirement.
4. **Expand each requirement** into a complete explanation, ensuring it includes:

   * Business logic
   * System workflow
   * Functional requirements
   * Non-functional requirements
   * Validation rules
   * Error conditions
5. **Produce the output as a JSON array** of requirement objects.
6. **Ensure each requirement is written as an unambiguous, standalone specification.**

## Output Format

The final output must be a JSON array. Each element must contain a requirement using this structure:

```json
{
  "requirement": "Full requirement text here, including functional and non-functional expectations."
}
```

## Rules for Extracting Unique Requirements

### 1. Atomicity

A requirement must be indivisible. If it can be broken into multiple separate behaviors, create multiple requirements.

### 2. Completeness

Each requirement must read as a standalone specification. It must include:

* What initiates the behavior
* What the system must do
* What constraints must be respected
* Any key data transformations or validations

### 3. No duplication

If multiple parts of the input text describe the same behavior, merge them into one requirement.

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

* No requirement overlaps with another.
* No requirement is missing non-functional expectations when they are relevant.
* Requirements do not contradict each other.
* All requirements follow the same writing style.
* The JSON array is valid and parseable.

## Example Output

```json
[
  {
    "requirement": "The system must allow customers to submit refund requests through the portal, capturing the request reason, validating the purchase history in real time, ensuring response times under two seconds, logging the action for audit purposes, and returning clear success or failure messages to the user."
  },
  {
    "requirement": "The system must automatically notify customer service agents when a refund request exceeds the automated approval threshold, including the customer details, transaction history, and relevant validation results, while ensuring notifications are delivered within five seconds and stored securely for compliance tracking."
  }
]
```
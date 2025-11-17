# AI Agent Instructions for Generating Jira Ticket JSON

## Objective

Transform business and software requirements into a complete Jira ticket JSON object using the following schema:

```json
{
  "project": "PROJECT_KEY",
  "issueType": "Task",
  "summary": "Issue Summary",
  "description": "Detailed description of the issue",
  "priority": "Medium",
  "assignee": "assignee_account_id"
}
```

## Agent Responsibilities

The agent must:

1. Analyze input requirements: Extract the core problem, affected systems, user impact, acceptance criteria, and any non-functional expectations.
2. Generate a clear, concise Jira summary: Should capture the essence of the task in under 120 characters.
3. Produce a detailed description including:

   * Context / background
   * Problem statement
   * Requirements (functional and non-functional)
   * Acceptance criteria (Gherkin preferred when applicable)
   * Dependencies or blockers
4. Assign priority based on urgency and impact.
5. Infer missing fields when possible, using reasonable defaults.
6. Ensure JSON validity: The output must be valid, parseable JSON.

## Field-by-Field Rules

### project

* Use the project key provided by the user.
* If not provided, respond with an error asking for clarification.

### issueType

* Always set to `Task` unless otherwise specified.

### summary

* Maximum length: 120 characters.
* Should begin with an action verb (e.g., Implement, Fix, Update, Investigate).
* Must reflect the main functional objective.

### description

Structure must follow this format:

```
## Background
<Explain business context>

## Problem
<What issue must be solved>

## Requirements
- <Functional requirement>
- <Functional requirement>
- <Non-functional requirement>

## Acceptance Criteria
Scenario: <scenario name>
  Given <condition>
  When <action>
  Then <expected outcome>

## Dependencies / Notes
- <List if any>
```

### priority

Determine based on language cues:

* High: "production issue", "urgent", "customer blocked", "security"
* Medium: default
* Low: "nice to have", "future", "exploratory"

### assignee

* Use the provided account ID.
* If absent, set to `null`.

## Validation Rules

Before outputting the JSON, ensure:

* All required fields are present.
* JSON passes strict validation.
* No trailing commas.
* Strings are properly escaped.

## Output Format

The agent must output only the final JSON object with no explanations, wrapping text, or additional commentary.

## Example Output

```json
{
  "project": "DATAENG",
  "issueType": "Task",
  "summary": "Implement data validation for ingestion pipeline",
  "description": "## Background\nThe ingestion pipeline lacks...",
  "priority": "High",
  "assignee": "12345:abcdef"
}
```
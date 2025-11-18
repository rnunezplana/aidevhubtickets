Extract technology stacks, design patterns, and services from Context based on scope categories (setup, mobile, frontend, backend, devops, ai agent, ai model, data engineering, data analysis, architecture foundation). Replace placeholders in the Template with extracted information. Remove entire category sections and their placeholders when Context provides no relevant information for that category.

## Scope Category Mapping

Map Context information to template categories using these scope categories:
- **setup** → Setup
- **mobile** → Mobile
- **frontend** → Frontend
- **backend** → Backend
- **devops** → Cloud, Cloud Services, QA Tech Stack, Security
- **ai agent** → AI Agent
- **ai model** → AI Model
- **data engineering** → Data Engineering
- **data analysis** → Data Analysis
- **architecture foundation** → Object Design Patterns, Architectural Patterns

## Extraction Rules

1. **Extract only from Context**: Use only technologies, patterns, and services explicitly mentioned in Context. Do not infer or add items not present.

2. **Remove empty categories**: If Context contains no information for a category, remove the entire section (heading and placeholder) from the output.

3. **Tech Stack Format**: `Technology Name vX.Y.Z` (one per line, bulleted). No descriptions.

4. **Pattern Format**: `Pattern Name: Process 1, Process 2, Process 3` (one per line, bulleted). No explanations.

5. **Service Format**: `Service Name: Process 1, Process 2, Process 3` (one per line, bulleted). No descriptions.

## Output Rules

**ONLY INCLUDE:**
- Technology names with versions
- Pattern names with process lists
- Service names with process lists

**DO NOT INCLUDE:**
- Descriptions, rationale, or explanations
- Configuration or integration details
- Technologies, patterns, or services not in Context
- Empty category sections

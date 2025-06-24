---
mode: "agent"
description: "Design custom chat mode for specific project role"
---
# Custom Chat Mode Generator

## Repository Context Analysis

First, analyze the current repository to understand:

1. **Project Domain**: The business or technical domain of the project
2. **Key User Roles**: The main roles involved in development (e.g., frontend developer, API developer, database administrator)
3. **Common Tasks**: Recurring tasks performed by each role
4. **Technology Stack**: The primary technologies used in each area of the project

## Chat Mode Definition

Based on this role and context, generate a custom chat mode file (`.chatmode.md`) that includes:

1. **Front Matter**:
   - A clear, concise description of the chat mode's purpose
   - The appropriate tools required for this role (e.g., #codebase, #selection, #problems)
   - Any other relevant metadata

2. **Main Instructions**:
   - A clear introduction explaining the purpose and focus of this chat mode
   - Specific guidance on how the AI should approach tasks in this role
   - Domain-specific knowledge and context relevant to this role
   - Common patterns and practices for this role in the project
   - Boundaries of responsibility for this role

3. **Task-Specific Guidelines**:
   - Instructions for handling common tasks for this role
   - Specific approaches for solving typical problems
   - Integration points with other roles or systems
   - Quality standards and requirements specific to this role

4. **Communication Style**:
   - How responses should be structured for this role
   - Level of technical detail expected
   - Appropriate terminology and jargon for the domain
   - Balance between explanation and direct solution

## Implementation Guidance

Provide instructions on where to place the generated chat mode file and how to start using it within VS Code.

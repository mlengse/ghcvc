---
mode: "agent"
description: "Design custom prompt template for recurring project task"
---
# Custom Prompt Template Generator

## Task Analysis

First, analyze the specific recurring task in the repository that requires a custom prompt:

1. **Task Purpose**: What is the goal of this task in the project context?
2. **Task Frequency**: How often is this task performed?
3. **Typical Steps**: What are the standard steps to complete this task?
4. **Required Context**: What context is needed to perform this task effectively?
5. **Common Challenges**: What difficulties or edge cases typically arise?
6. **Related Components**: Which parts of the codebase are typically involved?

## Prompt Template Creation

Based on this analysis, generate a custom prompt template (`.prompt.md`) that includes:

1. **Front Matter**:
   - Appropriate mode (ask, edit, agent)
   - Concise description of the prompt's purpose
   - Any other relevant metadata

2. **Main Prompt Content**:
   - Clear title describing the task
   - Structured sections that guide completion of the task
   - Placeholders for task-specific inputs
   - Required context references (#file, #selection, etc.)
   - Guidance on expected output format

3. **Task-Specific Guidelines**:
   - Project-specific requirements for this task
   - Quality standards to meet
   - Common pitfalls to avoid
   - Integration points to consider

4. **Documentation**:
   - Usage examples
   - When to use this prompt vs. alternatives
   - How to customize for specific instances of the task

## Repository Integration

Provide instructions on:
- Where to store the prompt file in the repository structure
- How to use the prompt within VS Code
- How to share this prompt with team members
- How to evolve the prompt as project requirements change

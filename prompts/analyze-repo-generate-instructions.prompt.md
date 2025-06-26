---
mode: "agent"
description: "Analyze repository and generate custom instructions"
---
# Repository Analysis and Instructions Generation

## Repository Analysis

Analyze the current repository structure and codebase to understand:

1. **Architecture**: The overall architectural pattern(s) used in the project (e.g., MVC, MVVM, Clean Architecture, Microservices)

2. **Technologies**: Primary programming languages, frameworks, libraries, and tools used in the project

3. **Organization**: The directory structure, module organization, and code separation principles

4. **Conventions**: Coding standards, naming conventions, and style patterns present in the codebase

5. **Domain**: The business domain and key concepts represented in the codebase

## Custom Instructions Generation

Based on the analysis, generate a `.github/copilot-instructions.md` file that includes:

1. **Project Overview**: A brief description of the project's purpose and domain

2. **Architecture Guidelines**: Instructions on how generated code should fit into the existing architecture

3. **Technology Stack**: Details on the preferred technologies and how they should be used

4. **Coding Standards**: Specific coding conventions to follow, based on observed patterns

5. **Testing Requirements**: Guidelines on how tests should be written for this project

6. **Documentation Standards**: Requirements for code comments and documentation

## Language-Specific Instructions

For each primary programming language detected, create a language-specific instruction file in `.github/instructions/` that includes:

1. **Naming Conventions**: Specific to this project's implementation of the language

2. **Common Patterns**: Recurring code patterns observed in the codebase

3. **Error Handling**: Project-specific error handling strategies 

4. **Performance Considerations**: Language-specific optimizations used in the project

5. **Testing Patterns**: How tests are typically written for this language in the project

## Integration Guidance

Provide guidance on how the generated instructions relate to the repository structure and how they should be used with GitHub Copilot.

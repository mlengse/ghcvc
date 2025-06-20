---
mode: "ask"
description: "Generate architecture-specific instructions"
---
# Architecture-Specific Instructions Generator

## Architecture Analysis

First, analyze the architectural patterns present in the repository:

1. **Architectural Pattern**: Identify the primary architectural pattern(s) in use (e.g., Clean Architecture, MVVM, Hexagonal, Microservices)

2. **Layer Separation**: How are concerns separated (e.g., presentation, business logic, data access)

3. **Component Communication**: How do components interact within and across layers

4. **Dependency Management**: How dependencies are managed and injected

5. **Cross-Cutting Concerns**: How aspects like logging, error handling, and security are addressed

## Custom Instructions Creation

Based on this analysis, generate a custom instructions file (`.instructions.md`) that includes:

1. **Front Matter**:
   - Appropriate file pattern to apply these instructions to
   - Any other relevant metadata

2. **Architecture Overview**:
   - Brief description of the architectural pattern
   - Key principles that guide this architecture
   - Visualization of the architecture (described textually)

3. **Layer-Specific Guidelines**:
   - Instructions for each architectural layer
   - Responsibilities and boundaries of each layer
   - How components within each layer should be structured
   - Patterns specific to each layer

4. **Cross-Layer Communication**:
   - How components should communicate across layers
   - Dependency direction and rules
   - Data transfer patterns between layers

5. **Testing Approach**:
   - How different architectural components should be tested
   - Mocking strategies for dependencies
   - Test scope recommendations for each layer

6. **Common Anti-patterns**:
   - Architecture violations to avoid
   - Common mistakes when implementing this architecture
   - Remediation strategies for architectural drift

## Implementation Guidance

Provide guidance on:
- How to apply these architectural instructions across the codebase
- How to ensure new code follows the architectural patterns
- How to refactor existing code that violates the architecture
- How to evolve the architecture as the project grows

---
mode: "agent"
description: "Perform a security review of code"
---
# Security Code Review

Perform a comprehensive security review of the provided code. Look for:

1. **Input Validation Issues**:
   - Missing or insufficient validation
   - Potential injection vulnerabilities (SQL, XSS, command injection)
   - Type confusion or unsafe type casting

2. **Authentication & Authorization**:
   - Improper access controls
   - Missing authentication checks
   - Insecure credential management

3. **Data Security**:
   - Sensitive data exposure
   - Improper encryption
   - Hard-coded credentials or secrets
   - Insecure data storage

4. **Resource Management**:
   - Memory leaks
   - Resource exhaustion possibilities
   - Unmanaged resources

5. **Error Handling**:
   - Information exposure through error messages
   - Improper error handling

6. **Secure Coding Practices**:
   - Race conditions
   - Time-of-check to time-of-use bugs
   - Insecure randomness

For each issue found, provide:
- A description of the vulnerability
- The potential impact
- The exact location in the code
- A recommendation for fixing it

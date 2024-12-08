# AI Instructions Template
Version: 1.0.0
Created: 2024-12-08
Last Modified: 2024-12-08

## Core Instructions

### Database and Schema
- Do not alter existing database schemas
- Document all proposed schema changes
- Always verify table/field names with project documentation
- Use appropriate field sizes and types

### Implementation Requirements
- No external dependencies (CDN, remote APIs, etc.)
- Application must work standalone without internet
- Focus on reliability and maintainability
- Implement comprehensive error handling
- Use logging for debugging
- Follow established coding patterns

### File Management
- Respect existing directory structure
- Use unique, descriptive filenames
- Include version numbers and paths in file headers
- Follow project naming conventions
- Document file locations for code snippets

### Documentation
- Translate user-facing text as specified
- Keep technical documentation in English
- Include clear implementation instructions
- Document all configuration options
- Provide usage examples

### Security Considerations
- Follow secure coding practices
- Implement proper input validation
- Use appropriate error handling
- Follow principle of least privilege
- Document security considerations

### Testing and Validation
- Include test cases
- Provide validation procedures
- Include error handling
- Document edge cases
- Consider performance implications

## Specific Instructions

### File Headers
Always include this header in generated files:
```python
"""
File: [filename]
Rev: [version]
Created: [creation_date]
Last Modified: [modification_date]
Author: [author]

Description: 
[file_description]

Changes:
- [change_history]
"""
```

### Directory Structure
Respect and maintain this structure:
```
project_root/
├── app/
├── data/
├── docs/
├── logs/
└── tests/
```

### Response Format
- Provide clear file locations for code snippets
- Include complete, working code rather than fragments
- Document any assumptions made
- Include error handling
- Provide usage examples

### Version Control
- Include version numbers
- Document changes
- Follow project branching strategy
- Provide meaningful commit messages

### Special Considerations
- Focus on maintainability
- Consider resource constraints
- Plan for scalability
- Document limitations
- Provide fallback options

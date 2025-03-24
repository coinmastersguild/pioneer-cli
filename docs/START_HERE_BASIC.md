# KeepKey Support Email System - Getting Started

## Introduction

This document provides the foundational guidelines for working with the KeepKey Support Email system following the Guild Protocol. Before starting any development work, please read through this document carefully to understand the proper workflow and process.

## Development Workflow Rules

1. **Always read the documentation first**
   - Review docs in `/docs` directory before writing any code
   - Understand the existing skills in `/skills` before creating new ones
   - Review deployment rules in `/docs/deployment/rules` before any deployment activity

2. **Follow Guild Protocol**
   - Use milestone-based development with properly documented sprints
   - Create proper documentation before implementation
   - Skills are implemented as bash commands, not as complex code libraries
   - Follow the proper directory structure for documentation

3. **Plan Before Implementation**
   - Create milestone documents first
   - Break down milestones into sprint plans
   - Document user stories with clear acceptance criteria
   - Only begin implementation after planning is complete

4. **Working with Skills**
   - Skills are shell scripts that perform specific tasks
   - Keep skills small, focused, and reusable
   - Document each skill's purpose, inputs, and outputs
   - Test skills thoroughly before deployment

## Getting Started

### 1. Project Setup

To set up the project for development:

```bash
# Install dependencies
npm install

# Set up development environment
npm run dev
```

### 2. Documentation Structure

Familiarize yourself with the documentation structure:

- `/docs/goals/` - Project goals and requirements
- `/docs/guild/` - Guild Protocol documentation and standards
- `/docs/milestones/` - Milestone planning documents
- `/docs/sprints/` - Sprint planning and reports
- `/docs/reference-code/` - Reference implementations

### 3. Creating Milestones and Sprints

Before starting development work:

1. Create milestone documents in `/docs/milestones/`
2. Break milestones into sprint plans in `/docs/sprints/`
3. Get approval for the milestone and sprint plans
4. Only then start implementation

### 4. Guild Protocol Skills

Skills in the Guild Protocol are:

- Shell scripts that perform specific tasks
- Located in the `/skills` directory
- Named according to their function (e.g., `deploy.sh`, `monitor.sh`)
- Documented with comments explaining usage and parameters

### 5. Testing and Validation

All implementations should:

- Include appropriate tests
- Be validated against acceptance criteria
- Follow the definition of done from the sprint plan

## Windsurf Rules

This project should be developed using the following Windsurf rules:

```
read the docs in /docs before starting!
read the skill in /skills use and keep good skills!
read docs/deployment/rules carefully before deploying or managing k8!
An Engineer is only as good as his tools. improve docs and skills over time!
```

## Next Steps

1. Review the project requirements in `/docs/goals/project.md`
2. Create the first milestone document
3. Break down the milestone into sprint plans
4. Begin implementation according to the sprint plan

Remember: Always start with documentation and planning before writing any code.

# DegenQuest Standard Prompt Structure

## Overview

This document defines the standard structure for creating prompts when working with AI assistants on the DegenQuest project. Following this structure ensures consistency, clarity, and effectiveness across the team.

## Basic Prompt Template

```
[Component]: <specific component name>
[Goal]: <clear, specific outcome>
[Context]: <relevant background information>
[Reference]: <link to documentation or protocol>

<request details>
```

### Example

```
Component: Colyseus Game Server
Goal: Fix schema definition errors in PlayerSchema
Context: Server crashes on startup with TypeError about _definition property
Reference: docs/troubleshooting/colyseus-schema-guide.md

The game server is failing to start with the following error:
TypeError: Cannot read properties of undefined (reading '_definition')
at Context.add (/node_modules/@colyseus/schema/src/annotations.ts:158:61)

Please identify and fix the schema definition issue in the PlayerSchema and GameRoomState files.
```

## Advanced Prompt Templates

### Diagnostic Prompt

Use when you need to diagnose an issue:

```
Component: <component name>
Goal: Diagnose <specific issue>
Context: <observable symptoms>
Reference: <relevant documentation>

Observed behavior:
1. <specific observation>
2. <specific observation>

Expected behavior:
1. <what should happen>

Logs:
```

### Implementation Prompt

Use when you need to implement a feature:

```
Component: <component name>
Goal: Implement <specific feature>
Context: <background and requirements>
Reference: <design doc or spec>

Requirements:
1. <requirement>
2. <requirement>

Acceptance criteria:
1. <criterion>
2. <criterion>
```

### Verification Prompt

Use to verify a solution:

```
Component: <component name>
Goal: Verify <implementation or fix>
Context: <what was implemented/fixed>
Reference: <original issue or requirement>

Verification steps:
1. <step>
2. <step>

Success criteria:
1. <criterion>
2. <criterion>
```

## Best Practices

1. **Be Specific**: Clearly state which component, file, or function you're working with
2. **Include Context**: Provide relevant background information
3. **Reference Documentation**: Link to relevant documentation
4. **Define Success**: Clearly state what a successful outcome looks like
5. **Progressive Prompting**: Start with diagnostics, then solutions, then verification
6. **Add Code Snippets**: Include relevant code with proper formatting
7. **Specify Constraints**: Mention any limitations or constraints

## Example Workflow

### Step 1: Diagnostic Prompt

```
Component: Game Server
Goal: Diagnose server crash on startup
Context: Server was working yesterday but crashes today after schema changes
Reference: docs/troubleshooting/server-startup.md

Error message:
TypeError: Cannot read properties of undefined (reading '_definition')
```

### Step 2: Solution Prompt

```
Component: Game Server
Goal: Fix schema definition error in PlayerSchema
Context: Identified issue with incorrect type decorator in MapSchema
Reference: docs/troubleshooting/colyseus-schema-guide.md

Please implement the fix for the MapSchema type decorator as outlined in the troubleshooting guide.
```

### Step 3: Verification Prompt

```
Component: Game Server
Goal: Verify server startup after schema fix
Context: Fixed type decorator in MapSchema
Reference: Original diagnostic issue

Please start the server and verify:
1. No schema errors occur on startup
2. Client can connect successfully
3. Player entities can be created and synchronized
``` 
# Sprint Writing Protocol

**Document Type**: Protocol Guide  
**Created**: 2025-03-22  
**Status**: Active

## Purpose

This document outlines the required format and approach for writing effective sprint planning documents within the Pioneer Agent project. It serves as a correction to previously abstract and ineffective sprint planning approaches.

## Fundamental Principles

1. **Be Specific and Actionable**: Every task must identify exact files, scripts, or components to modify
2. **Focus on Implementation**: Describe how to implement, not just what to implement
3. **Specify Verification Methods**: Include concrete test criteria with exact endpoints and expected responses
4. **Reference Existing Codebase**: Always reference specific files and location paths
5. **Prioritize Working Software**: Emphasize running and testing over theoretical architecture

## Anti-Patterns to Avoid

The following demonstrates what NOT to do in sprint planning:

```markdown
❌ BAD EXAMPLE:
## Detailed Requirements

1. **Server Setup**
   - Prepare the Eliza server component for deployment
   - Configure appropriate environment variables
   - Set up model providers (OpenAI, Anthropic, etc.)
   - Configure a basic character for demonstration
```

This approach fails because it:
- Lacks specificity about actual files to modify
- Doesn't specify how to verify success
- Doesn't reference existing code artifacts
- Focuses on abstract goals rather than executable tasks

## Correct Format Exemplar

Sprint planning documents MUST follow this specific pattern, demonstrated in this corrected example:

```markdown
✅ GOOD EXAMPLE:
## Current Architecture Analysis

1. **Executable Scripts**
   - top level package.json/scripts has deploy server and deploy client
   - run them, make sure they work

2. **Port Configuration**
   - verify ports, and assign ports not used by other projects
   - use 5000+ range

3. **Health Check Implementation**
   - Build a local test script
   - verify server has /health endpoint
   - verify server /health returns a version number

4. **Client Verification**
   - Test client loading: check for 404 vs successful load
   - Implement appropriate health checks
   - Open in browser to visually verify operation
```

This approach succeeds because it:
- Identifies specific implementation artifacts (package.json)
- Specifies exact verification methods (/health endpoint)
- Gives concrete implementation guidelines (use ports 5000+)
- Focuses on running and testing code

## Sprint Document Structure

All sprint planning documents MUST include:

1. **Header Section**: Sprint number, dates, status
2. **Objective**: Brief, specific goal statement
3. **Implementation Tasks**: Specific, actionable tasks referencing exact files and scripts
4. **Verification Methods**: Concrete test criteria with endpoints and expected responses
5. **Dependencies**: Required tools, services, and permissions

## Implementation vs Theory

- **80% implementation, 20% theory**: Most content should focus on HOW to implement
- **Reference real files**: Always include paths to actual files in the codebase
- **Specify commands**: Include actual commands to run during implementation
- **Test-first mentality**: Define verification criteria for each implementation task

## Implementation Code Examples

Sprint planning documents MUST include concrete implementation examples for critical components. Abstract descriptions are insufficient.

### BAD Implementation Example

```markdown
❌ BAD:
Implement a server selection component that allows users to switch between environments.
```

### GOOD Implementation Example

```markdown
✅ GOOD:
Create ServerSelector component in `/apps/client/src/components/ServerSelector.tsx`:

```tsx
import React, { useState } from 'react';
import { useServerStore } from '../store/serverStore';

export const ServerSelector = () => {
  const { currentServer, setServer, servers } = useServerStore();
  const [showDropdown, setShowDropdown] = useState(false);
  
  return (
    <div className="server-selector">
      <button onClick={() => setShowDropdown(!showDropdown)}>
        Server: {currentServer.name} ▼
      </button>
      
      {showDropdown && (
        <div className="server-dropdown">
          {servers.map(server => (
            <div 
              key={server.id} 
              className="server-option"
              onClick={() => {
                setServer(server);
                setShowDropdown(false);
              }}
            >
              {server.name} ({server.url})
            </div>
          ))}
        </div>
      )}
    </div>
  );
};
```

## Failure Point Analysis

Every sprint plan MUST include an analysis of potential failure points and how to address them.

### BAD Failure Analysis

```markdown
❌ BAD:
Make sure the server is working before connecting the client.
```

### GOOD Failure Analysis

```markdown
✅ GOOD:
### Potential Failure Points:

1. **Server Port Conflict**
   - **Symptom**: Error `EADDRINUSE: address already in use :::5001`
   - **Verification**: Run `lsof -i :5001` to check if port is in use
   - **Resolution**: Modify `SERVER_PORT=5001` in `.env` to use a different port

2. **Missing Health Endpoint**
   - **Symptom**: 404 when calling `/health`
   - **Verification**: `curl http://localhost:5001/health`
   - **Resolution**: Create the endpoint in `apps/server/routes/health.js`:
   
   ```js
   app.get('/health', (req, res) => {
     res.json({
       status: 'ok',
       version: process.env.npm_package_version || '1.0.0',
       timestamp: new Date().toISOString()
     });
   });
   ```

3. **API Connection Failure**
   - **Symptom**: Network error in browser console
   - **Verification**: Open DevTools > Network tab and check for failed requests
   - **Resolution**: Ensure CORS is properly configured in server:
   
   ```js
   // In app.js or server.js
   app.use(cors({
     origin: ['http://localhost:5002', 'https://leeroy.live'],
     methods: ['GET', 'POST'],
     credentials: true
   }));
   ```

## Verification Steps Format

Every implementation task MUST have corresponding verification steps in a checklist format with exact commands.

### BAD Verification Steps

```markdown
❌ BAD:
Test that everything works.
```

### GOOD Verification Steps

```markdown
✅ GOOD:
### Server Verification Checklist

- [ ] Verify server starts without errors:
  ```bash
  npm run deploy-server
  # Should show "Server running on port 5001"
  ```

- [ ] Verify health endpoint returns correct format:
  ```bash
  curl http://localhost:5001/health
  # Should return: {"status":"ok","version":"1.0.0","timestamp":"..."}
  ```

- [ ] Verify server connects to required services:
  ```bash
  curl http://localhost:5001/health/dependencies
  # Should return status of all dependencies: DB, Redis, etc.
  ```

## Skills Protocol

All skills in the Pioneer Agent project MUST be implemented as self-contained bash scripts following these guidelines:

1. **Location**: All skill scripts MUST be saved in the `/skills` directory
   - Untested or in-progress skills should be in `/skills/untested/`
   - Tested and validated skills should be in the root `/skills` directory

2. **Self-Containment**: Each skill script MUST be completely self-contained
   - All dependencies should be explicitly checked at the beginning
   - No external configuration required beyond environment variables

3. **Verbose Error Handling**: Scripts MUST implement verbose error messaging
   - Use `set -e` to fail fast on errors
   - Implement detailed error messages that explain the issue and how to fix it
   - Log errors and successes to both console and log files

4. **Structure Requirements**:
   - Begin with a clear shebang (`#!/bin/bash`)
   - Include usage documentation in comments
   - Check for required environment variables
   - Validate existence of required files/directories
   - Implement clear logging functions for output
   - Track and report execution time

### Skills Script Template

```bash
#!/bin/bash
# skill-name.sh - Brief description of what this skill does
# Usage: ./skill-name.sh [optional-args]

set -e

# Configuration
SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
LOG_FILE="${SCRIPT_DIR}/skill-name.log"
START_TIME=$(date +%s)

# Initialize log file
echo "=== Skill Execution: $(date) ===" > $LOG_FILE

# Log function for consistent output
log() {
  local level=$1
  local message=$2
  local timestamp=$(date +"%Y-%m-%d %H:%M:%S")
  echo "[$timestamp] [$level] $message" | tee -a $LOG_FILE
}

# Check required environment
check_environment() {
  # Check for required tools
  if ! command -v some-required-tool &> /dev/null; then
    log "ERROR" "Required tool 'some-required-tool' is not installed."
    log "ERROR" "Please install it with: [installation instructions]"
    exit 1
  fi
  
  # Check for required environment variables
  if [ -z "$REQUIRED_ENV_VAR" ]; then
    log "ERROR" "Environment variable REQUIRED_ENV_VAR is not set."
    log "ERROR" "Please set it with: export REQUIRED_ENV_VAR=value"
    exit 1
  fi
  
  log "INFO" "Environment check passed"
}

# Main execution function
main() {
  log "INFO" "Starting skill execution"
  
  # Skill implementation goes here
  # [...]
  
  # Report execution time
  local end_time=$(date +%s)
  local duration=$((end_time - START_TIME))
  log "INFO" "Skill completed successfully in ${duration} seconds"
}

# Run the skill
check_environment
main
```

## Environment Variables and Configuration

All sprint plans MUST explicitly document required environment variables and configuration.

### BAD Configuration Documentation

```markdown
❌ BAD:
Configure the server with proper environment variables.
```

### GOOD Configuration Documentation

```markdown
✅ GOOD:
### Server Configuration

Create/update `.env` file in the `/apps/server` directory:

```env
# Server Configuration
SERVER_PORT=5001
NODE_ENV=development

# API Keys
OPENAI_API_KEY=sk-...  # Get from shared password manager
ANTHROPIC_API_KEY=sk-...  # Get from shared password manager

# Database
DB_HOST=localhost
DB_PORT=5432
DB_NAME=eliza_dev
DB_USER=eliza
DB_PASSWORD=dev_password  # Get from shared password manager
```

**IMPORTANT:** Never commit `.env` files to the repository. Use `.env.example` instead.

## Timeline and Dependencies

Sprint plans MUST include explicit timelines with dependencies between tasks clearly marked.

### BAD Timeline

```markdown
❌ BAD:
Complete the sprint in 7 days.
```

### GOOD Timeline

```markdown
✅ GOOD:
### Implementation Timeline

1. **Day 1**: Server Configuration and Health Endpoint (1 day)
   - Environment setup
   - Port configuration
   - Health endpoint implementation
   
2. **Day 2-3**: Client Setup and Server Selection (2 days)
   - Client port configuration
   - ServerSelector component
   - Server state management
   - **Depends on:** Server health endpoint completion

3. **Day 4-5**: API Integration (2 days)
   - API client implementation
   - Server selection integration
   - **Depends on:** ServerSelector component

4. **Day 6**: Testing and Bug Fixes (1 day)
   - Create test script
   - Run verification checks
   - Fix identified issues
   - **Depends on:** All previous tasks

Each day should end with a working increment that can be demonstrated.

## Compliance and Review

All sprint planning documents will be reviewed against this protocol. The following checklist will be used to evaluate compliance:

- [ ] Includes specific file paths for all implementations
- [ ] Contains actual code examples for critical components
- [ ] Includes verification steps with exact commands
- [ ] Documents potential failure points and resolutions
- [ ] Specifies environment variables and configuration
- [ ] Provides detailed timeline with dependencies
- [ ] Focuses 80% on implementation, 20% on theory

Non-compliant documents will be returned for revision.

## Compliance

All sprint planning documents MUST adhere to this protocol. Documents that fail to provide specific, actionable implementation guidance will be rejected.

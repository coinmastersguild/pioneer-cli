# Pioneer Agent Guild Development Protocols

**Version**: 1.0  
**Last Updated**: March 22, 2025  
**Status**: Active  

This document outlines the mandatory protocols for all Pioneer Agent development, ensuring consistency, quality, and compliance with Guild standards.

## 1. Sprint Development Lifecycle

### 1.1 Sprint Planning

**MANDATORY**: All development work MUST begin with a formal sprint planning document.

- Location: `/docs/sprint-planning/sprint-[number]-[name].md`
- Required Sections:
  - Overview & Objectives
  - Current Architecture Analysis
  - Detailed Requirements
  - Implementation Approach
  - Acceptance Criteria
  - Timeline

**Protocol Violation**: Implementing features without an approved sprint planning document is prohibited.

### 1.2 Implementation

Implementation must strictly adhere to the sprint planning document:

- Follow the exact requirements and specifications outlined in planning
- Use the actual application architecture - never build standalone alternatives
- Reference existing code patterns from the codebase
- Make changes within the proper directories:
  - Main application: `eliza-clean/client` 
  - Multi-agent system: `eliza-multi-agent`

**Architecture Rule**: Always integrate with the existing application components rather than creating parallel implementations.

### 1.3 Sprint Review

Before submitting any work as complete:

- Verify all acceptance criteria from the sprint planning document
- Run all relevant tests
- Create a sprint completion report at `/docs/sprint-reports/sprint-[number]-completion-report.md`

## 2. Data Integrity Rules

### 2.1 Prohibition on Fictional Data

**CRITICAL RULE**: Creating fictional data is strictly prohibited.

- Never create mock entities with fictional names (e.g., "Assistant Bot")
- Never fabricate metrics or statistics
- Never simulate responses that imply real-world existence

### 2.2 Proper Test/Mock Data Approach

When testing is required:

- Use clearly labeled test data with prefixes like "TEST_" or "MOCK_"
- Document all test data in code comments
- Remove test data before submitting to production
- Use actual entity names and structures from the codebase

### 2.3 Reporting Standards

When reporting status or metrics:

- Only report verifiable data from actual system components
- Clearly indicate estimated or derived values
- Never present assumptions as facts

## 3. Production Environment Protocol

### 3.1 Production Focus

**CRITICAL RULE**: Production environment status is the primary concern.

- Production domain: `leeroy.live`
- Production health endpoint: `https://leeroy.live/api/health`
- K8s deployment: `pioneer-agent` 

### 3.2 Status Checking Protocol

When asked for status, always prioritize production metrics:

1. Use the production monitoring script: `scripts/check-prod-status.sh`
2. Focus reporting on:
   - Production domain accessibility
   - Health endpoint status
   - Kubernetes deployment status
   - Pod status
   - Service availability
   - External IP verification

### 3.3 Local vs. Production Separation

- Local development environments are for testing only
- Local status is never a substitute for production status
- Always maintain clear separation in reporting
- Local environments should mirror production configuration

## 4. Code Search and Repository Navigation

### 4.1 Repository Structure

Before modifying any code, understand the repository structure:

- Primary application: `eliza-clean/client`
- Multi-agent system: `eliza-multi-agent`
- API server: `eliza-multi-agent/packages/client-direct/src`
- Agent implementation: `eliza-multi-agent/packages/core/src`

### 4.2 Code Search Protocol

When searching the codebase:

1. Perform thorough exploratory search before proposing changes
2. Search across all relevant directories
3. Cross-reference with documentation
4. Examine related components to understand context
5. Verify assumptions through multiple search methods

## 5. Code Modification Standards

### 5.1 Architecture Compliance

All code changes must:

- Follow existing architectural patterns
- Maintain separation of concerns
- Preserve API contracts
- Use established naming conventions
- Integrate with existing systems

### 5.2 Modification Process

The process for modifying code is:

1. Verify sprint planning document
2. Search for relevant existing code
3. Understand architectural context
4. Make minimal, targeted changes
5. Test changes against acceptance criteria
6. Document all modifications

## 6. Guild Rule Violations

### 6.1 Violation Handling

If a Guild rule violation occurs:

1. Immediately document the violation
2. Stop current work
3. Create a performance review document
4. Develop corrective action plan
5. Implement remediation steps

### 6.2 Repeated Violations

Repeated violations of Guild protocols will result in:

1. Comprehensive review of development practices
2. Mandatory retraining
3. Restricted development permissions
4. Potential removal from Guild projects

---

*This document serves as the definitive reference for all development activities within the Pioneer Agent Guild. All developers are required to adhere to these protocols without exception.*

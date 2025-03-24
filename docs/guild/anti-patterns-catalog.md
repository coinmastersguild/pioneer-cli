# Anti-Patterns Catalog

**Version**: 1.0  
**Last Updated**: Current Date  
**Status**: Active  

This catalog documents anti-patterns identified through our knowledge distillation process. Anti-patterns are recurring solutions that appear beneficial but ultimately produce more problems than they solve. Recognizing these patterns helps us avoid common pitfalls.

## Anti-Pattern Structure

Each anti-pattern follows this structure:

```
## [Anti-Pattern Name]

**Impact**: [High | Medium | Low]
**Frequency**: [Common | Occasional | Rare]
**Origin**: [Source: Retrospectives/Incidents/Code Reviews]

### Symptoms
[Observable signs that this anti-pattern is present]

### Harmful Consequences
[The negative outcomes of this anti-pattern]

### Root Causes
[Underlying reasons why teams fall into this pattern]

### Refactored Solution
[The correct approach to solve the original problem]

### Prevention Strategies
[How to avoid this anti-pattern in the first place]

### Recovery Examples
[References to specific instances where this was fixed]
```

## Architectural Anti-Patterns

### Distributed Monolith

**Impact**: High  
**Frequency**: Common  
**Origin**: System architecture reviews, Deployment incidents  

#### Symptoms
- Microservices that must be deployed together
- Multiple services sharing databases
- Services with tight runtime coupling
- "All or nothing" deployment requirements
- Cascading failures across services

#### Harmful Consequences
- Combines the complexity of distributed systems with the rigidity of monoliths
- Deployment coordination becomes extremely difficult
- Testing becomes complex and unreliable
- Performance issues from unnecessary network calls
- Resilience benefits of microservices are lost

#### Root Causes
- Insufficient bounded context analysis
- Premature decomposition into microservices
- Focus on technical separation without business domain separation
- Incremental migration without clear boundaries

#### Refactored Solution
- Properly define service boundaries based on business domains
- Ensure services own their data
- Design for independent deployability
- Implement proper contract testing
- Use asynchronous communication where appropriate

#### Prevention Strategies
- Domain-driven design workshops before architecture decisions
- Clear ownership boundaries for data and functionality
- Architecture reviews focused on coupling
- Deployment independence as a key requirement

#### Recovery Examples
- Auth service consolidation (Sprint 5)
- Product catalog restructuring (Sprint 7)
- Metrics collection refactoring (Sprint 9)

### Magic Configuration

**Impact**: Medium  
**Frequency**: Common  
**Origin**: Production incidents, Onboarding feedback  

#### Symptoms
- Configuration values with unclear purposes
- Values duplicated across multiple configuration files
- Configuration changes causing unexpected side effects
- High cognitive load for new team members
- Frequent configuration-related production issues

#### Harmful Consequences
- Brittle system that breaks with minor configuration changes
- Difficult onboarding for new team members
- Long troubleshooting cycles for configuration issues
- Fear of changing configuration
- Tribal knowledge dependencies

#### Root Causes
- Accumulation of configuration without documentation
- Quick fixes that add configuration without system understanding
- Lack of configuration validation
- Missing default values or fallback behavior

#### Refactored Solution
- Document all configuration values clearly
- Group related configuration together with purpose
- Implement validation for configuration values
- Design for reasonable defaults
- Centralize configuration management
- Establish configuration governance process

#### Prevention Strategies
- Configuration review in code reviews
- Documentation requirements for new configuration
- Regular configuration audits
- Configuration validation tests

#### Recovery Examples
- API service configuration refactoring (Sprint 4)
- Environment-specific configuration streamlining (Sprint 8)

## Design Anti-Patterns

### God Object

**Impact**: High  
**Frequency**: Occasional  
**Origin**: Code reviews, Refactoring initiatives  

#### Symptoms
- Classes with excessive methods or properties
- Objects with multiple responsibilities
- High rate of change across unrelated features
- Objects referenced throughout the codebase
- Excessive conditional logic based on state

#### Harmful Consequences
- Difficult to understand and maintain
- High likelihood of introducing bugs during changes
- Difficult to test effectively
- Code reuse challenges
- Merge conflicts from multiple developers

#### Root Causes
- Incremental addition of features without refactoring
- Insufficient domain modeling
- Convenience of adding "just one more" method
- Time pressure leading to shortcuts

#### Refactored Solution
- Split into multiple classes with single responsibilities
- Extract interfaces for different capabilities
- Apply composition over inheritance
- Identify proper boundaries within the domain
- Use dependency injection for collaborators

#### Prevention Strategies
- Regular complexity metrics monitoring
- Class size and responsibility limits
- Architecture reviews
- Refactoring sprints

#### Recovery Examples
- UserManager decomposition (Sprint 6)
- ConfigurationService refactoring (Sprint 7)

### Shotgun Surgery

**Impact**: Medium  
**Frequency**: Common  
**Origin**: Feature implementation feedback, Code reviews  

#### Symptoms
- Changes requiring updates to multiple unrelated files
- Feature implementations spread across many components
- Simple changes requiring deep system knowledge
- High risk of missing necessary changes
- Recurring bugs from incomplete changes

#### Harmful Consequences
- High cognitive load for developers
- Difficult onboarding for new team members
- Increased likelihood of introducing bugs
- Longer implementation times for features
- Resistance to making necessary changes

#### Root Causes
- Poor cohesion in design
- Cross-cutting concerns not properly addressed
- Feature implementation without architectural consideration
- Accumulation of technical debt

#### Refactored Solution
- Consolidate related functionality
- Implement proper abstraction layers
- Apply SOLID principles, especially Single Responsibility
- Use design patterns like Facade or Adapter
- Implement aspect-oriented approaches for cross-cutting concerns

#### Prevention Strategies
- Architecture reviews for feature implementations
- Refactoring when shotgun surgery is detected
- Code ownership and modularization
- Technical debt tracking

#### Recovery Examples
- Error handling consolidation (Sprint 5)
- Authentication flow refactoring (Sprint 8)

## Implementation Anti-Patterns

### Copy-Paste Programming

**Impact**: Medium  
**Frequency**: Common  
**Origin**: Code reviews, Bug pattern analysis  

#### Symptoms
- Duplicated code blocks with minor variations
- Similar bugs appearing in multiple places
- High code churn during changes
- Inconsistent implementations of similar features

#### Harmful Consequences
- Bug fixes not applied consistently
- Higher maintenance costs
- Inconsistent behavior
- Knowledge fragmentation
- Increased codebase size

#### Root Causes
- Time pressure
- Lack of awareness about existing code
- Insufficient abstraction
- Preference for "working code" over proper solutions

#### Refactored Solution
- Extract shared functionality into reusable components
- Identify common patterns and abstract them
- Implement proper inheritance or composition
- Create utility functions or services
- Document reusable components

#### Prevention Strategies
- Code review focus on duplication
- Automated duplication detection
- Developer education on abstraction
- Shared component libraries

#### Recovery Examples
- Validation logic consolidation (Sprint 4)
- API error handling standardization (Sprint 6)

### Premature Optimization

**Impact**: Medium  
**Frequency**: Occasional  
**Origin**: Performance troubleshooting, Code reviews  

#### Symptoms
- Complex code with performance justifications
- Optimization without measurement
- Difficult-to-understand algorithms
- Custom implementations of standard functions
- Maintainability sacrificed for theoretical performance

#### Harmful Consequences
- Increased complexity without verified benefits
- Higher maintenance costs
- Difficult onboarding
- Potential for introducing bugs
- Wasted development effort

#### Root Causes
- Anticipating performance issues without evidence
- Developer experience with previous (different) systems
- Technical ego and desire to write "clever" code
- Misunderstanding of performance bottlenecks

#### Refactored Solution
- Write clear, maintainable code first
- Measure performance with realistic workloads
- Profile to identify actual bottlenecks
- Optimize only where measurements show necessary
- Document performance requirements and trade-offs

#### Prevention Strategies
- Require performance measurements before optimization
- Clear performance requirements
- Regular profiling of production systems
- Education on modern runtime optimizations

#### Recovery Examples
- Custom caching layer simplification (Sprint 5)
- Database access layer refactoring (Sprint 7)

## Process Anti-Patterns

### Analysis Paralysis

**Impact**: High  
**Frequency**: Occasional  
**Origin**: Sprint retrospectives, Project delays  

#### Symptoms
- Excessive planning without action
- Multiple design documents without implementation
- Recurring meetings discussing the same issues
- Inability to make decisions
- Delay of implementation start

#### Harmful Consequences
- Project delays
- Team frustration
- Loss of momentum
- Wasted effort on unused designs
- Potential market opportunity costs

#### Root Causes
- Fear of making mistakes
- Unclear decision-making authority
- Perfectionism
- Previous experiences with failed projects
- Lack of iterative mindset

#### Refactored Solution
- Time-box analysis and design phases
- Define clear decision-making processes
- Embrace iterative approaches
- Create minimum viable designs
- Split large problems into smaller, tractable pieces

#### Prevention Strategies
- Sprint timeboxes for design activities
- Decision frameworks with clear owners
- Minimum viable product focus
- Regular progress check-ins

#### Recovery Examples
- Authentication redesign pivot (Sprint 3)
- Metrics implementation approach (Sprint 6)

### Hero Culture

**Impact**: High  
**Frequency**: Occasional  
**Origin**: Incident post-mortems, Team feedback  

#### Symptoms
- Reliance on specific individuals to solve problems
- Knowledge silos
- Burnout of key team members
- Bottlenecks in development or operations
- Delayed responses when key individuals are unavailable

#### Harmful Consequences
- Single points of failure
- Uneven workload distribution
- Loss of critical knowledge when people leave
- Reduced overall team capability
- Team morale issues

#### Root Causes
- Rewarding crisis management over prevention
- Insufficient knowledge sharing mechanisms
- Time pressure leading to shortcuts
- Individual preferences for control or recognition

#### Refactored Solution
- Implement structured knowledge sharing
- Pair programming and cross-training
- Documentation requirements
- Balanced work allocation
- Recognition for team success rather than individual heroics

#### Prevention Strategies
- Rotation of responsibilities
- Mentoring programs
- Documentation standards
- Celebration of collaborative successes
- Post-mortem focus on systemic issues

#### Recovery Examples
- Deployment process documentation (Sprint 5)
- On-call rotation implementation (Sprint 7)
- Shared responsibility model for core services (Sprint 9)

## Related Resources

- [Knowledge Distillation Framework](./knowledge-distillation-framework.md)
- [Architectural Principles Library](./architectural-principles-library.md)
- [Pattern Library](./pattern-library/)

---

*This catalog should evolve as new anti-patterns are identified and existing ones addressed. It serves as both a warning system and a learning resource for the team.* 
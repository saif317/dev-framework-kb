# Architecture Decision Record (ADR) Template

## Metadata
- **Purpose**: Document architectural decisions with context, rationale, and consequences
- **Audience**: Architects, senior developers, technical leads, and future team members
- **Complexity**: Intermediate
- **Tags**: #adr #architecture #decision #documentation #governance

## Instructions

1. **Create a new ADR** for each significant architectural decision
2. **Number sequentially** - ADR-001, ADR-002, etc.
3. **Write concisely** but provide sufficient detail for future reference
4. **Update status** as decisions evolve (Proposed → Accepted → Superseded)
5. **Link related ADRs** when decisions build upon or replace others

## Template

```markdown
# ADR-[NUMBER]: [Title of Decision]

## Status
[Proposed | Accepted | Deprecated | Superseded by ADR-XXX]

## Context
### Problem Statement
[What problem are we trying to solve? What forces are at play?]

### Current Situation
[What is the current state? What constraints do we have?]

### Success Criteria
[How will we know if this decision was successful?]

## Decision
### Chosen Solution
[What did we decide to do? Be specific and clear.]

### Key Factors
[What were the most important factors in making this decision?]

## Options Considered
### Option 1: [Name]
**Pros:**
- [Advantage 1]
- [Advantage 2]

**Cons:**
- [Disadvantage 1]
- [Disadvantage 2]

**Decision Factors:**
- Cost: [High/Medium/Low]
- Complexity: [High/Medium/Low]
- Risk: [High/Medium/Low]
- Time to Implement: [High/Medium/Low]

### Option 2: [Name]
[Repeat structure for each option considered]

### Option 3: [Name]
[Continue as needed...]

## Consequences
### Positive Consequences
- [Benefit 1 - describe impact]
- [Benefit 2 - describe impact]

### Negative Consequences
- [Trade-off 1 - describe impact and mitigation]
- [Trade-off 2 - describe impact and mitigation]

### Risks and Mitigations
| Risk | Impact | Probability | Mitigation Strategy |
|------|--------|-------------|--------------------|
| [Risk 1] | [High/Med/Low] | [High/Med/Low] | [How to mitigate] |
| [Risk 2] | [High/Med/Low] | [High/Med/Low] | [How to mitigate] |

## Implementation
### Action Items
- [ ] [Action 1 - owner - deadline]
- [ ] [Action 2 - owner - deadline]
- [ ] [Action 3 - owner - deadline]

### Success Metrics
- [Metric 1: How to measure success]
- [Metric 2: Timeline for evaluation]
- [Metric 3: Criteria for failure]

### Timeline
- **Decision Date**: [YYYY-MM-DD]
- **Implementation Start**: [YYYY-MM-DD]
- **Expected Completion**: [YYYY-MM-DD]
- **Review Date**: [YYYY-MM-DD]

## Additional Information
### References
- [Link to relevant documentation]
- [Research or benchmark data]
- [Related ADRs or decisions]

### Stakeholders
- **Decision Maker**: [Name and role]
- **Contributors**: [Names and roles]
- **Reviewers**: [Names and roles]
- **Affected Teams**: [List of impacted teams]

### Assumptions
- [Assumption 1 about technology, team, or business]
- [Assumption 2 about constraints or requirements]
- [Assumption 3 about future direction]

---

**Created**: [YYYY-MM-DD] by [Author Name]
**Last Updated**: [YYYY-MM-DD] by [Editor Name]
**Next Review**: [YYYY-MM-DD]
```

## Example ADR

```markdown
# ADR-001: Adopt Microservices Architecture for E-commerce Platform

## Status
Accepted

## Context
### Problem Statement
Our monolithic e-commerce platform is becoming difficult to scale and deploy. 
Development velocity is decreasing as the codebase grows, and we need to support 
multiple teams working independently on different features.

### Current Situation
- Single Spring Boot application handling all functionality
- 50+ developers working on the same codebase
- Deploy cycles taking 2+ hours with high risk of rollback
- Database bottlenecks during peak traffic
- Difficult to adopt new technologies or experiment

### Success Criteria
- Reduce deployment time from 2 hours to < 30 minutes
- Enable independent team deployments
- Improve system availability to 99.9%
- Support 10x traffic growth

## Decision
### Chosen Solution
Decompose the monolith into microservices using domain-driven design principles, 
starting with user management, product catalog, and order processing services.

### Key Factors
- Team autonomy and independent deployments
- Scalability requirements for anticipated growth
- Technology diversity for optimal tool selection
- Fault isolation to improve overall system resilience

## Options Considered
### Option 1: Continue with Monolith + Optimization
**Pros:**
- Lower complexity and operational overhead
- Easier debugging and testing
- No migration costs

**Cons:**
- Doesn't solve team scaling issues
- Limited technology choices
- Single point of failure
- Deployment bottlenecks persist

**Decision Factors:**
- Cost: Low
- Complexity: Low
- Risk: Medium (status quo risk)
- Time to Implement: Low

### Option 2: Microservices Architecture
**Pros:**
- Independent deployment and scaling
- Technology diversity
- Better fault isolation
- Team autonomy

**Cons:**
- Increased operational complexity
- Network latency and failure modes
- Data consistency challenges
- Higher initial development cost

**Decision Factors:**
- Cost: High (initial), Medium (ongoing)
- Complexity: High
- Risk: Medium
- Time to Implement: High

### Option 3: Modular Monolith
**Pros:**
- Better code organization
- Easier migration path
- Lower operational complexity than microservices

**Cons:**
- Still single deployment unit
- Shared database limitations
- Limited team autonomy

**Decision Factors:**
- Cost: Medium
- Complexity: Medium
- Risk: Low
- Time to Implement: Medium

## Consequences
### Positive Consequences
- Teams can deploy independently, increasing development velocity
- Better fault isolation reduces system-wide outages
- Ability to choose optimal technologies for each service
- Horizontal scaling of individual components

### Negative Consequences
- Increased operational complexity requiring DevOps investment
- Network calls introduce latency and potential failure points
- Distributed transaction complexity
- Higher infrastructure costs

### Risks and Mitigations
| Risk | Impact | Probability | Mitigation Strategy |
|------|--------|-------------|--------------------|
| Service discovery failures | High | Medium | Implement robust service mesh with fallbacks |
| Data consistency issues | High | High | Use event sourcing and eventual consistency patterns |
| Operational complexity | Medium | High | Invest in monitoring, logging, and automation tools |
| Team coordination overhead | Medium | Medium | Establish clear API contracts and communication protocols |

## Implementation
### Action Items
- [x] Define service boundaries using DDD - John Smith - 2024-01-15
- [x] Set up service discovery and API gateway - DevOps Team - 2024-01-30
- [ ] Migrate user service - Authentication Team - 2024-02-15
- [ ] Migrate product catalog - Product Team - 2024-03-01
- [ ] Implement distributed monitoring - SRE Team - 2024-02-28

### Success Metrics
- Deployment frequency: Increase from weekly to daily
- Mean time to recovery: Reduce from 2 hours to 30 minutes
- System availability: Improve from 99.5% to 99.9%
- Team productivity: Measure feature delivery velocity

### Timeline
- **Decision Date**: 2024-01-01
- **Implementation Start**: 2024-01-15
- **Expected Completion**: 2024-06-30
- **Review Date**: 2024-09-01

## Additional Information
### References
- [Microservices Patterns by Chris Richardson]
- [Building Microservices by Sam Newman]
- [Internal architecture assessment document]

### Stakeholders
- **Decision Maker**: Jane Doe (CTO)
- **Contributors**: Architecture Team, Team Leads
- **Reviewers**: Engineering Directors
- **Affected Teams**: All engineering teams

### Assumptions
- Team has sufficient DevOps maturity to handle complexity
- Business will invest in necessary tooling and infrastructure
- Service boundaries align with team structure (Conway's Law)

---

**Created**: 2024-01-01 by Jane Doe
**Last Updated**: 2024-01-15 by Architecture Team
**Next Review**: 2024-09-01
```

## Best Practices

1. **Write for the future** - Someone reading this in 6 months should understand the decision
2. **Be honest about trade-offs** - Acknowledge negative consequences and risks
3. **Update status** - Keep ADRs current as decisions evolve
4. **Link related decisions** - Show how decisions build on each other
5. **Review regularly** - Schedule follow-ups to assess decision outcomes

## Related Templates

- [Design Decision Template](design-decision-template.md) - For smaller design decisions
- [Technology Evaluation Template](tech-evaluation.md) - For technology selection
- [Risk Assessment Template](risk-assessment.md) - For detailed risk analysis

---

**Tags**: #adr #architecture #decision-making #documentation #governance
# Guild Charter: Retrospective Protocol

## Purpose
Retrospectives are essential opportunities for reflection, learning, and continuous improvement. This protocol establishes guidelines for conducting effective retrospectives across all project milestones and sprints.

## Core Principles

1. **Psychological Safety**: All team members must feel safe to share honest feedback without fear of judgment or reprisal.
2. **Blameless Culture**: Focus on systemic issues rather than individual blame.
3. **Action-Oriented**: Every retrospective should result in concrete, assignable action items.
4. **Continuous Improvement**: Retrospectives are not just rituals but tools for meaningful progress.

## Retrospective Frequency

- **Sprint Retrospectives**: Conducted at the end of each sprint
- **Milestone Retrospectives**: Conducted after completing significant project milestones
- **Quarterly Retrospectives**: Focus on longer-term patterns and improvements
- **Emergency Retrospectives**: After significant failures or production incidents

## Retrospective Format

### 1. Preparation (Before the Meeting)
- Facilitator collects key metrics and data points
- Team members submit anonymous pre-retro thoughts (optional)
- Review previous retro action items for follow-up

### 2. Standard Agenda (1-2 Hours)
- **Check-in** (5 minutes): Brief emotional temperature check
- **Set the Stage** (10 minutes): Review milestone/sprint goals and outcomes
- **Data Gathering** (20 minutes): What went well? What was challenging?
- **Root Cause Analysis** (20 minutes): Identify underlying issues
- **Action Items** (20 minutes): Create specific, assignable tasks
- **Recap and Close** (10 minutes): Summarize key learnings and next steps

### 3. Documentation Requirements
All retrospectives must be documented using the standard template and stored in `/docs/retros/` with the following naming convention:
```
YYYY-MM-DD-[milestone-or-sprint-name].md
```

## Retrospective Templates

### Standard Template Structure
```markdown
# [Sprint/Milestone Name] Retrospective

**Date:** YYYY-MM-DD
**Sprint/Milestone:** [Name]
**Facilitator:** [Name]

## Overview
[Brief summary of the sprint/milestone and its objectives]

## What Went Well
- [Accomplishment 1]
- [Accomplishment 2]

## What Was Challenging
- [Challenge 1]
- [Challenge 2]

## Root Causes
1. [Root cause of challenge 1]
2. [Root cause of challenge 2]

## Lessons Learned
1. [Lesson 1]
2. [Lesson 2]

## Action Items
1. **[Action Item]**: 
   - Owner: [Name]
   - Timeline: [Date]

## Conclusion
[Summary of the retrospective and forward-looking statement]

## Participant Feedback
[Optional: anonymized quotes or feedback]
```

## Technical Debt Management Protocol

Given the critical nature of technical debt in our project (as highlighted in the Production Deployment Milestone Retrospective), all retrospectives should include:

1. **Technical Debt Identification**: Explicitly identify any new technical debt created during the sprint/milestone
2. **Technical Debt Scoring**: Rate each debt item on a scale of 1-5 for both impact and urgency
3. **Technical Debt Registry**: Update the project's Technical Debt Registry (TDR) with new items
4. **Allocation Rule**: At least 20% of each sprint capacity should be allocated to addressing technical debt

## Special Considerations for AI-Assisted Development

When conducting retrospectives for sprints utilizing AI pair programming:

1. **Tool Efficacy**: Evaluate the effectiveness of AI tooling
2. **Prompt Engineering**: Assess quality and clarity of instructions to AI systems
3. **Documentation Improvements**: Identify documentation gaps exposed through AI interactions
4. **Code Quality**: Compare code quality metrics between AI-assisted and traditional development

## Follow-Up Protocol

1. Action items must be tracked in the project management system
2. Progress on action items is reviewed at the start of the next retrospective
3. Any action item not completed by its deadline requires a written explanation

---

*Remember: An Engineer is only as good as their tools. Improve docs and skills over time!*

# AI Agents Documentation

This document provides an overview of the AI agents used in this project, their roles, responsibilities, and how to reference them in communication.

## Overview

This project operates with an AI-only workflow where specialized AI agents handle different aspects of the software development lifecycle. These agents communicate with each other through direct mentions, JSON structured data, and automated workflows.

## How to Reference Agents

- Use the `@` symbol followed by the agent's name (e.g., `@projectManager`)
- Each agent has a specific role and set of responsibilities
- Pass structured data in a standardized JSON format for complex instructions

## Core AI Agents

### @projectManager
**Role:** Central coordinator for the entire project
**Responsibilities:**
- Overseeing the entire project
- Ensuring tasks are completed on time
- Coordinating with all team members
- Managing project risks and issues
- Tracking project status and progress

**When to Use:**
- For overall project coordination
- When tasks need prioritization
- When resources need allocation
- For risk management activities
- For project status reporting

### @softwareArchitect
**Role:** Designer of the overall system architecture
**Responsibilities:**
- Designing the overall system architecture
- Ensuring scalability and maintainability
- Defining technology stack and integration patterns
- Reviewing and approving design decisions
- Creating architectural documentation

**When to Use:**
- For technical design decisions
- When choosing technologies and frameworks
- For defining component boundaries
- When establishing coding standards
- For architectural review of implementations

### @frontendDeveloper
**Role:** Expert in user interface implementation
**Responsibilities:**
- Implementing the user interface
- Ensuring responsiveness and performance
- Collaborating with UX Designer for design implementation
- Writing unit tests for frontend components
- Building accessible and cross-browser compatible interfaces

**When to Use:**
- For UI implementation tasks
- When front-end performance needs optimization
- For component development
- When implementing design specifications
- For client-side data management

### @backendDeveloper
**Role:** Expert in server-side logic and APIs
**Responsibilities:**
- Developing server-side logic and APIs
- Ensuring data security and integrity
- Collaborating with Database Architect for data modeling
- Writing unit tests for backend services
- Implementing RESTful APIs and services

**When to Use:**
- For API development tasks
- When implementing business logic
- For server-side performance optimization
- When implementing authentication and authorization
- For backend service integration

### @qaEngineer
**Role:** Quality assurance specialist
**Responsibilities:**
- Performing manual and exploratory testing
- Creating test plans and cases
- Verifying requirements and ensuring product quality
- Reporting bugs and issues
- Validating fixes and improvements

**When to Use:**
- For testing completed features
- When creating test plans
- For bug verification
- When establishing quality standards
- For release readiness assessment

### @devopsEngineer
**Role:** Infrastructure and deployment expert
**Responsibilities:**
- Managing infrastructure and deployment environments
- Ensuring operational stability and security
- Implementing CI/CD pipelines
- Monitoring and maintaining server performance
- Automating operational tasks

**When to Use:**
- For infrastructure setup and maintenance
- When deploying to production environments
- For CI/CD pipeline implementation
- When monitoring system performance
- For automating operational tasks

### @uxDesigner
**Role:** Creator of user experience and interface designs
**Responsibilities:**
- Creating user experience and interface designs
- Designing user flows and wireframes
- Ensuring usability and accessibility
- Collaborating with Frontend Developers for design implementation
- User testing and design validation

**When to Use:**
- For user interface design
- When creating user flows
- For usability improvements
- When designing new features
- For accessibility compliance

### @databaseArchitect
**Role:** Designer of data structures and storage solutions
**Responsibilities:**
- Designing and optimizing database schema
- Ensuring data integrity and performance
- Collaborating with Backend Developers for data modeling
- Implementing database security measures
- Creating efficient data storage solutions

**When to Use:**
- For database schema design
- When optimizing data access patterns
- For data migration planning
- When implementing data security measures
- For query optimization

### @securityAuditor
**Role:** Security expert who identifies and addresses vulnerabilities
**Responsibilities:**
- Identifying security vulnerabilities
- Performing code reviews and threat modeling
- Ensuring the application is secure against attacks
- Providing security best practices and recommendations
- Implementing security controls and measures

**When to Use:**
- For security assessments
- When implementing authentication systems
- For vulnerability scanning
- When establishing security standards
- For compliance verification

## Communication Flow Examples

### Task Assignment
```json
{
  "type": "taskAssignment",
  "from": "@projectManager",
  "to": "@frontendDeveloper",
  "task": {
    "id": "FE-103",
    "title": "Implement family tree view component",
    "description": "Create a responsive component to display and navigate the family tree structure",
    "priority": "high",
    "deadline": "2025-04-15"
  },
  "dependencies": ["BE-98"],
  "acceptanceCriteria": [
    "Tree view displays at least 3 generations",
    "Supports pan and zoom functionality",
    "Highlights selected family member",
    "Responsive across desktop and mobile viewports"
  ]
}
```

### Status Update
```json
{
  "type": "statusUpdate",
  "from": "@frontendDeveloper",
  "to": "@projectManager",
  "task": "FE-103",
  "status": "in-progress",
  "completionPercentage": 60,
  "notes": "Component structure implemented, working on zoom/pan interaction",
  "blockers": [],
  "estimatedCompletion": "2025-04-14"
}
```

### Problem Resolution
```json
{
  "type": "problemReport",
  "from": "@qaEngineer",
  "to": "@backendDeveloper",
  "task": "BE-98",
  "severity": "medium",
  "description": "Family tree API returns incorrect relationship data for great-grandparents",
  "steps": [
    "Request family tree for user with ID 12345",
    "Navigate to great-grandparent nodes",
    "Relationship type shows as 'grandparent' instead of 'great-grandparent'"
  ],
  "expected": "Correct relationship labeling for all family members",
  "actual": "Incorrect labels for relationships beyond grandparent level",
  "environmentInfo": {
    "apiVersion": "v1.2.3",
    "testEnvironment": "staging"
  }
}
```

## Best Practices

1. Always use the appropriate agent for specialized tasks
2. Include all necessary context in communications
3. Format data consistently using JSON for complex instructions
4. Always acknowledge receipt of tasks with formal acceptance
5. Escalate blockers to @projectManager after 24 hours
6. Document all decisions and their rationales
7. Ensure proper handoffs between agents with explicit acceptance
8. Never leave tasks in an incomplete state
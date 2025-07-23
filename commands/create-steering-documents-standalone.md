# Create Steering Documents - Standalone

Create comprehensive steering documents for a development project based on the project type and requirements.

## Usage

```
Create steering documents for [project description]
```

## Examples

- `Create steering documents for a React TypeScript e-commerce application`
- `Create steering documents for a Python Django REST API with PostgreSQL`
- `Create steering documents for a Node.js microservices architecture`
- `Create steering documents for a Vue.js component library`

## Process

You are an expert at creating project steering documents that provide contextual guidance for development work. Follow this systematic approach:

### 1. Project Analysis

First, analyze the project requirements and determine which steering documents are needed:

**For Frontend Projects (React, Vue, Angular):**

- Include: project-standards.md, git-workflow.md, frontend-standards.md, development-environment.md
- Consider: component-library.md, testing-strategy.md

**For Backend/API Projects (Node.js, Python, Java):**

- Include: project-standards.md, git-workflow.md, api-design.md, development-environment.md
- Consider: database-standards.md, security-guidelines.md

**For Full-Stack Projects:**

- Include: All core documents plus technology-specific ones
- Consider: deployment-standards.md, monitoring-guidelines.md

**For Library/Package Projects:**

- Include: project-standards.md, git-workflow.md, documentation-standards.md
- Consider: versioning-strategy.md, publishing-guidelines.md

### 2. Document Creation Strategy

Create steering documents using these templates and guidelines:

#### Core Documents (Always Create)

**project-standards.md Template:**

```markdown
# Project Standards and Guidelines

## Code Quality Standards

- Follow language-specific style guides (ESLint for JS/TS, Black for Python, etc.)
- Maintain consistent naming conventions across the codebase
- Write self-documenting code with clear variable and function names
- Include meaningful comments for complex business logic
- Keep functions small and focused on single responsibilities

## Testing Requirements

- Write unit tests for all business logic functions
- Maintain minimum 80% code coverage
- Include integration tests for API endpoints
- Write end-to-end tests for critical user flows
- Use descriptive test names that explain the scenario being tested

## Documentation Standards

- Update README.md for any significant changes
- Document API endpoints with clear examples
- Include setup and deployment instructions
- Maintain changelog for version releases
- Document architectural decisions in ADR format

## Security Practices

- Never commit secrets, API keys, or passwords
- Use environment variables for configuration
- Validate all user inputs
- Implement proper authentication and authorization
- Follow OWASP security guidelines

## Performance Guidelines

- Optimize database queries and avoid N+1 problems
- Implement caching where appropriate
- Use lazy loading for large datasets
- Monitor and profile performance regularly
- Consider scalability in architectural decisions
```

**git-workflow.md Template:**

```markdown
# Git Workflow and Branching Strategy

## Branch Naming Convention

- Feature branches: `feature/description-of-feature`
- Bug fixes: `fix/description-of-bug`
- Hotfixes: `hotfix/critical-issue-description`
- Releases: `release/version-number`

## Commit Message Format

Follow conventional commits format:
```

type(scope): description

[optional body]

[optional footer]

```

Types: feat, fix, docs, style, refactor, test, chore

## Pull Request Guidelines
- Create PR from feature branch to main/develop
- Include clear description of changes
- Link related issues using keywords (fixes #123)
- Ensure all tests pass before requesting review
- Squash commits when merging to keep history clean

## Code Review Process
- At least one approval required before merge
- Review for code quality, security, and performance
- Check that tests cover new functionality
- Verify documentation is updated if needed
- Ensure no breaking changes without proper versioning
```

#### Conditional Documents (Create Based on Project Type)

**frontend-standards.md Template:**

```markdown
---
inclusion: fileMatch
fileMatchPattern: "*.tsx|*.jsx|*.vue|*.svelte"
---

# Frontend Development Standards

## Component Architecture

- Use functional components with hooks (React)
- Keep components small and focused
- Implement proper prop validation
- Use TypeScript for type safety
- Follow component composition patterns

## State Management

- Use local state for component-specific data
- Implement global state for shared application data
- Use proper state management libraries (Redux, Zustand, Pinia)
- Avoid prop drilling with context or state management

## Styling Guidelines

- Use CSS modules or styled-components for component styling
- Follow BEM methodology for CSS class naming
- Implement responsive design with mobile-first approach
- Use CSS custom properties for theming
- Maintain consistent spacing and typography scales

## Performance Optimization

- Implement code splitting and lazy loading
- Use React.memo or similar for expensive components
- Optimize images and assets
- Implement proper caching strategies
- Monitor bundle size and performance metrics

## Accessibility Standards

- Use semantic HTML elements
- Implement proper ARIA attributes
- Ensure keyboard navigation support
- Maintain proper color contrast ratios
- Test with screen readers

## Testing Strategy

- Write unit tests for utility functions
- Use React Testing Library for component tests
- Implement visual regression testing
- Test user interactions and workflows
- Mock external dependencies properly
```

**api-design.md Template:**

````markdown
---
inclusion: manual
---

# API Design Guidelines

## RESTful API Standards

- Use HTTP methods appropriately (GET, POST, PUT, DELETE, PATCH)
- Follow resource-based URL patterns: `/api/v1/users/{id}`
- Use plural nouns for resource collections
- Implement proper HTTP status codes
- Include API versioning in URL path

## Request/Response Format

- Use JSON for request and response bodies
- Follow consistent naming conventions (camelCase or snake_case)
- Include pagination for list endpoints
- Implement proper error response format:

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input provided",
    "details": ["Email is required", "Password too short"]
  }
}
```
````

## Authentication and Authorization

- Use JWT tokens for stateless authentication
- Implement proper token refresh mechanisms
- Use role-based access control (RBAC)
- Rate limit API endpoints to prevent abuse

## Documentation

- Use OpenAPI/Swagger for API documentation
- Include request/response examples
- Document all possible error responses
- Provide SDK or client library examples

#[[file:openapi.yml]]

````

**development-environment.md Template:**
```markdown
---
inclusion: fileMatch
fileMatchPattern: 'package.json|requirements.txt|Dockerfile|docker-compose.yml'
---

# Development Environment Setup

## Local Development
- Use Node.js version specified in .nvmrc file
- Install dependencies with `npm ci` for consistent builds
- Use Docker for local database and service dependencies
- Run linting and formatting before committing changes

## Environment Variables
- Copy `.env.example` to `.env` for local development
- Never commit actual environment files
- Document all required environment variables in README
- Use different prefixes for different environments (DEV_, PROD_, etc.)

## Database Management
- Use migrations for all schema changes
- Include rollback scripts for migrations
- Seed data should be idempotent
- Backup database before major changes

## Build and Deployment
- Ensure builds are reproducible across environments
- Use multi-stage Docker builds for optimization
- Include health checks in containerized applications
- Document deployment procedures and rollback steps

## Debugging and Logging
- Use structured logging with appropriate log levels
- Include correlation IDs for request tracing
- Set up proper error monitoring and alerting
- Use debugger instead of console.log for development
````

### 3. Content Customization Guidelines

**Language/Framework Specific Adaptations:**

- **JavaScript/TypeScript**: ESLint, Prettier, Jest, package.json scripts
- **Python**: Black, flake8, pytest, requirements.txt, virtual environments
- **Java**: Checkstyle, Maven/Gradle, JUnit, Spring Boot conventions
- **Go**: gofmt, go mod, testing patterns, project structure
- **Rust**: rustfmt, Cargo.toml, cargo test, clippy

**Project Scale Adaptations:**

- **Small Projects**: Lightweight processes, minimal tooling
- **Team Projects**: Code review requirements, shared standards
- **Enterprise**: Comprehensive security, compliance, documentation

**Domain Specific Considerations:**

- **E-commerce**: PCI compliance, performance, security
- **Healthcare**: HIPAA compliance, data privacy, audit trails
- **Finance**: Security standards, regulatory compliance
- **Open Source**: Contribution guidelines, licensing, community standards

### 4. File Reference Integration

Include relevant external files using the `#[[file:path]]` syntax:

- OpenAPI specifications for API projects
- Database schemas for backend projects
- Design system tokens for frontend projects
- Configuration files for environment setup

### 5. Quality Checklist

Before finalizing steering documents, ensure:

- [ ] All documents have appropriate front-matter for inclusion logic
- [ ] Guidelines are specific and actionable, not generic
- [ ] Examples are provided for complex concepts
- [ ] No conflicting standards between documents
- [ ] Security and performance considerations are included
- [ ] Documentation covers the full development lifecycle
- [ ] File references are correctly formatted and valid

## Steering Document Creation and Usage Guide

### What Are Steering Documents?

Steering documents are contextual guidelines that influence how AI assistants approach development tasks. They contain project-specific standards, conventions, and best practices that help provide more relevant and consistent assistance.

### How Steering Documents Work

#### Inclusion Mechanisms

1. **Always Included (Default)**: Documents without front-matter are included in every interaction
2. **File Match Conditional**: Documents with `inclusion: fileMatch` and `fileMatchPattern` are included when specific files are in context
3. **Manual Inclusion**: Documents with `inclusion: manual` are only included when explicitly referenced with `#steering-name`

#### Context Integration

- Steering content is injected into the AI's system context before processing user requests
- The AI receives the full content of applicable steering documents
- Multiple steering documents can be active simultaneously
- File references using `#[[file:path]]` syntax are resolved and included

### What Goes Into Steering Documents

#### Core Categories to Create:

1. **Development Environment Standards**

   - Local setup procedures
   - Tool configurations
   - Environment variable management
   - Build and deployment processes

2. **Code Quality Guidelines**

   - Language-specific style guides
   - Naming conventions
   - Code organization patterns
   - Documentation requirements

3. **Git Workflow Standards**

   - Branch naming conventions
   - Commit message formats
   - Pull request processes
   - Code review guidelines

4. **Technology-Specific Standards**

   - Frontend development patterns
   - Backend API design
   - Database management
   - Testing strategies

5. **Security and Performance**
   - Security best practices
   - Performance optimization guidelines
   - Monitoring and alerting standards

#### Content Structure to Follow:

```markdown
---
inclusion: [always|fileMatch|manual]
fileMatchPattern: "pattern" # if fileMatch
---

# Clear Title

## Organized Sections

- Specific, actionable guidelines
- Code examples where relevant
- Tool configurations
- Reference to external files using #[[file:path]]

## Implementation Details

- Step-by-step procedures
- Common pitfalls to avoid
- Quality checkpoints
```

### How to Build Steering Documents

#### Assessment Process:

1. **Project Analysis**: Examine the codebase structure, technologies used, and existing patterns
2. **Gap Identification**: Identify areas where standards would improve consistency
3. **Priority Ranking**: Focus on high-impact areas first (security, code quality, workflow)
4. **Template Selection**: Choose appropriate templates based on project type

#### Content Development:

1. **Research Best Practices**: Draw from industry standards and proven patterns
2. **Contextualize for Project**: Adapt generic practices to specific project needs
3. **Include Examples**: Provide concrete code examples and configurations
4. **Reference Integration**: Link to existing project files and specifications

#### Quality Assurance:

1. **Completeness Check**: Ensure all critical areas are covered
2. **Consistency Validation**: Verify guidelines don't conflict with each other
3. **Practicality Assessment**: Confirm guidelines are actionable and realistic
4. **Update Mechanism**: Plan for maintaining documents as project evolves

### Inclusion Strategy and Context Transmission

#### What Gets Sent:

- **Full Content**: Complete steering document content is transmitted
- **Resolved References**: Files referenced with `#[[file:path]]` are read and included
- **Multiple Documents**: All applicable steering documents are combined
- **Real-time Evaluation**: Inclusion rules are evaluated for each interaction

#### When Documents Are Included:

- **Always**: Default behavior for documents without front-matter
- **File Context Triggers**: When specific file patterns are in the conversation context
- **Manual Triggers**: When user explicitly references with `#steering-name`
- **Automatic Resolution**: System determines relevance based on file patterns

#### Context Limitations:

- Large steering documents may be truncated if they exceed context limits
- Priority is given to more specific/relevant steering documents
- Recent interactions may influence which documents are prioritized

### Best Practices for Steering Creation

#### Do:

- Keep documents focused and specific
- Use clear, actionable language
- Include concrete examples
- Reference external specifications
- Update regularly as project evolves
- Use appropriate inclusion mechanisms

#### Don't:

- Create overly broad or generic guidelines
- Duplicate information across multiple documents
- Include sensitive information or secrets
- Create conflicting standards
- Make documents too long or complex

### Maintenance and Evolution

#### Regular Review:

- Assess effectiveness of existing steering documents
- Update based on project changes and learnings
- Remove outdated or conflicting guidelines
- Add new standards as project grows

#### Feedback Integration:

- Monitor how well steering documents influence code quality
- Adjust based on team feedback and development patterns
- Refine inclusion patterns for better relevance
- Optimize document structure for clarity

### Technical Implementation Notes

#### File Structure:

```
.spec-driven-development/steering/
├── project-standards.md (always included)
├── git-workflow.md (always included)
├── frontend-standards.md (fileMatch: *.tsx,*.jsx)
├── api-design.md (manual inclusion)
└── development-environment.md (fileMatch: package.json)
```

#### Front-matter Options:

```yaml
---
inclusion: always|fileMatch|manual
fileMatchPattern: "glob-pattern" # for fileMatch only
---
```

#### File Reference Syntax:

```markdown
#[[file:relative/path/to/file.ext]]
```

## Output Format

Create a complete set of steering documents in the `.spec-driven-development/steering/` directory with:

1. Appropriate front-matter for inclusion logic
2. Project-specific content and examples
3. Clear, actionable guidelines
4. Proper file references where applicable
5. Consistent formatting and structure

The steering documents should immediately improve development consistency and provide contextual guidance for the specific project requirements.

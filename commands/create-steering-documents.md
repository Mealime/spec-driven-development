# Create Steering Documents

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

**project-standards.md** - #[[file:.spec-driven-development/steering/project-standards.md]]

- Adapt code quality standards to project language/framework
- Customize testing requirements based on project complexity
- Include project-specific documentation needs
- Set security practices relevant to the domain

**git-workflow.md** - #[[file:.spec-driven-development/steering/git-workflow.md]]

- Adjust branch naming for team size and release strategy
- Customize commit message format for project needs
- Set appropriate review requirements
- Define merge strategies

#### Conditional Documents (Create Based on Project Type)

**frontend-standards.md** - #[[file:.spec-driven-development/steering/frontend-standards.md]]

```yaml
---
inclusion: fileMatch
fileMatchPattern: "*.tsx|*.jsx|*.vue|*.svelte|*.ts|*.js"
---
```

- Customize for specific framework (React/Vue/Angular)
- Include design system and styling approach
- Set accessibility requirements
- Define performance standards

**api-design.md** - #[[file:.spec-driven-development/steering/api-design.md]]

```yaml
---
inclusion: fileMatch
fileMatchPattern: "*api*|*route*|*controller*|*endpoint*"
---
```

- Adapt REST/GraphQL standards to project needs
- Include authentication/authorization patterns
- Set error handling conventions
- Define API versioning strategy

**development-environment.md** - #[[file:.spec-driven-development/steering/development-environment.md]]

```yaml
---
inclusion: fileMatch
fileMatchPattern: "package.json|requirements.txt|Dockerfile|docker-compose.yml|Makefile"
---
```

- Customize for project's tech stack
- Include specific tooling requirements
- Set environment variable patterns
- Define build and deployment processes

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

## Reference Materials

Use these comprehensive guides for creating steering documents:

**Creation Guide:** #[[file:.spec-driven-development/steering/steering-creation-guide.md]]

**Template Examples:**

- #[[file:.spec-driven-development/steering/project-standards.md]]
- #[[file:.spec-driven-development/steering/git-workflow.md]]
- #[[file:.spec-driven-development/steering/frontend-standards.md]]
- #[[file:.spec-driven-development/steering/api-design.md]]
- #[[file:.spec-driven-development/steering/development-environment.md]]

## Output Format

Create a complete set of steering documents in the `.spec-driven-development/steering/` directory with:

1. Appropriate front-matter for inclusion logic
2. Project-specific content and examples
3. Clear, actionable guidelines
4. Proper file references where applicable
5. Consistent formatting and structure

The steering documents should immediately improve development consistency and provide contextual guidance for the specific project requirements.

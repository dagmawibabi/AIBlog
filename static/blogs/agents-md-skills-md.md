---
title: AGENTS.md and SKILLS.md - The Complete Guide
date: 2026-01-15
category: 'AI'
description: 'A comprehensive guide to AGENTS.md and SKILLS.md - the open standards for configuring AI coding agents. Learn setup, usage, best practices, and how they impact context windows.'
---

# AGENTS.md and SKILLS.md: The Complete Guide to Configuring AI Coding Agents

The landscape of AI-assisted software development has evolved dramatically. What began as simple code completion has transformed into full-fledged coding agents capable of understanding project context, executing complex tasks, and following team conventions. At the heart of this evolution are two powerful open standards: **AGENTS.md** and **SKILLS.md**. These files have become essential tools for teams looking to get the most out of their AI coding assistants, with over 60,000 open-source projects now using AGENTS.md according to GitHub search data.

Whether you are a developer just starting with AI agents or an engineering team looking to standardize how agents interact with your codebase, understanding these two standards is crucial. This guide will walk you through everything from basic concepts to advanced implementation strategies, with particular attention to how these files interact with context windows—a consideration that becomes increasingly important as projects grow larger.

## What is AGENTS.md?

At its core, AGENTS.md is a markdown file that lives in your project root and serves as a dedicated instruction manual for AI coding agents. Think of it as a README specifically designed for artificial intelligence rather than human developers. While your traditional README.md explains what your project does and how to get started for humans, AGENTS.md contains the additional context that agents need to work effectively within your codebase.

The format emerged from collaborative efforts across the AI software development ecosystem, with contributions from OpenAI Codex, Cursor, Google Jules, Factory, and other leading platforms. In November 2025, the Agentic AI Foundation—operating under the Linux Foundation—officially became the steward of this open standard, ensuring its continued development and cross-platform compatibility.

The philosophy behind AGENTS.md is straightforward: provide a single, predictable location where agents can find project-specific guidance without cluttering your human-facing documentation. This separation allows your README to remain concise and focused on human contributors while giving agents access to the detailed instructions they need to follow your team's conventions, run the correct build commands, and produce code that matches your existing patterns.

### How AGENTS.md Differs from Traditional Documentation

Traditional documentation files like README.md serve human readers. They typically include project overviews, installation instructions, and contribution guidelines written in natural language that assumes human context and experience. While AI agents can parse this information, it often contains details irrelevant to their work and may miss crucial information about build processes, testing requirements, and code conventions.

AGENTS.md solves this problem by creating a dedicated space for agent-specific instructions. The file is intentionally plain Markdown with no required fields or specific formatting constraints—agents simply parse the text you provide. This flexibility allows you to include exactly what matters for AI interactions, whether that is specific npm commands, TypeScript configuration details, or patterns for how your team structures components.

The file also supports hierarchical configuration through nested AGENTS.md files. Large monorepos can place additional AGENTS.md files within specific packages or subdirectories, and agents automatically read the nearest file in the directory tree. This means each subproject can have tailored instructions that override or supplement the root-level guidance. The main OpenAI repository, for example, contains 88 different AGENTS.md files across its various packages and subprojects.

## What is SKILLS.md?

While AGENTS.md focuses on project-specific instructions, SKILLS.md is part of a broader concept called Agent Skills—a standardized format for giving agents new capabilities and expertise beyond their default abilities. Agent Skills originated at Anthropic and were released as an open standard, subsequently being adopted by an growing ecosystem of agent products and tools.

An Agent Skill is essentially a folder containing instructions, scripts, and resources that agents can discover and use to perform specialized tasks. Unlike the single-file approach of AGILLS.md, a skill is a cohesive package that might include detailed procedural knowledge, example code, reference documentation, and even executable scripts. This allows skills to represent complete capabilities—from legal review processes to data analysis pipelines—rather than just configuration preferences.

The SKILLS.md file serves as the manifest or specification document within a skill folder. It defines what the skill does, what resources it requires, how it should be used, and what capabilities it provides. When an agent encounters a skill, it reads the SKILLS.md to understand how to apply the skill's capabilities to the task at hand.

### The Relationship Between AGENTS.md and SKILLS.md

These two standards complement rather than compete with each other. AGENTS.md tells agents how to work within your specific project—your build commands, your coding style, your testing requirements. SKILLS.md defines reusable capabilities that agents can load when needed—specialized knowledge or workflows that extend an agent's base abilities.

In practice, an AGENTS.md file might reference specific skills that are relevant to your project, telling agents which skills to load and when to use them. Conversely, a skill's SKILLS.md might include guidance on how it should be integrated with project-level instructions. This layered approach allows for both project-specific customization and portable, reusable expertise.

## Why These Standards Matter for AI Development

The adoption of AGENTS.md and SKILLS.md reflects a broader shift in how teams approach AI-assisted development. Rather than repeatedly explaining project conventions in every conversation with an agent, teams can encode this knowledge once and have it automatically applied across all interactions. This consistency saves time, reduces errors, and helps agents produce output that more closely matches team expectations.

Consider a typical development scenario without AGENTS.md: a new team member or AI agent must explore the repository to understand how to build and test the project, what coding conventions to follow, and where various components live. This discovery phase repeats for every new chat session and every new team member, burning time and resources. With AGENTS.md, this context is immediately available, allowing agents to start productive work immediately.

The open nature of these standards provides additional benefits. Because they are not proprietary to any single AI provider, investment in creating AGENTS.md and SKILLS.md files pays off regardless of which coding agent you use. Whether your team uses GitHub Copilot, Claude Code, Cursor, OpenAI Codex, or any other supported tool, these files provide consistent guidance. The AGENTS.md specification explicitly notes compatibility with dozens of agents and tools, including VS Code, Zed, Windsurf, Devin, Aider, and many others.

## Impact on Context Windows

Understanding how AGENTS.md and SKILLS.md interact with context windows is essential for maximizing their effectiveness. Context windows—the amount of text an AI model can process at once—represent a fundamental constraint on agent capabilities. Both of these standards were designed with this constraint in mind, providing efficient ways to convey important information without consuming excessive context.

### How AGENTS.md Affects Context Usage

When an agent loads your project, it incorporates your AGENTS.md content into its context. This means the file consumes part of your available context window, but in a highly efficient way. Rather than requiring you to repeat the same instructions in every conversation, the information is loaded once and available throughout the session.

The OpenAI Codex implementation provides a concrete example of how this works. Codex builds an instruction chain when it starts, with discovery following a specific precedence order. First, it reads any global guidance from your Codex home directory. Then it walks down from the project root to your current working directory, checking for AGENTS.md files at each level. The files are concatenated with blank lines, with later files overriding earlier guidance because they appear later in the combined prompt.

Codex stops adding files once the combined size reaches the limit defined by `project_doc_max_bytes`, which defaults to 32 KiB. This design recognizes that context windows, while growing, are still finite. By implementing size limits and hierarchical overrides, the system ensures that the most relevant guidance gets priority while preventing context overflow.

For users, this means being intentional about AGENTS.md size and organization. A file that tries to cover everything in exhaustive detail may hit size limits, causing important guidance to be truncated. The recommended approach is to keep files focused and use nested AGENTS.md files for package-specific or directory-specific guidance. This distributed approach allows each file to remain small while collectively providing comprehensive coverage.

### How SKILLS.md Optimizes Context

SKILLS.md takes a different approach to context optimization by enabling on-demand capability loading. Rather than including all possible knowledge in the context at once, skills allow agents to load relevant expertise when needed. This follows the same principle as lazy loading in software development—initialize or load resources only when they are actually used.

When an agent determines that a task requires a particular skill, it loads the corresponding SKILLS.md and associated resources into context. This means the context is not cluttered with skills that are irrelevant to the current task, but the agent still has access to specialized knowledge when it would be helpful. The skill's instructions, examples, and resources are available exactly when needed, without the overhead of having them present constantly.

This approach is particularly valuable for complex projects that span multiple domains. A single project might involve frontend development, backend APIs, data processing, and deployment workflows. Rather than loading all domain knowledge into context simultaneously, agents can load relevant skills for each specific subtask, keeping context focused and efficient.

### Practical Implications for Large Projects

For large projects, context window management becomes a critical consideration. The GitHub Copilot implementation of AGENTS.md allows defining multiple specialized agents through frontmatter, enabling you to create distinct configurations for different types of tasks. A `@docs-agent` might have different instructions than a `@test-agent` or `@security-agent`, and each configuration only includes what that specific agent type needs.

This specialization reduces context consumption while ensuring each agent has the guidance relevant to its function. When you switch between agent types, the system loads the appropriate configuration, keeping context focused on the task at hand.

The OpenAI Codex approach to context management through hierarchical file discovery and byte limits provides another model for handling large projects. By allowing nested AGENTS.md files with override capabilities, the system enables precise control over what guidance is active in different parts of the repository. A developer working on payment services sees different guidance than one working on user authentication, and neither is burdened with irrelevant context.

## Setting Up AGENTS.md for Your Project

Creating an effective AGENTS.md file is straightforward, but crafting one that truly improves agent interactions requires thoughtfulness. The following sections walk through the setup process, from basic creation to advanced configuration.

### Creating Your First AGENTS.md

The simplest AGENTS.md file contains just a few key sections. Place the file in your repository root—typically the same directory as your README.md and package.json or equivalent configuration file. Most modern coding agents will automatically detect and read this file without any additional configuration.

Here is a minimal example to get started:

```markdown
# AGENTS.md

## Setup Commands

- Install dependencies: `npm install` (or `pnpm install`, `yarn install`)
- Start development server: `npm run dev`
- Run tests: `npm test`
- Build for production: `npm run build`

## Code Style

- Language: TypeScript with strict mode enabled
- Formatting: Prettier with single quotes, no semicolons
- Linting: ESLint with the recommended configurations

## Testing

- Run unit tests: `npm run test:unit`
- Run integration tests: `npm run test:integration`
- View coverage: `npm run test:coverage`
```

This basic structure covers the three areas most commonly needed by agents: how to set up the project, what coding style to follow, and how to run tests. With just this much information, agents can work much more effectively than with no guidance at all.

### Adding Project Structure Information

One of the most valuable additions to AGENTS.md is information about your project structure. Agents can search your codebase, but providing explicit pointers saves time and helps them start in the right place. Consider adding a section like this:

```markdown
## Project Structure

- Source code: `src/`
- Components: `src/components/`
- API routes: `src/routes/api/`
- Utilities: `src/lib/utils/`
- Styles: `src/styles/`
- Tests: `__tests__/` (co-located with source files)

### Key Files

- Entry point: `src/index.tsx`
- App configuration: `src/App.tsx`
- API client: `src/lib/api/client.ts`
- Theme: `src/lib/theme/`
```

This guidance helps agents quickly locate relevant files rather than exploring the entire repository. When you ask an agent to add a new API endpoint, it can immediately navigate to the routes directory rather than searching through the entire src folder.

### Defining Do's and Don'ts

Beyond structure and commands, AGENTS.md excels at communicating your team's preferences and conventions. The "dos and don'ts" pattern has proven particularly effective, as it allows you to be explicit about what agents should and should not do:

```markdown
## Do

- Use functional components with hooks (see `src/components/Button.tsx` for example)
- Use the design system components from `@acme/ui`
- Put tests next to the files they test with `.test.tsx` extension
- Use the API client from `src/lib/api/client.ts` for HTTP requests
- Follow the component structure shown in `src/components/Form/`

## Don't

- Use class components (legacy code in `src/legacy/` should not be copied)
- Add new dependencies without team approval
- Hardcode colors or styling—use tokens from the theme
- Create new utility files without checking `src/lib/utils/` first
- Modify files in `src/config/` without explicit permission
```

This section should evolve over time. As you work with agents and notice patterns in their output that you like or dislike, update this section to encode your preferences. After a few iterations, you will have a comprehensive guide that significantly improves agent behavior.

### Configuring File-Scoped Commands

For larger projects, running full project-wide commands on every change is impractical. Type checking, linting, and testing can take minutes to complete, and running these commands unnecessarily wastes time and resources. AGENTS.md allows you to specify file-scoped alternatives that agents can run for faster feedback:

```markdown
## Commands

### File-scoped (preferred)

- Type check single file: `npx tsc --noEmit --project tsconfig.json`
- Format single file: `npx prettier --write <path>`
- Lint single file: `npx eslint --fix <path>`
- Test single file: `npx vitest run <path>`

### Project-wide (when needed)

- Full type check: `npm run typecheck`
- Full build: `npm run build`
- All tests: `npm test`
- Full lint: `npm run lint`

### When to Use Which

Always use file-scoped commands for single-file changes. Use project-wide commands only when explicitly requested or when changes might affect multiple files.
```

This guidance helps agents provide fast feedback loops while ensuring comprehensive checks when they are actually needed.

### Setting Up Nested AGENTS.md Files

For monorepos or multi-package projects, nested AGENTS.md files provide targeted guidance for each component. Place an AGENTS.md file within each package or subdirectory that needs specific instructions. Agents automatically read the nearest file, allowing more specific guidance to override broader project-level rules.

Consider this structure for a monorepo with frontend and backend packages:

```
/repository-root/
├── AGENTS.md              # Project-level guidance
├── package.json
├── packages/
│   ├── frontend/
│   │   ├── AGENTS.md      # Frontend-specific rules
│   │   ├── package.json
│   │   └── src/
│   └── backend/
│       ├── AGENTS.md      # Backend-specific rules
│       ├── package.json
│       └── src/
```

The frontend AGENTS.md might specify React-specific patterns and commands, while the backend AGENTS.md focuses on Python or Node.js patterns appropriate to that service. Both inherit the root-level guidance while having their own specialized instructions.

### Global AGENTS.md Configuration

Beyond project-specific files, you can create a global AGENTS.md in your home directory or agent configuration directory. This allows you to define working preferences that apply across all your projects, reducing repetition when you work on multiple repositories.

For OpenAI Codex, the global file goes in `~/.codex/AGENTS.md`. For other tools, check their documentation for the appropriate location. A global file might look like:

```markdown
# ~/.codex/AGENTS.md

## Global Working Agreements

- Always run `npm test` after modifying JavaScript/TypeScript files
- Prefer `pnpm` over npm or yarn when installing dependencies
- Ask for confirmation before adding new production dependencies
- Use conventional commit messages for all changes
- Always run linting before committing
```

When you open a project that also has a local AGENTS.md, the agent combines both files, with the local file taking precedence for project-specific matters. This allows global preferences to apply everywhere while still accommodating project-specific differences.

## Creating and Using SKILLS.md

While AGENTS.md is about project configuration, SKILLS.md represents a more ambitious capability—creating reusable packages of expertise that agents can load and apply.

### Understanding the Agent Skills Format

An Agent Skill is distributed as a folder containing everything needed to perform a specialized task. According to the Agent Skills specification, this includes the SKILLS.md manifest file, instructions, scripts, examples, and any reference materials. When an agent encounters a skill, it can understand what the skill does, how to use it, and what resources are available.

The key insight behind skills is that procedural knowledge—knowing how to accomplish a task step by step—is different from declarative knowledge about facts. A skill captures the former, encoding not just information but the process for applying it. This makes skills particularly valuable for complex, multi-step workflows that would be difficult to describe in a single prompt.

### Anatomy of a SKILLS.md File

The SKILLS.md file serves as the manifest for a skill. It uses YAML frontmatter to define metadata followed by markdown content explaining the skill:

```markdown
---
name: Data Analysis Pipeline
description: Perform exploratory data analysis on CSV datasets
version: 1.0.0
author: Data Science Team
tags: [data-analysis, pandas, visualization]
requires: [python-3.9+, pandas, matplotlib]
---

# Data Analysis Skill

This skill provides capabilities for exploring and analyzing tabular data
in CSV format.

## Capabilities

- Load and validate CSV files
- Generate summary statistics
- Create visualizations
- Identify data quality issues
- Export analysis reports

## Usage

When working with CSV data analysis tasks, load this skill and use the
following patterns:

1. Load data: `load_csv(path, options)`
2. Explore: `get_summary(df)`, `get_correlations(df)`
3. Visualize: `create_histogram(df, column)`, `create_scatter(df, x, y)`
4. Report: `generate_report(df, output_path)`

## Examples

See the `examples/` directory for complete analysis workflows.

## Limitations

- Optimized for datasets under 1GB
- Supports CSV with standard delimiters
- Requires pandas-compatible column types
```

This structure tells agents when to use the skill, what capabilities it provides, and how to apply those capabilities to tasks. The skill can then be discovered and loaded by compatible agents when relevant work is being done.

### Creating Custom Skills

Building a custom skill involves creating a folder with the necessary components:

1. **SKILLS.md**: The manifest and documentation
2. **Instructions/**: Detailed procedural guidance
3. **Examples/**: Reference implementations showing correct usage
4. **Scripts/**: Any executable components
5. **Resources/**: Reference materials, data files, or documentation

For a data analysis skill, the folder structure might look like:

```
data-analysis-skill/
├── SKILLS.md
├── instructions/
│   ├── loading-data.md
│   ├── exploration.md
│   └── visualization.md
├── examples/
│   ├── sales-analysis/
│   │   ├── data.csv
│   │   └── analysis.py
│   └── customer-churn/
│       ├── dataset.csv
│       └── investigation.py
├── scripts/
│   ├── validate_csv.py
│   └── generate_report.py
└── resources/
    ├── pandas-cheatsheet.md
    └── visualization-guide.md
```

When an agent loads this skill, it has access to all of these resources, allowing it to provide expert-level assistance for data analysis tasks without requiring you to explain the domain each time.

### Integrating Skills with AGENTS.md

AGENTS.md can reference relevant skills for your project, telling agents which capabilities are available and when to use them:

```markdown
## Available Skills

The following skills are available for this project:

- **Data Analysis**: Use for CSV analysis and visualization tasks
- **API Documentation**: Use when working with our REST API endpoints
- **Testing Patterns**: Use when writing or updating tests

## Skill Configuration

Load skills automatically for relevant tasks. The agent will determine
which skill applies based on the current task context.

### Skill Locations

- Project skills: `/.skills/`
- User skills: `~/.skills/`
- System skills: (built-in)
```

This integration means agents can benefit from specialized skills without requiring you to manually load them each time. The agent determines which skills are relevant to the current task and loads them as needed.

### Publishing and Sharing Skills

Because Agent Skills is an open standard, skills you create are portable across different tools and platforms. Skills published to registries or shared through version control can be discovered and used by any skills-compatible agent. This ecosystem approach means investment in creating skills pays dividends across your entire toolchain.

The Agent Skills specification notes adoption by leading AI development tools, including GitHub Copilot, VS Code, OpenAI Codex, and others. This cross-platform support means skills created for one tool can often be used with others, maximizing the value of your skill development efforts.

## Best Practices for AGENTS.md

Based on analysis of thousands of repositories using AGENTS.md, certain patterns consistently produce better results. The following practices reflect lessons learned from real-world usage.

### Keep It Focused and Scoped

The most effective AGENTS.md files are focused on what agents actually need to know. Resist the temptation to include every piece of project documentation. Instead, focus on information that affects code generation: build commands, testing requirements, coding conventions, and project structure.

If you find your AGENTS.md growing excessively long, consider whether some information would be better placed in a nested file for a specific directory or package. Large, undifferentiated files may hit context limits, causing important guidance to be truncated.

### Use Concrete Examples

抽象的指导不如具体的例子有效。Instead of saying "follow our component patterns," point to actual files that demonstrate those patterns:

```markdown
## Good Examples

- Forms: follow `src/components/forms/SearchForm.tsx`
- Data tables: follow `src/components/tables/UserTable.tsx`
- API integration: follow `src/lib/api/requests.ts`
- State management: follow `src/lib/state/auth.ts`

## Anti-Patterns to Avoid

- Avoid patterns from `src/legacy/` (outdated approaches)
- Avoid direct API calls in components (use the API layer)
- Avoid styled-components (use our design system instead)
```

When agents see real code examples, they can more accurately reproduce your team's style and patterns.

### Iterate Based on Experience

Your AGENTS.md should evolve based on your actual experience working with agents. When you notice an agent making the same mistake repeatedly, add guidance to prevent it. When an agent produces output you like, consider what guidance contributed to that success.

Treat AGENTS.md as living documentation that improves over time. Many teams schedule periodic reviews to update their AGENTS.md based on recent experience, ensuring the file remains accurate and helpful.

### Be Specific About Commands

Vague command references are less helpful than precise ones. Instead of "run tests," specify the exact command and what it does:

```markdown
## Testing Commands

- Run all tests: `npm test` (runs Vitest suite)
- Run single test file: `npm test -- src/utils/formatters.test.ts`
- Run tests matching pattern: `npm test -- -t "should format currency"`
- Watch mode for development: `npm test:watch`
- Generate coverage report: `npm run test:coverage`
```

Specific commands allow agents to run exactly what you intend without guessing or exploring alternative approaches.

### Include Security Considerations

If your project has security requirements or sensitive operations, make them explicit in AGENTS.md:

```markdown
## Security

### Allowed Operations Without Confirmation

- Read files within the project
- Run linting and type checking
- Execute test suites

### Requires Explicit Confirmation

- Installing new packages
- Modifying environment variables
- Running database migrations
- Pushing changes to any branch
- Accessing credentials or secrets

### Protected Resources

- Never modify files in `src/config/secrets/`
- Never commit credentials or API keys
- Always use the secrets service for sensitive data
```

This clarity helps agents understand boundaries and prevents unintended operations that could compromise security.

## Advanced Configuration and Troubleshooting

Even with well-crafted AGENTS.md files, you may encounter issues requiring debugging or advanced configuration.

### Resolving Conflicts Between Files

When multiple AGENTS.md files are active, conflicts can arise. The resolution mechanism varies by agent, but common patterns include:

1. **Nearest file wins**: Most agents give precedence to the AGENTS.md closest to the file being edited
2. **Override files**: Some agents support `AGENTS.override.md` for temporary overrides
3. **User prompts override everything**: Explicit instructions in conversation take precedence over file-based guidance

When conflicts occur, review which files are active in the current directory and consider whether the precedence order matches your intent.

### Debugging Discovery Issues

If your AGENTS.md is not being read, several common issues may be responsible:

- **File location**: Verify the file is in the expected location (repository root or relevant subdirectory)
- **File naming**: Confirm the exact filename is `AGENTS.md` (case-sensitive on some systems)
- **File content**: Ensure the file is not empty—agents skip empty files
- **Configuration**: Check agent settings for custom fallback filenames or disabled AGENTS.md support

Most agents provide ways to verify which instruction files are active. For Codex, running `codex --ask-for-approval never "Show which instruction files are active."` will list loaded files.

### Handling Large Files and Context Limits

When your combined AGENTS.md content exceeds context limits, agents may truncate or skip files. Solutions include:

1. **Reduce file size**: Remove outdated information, condense examples, focus on essentials
2. **Use nested files**: Distribute guidance across multiple AGENTS.md files at different directory levels
3. **Adjust limits**: Some agents allow increasing `project_doc_max_bytes` or equivalent settings
4. **Prioritize**: Ensure the most important guidance appears early in files, where it is less likely to be truncated

The key is treating AGENTS.md as a targeted, essential resource rather than comprehensive documentation.

### Migrating from Other Formats

Some projects may already have agent configuration files in other formats. Migration is straightforward:

For tool-specific files like `.cursorrules` or `.claude.md`, you can create a simple reference file:

```markdown
# CLAUDE.md

See AGENTS.md for project instructions.
```

Or use symbolic links to point tool-specific files to your AGENTS.md:

```bash
ln -s AGENTS.md .cursorrules
ln -s AGENTS.md .claude.md
```

This approach maintains compatibility with tools that expect their specific filenames while centralizing your guidance in AGENTS.md.

## The Future of Agent Configuration

The AGENTS.md and SKILLS.md standards continue to evolve as AI agents become more capable and widespread. The Agentic AI Foundation's stewardship ensures ongoing development, and growing adoption across the industry suggests these standards will remain relevant.

Several trends are worth watching. First, the integration between AGENTS.md and skills is deepening, with agents becoming more sophisticated about when to load which resources. Second, the ecosystem of shared skills is growing, enabling teams to benefit from specialized expertise created by others. Third, agent configuration is increasingly integrated into development workflows, with linters, formatters, and other tools beginning to validate AGENTS.md content.

For teams beginning with these standards, the key is to start simple and iterate. A basic AGENTS.md with setup commands, code style, and testing instructions provides immediate value. As you gain experience working with agents, you can progressively add more sophisticated guidance, nested configurations, and skill integrations.

## Conclusion

AGENTS.md and SKILLS.md represent a significant advancement in how teams work with AI coding agents. By providing structured, persistent guidance, these open standards help agents understand project-specific context, follow team conventions, and produce higher-quality output. The impact on context windows—while real—is managed through thoughtful design that prioritizes relevant information and enables on-demand loading of specialized capabilities.

Whether you are a solo developer looking to improve your workflow or part of a large team standardizing AI-assisted development, investing time in AGENTS.md and SKILLS.md pays dividends in agent effectiveness. Start with a focused AGENTS.md that covers your essential project information, iterate based on your experience, and consider skills when you have complex workflows worth encapsulating.

The standards are open, the ecosystem is growing, and the tools are ready to use. Your AGENTS.md file is waiting to be written.

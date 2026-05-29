# BoxLang IDE Documentation Project Instructions

## Project Overview

This repository contains the documentation for **BoxLang IDE** — the BoxLang language plugin for JetBrains IDEs and VSCode. The documentation is built using **GitBook** and covers IDE installation, language tooling (LSP, linting, formatting), and editor-specific features.

The plugin is available from:

- [JetBrains Marketplace](https://plugins.jetbrains.com/plugin/30311-boxlang-ide)
- [VSCode Marketplace](https://marketplace.visualstudio.com/items?itemName=ortus-solutions.vscode-boxlang)

## Architecture & Organization

### Core Structure

- **`introduction/`** — Contributing guide, release history, and book metadata
- **`language-tools/`** — BoxLang LSP overview, linting configuration (`.bxlint.json`), formatting (`.bxformat.json`)
- **`vscode/`** — VSCode extension overview, installation, MiniServer, BoxLang Home configuration, commands
- **`overview.md`** + **`installation.md`** — JetBrains IDE plugin overview and installation

### Documentation Types

1. **Installation Guides** — Step-by-step instructions for installing the plugin in different editors
2. **Language Tooling Reference** — LSP diagnostics, lint rules, formatting, and configuration file schemas
3. **Editor Feature Docs** — Editor-specific features (MiniServer, debugger, commands, BoxLang Home management)

## File Conventions

### Frontmatter Structure

Every documentation file uses YAML frontmatter with specific patterns:

```yaml
---
description: Brief, descriptive summary for SEO/navigation
icon: gitbook-icon-name  # From Font Awesome icon library
---
```

### Content Patterns

- **Emojis in headings** for visual hierarchy: `## 🚀 Getting Started`
- **Table-based API references** with consistent columns
- **Code examples** in `js` blocks (BoxLang syntax highlighting) until BoxLang is offered by GitBook
- **Callouts** for important notes, warnings, and tips using GitBook's hint system
- **GitBook callouts** using `{% hint style="info|warning|danger|success" %}`
- **Markdown spacing** — All headers must be surrounded by blank lines (before and after). All code blocks must be surrounded by blank lines (before and after the fences).

### Navigation Integration

- **`SUMMARY.md`** defines the complete table of contents structure
- Cross-references use `{% content-ref url="relative/path.md" %}`
- External embeds with `{% embed url="..." %}`

## Documentation Workflows

### Content Creation Patterns

1. **Start with frontmatter** — Always include description and appropriate icon
2. **Use consistent heading hierarchy** — H1 (title), H2 (major sections), H3 (subsections)
3. **Include practical examples** — Every feature should have working code samples
4. **Cross-link related content** — Reference other docs for comprehensive coverage

### Reference Documentation

- **Lint rules** follow pattern: Rule ID → Default Severity → Description
- **Commands** follow pattern: Command name → Description
- **Configuration tables** follow pattern: Key → Type → Default → Description

## Language-Specific Patterns

### BoxLang Syntax Conventions

- Use `js` syntax highlighting for BoxLang code blocks
- Function calls: `functionName( arg1, arg2 )`
- Structure access: `struct.key` or `struct[ "key" ]`
- **Semicolon Usage**:
  - **DO NOT use semicolons** in documentation code examples unless required for specific syntax
  - Semicolons are optional in BoxLang and should be omitted for cleaner, more readable examples
  - **Exceptions where semicolons ARE required**:
    - Property declarations in classes: `property name="fieldName" type="string";`
    - Specific termination contexts where ambiguity would occur
    - Multiple statements on a single line (avoid this pattern in docs)
  - Example: Use `result = calculate( x, y )` NOT `result = calculate( x, y );`
- **Closures vs Lambdas**:
  - Use **lambdas** (`->`) for deterministic functions that ONLY work with local variables or arguments passed to them
  - Use **closures** (`=>`) for functions that access variables from enclosing scope OR call external functions/BIFs
  - Example lambda: `array.map( ( item ) -> item * 2 )` (only uses the item argument)
  - Example closure: `array.filter( ( item ) => item > threshold )` (accesses threshold from outer scope)
  - Example closure: `() => loadUserFromDatabase( 123 )` (calls external function)

## GitBook Integration

### GitBook MCP Server

This project uses the GitBook Model Context Protocol (MCP) server for enhanced documentation capabilities. The MCP server provides access to GitBook's documentation and best practices.

**Reference:** [GitBook MCP Documentation](https://gitbook.com/docs/~gitbook/mcp)

Use the GitBook MCP to:

- Learn GitBook-specific syntax and features
- Understand code block formatting and options
- Access GitBook blocks and components documentation
- Follow GitBook best practices for content creation

### Styling Elements

- **Hint blocks** for callouts: `{% hint style="type" %}content{% endhint %}`
  - Available styles: `info`, `warning`, `danger`, `success`
  - Reference: [GitBook Hint Blocks](https://gitbook.com/docs/creating-content/blocks/hint)
- **Content references** for internal navigation
- **Embed blocks** for external resources
- **Table components** with GitBook-specific formatting
- **Code blocks** with syntax highlighting and optional features (line numbers, overflow handling)

### File Organization

- **README.md files** serve as section introductions
- **Reference materials** organized by functional categories
- **Progressive disclosure** — overview → details → examples → advanced patterns

## Contributing Guidelines

### Content Standards

- **Comprehensive examples** — Every feature needs working code samples
- **Cross-platform considerations** — Note OS-specific behaviors where relevant
- **Error handling patterns** — Include exception handling in examples
- **Performance considerations** — Document resource implications

### Documentation Maintenance

- **Version compatibility** — Note BoxLang version requirements
- **External link validation** — Ensure embedded content remains accessible
- **Code example testing** — Verify all code samples work with current BoxLang
- **Cross-reference accuracy** — Maintain valid internal links

This documentation serves as a user guide for the BoxLang IDE plugins, emphasizing practical usage patterns while maintaining comprehensive feature coverage.

## AI Skills

This repository ships AI skill packs that teach coding agents specialized BoxLang and Ortus domain knowledge. Skills are stored in `.agents/skills/` (the canonical location) and mirrored into `.claude/skills/` via symlinks.

**BLOCKING REQUIREMENT:** When a skill applies to the user's request, load the relevant `SKILL.md` file **immediately** as your first action — before generating any response or writing code. Use `read_file` to load it.

### Available Skills

| Skill | Path | When to use |
| --- | --- | --- |
| `boxlang-core-dev-async-tasks` | `.agents/skills/boxlang-core-dev-async-tasks/SKILL.md` | BoxFuture, AsyncService, executor types, BaseScheduler, ScheduledTask fluent API, scheduling with cron constraints, task lifecycle callbacks, registering schedulers via ModuleConfig.bx |
| `boxlang-core-dev-bif-development` | `.agents/skills/boxlang-core-dev-bif-development/SKILL.md` | Creating custom BoxLang BIFs: @BoxBIF annotation, invoke() method, argument handling, accessing BoxRuntime, member functions, registering BIFs via modules |
| `boxlang-core-dev-component-development` | `.agents/skills/boxlang-core-dev-component-development/SKILL.md` | Creating custom BoxLang components (tags): file structure, attribute declarations, body/output handling, registering component paths in modules, testing custom components |
| `boxlang-core-dev-interceptors` | `.agents/skills/boxlang-core-dev-interceptors/SKILL.md` | Creating BoxLang interceptors: Observer/Intercepting Filter patterns, interceptor pools, BoxLang class vs Java interceptors, lambda interceptors, registration via BIFs/InterceptorService/ModuleConfig |
| `boxlang-core-dev-logging` | `.agents/skills/boxlang-core-dev-logging/SKILL.md` | BoxLang logging: LoggingService, BoxLangLogger (trace/debug/info/warn/error), pre-configured common loggers, named loggers, parameterized messages, logging configuration in boxlang.json |
| `boxlang-core-dev-module-development` | `.agents/skills/boxlang-core-dev-module-development/SKILL.md` | Creating a BoxLang module: ModuleConfig.bx structure, lifecycle methods (configure/onLoad/onUnload), module metadata, registering interceptors and BIFs, Gradle build setup, publishing to ForgeBox |
| `boxlang-core-dev-runtime-architecture` | `.agents/skills/boxlang-core-dev-runtime-architecture/SKILL.md` | BoxLang internals: BoxRuntime services, IBoxContext hierarchy, scope chain resolution, DynamicObject, type system, parsing pipeline, class loader isolation, virtual threads, AST debugging |
| `code-documenter` | `.agents/skills/code-documenter/SKILL.md` | Producing or improving developer-facing documentation for codebases, APIs, modules, and architecture decisions. Invoke for inline comments, docstrings, API references, onboarding guides, runbooks, and consistency audits across documentation assets |
| `gitbook-docs-expert` | `.agents/skills/gitbook-docs-expert/SKILL.md` | Creating or editing GitBook documentation: frontmatter, hint blocks, content-ref, embed blocks, tabs, code blocks, tables, SUMMARY.md navigation, and GitBook-specific syntax for use in external editors |

### Adding New Skills

To add a new skill to this repository:

1. Create the skill folder and `SKILL.md` in `.agents/skills/<skill-name>/`.
2. Add a symlink in `.claude/skills/` pointing to the same folder:

   ```bash
   cd .claude/skills
   ln -s ../../.agents/skills/<skill-name> <skill-name>
   ```

3. Register the skill in the `Available Skills` table above.

## MCP Integrations

- This book is published at https://boxlang-ide.ortusbooks.com
- It has its own MCP server: https://boxlang-ide.ortusbooks.com/~gitbook/mcp

Here are other relevant MCP servers to integrate with:

- GitBook Docs: https://gitbook.com/docs/~gitbook/mcp
- BoxLang Language: https://boxlang.ortusbooks.com/~gitbook/mcp
- BoxLang AI: https://ai.ortusbooks.com/~gitbook/mcp
- ColdBox: https://coldbox.ortusbooks.com/~gitbook/mcp
- CommandBox: https://commandbox.ortusbooks.com/~gitbook/mcp
- TestBox: https://testbox.ortusbooks.com/~gitbook/mcp
- WireBox: https://wirebox.ortusbooks.com/~gitbook/mcp
- CacheBox: https://cachebox.ortusbooks.com/~gitbook/mcp
- LogBox: https://logbox.ortusbooks.com/~gitbook/mcp

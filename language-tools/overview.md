---
description: >-
  How BoxLang language tools power diagnostics, hints, formatting, and config
  support
icon: terminal
---

# Overview

BoxLang language tools are built around the BoxLang Language Server. It gives editors a shared set of smart features through the Language Server Protocol.

This keeps diagnostics, hints, and formatting consistent across supported IDEs.

### Core components

#### BoxLang LSP

The [BoxLang Language Server](https://github.com/ortus-boxlang/boxlang-lsp) is the main implementation. It parses BoxLang code, tracks project context, and returns language features to any compatible editor.

It powers:

* diagnostics for static analysis
* hints for symbols, definitions, and type information
* formatting and project-aware configuration support

#### LSP4J

[LSP4J](https://github.com/eclipse-lsp4j/lsp4j) provides the Java bindings for the Language Server Protocol. It handles the protocol message model between the editor and the BoxLang server.

That lets BoxLang focus on language behavior instead of protocol plumbing.

### Diagnostics

Diagnostics report problems directly in the editor. They help catch issues before runtime.

Current checks include:

* unused variables
* unscoped variables
* duplicate members

You can control rules, severity, and file scope in `.bxlint.json`. See [Linting](linting.md).

### Hints

Hints surface useful language information while you type. They reduce context switching and speed up navigation.

These tools include:

* code outlines
* function and definition lookup
* type hints and inline language information

### Formatting

Formatting keeps BoxLang source code consistent. It helps teams apply the same style across files and editors.

Formatting support runs through the same language tooling stack. That keeps editor behavior predictable.

### Configuration file schemas

Language tools also support project configuration files. This makes settings easier to discover and validate.

Important files include:

* `.bxlint.json` for diagnostics configuration
* `boxlang.json` for mappings, class paths, and modules
* `boxlang.lsp.*` workspace settings in the IDE

Schema support improves validation, autocomplete, and editor guidance.

### Editor support

Any editor with an LSP client can connect to the BoxLang language server. The most complete integration today is the [VSCode overview](../vscode/overview.md).

That gives BoxLang a shared foundation for editor tooling while keeping each client lightweight.

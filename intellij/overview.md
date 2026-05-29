---
description: >-
  Overview of the BoxLang IDE plugin for JetBrains IDEs — syntax highlighting,
  LSP integration, run configurations, debugging, and TestBox support.
icon: info
---

# Overview

The **BoxLang IDE** plugin brings comprehensive BoxLang language support to JetBrains IDEs. It is available from the [JetBrains Marketplace](https://plugins.jetbrains.com/plugin/30311-boxlang-ide).

The plugin is built to give JetBrains users the same core BoxLang editor experience available in other supported IDEs, powered by the same Language Server Protocol (LSP) engine.

---

## Features at a Glance

| Feature | Description |
| --- | --- |
| **Syntax Highlighting** | Full lexer-based highlighting for `.bx`, `.bxm`, `.bxs`, `.cfc`, and `.cfm` files with 16 customizable color attributes |
| **LSP Integration** | Semantic tokens, real-time diagnostics, document symbols, and completions via the BoxLang Language Server |
| **Run Configurations** | Execute BoxLang scripts directly with configurable arguments, working directory, and environment |
| **Debugger** | Full DAP-based debugging with breakpoints, stepping, variable inspection, watch expressions, and expression evaluation |
| **TestBox Integration** | Run and debug TestBox tests with gutter icons, test result tree, and suite/spec filtering |
| **Structure View** | Navigate code structure with document outline powered by LSP |
| **File Templates** | Create new BoxLang Class, Script, and Template files from the New menu |
| **Runtime Management** | Automatic BoxLang runtime download, version selection, and `.bvmrc` support |
| **Navigation** | Go to File, Class, and Symbol support with Search Everywhere integration |

---

## Supported File Types

| Extension | Type | Description |
| --- | --- | --- |
| `.bx` | Class | BoxLang class/component files |
| `.bxs` | Script | BoxLang script files |
| `.bxm` | Template | BoxLang markup template files |
| `.cfc` | Class | CFML component files (compatibility) |
| `.cfm` | Template | CFML template files (compatibility) |

---

## Requirements

- **IntelliJ IDEA** 2024.2 or later (Community or Ultimate)
- **Java 21** or later (for running BoxLang)

---

## Getting Started

1. Install the plugin from the JetBrains Marketplace
2. Open or create a BoxLang project
3. Configure BoxLang settings in **Settings → Languages & Frameworks → BoxLang**
4. Create new files via **New → BoxLang File**
5. Run scripts using gutter icons or run configurations

---

## Documentation

| Page | Description |
| --- | --- |
| [Installation](installation.md) | How to install the plugin from Marketplace or disk |
| [Settings Reference](settings-reference.md) | All application and project settings |
| [Run Configurations](run-configurations.md) | Running BoxLang scripts and attaching to processes |
| [Debugging](debugging.md) | Breakpoints, stepping, variable inspection, and expression evaluation |
| [TestBox Integration](testbox-integration.md) | Running and debugging TestBox tests |
| [LSP Features](lsp-features.md) | Diagnostics, semantic tokens, structure view, and completions |
| [File Templates](file-templates.md) | Creating new BoxLang files from templates |
| [Runtime Management](runtime-management.md) | Version management, `.bvmrc`, and automatic downloads |

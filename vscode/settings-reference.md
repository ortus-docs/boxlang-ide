---
description: >-
  Complete reference for all BoxLang VS Code extension settings — Java, LSP,
  debugger, updates, CFML features, dump panel, and mappings.
icon: sliders
---

# Settings Reference

The BoxLang VS Code extension provides over 40 configuration settings to control runtime behavior, language features, and editor integration.

All settings use the `boxlang.*` prefix and can be configured in VS Code's `settings.json` or through the Settings UI.

---

## Java Settings

Settings that control the Java runtime used by BoxLang.

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.java.javaHome` | `string` | — | machine | Path to a JDK 21+ installation. If not set, the extension uses the system `java` command. Use double backslashes on Windows (e.g. `C:\\\\Program Files\\\\Eclipse Adoptium\\\\jdk-21.0.2.13-hotspot`). |

{% hint style="warning" %}
BoxLang requires **JDK 21 or higher**. Older JDK versions will cause the extension to fail.
{% endhint %}

### Example

```json
{
  "boxlang.java.javaHome": "/usr/lib/jvm/temurin-21-jdk-amd64"
}
```

If Java 21 is not installed, run the **BoxLang: Download Java 21** command to automatically download and configure a compatible JRE.

---

## Runtime Settings

Settings that control which BoxLang runtime artifacts are used.

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.boxlangVersion` | `string` | `"1.13.0"` | resource | The BoxLang runtime version used for execution. Managed automatically when using version selection commands. |
| `boxlang.jarpath` | `string` | — | machine | Path to a custom BoxLang JAR. Overrides the version-managed JAR. |
| `boxlang.miniserverjarpath` | `string` | — | machine | Path to a custom MiniServer JAR. Overrides the version-managed JAR. |
| `boxlang.lspjarpath` | `string` | — | machine | Path to a custom LSP JAR. Overrides the version-managed JAR. |
| `boxlang.boxLangHome` | `string` | — | resource | Alternative location to use as BoxLang Home. The default location is `~/.boxlang`. |

---

## Language Server (LSP) Settings

Settings that control the BoxLang Language Server Protocol process.

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.lsp.lspVersion` | `string` | `"bx-lsp@1.10.0+9"` | resource | The LSP module version to use. |
| `boxlang.lsp.boxLangHome` | `string` | — | resource | Home directory override for the LSP runtime. |
| `boxlang.lsp.boxLangVersion` | `string` | — | resource | BoxLang runtime version used by the LSP. Set at your own risk — errors may occur if the LSP module doesn't match this version. |
| `boxlang.lsp.maxHeapSize` | `integer` | — | window | JVM maximum heap size in megabytes. Default is `512`. |
| `boxlang.lsp.jvmArgs` | `string` | — | machine | Additional JVM arguments passed to the LSP process. |
| `boxlang.lsp.enableExperimentalDiagnostics` | `boolean` | — | window | Enable experimental diagnostic reporting features. |
| `boxlang.lsp.enableBackgroundParsing` | `boolean` | `false` | window | When true, triggers a workspace-wide parse and index of all BoxLang files on startup. Improves symbol discovery at the cost of startup time. |
| `boxlang.lsp.processDiagnosticsInParallel` | `boolean` | `true` | window | When true, lint diagnostics for open documents are calculated in parallel threads. Disable if you experience threading issues. |
| `boxlang.lsp.modules` | `string` | `""` | resource | Comma-delimited list of BoxLang modules to install in the LSP home before booting. |
| `boxlang.lsp.sendLogToIDE` | `boolean` | `true` | window | Whether the LSP sends its logging output to the VS Code output channel. |
| `boxlang.lsp.logLevel` | `string` | `"WARN"` | window | The log level for the BoxLang Language Server. One of: `TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR`, `FATAL`, `OFF`. |
| `boxlang.lsp.versionUpdateMode` | `string` | `"auto"` | machine | Controls how the LSP checks for and applies version updates. One of: `auto`, `prompt`, `manual`. |
| `boxlang.mappings` | `object{}` | `{}` | resource | Workspace mapping overrides for the LSP. Keys are logical paths such as `/models` and values are path strings. These take precedence over project mappings in `boxlang.json`. |

### LSP Log Levels

| Level | Description |
| --- | --- |
| `TRACE` | Most verbose — all diagnostic detail |
| `DEBUG` | Debug-level information |
| `INFO` | General operational messages |
| `WARN` | Warning conditions (default) |
| `ERROR` | Error conditions only |
| `FATAL` | Fatal errors only |
| `OFF` | Disable LSP logging entirely |

### LSP Version Update Modes

| Mode | Behavior |
| --- | --- |
| `auto` | Automatically download the latest version |
| `prompt` | Check for updates and prompt before downloading |
| `manual` | Never check for updates automatically |

---

## Debugger Settings

Settings that control the BoxLang debugger behavior.

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.debugger.mode` | `string` | `"legacy"` | resource | Which debugger implementation to use. One of: `legacy`, `module`. |
| `boxlang.debugger.moduleName` | `string` | `"bx-debugger"` | resource | ForgeBox module slug for the module-based debugger. Used when `mode` is `module`. |
| `boxlang.debugger.moduleVersion` | `string` | `"1.0.0-snapshot"` | resource | Debugger module version when using module mode. |
| `boxlang.debugger.boxLangHome` | `string` | — | resource | Home directory override for the debugger module runtime. |
| `boxlang.debugger.versionUpdateMode` | `string` | `"auto"` | machine | Controls how the debugger checks for version updates. One of: `auto`, `prompt`, `manual`. |

### Debugger Modes

| Mode | Description |
| --- | --- |
| `legacy` | Use the built-in debugger from the BoxLang JAR. |
| `module` | Use a ForgeBox debugger module managed by version. |

---

## Update Settings

Settings that control automatic update behavior for BoxLang components.

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.updates.runtime` | `string` | `"prompt"` | machine | Update mode for the BoxLang runtime. One of: `auto`, `prompt`, `manual`. |
| `boxlang.updates.miniserver` | `string` | `"prompt"` | machine | Update mode for the MiniServer. One of: `auto`, `prompt`, `manual`. |
| `boxlang.updates.preRelease` | `boolean` | `false` | machine | When enabled, update checks include pre-release versions (snapshot, beta, alpha). |

### Update Modes

| Mode | Behavior |
| --- | --- |
| `auto` | Automatically download and apply updates |
| `prompt` | Check for updates and prompt before applying (default for runtime) |
| `manual` | Never check for updates automatically |

---

## MiniServer Settings

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.webPort` | `number` | — | window | The port to use for local development with the MiniServer. |

---

## Dump Panel Settings

Settings that control the variable dump panel behavior during debugging.

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.dump.panelMode` | `string` | `"replace"` | window | Controls how dump content is displayed. One of: `replace`, `newTab`. |
| `boxlang.dump.panelLocation` | `string` | `"beside"` | window | Controls which editor column the dump panel opens in. One of: `beside`, `active`, `one`, `two`, `three`. |

### Dump Panel Modes

| Mode | Description |
| --- | --- |
| `replace` | Each dump replaces the content of the existing dump panel (default). |
| `newTab` | Each dump opens in its own editor tab. |

### Dump Panel Locations

| Location | Description |
| --- | --- |
| `beside` | Open beside the currently active editor (default). |
| `active` | Open in the currently active editor column. |
| `one` | Open in editor column one. |
| `two` | Open in editor column two. |
| `three` | Open in editor column three. |

---

## CFML Feature Settings

Settings that control CFML-specific language features. These apply primarily to `.cfm`, `.cfc`, and `.cfml` files.

### Hover

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.cfml.hover.enable` | `boolean` | `true` | resource | Enable hover information for CFML entities. |
| `boxlang.cfml.hover.html.enable` | `boolean` | `true` | resource | Enable hover for HTML entities. |
| `boxlang.cfml.hover.css.enable` | `boolean` | `true` | resource | Enable hover for CSS entities. |

### Suggestions / Completions

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.cfml.suggest.enable` | `boolean` | `true` | resource | Enable completion help. |
| `boxlang.cfml.suggest.snippets.enable` | `boolean` | `true` | resource | Whether snippets are included in completions. |
| `boxlang.cfml.suggest.snippets.exclude` | `string[]` | `[]` | resource | Snippet keys to exclude from suggestions. |
| `boxlang.cfml.suggest.snippets.localPath` | `string` | — | machine-overridable | Custom path for user-defined snippets. |
| `boxlang.cfml.suggest.globalFunctions.enable` | `boolean` | `true` | resource | Whether global functions appear in completions. |
| `boxlang.cfml.suggest.globalFunctions.firstLetterCase` | `string` | `"default"` | resource | Case for the first letter of global function suggestions. One of: `unchanged`, `lower`, `upper`. |
| `boxlang.cfml.suggest.globalTags.enable` | `boolean` | `true` | resource | Whether global tags appear in completions. |
| `boxlang.cfml.suggest.globalTags.attributes.quoteType` | `string` | `"double"` | resource | Quote type for attribute value completion. One of: `none`, `double`, `single`. |
| `boxlang.cfml.suggest.globalTags.attributes.defaultValue` | `boolean` | `false` | resource | Whether to populate the default value for attributes. |
| `boxlang.cfml.suggest.globalTags.includeAttributes.setType` | `string` | `"none"` | resource | Which attributes to auto-include when a tag is selected. One of: `none`, `required`, `all`. |
| `boxlang.cfml.suggest.globalTags.includeAttributes.custom` | `object{}` | `{}` | resource | Custom set of attributes to include for specific tags. Overrides `setType`. |
| `boxlang.cfml.suggest.htmlTags.enable` | `boolean` | `true` | resource | Whether HTML tags appear in completions. |
| `boxlang.cfml.suggest.htmlTags.attributes.quoteType` | `string` | `"double"` | resource | Quote type for HTML attribute value completion. One of: `none`, `double`, `single`. |
| `boxlang.cfml.suggest.css.enable` | `boolean` | `true` | resource | Whether CSS properties and values appear in completions. |
| `boxlang.cfml.suggest.scopes.case` | `string` | `"lower"` | resource | Case for scope names in completions. One of: `lower`, `upper`. |
| `boxlang.cfml.suggest.replaceComments` | `boolean` | `true` | resource | Whether comments are replaced during parsing. |

### Definitions

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.cfml.definition.enable` | `boolean` | `true` | resource | Enable Go to Definition for CFML entities. |
| `boxlang.cfml.definition.userFunctions.search.enable` | `boolean` | `false` | resource | Whether to search the entire workspace for matching functions when a reliable match cannot be determined. |

### Signature Help

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.cfml.signature.enable` | `boolean` | `true` | resource | Enable function signature help. |

### Document Outline

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.cfml.outline.showImplicitFunctions` | `boolean` | `true` | resource | Whether to show implicit functions in the Outline view. |

### Component Indexing

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.cfml.indexComponents.enable` | `boolean` | `true` | window | Whether to index workspace components on startup. Required for most features. |

### Auto-Close Tags

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.cfml.autoCloseTags.enable` | `boolean` | `true` | window | Whether to enable auto-closing tags for CFML. Uses the `auto-close-tag` extension. Only checked on startup. |
| `boxlang.cfml.autoCloseTags.configurationTarget` | `string` | `"Global"` | window | Where to apply auto-close tag settings. One of: `Global`, `Workspace`. |

### DocBlock

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.cfml.docBlock.gap` | `boolean` | `true` | resource | Whether there should be a gap between the hint and other tags in a DocBlock. |
| `boxlang.cfml.docBlock.extra` | `object[]` | `[]` | resource | Extra tags to include in every DocBlock. Each entry has `name`, `default`, and `types` fields. |

### CFML Engine

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.cfml.engine.name` | `string` | — | window | Filter completions by CFML engine. One of: `coldfusion`, `lucee`, `railo`, `openbd`. |
| `boxlang.cfml.engine.version` | `string` | — | window | Filter completions by CFML engine version. SemVer format is preferred. |

### Global Definitions

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.cfml.globalDefinitions.source` | `string` | `"cfdocs"` | window | Source of global definitions for CFML entities. |

### CFDocs

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.cfml.cfDocs.source` | `string` | `"extension"` | window | Source location for CFDocs. One of: `remote` (GitHub), `local`, `extension` (built-in). |
| `boxlang.cfml.cfDocs.localPath` | `string` | — | machine-overridable | Physical path to the CFDocs `data/language` directory (used when source is `local`). |

---

## Mappings (Deprecated)

{% hint style="warning" %}
`boxlang.cfml.mappings` is **deprecated**. Use `boxlang.mappings` instead. Legacy mappings are automatically migrated.
{% endhint %}

---

## Lexer & Parser Settings

Settings for ANTLR-based AST visualization tools (advanced use).

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.showLexerTokens` | `boolean` | `false` | window | Controls whether to show lexer processing output. |
| `boxlang.lexerPath` | `string` | — | machine | Path to the ANTLR lexer file for AST visualizations. |
| `boxlang.parserPath` | `string` | — | machine | Path to the ANTLR parser file for AST visualizations. |
| `boxlang.customAntlrToolsCommand` | `string` | — | window | Custom command to execute when generating an ANTLR graph. |

---

## Settings Migration

| Setting | Type | Default | Scope | Description |
| --- | --- | --- | --- | --- |
| `boxlang.settings.ignoreOldSettings` | `boolean` | `false` | application | Suppress prompts to migrate legacy settings. Set automatically after migration. Run **BoxLang: Migrate VSCode Settings** to migrate manually. |

---

## Live-Reload vs Restart

Some settings take effect immediately, while others require a restart:

| Change | Effect |
| --- | --- |
| Java, LSP, BoxLang Home changes | Restarts all processes automatically |
| Lint configuration changes | Detected live — no reload needed |
| CFML feature settings | Applied on next file open or cache refresh |
| Format-on-save settings | Immediate |
| Most `boxlang.lsp.*` changes | Restarts the LSP process |

---

## Related Pages

{% content-ref url="debugging.md" %}
{% endcontent-ref %}

{% content-ref url="version-management.md" %}
{% endcontent-ref %}

{% content-ref url="project-configuration.md" %}
{% endcontent-ref %}

{% content-ref url="../language-tools/linting.md" %}
{% endcontent-ref %}

{% content-ref url="../language-tools/formatting.md" %}
{% endcontent-ref %}

---
icon: prescription
description: >-
  Static analysis with .bxlint.json — rule configuration, severity levels,
  file filtering, in-file suppression, quick fixes, and a complete JSON
  reference.
---

# Linting

BoxLang linting (static analysis) is powered by the **BoxLang Language Server Protocol** (bx-lsp). It scans your source files in real time, surfaces diagnostics in the editor, and offers automated quick fixes where applicable.

**Config file:** `.bxlint.json`

Place `.bxlint.json` at the workspace root to control static analysis. Changes are detected live — you never need to reload the editor or restart the language server.

{% hint style="info" %}
The **VS Code** and **JetBrains** plugins both ship the same LSP engine, so the lint rules and configuration format are identical across IDEs.
{% endhint %}

---

## Configuration Reference

### Top-level keys

| Key           | Type       | Default | Description                                                                                                                                                    |
| ------------- | ---------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `diagnostics` | `object{}` | `{}`    | Per‑rule configuration map. Each key is a rule ID; each value is an object with optional `enabled`, `severity`, and `params` fields.                           |
| `include`     | `string[]` | `[]`    | Workspace‑relative glob patterns. When non‑empty, **only** matching files are analyzed.                                                                        |
| `exclude`     | `string[]` | `[]`    | Workspace‑relative glob patterns. Files matching any exclude pattern are **never** analyzed, even if they match an include pattern. Evaluated after `include`. |
| `mappings`    | `object{}` | `{}`    | Virtual‑path‑to‑filesystem‑path map used by the LSP for symbol resolution during analysis. Paths resolve relative to the workspace root.                       |
| `formatting`  | `object{}` | `{}`    | Workspace‑shared formatting configuration. Houses the `experimental.enabled` toggle for the BoxLang formatter.                                                 |

### Glob syntax

Glob patterns support three wildcards:

| Token | Meaning                                                               |
| ----- | --------------------------------------------------------------------- |
| `*`   | Matches any characters except `/` within a single path segment.       |
| `**`  | Matches any characters, including `/`, across multiple path segments. |
| `?`   | Matches any single character except `/`.                              |

Always use forward slashes (`/`) regardless of operating system.

## Full JSON Example

Below is a complete `.bxlint.json` file showing every available key and every lint rule with its default severity:

```json
{
  "diagnostics": {
    "duplicateMethod": {
      "enabled": true,
      "severity": "error"
    },
    "duplicateProperty": {
      "enabled": true,
      "severity": "error"
    },
    "emptyCatchBlock": {
      "enabled": true,
      "severity": "warning"
    },
    "invalidExtends": {
      "enabled": true,
      "severity": "error"
    },
    "invalidImplements": {
      "enabled": true,
      "severity": "error"
    },
    "missingQueryParamCfsqltype": {
      "enabled": true,
      "severity": "warning"
    },
    "missingReturnStatement": {
      "enabled": true,
      "severity": "warning"
    },
    "shadowedVariable": {
      "enabled": true,
      "severity": "warning"
    },
    "unescapedQueryParam": {
      "enabled": true,
      "severity": "warning"
    },
    "unreachableCode": {
      "enabled": true,
      "severity": "warning"
    },
    "unscopedVariable": {
      "enabled": true,
      "severity": "warning"
    },
    "unusedImport": {
      "enabled": true,
      "severity": "warning"
    },
    "unusedPrivateMethod": {
      "enabled": true,
      "severity": "warning"
    },
    "unusedVariable": {
      "enabled": true,
      "severity": "hint"
    }
  },
  "include": [],
  "exclude": [],
  "mappings": {},
  "formatting": {
    "experimental": {
      "enabled": false
    }
  }
}
```

{% hint style="tip" %}
Run the **`boxlang.createBxlintConfig`** command in your editor to generate a fresh `.bxlint.json` with all rules and defaults automatically. In VS Code, open the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`) and type "Create .bxlint.json".
{% endhint %}

---

## Lint Rules

The LSP ships with **14** diagnostic rules, each identified by a stable rule ID. The default severity reflects how severe the issue typically is.

| Rule ID                      | Default Severity | Description                                                                                                       |
| ---------------------------- | ---------------- | ----------------------------------------------------------------------------------------------------------------- |
| `duplicateMethod`            | error            | Flags multiple method definitions with the same name within the same class.                                       |
| `duplicateProperty`          | error            | Flags multiple property definitions with the same name within the same class.                                     |
| `invalidExtends`             | error            | Flags `extends` references to classes or interfaces that cannot be resolved.                                      |
| `invalidImplements`          | error            | Flags `implements` references to interfaces that cannot be resolved.                                              |
| `emptyCatchBlock`            | warning          | Flags `catch` blocks that contain no executable code, which silently swallows exceptions.                         |
| `missingQueryParamCfsqltype` | warning          | Flags `<cfqueryparam>` tags that are missing a `cfsqltype` attribute.                                             |
| `missingReturnStatement`     | warning          | Flags functions with a non‑void return type that lack a `return` statement in all code paths.                     |
| `shadowedVariable`           | warning          | Flags local variables that share the same name as a function parameter, shadowing it.                             |
| `unescapedQueryParam`        | warning          | Flags query string interpolations (`#var#`) that should be wrapped in `<cfqueryparam>`.                           |
| `unreachableCode`            | warning          | Flags code appearing after control‑flow statements like `return`, `throw`, or `break` that can never be executed. |
| `unscopedVariable`           | warning          | Flags variables used without an explicit scope prefix (e.g., `foo` instead of `variables.foo`).                   |
| `unusedImport`               | warning          | Flags `import` statements for classes or packages that are never referenced in the file.                          |
| `unusedPrivateMethod`        | warning          | Flags `private` methods that are never called within the class, indicating dead code.                             |
| `unusedVariable`             | hint             | Flags local variables that are declared but never used in the code.                                               |

---

## Rule Settings

Every rule supports the following fields in `.bxlint.json` under the `diagnostics` key:

- **`enabled`** (boolean) — Set to `false` to disable the rule entirely. Defaults to `true`.
- **`severity`** (string) — Override the default severity. Accepted values:
  - `"error"` — Red squiggle; treated as a compilation error.
  - `"warning"` — Yellow squiggle; potential problem that should be addressed.
  - `"information"` or `"info"` — Blue squiggle; informational note.
  - `"hint"` — Grey hint; subtle suggestion with minimal visual noise.
- **`params`** (object) — Rule‑specific parameters (reserved for future use; currently unused by any rule).

### Example: tuning specific rules

```json
{
  "diagnostics": {
    "unusedVariable": {
      "enabled": false
    },
    "unscopedVariable": {
      "severity": "error"
    },
    "missingQueryParamCfsqltype": {
      "severity": "information"
    }
  }
}
```

---

## File Filtering

Use `include` and `exclude` to narrow analysis to subsets of your workspace.

### Include-only example

Analyze only files under `src/` and `models/`:

```json
{
  "include": ["src/**", "models/**"]
}
```

### Include + exclude example

Analyze everything under `src/` except generated files:

```json
{
  "include": ["src/**"],
  "exclude": ["src/generated/**", "**/*.gen.bx"]
}
```

**Rules:**

- When `include` is empty, **all** files are analyzed by default.
- When `include` is non‑empty, a file must match at least one include pattern.
- A file matching **any** exclude pattern is skipped, regardless of include matches.
- Exclude is evaluated **after** include.

---

## In‑File Suppression

You can suppress diagnostics directly in source code using special comments. Suppression comments apply to a **scope** (block, function, or class) and target one or more rule IDs.

### Block‑level suppression

Disable one or more rules for a section of code, then re‑enable them:

```js
// bxlint-disable unusedVariable
var temp = calculateSomething()
// bxlint-enable unusedVariable
```

To suppress **all** rules in a block:

```js
// bxlint:disable
suppressedVar = doWork()
anotherIgnored = doMoreWork()
// bxlint:enable
```

### Function‑level suppression

Suppress rules for the **next function only**:

```js
// bxlint-disable-for-function unusedVariable
function legacyHelper( arg ) {
    result = transform( arg )
    return result
}
```

Re‑enable a rule for the next function inside an already‑disabled section:

```js
// bxlint-disable unusedVariable

// bxlint-enable-for-function unusedVariable
function newCode( arg ) {
    result = transform( arg )
    return result
}
```

### Class‑level suppression

Suppress rules for the **next class only**:

```js
// bxlint-disable-for-class unusedVariable
class LegacyService {
    function doThing() {
        temp = calculate()
    }
}
```

Re‑enable for the next class:

```js
// bxlint-disable unusedVariable

// bxlint-enable-for-class unusedVariable
class ModernService {
    function doThing() {
        temp = calculate()
    }
}
```

### CFML comment syntax

In `.cfm` and `.cfc` files, use CFML comment syntax instead:

```cfm
<!--- bxlint-disable missingQueryParamCfsqltype --->
<cfquery>
    <cfqueryparam value="#paramRef#">
</cfquery>
```

### Safe marker for unescaped query params

If you have a string interpolation inside a `<cfquery>` that you **know** is safe, mark it with `/*safe*/`:

```js
<cfquery>
    SELECT * FROM items
    WHERE code = '#/*safe*/paramRef#'
</cfquery>
```

This suppresses the `unescapedQueryParam` diagnostic for that specific interpolation.

---

## Mappings (LSP Resolution)

The `mappings` key in `.bxlint.json` tells the language server where to find source code for virtual path prefixes. This helps the LSP resolve symbols during analysis, which in turn produces more accurate diagnostics.

```json
{
  "mappings": {
    "/models": "src/models",
    "/handlers": "src/handlers"
  }
}
```

{% hint style="info" %}
Mappings in `.bxlint.json` serve the same purpose as the `mappings` key in `boxlang.json`, but they are scoped to the LSP analysis context and do not affect runtime behavior.
{% endhint %}

When the LSP resolves classes for diagnostics such as `invalidExtends`, it merges mapping sources in this order:

1. ColdBox implicit module mappings
2. `boxlang.json`
3. `.bxlint.json`
4. The nearest `Application.bx` or `Application.cfc`
5. VS Code `boxlang.mappings` overrides

Saving `.bxlint.json`, `boxlang.json`, `Application.bx`, or `Application.cfc` causes the language server to recompute mapping-dependent diagnostics for open documents. You do not need to restart the editor to clear a now-valid `extends` reference.

---

## Quick Fixes (Code Actions)

For certain rules, the LSP offers **quick fixes** — automated refactorings you can apply with a single click.

### Invalid extends (`invalidExtends`)

When an `extends` reference cannot be resolved but the workspace contains a likely filesystem match, the LSP downgrades the diagnostic to a warning and offers mapping quick fixes.

- **Add mapping to `Application.bx` / `Application.cfc`** — Inserts a static `this.mappings[ "key" ] = "path"` entry into the nearest application config file.
- **Add mapping to `boxlang.json`** — Creates or updates the project `mappings` block.
- **Add mapping to `.bxlint.json`** — Creates or updates lint-only mappings used during analysis.

Suggestions are ordered by the longest suffix match. For example, `models.machines.Vehicle` prefers a class found at `src/models/machines/Vehicle.bx` over a shorter partial match elsewhere in the workspace.

### Unescaped query params (`unescapedQueryParam`)

When a string interpolation like `'#paramRef#'` is detected inside a `<cfquery>`, the LSP provides:

- **Wrap in `<cfqueryparam>`** — Converts `'#paramRef#'` into `<cfqueryparam value="#paramRef#">`.
- **Refactor all unescaped query params** — Applies the same fix to every occurrence in the file.
- **Refactor similar as: `cf_sql_varchar`** — Wraps the param and adds a specific `cfsqltype`.
- **Mark as safe** — Inserts `/*safe*/` to suppress the diagnostic.

### Missing `cfsqltype` (`missingQueryParamCfsqltype`)

When a `<cfqueryparam>` tag lacks a `cfsqltype` attribute, the LSP offers:

- **Refactor similar as: `cf_sql_varchar`** — Adds `cfsqltype="cf_sql_varchar"` (and variations for all SQL types).

{% hint style="success" %}
Use `Ctrl+.` (Windows/Linux) or `Cmd+.` (macOS) on a highlighted diagnostic to open the Quick Fix menu.
{% endhint %}

---

## Experimental Formatting Toggle

The `formatting` key in `.bxlint.json` enables the experimental BoxLang formatter for the workspace:

```json
{
  "formatting": {
    "experimental": {
      "enabled": true
    }
  }
}
```

Formatting requires **BoxLang 1.13.0+** and **bx‑lsp 1.10.0+**. See the [Formatting](formatting.md) page for details.

---

## Project Mappings (`boxlang.json`)

In addition to `.bxlint.json`, the LSP also reads `boxlang.json` at the workspace root to resolve classpaths and virtual path mappings for type resolution during analysis.

| Key                | Type       | Default               | Description                                                                                                                         |
| ------------------ | ---------- | --------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `mappings`         | `object{}` | `{}`                  | Virtual path prefix to filesystem path map. Supports `${user-dir}`, `${boxlang-home}`, and `${env.VAR:default}` variable expansion. |
| `classPaths`       | `string[]` | `[]`                  | Directories to include in the classpath for type resolution. Paths may be absolute or relative to the `boxlang.json` file.          |
| `modulesDirectory` | `string[]` | `["boxlang_modules"]` | Directories containing BoxLang modules. Defaults to `boxlang_modules/` relative to `boxlang.json`.                                  |

{% hint style="warning" %}
`boxlang.json` supports `//` line comments for inline documentation.
{% endhint %}

---

## Related Pages

- [Language Tools Overview](overview.md) — Full language tooling stack.
- [Formatting](formatting.md) — Enabling and configuring the BoxLang formatter.
- [BoxLang LSP Repository](https://github.com/ortus-solutions/boxlang-lsp) — LSP source code and issue tracker.

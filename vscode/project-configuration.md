---
description: >-
  How to configure BoxLang projects — boxlang.json structure, mappings,
  classpaths, modules, variable expansion, and VS Code integration.
icon: file-code
---

# Project Configuration

The BoxLang extension reads project configuration from `boxlang.json` files placed at the workspace root (or any ancestor directory). This file defines virtual path mappings, classpaths, module directories, and more.

{% hint style="info" %}
`boxlang.json` supports `//` and `/* */` comments for documentation within the file.
{% endhint %}

---

## Quick Start

Create a `boxlang.json` at your workspace root:

```json
{
  "mappings": {
    "/models": "models",
    "/views": "views"
  },
  "modulesDirectory": [
    "boxlang_modules"
  ]
}
```

This tells the LSP that the logical path `/models` maps to the `models/` directory in your workspace.

---

## Configuration Reference

### Top-Level Keys

| Key | Type | Default | Description |
| --- | --- | --- | --- |
| `mappings` | `object{}` | `{"/": "${user-dir}"}` | Virtual path prefix to filesystem path mappings. The key is the logical prefix (must start with `/`) and the value is a relative or absolute directory path. |
| `classPaths` | `string[]` | `[]` | Additional directories to include in the classpath for type resolution. Paths may be absolute or relative to `boxlang.json`. |
| `modulesDirectory` | `string[]` | `["boxlang_modules"]` | Directories containing BoxLang modules. Defaults to `boxlang_modules/` relative to `boxlang.json`. Paths may be absolute or relative. |

### Mappings

Mappings are the core of project configuration. They tell the LSP how to resolve logical module paths (like `/models`, `/coldbox`) to actual filesystem locations.

```json
{
  "mappings": {
    "/": "src",
    "/models": "src/models",
    "/views": "src/views",
    "/coldbox": "/absolute/path/to/coldbox"
  }
}
```

**Rules:**

- Keys must start with `/`
- Values can be relative (to `boxlang.json`) or absolute
- The `/` mapping defines the root of your application

### ClassPaths

Use `classPaths` to include additional directories for Java class resolution:

```json
{
  "classPaths": [
    "lib",
    "/usr/local/share/java-libs"
  ]
}
```

### Modules Directory

BoxLang modules are located in standardized directories:

```json
{
  "modulesDirectory": [
    "boxlang_modules",
    "/opt/boxlang/shared-modules"
  ]
}
```

The default `boxlang_modules/` directory is relative to your `boxlang.json` file.

---

## Variable Expansion

Paths support variable expansion using the `${variable}` syntax:

| Variable | Expands to |
| --- | --- |
| `${boxlang-home}` | The active BoxLang Home directory (default: `~/.boxlang`) |
| `${user-dir}` | The user's home directory |
| `${env.VAR}` | The value of the environment variable `VAR` |
| `${env.VAR:default}` | The value of `VAR`, or `default` if not set |

### Example

```json
{
  "mappings": {
    "/coldbox": "${boxlang-home}/modules/coldbox",
    "/models": "${env.APP_MODELS:src/models}"
  }
}
```

---

## VS Code Integration

### boxlang.json Schema Validation

The extension provides JSON schema validation for `boxlang.json` files. This gives you:

- **Autocomplete** for top-level keys
- **Validation** of value types
- **Hover documentation** for each setting
- **Error highlighting** for invalid values

The schema matches any file named `boxlang.json` (e.g., `boxlang.json`, `my-boxlang.json`).

### Workspace Mappings Override

The VS Code setting `boxlang.mappings` allows you to override project mappings directly in your editor settings:

```json
{
  "boxlang.mappings": {
    "/models": "/absolute/path/to/models",
    "/custom": "./relative/path"
  }
}
```

{% hint style="warning" %}
`boxlang.mappings` takes **precedence** over `boxlang.json` mappings. Use it for personal overrides that shouldn't be committed to the project.
{% endhint %}

---

## Complete Example

A comprehensive `boxlang.json` for a ColdBox application:

```json
{
  "mappings": {
    "/": "src",
    "/coldbox": "${boxlang-home}/modules/coldbox",
    "/testbox": "${boxlang-home}/modules/testbox"
  },
  "classPaths": [
    "lib",
    "lib/java"
  ],
  "modulesDirectory": [
    "boxlang_modules",
    "${boxlang-home}/modules"
  ]
}
```

---

## Relationship to Other Config Files

| File | Purpose |
| --- | --- |
| `boxlang.json` | Project structure — mappings, classpaths, modules |
| `.bxlint.json` | Static analysis rules and file filters |
| `.bxformat.json` | Code formatting rules |
| VS Code `settings.json` | Editor-level overrides and IDE preferences |

{% hint style="tip" %}
`.bxlint.json` can also define `mappings` used specifically for lint analysis. These are separate from `boxlang.json` mappings and serve different purposes — see [Linting](../language-tools/linting.md) for details.
{% endhint %}

---

## Related Pages

{% content-ref url="settings-reference.md" %}
{% endcontent-ref %}

{% content-ref url="version-management.md" %}
{% endcontent-ref %}

{% content-ref url="../language-tools/linting.md" %}
{% endcontent-ref %}

{% content-ref url="../language-tools/formatting.md" %}
{% endcontent-ref %}

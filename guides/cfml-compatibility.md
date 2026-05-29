---
description: >-
  Using CFML files with the BoxLang extension — .cfm/.cfc/.cfml support,
  engine filtering, CFDocs integration, auto-close tags, and DocBlock.
icon: code-merge
---

# CFML Compatibility

The BoxLang extension provides first-class support for **CFML** (ColdFusion Markup Language) files along with native BoxLang files. This guide covers the CFML-specific features and how they differ from BoxLang support.

---

## Supported File Types

The extension recognizes two language IDs:

| Language ID | Extensions | Description |
| --- | --- | --- |
| `boxlang` | `.bx`, `.bxs`, `.bxm`, `.cfs` | Native BoxLang files |
| `cfml` | `.cfml`, `.cfm`, `.cfc` | Legacy CFML files |

Both language IDs receive syntax highlighting, diagnostics, completions, and hover information.

{% hint style="info" %}
CFML files use the same LSP engine as BoxLang files. Most language features work identically across both.
{% endhint %}

---

## CFML-Specific Features

### Engine Filtering

Filter completions and documentation to match a specific CFML engine:

```json
{
  "boxlang.cfml.engine.name": "coldfusion",
  "boxlang.cfml.engine.version": "2023"
}
```

| Setting | Values |
| --- | --- |
| `boxlang.cfml.engine.name` | `coldfusion`, `lucee`, `railo`, `openbd` |
| `boxlang.cfml.engine.version` | SemVer format (e.g., `2023`, `6.0`, `5.3.9`) |

When an engine is specified, completions only show functions and tags available in that engine version.

### CFDocs Integration

The extension integrates with **CFDocs** for online documentation lookup:

- **Hover** over a CFML function or tag to see its CFDocs documentation
- **BoxLang: Open CFDocs Page** — Open the CFDocs reference for the word under cursor
- **BoxLang: Open Engine Docs** — Open engine-specific documentation

Configure CFDocs behavior:

```json
{
  "boxlang.cfml.cfDocs.source": "extension"
}
```

| Source | Description |
| --- | --- |
| `extension` | Use built-in documentation (default, works offline) |
| `remote` | Fetch documentation from GitHub (always up-to-date) |
| `local` | Use a local copy (configure `boxlang.cfml.cfDocs.localPath`) |

### Global Definitions

Global CFML function and tag definitions are sourced from CFDocs:

```json
{
  "boxlang.cfml.globalDefinitions.source": "cfdocs"
}
```

---

## Editor Features for CFML

### Auto-Close Tags

The extension integrates with the popular **Auto Close Tag** extension (`formulahendry.auto-close-tag`) to automatically close CFML tags:

```json
{
  "boxlang.cfml.autoCloseTags.enable": true
}
```

When enabled, typing `</` after a CFML tag automatically inserts the matching closing tag. Configure where the settings are applied:

```json
{
  "boxlang.cfml.autoCloseTags.configurationTarget": "Global"
}
```

### Go to Matching Tag

Use **BoxLang: Go to Matching Tag** to jump between opening and closing CFML tags. This works for both CFML tags (`<cfoutput>...</cfoutput>`) and BoxLang template tags (`<bx:output>...</bx:output>`).

### Fold All Functions

Use **BoxLang: Fold All Functions** to collapse all function bodies in the current CFML file, making it easier to navigate large files.

### Open Application File

Use **BoxLang: Open Application File** to quickly open the `Application.cfc` or `Application.cfm` for the currently active document, based on the file's directory hierarchy.

---

## DocBlock Support

The extension provides DocBlock comment completion for CFML components and functions. Type `/**` above a function or component declaration and press Enter to generate a documentation block.

### Customizing DocBlocks

```json
{
  "boxlang.cfml.docBlock.gap": true,
  "boxlang.cfml.docBlock.extra": [
    {
      "name": "@author",
      "default": "Your Name",
      "types": ["component", "function"]
    }
  ]
}
```

| Setting | Description |
| --- | --- |
| `boxlang.cfml.docBlock.gap` | Add a blank line between the hint and other DocBlock tags |
| `boxlang.cfml.docBlock.extra` | Custom tags to include in every DocBlock |

---

## Differences from Native BoxLang

| Feature | BoxLang (`.bx`) | CFML (`.cfc`) |
| --- | --- | --- |
| File extensions | `.bx`, `.bxs`, `.bxm`, `.cfs` | `.cfc`, `.cfm`, `.cfml` |
| Template syntax | `<bx:component>` | `<cfcomponent>` |
| Language features | Full BoxLang syntax | CFML syntax (bx-compat-cfml compatibility) |
| Engine filtering | N/A | Available |
| CFDocs lookup | BoxLang docs | CFDocs |

---

## Migration Path

If you're migrating from CFML to BoxLang:

1. Install the **bx-compat-cfml** module for backward compatibility
2. Rename `.cfc` → `.bx`, `.cfm` → `.bxm`
3. Optionally convert `<cf*>` tags to `<bx:*>` equivalents
4. Use the [Feature Audit Tool](../vscode/feature-audit.md) to identify CFML-specific patterns

---

## Related Pages

{% content-ref url="../vscode/settings-reference.md" %}
{% endcontent-ref %}

{% content-ref url="../vscode/commands-reference.md" %}
{% endcontent-ref %}

{% content-ref url="../vscode/feature-audit.md" %}
{% endcontent-ref %}

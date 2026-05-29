---
description: >-
  How to use the BoxLang Feature Audit Tool — analyze BoxLang feature usage
  across your workspace for migration planning and code modernization.
icon: magnifying-glass-chart
---

# Feature Audit Tool

The **Feature Audit Tool** is a webview-based analysis tool that scans your entire workspace and catalogs all BoxLang language features in use. It helps you understand your codebase at a glance — ideal for migration planning, code modernization, and team onboarding.

---

## Opening the Tool

**From the Command Palette:**
1. Open the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`).
2. Type **BoxLang: Open Feature Audit Tool**.
3. Press Enter.

**From the Explorer:**
1. Right-click any folder in the Explorer sidebar.
2. Select **BoxLang: Open Feature Audit Tool**.

---

## What It Analyzes

The Feature Audit scans all BoxLang and CFML files in your workspace and reports on:

| Category | Examples |
| --- | --- |
| **Language constructs** | Classes, interfaces, components, functions, properties |
| **Built-in Functions (BIFs)** | `queryExecute`, `arrayMap`, `fileRead`, `structKeyExists` |
| **Tags / Components** | `<bx:query>`, `<bx:loop>`, `<bx:output>`, `<bx:include>` |
| **Scopes** | `variables`, `application`, `session`, `request`, `server` |
| **Control flow** | `if/else`, `for`, `while`, `switch`, `try/catch` |
| **Imports** | Java imports, BoxLang imports |
| **Annotations** | `@BoxBIF`, `@BoxComponent`, property annotations |
| **CFML-specific** | `<cfquery>`, `<cfoutput>`, `<cfloop>`, `<cfinclude>` |

---

## Use Cases

### Migration Planning

Before migrating from Adobe ColdFusion or Lucee to BoxLang, use the Feature Audit to:

- Identify CFML-specific tags and functions that need conversion
- Find deprecated language features
- Estimate migration effort based on feature usage counts

### Code Modernization

After migration or during refactoring:

- Identify legacy patterns (e.g., `<cfquery>` instead of `queryExecute()`)
- Find areas where modern BoxLang features could replace older approaches
- Track modernization progress over time

### Team Onboarding

For new team members:

- Get a quick overview of the codebase's technical profile
- Understand which language features are most heavily used
- Identify areas to focus learning efforts

### Compliance & Standards

For enforcing coding standards:

- Detect use of discouraged features
- Verify that deprecated APIs are no longer in use
- Audit codebase for security-sensitive patterns

---

## Interpreting Results

The audit results are displayed in an interactive webview panel. Results are grouped by feature category with counts for each item found.

{% hint style="tip" %}
Run the audit periodically during migration or refactoring projects to track progress. Compare results before and after to measure impact.
{% endhint %}

---

## Related Pages

{% content-ref url="commands-reference.md" %}
{% endcontent-ref %}

{% content-ref url="settings-reference.md" %}
{% endcontent-ref %}

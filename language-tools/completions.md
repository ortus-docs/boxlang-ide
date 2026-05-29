---
description: >-
  All BoxLang LSP completion types — BIFs, components, member access, variables,
  functions, imports, keywords, snippets, and BXM tag attributes.
icon: list-check
---

# Completions

The BoxLang Language Server provides rich, context-aware code completions that help you write code faster and with fewer errors. Completions are triggered automatically as you type or manually with `Ctrl+Space`.

{% hint style="info" %}
All completions are powered by the same LSP engine across **VS Code**, **JetBrains**, and any LSP-compatible editor.
{% endhint %}

---

## Completion Types

The LSP provides the following categories of completions, each triggered by specific contexts in your code:

### Built-In Functions (BIFs)

All BoxLang built-in functions are available as completions. They include:

- Function name, signature, and parameter information
- Documentation from the BoxLang runtime
- Return type information where available

**Triggered:** At the start of an expression, after a scope prefix, or when typing a function name.

```js
arr // → arrayAppend, arrayMap, arrayFilter, arrayReduce...
str // → structAppend, structKeyExists, structFind...
```

### Components & Tags (BXM)

Template components (formerly CFML tags) are completed when working in `.bxm` template files:

- **Tag name completion** — Typing `<bx:` shows all available BXM tags
- **Rich documentation** — Each tag shows its type (requires body, allows body, self-closing), all attributes with required/optional status, and default values
- **Attribute name completion** — After a tag name, attributes are suggested
- **Attribute value completion** — Inside attribute values, enum values are suggested

**Triggered:** Inside `.bxm` template files when typing `<bx:` followed by a tag name, or within a tag's attributes.

```xml
<bx:     <!-- → <bx:query, <bx:loop, <bx:output, <bx:include... -->
<bx:query     <!-- → name, datasource, sql, params, ... -->
```

### Member Access

After typing `.` on an object, the LSP attempts to infer the object's type and provide relevant member completions:

- **Properties** of known components/classes
- **Methods** with parameter signatures
- **Built-in member functions** for arrays, structs, strings, queries, etc.

**Triggered:** After `.` on a variable or expression.

```js
myQuery.     // → addColumn, addRow, each, execute, filter...
myArray.     // → map, filter, reduce, each, append, find...
myStruct.    // → keyExists, append, clear, count, find...
```

### Variables

Local and scoped variables are suggested based on the current context:

- **Local variables** declared with `var` or `local.` prefix
- **Argument variables** from function parameters
- **Scope variables** from recognized scopes (`variables.`, `application.`, `session.`, etc.)
- **Loop variables** from enclosing `for` or `each` loops

**Triggered:** When typing a variable name or after a scope prefix.

### Functions

User-defined functions and methods are completed with their signatures:

- **Local functions** defined in the current file
- **Component methods** from `this` or known component references
- **Imported functions** from other modules

**Triggered:** When typing a function call.

### Classes & Types

BoxLang class names and Java class names are available for `new` expressions and type annotations:

- **BoxLang classes** from your project and installed modules
- **Java classes** from the classpath
- **Interfaces** for `implements` declarations

**Triggered:** After `new`, `extends`, `implements`, or in type annotations.

### Imports

Available import paths for BoxLang and Java classes:

- **BoxLang imports** using the BoxLang module path convention
- **Java imports** for classes on the classpath
- Automatic filtering based on already-imported packages

**Triggered:** After an `import` statement.

### Keywords

BoxLang language keywords are completed with descriptions:

- Control flow: `if`, `else`, `for`, `while`, `switch`, `try`, `catch`, `finally`
- Declarations: `class`, `interface`, `function`, `property`, `var`
- Modifiers: `public`, `private`, `package`, `final`, `abstract`, `static`
- Other: `return`, `throw`, `new`, `import`, `include`

**Triggered:** At the start of a statement or declaration.

### Snippets

Pre-built code snippets accelerate common patterns:

- Class declarations
- Function declarations with DocBlock
- Try/catch blocks
- For/each loops
- Query execution patterns
- Component (tag) declarations

**Triggered:** At the start of a line or after specific keywords.

### Properties

When inside a component/class body, property declarations are suggested with type information and annotations.

**Triggered:** Inside a class body.

### Arguments

When inside a function/method body, argument names are suggested.

**Triggered:** When referencing function parameters.

---

## Context Awareness

The LSP analyzes your code context to provide only relevant completions:

| Context | Completions Provided |
| --- | --- |
| **Script** (`.bxs`, `.bx`) | BIFs, variables, functions, keywords, imports, snippets |
| **Template** (`.bxm`) | Components/tags, attributes, attribute values |
| **Class body** | Properties, methods, annotations |
| **Function body** | BIFs, variables, arguments, keywords |
| **After `.`** | Member access — properties, methods, built-in members |
| **After `new`** | Class names, Java classes |
| **After `import`** | Import paths |
| **After `extends`/`implements`** | Class/interface names |
| **Inside `.bxlint.json`** | Lint rule IDs for autocomplete |
| **Inside `.bxformat.json`** | Formatter option keys |

---

## Completion Item Kinds

Each completion suggestion is tagged with a VS Code completion kind, shown as an icon:

| Icon | Kind | Examples |
| --- | --- | --- |
| 🔤 | Text | Keywords |
| ⚡ | Function | BIFs, user functions |
| 🏗️ | Constructor | `new` expressions |
| 📦 | Class | Class names |
| 🔌 | Interface | Interface names |
| 📋 | Property | Component properties |
| 📐 | Snippet | Code snippets |
| 🔑 | Field | Variables, scopes |
| 📄 | File | Import paths |
| 📂 | Module | Module references |

---

## Configuration

CFML-specific completion settings can be customized in your VS Code settings:

```json
{
  "boxlang.cfml.suggest.enable": true,
  "boxlang.cfml.suggest.snippets.enable": true,
  "boxlang.cfml.suggest.globalFunctions.enable": true,
  "boxlang.cfml.suggest.globalTags.enable": true,
  "boxlang.cfml.suggest.htmlTags.enable": true,
  "boxlang.cfml.suggest.css.enable": true
}
```

See the complete [Settings Reference](../vscode/settings-reference.md) for all completion-related settings.

---

## Related Pages

{% content-ref url="overview.md" %}
{% endcontent-ref %}

{% content-ref url="linting.md" %}
{% endcontent-ref %}

{% content-ref url="formatting.md" %}
{% endcontent-ref %}

{% content-ref url="../vscode/settings-reference.md" %}
{% endcontent-ref %}

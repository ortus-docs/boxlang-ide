---
description: >-
  How to use the @boxlang chat participant in VS Code — AI-assisted BoxLang
  coding, documentation lookup, and the /docs command.
icon: message-bot
---

# Chat Integration

The BoxLang extension includes an AI chat participant that provides BoxLang-aware assistance directly in VS Code's Chat view. It integrates with GitHub Copilot Chat to answer questions, suggest code, and look up documentation.

---

## Getting Started

### Invoke the Chat Participant

1. Open the **Chat** view (`Ctrl+Shift+I` / `Cmd+Shift+I`).
2. Type `@boxlang` followed by your question.
3. Press Enter.

```
@boxlang How do I use queryExecute with parameterized queries?
```

The chat participant responds with BoxLang-specific answers, drawing from the BoxLang documentation and runtime knowledge.

---

## Features

### BoxLang-Aware Responses

The `@boxlang` participant is tuned for BoxLang and CFML development. It can:

- Write BoxLang code snippets
- Explain language features and built-in functions (BIFs)
- Help debug errors and suggest fixes
- Recommend best practices and patterns
- Explain framework concepts (ColdBox, TestBox, etc.)

### Documentation Lookup Tool

The chat participant has access to a built-in **Documentation Lookup** tool (`lookupBoxLangDocumentation`) that:

1. Searches the complete BoxLang documentation index
2. Identifies the most relevant documentation pages for your question
3. Fetches those pages and includes them in the chat context
4. Bases its answers on authoritative documentation

This means answers are grounded in real BoxLang docs, not just model training data.

### /docs Command

Use the `/docs` slash command to get quick links to relevant documentation without asking a specific question:

```
@boxlang /docs caching
```

This returns direct links to the BoxLang documentation pages most relevant to your topic.

---

## Example Prompts

### Code Generation

```
@boxlang Write a BoxLang component that reads a CSV file and returns an array of structs
```

### Debugging Help

```
@boxlang I'm getting "variable [myVar] doesn't exist" but I defined it in Application.bx. What's wrong?
```

### Learning

```
@boxlang What's the difference between a closure and a lambda in BoxLang? Show examples.
```

### Framework Questions

```
@boxlang How do I register an interceptor in a ColdBox module?
```

### Documentation Links

```
@boxlang /docs queryExecute
```

---

## How It Works

The `@boxlang` chat participant uses the `@vscode/chat-extension-utils` library to:

1. **Receive** your prompt with full chat history context
2. **Filter** available language model tools to BoxLang-relevant ones
3. **Send** the request to the AI model with a specialized BoxLang system prompt
4. **Stream** the response back with reference links

The system prompt is loaded from a bundled resource file that contains BoxLang-specific instructions, conventions, and knowledge.

---

## Requirements

- **GitHub Copilot Chat** must be installed and active
- An active **GitHub Copilot subscription**
- The BoxLang extension must be activated (open any `.bx`, `.bxs`, `.bxm`, or `.cfc` file)

---

## Related Pages

{% content-ref url="commands-reference.md" %}
{% endcontent-ref %}

{% content-ref url="settings-reference.md" %}
{% endcontent-ref %}

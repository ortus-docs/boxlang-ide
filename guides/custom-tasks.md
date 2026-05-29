---
description: >-
  How to define and run BoxLang tasks in VS Code — task.json configuration,
  custom commands, and integration with the build system.
icon: play
---

# Custom Tasks

The BoxLang extension contributes a custom **task type** that lets you define BoxLang commands as VS Code tasks. These tasks can be run from the **Tasks: Run Task** menu, bound to keyboard shortcuts, or included in build workflows.

---

## Task Definition

Define BoxLang tasks in `.vscode/tasks.json`:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Run Tests",
      "type": "boxlang",
      "command": "testbox run",
      "args": ["tests/"]
    }
  ]
}
```

### Task Properties

| Property | Required | Type | Description |
| --- | --- | --- | --- |
| `label` | Yes | `string` | Display name for the task. |
| `type` | Yes | `"boxlang"` | Must be `"boxlang"`. |
| `command` | Yes | `string` | The BoxLang command to execute. |
| `args` | No | `string[]` | Arguments to pass to the command. |

---

## Example Tasks

### Run a BoxLang Script

```json
{
  "label": "Run Main Script",
  "type": "boxlang",
  "command": "run",
  "args": ["${workspaceFolder}/main.bxs"]
}
```

### Run TestBox Tests

```json
{
  "label": "Run All Tests",
  "type": "boxlang",
  "command": "testbox run",
  "args": ["${workspaceFolder}/tests/"]
}
```

### Compile a Module

```json
{
  "label": "Build Module",
  "type": "boxlang",
  "command": "compile",
  "args": ["--output", "${workspaceFolder}/dist/"]
}
```

### Run with Specific BoxLang Version

```json
{
  "label": "Run with BoxLang 1.13",
  "type": "boxlang",
  "command": "run",
  "args": ["${workspaceFolder}/app.bx"]
}
```

---

## VS Code Variables in Tasks

You can use standard VS Code variables in task arguments:

| Variable | Description |
| --- | --- |
| `${workspaceFolder}` | Root of the open workspace |
| `${file}` | Currently active file |
| `${relativeFile}` | Active file relative to workspace |
| `${selectedText}` | Currently selected text |
| `${command:commandID}` | Output of a VS Code command |

---

## Running Tasks

### From the Command Palette

1. Open the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`).
2. Select **Tasks: Run Task**.
3. Choose your BoxLang task from the list.

### As a Build Task

Mark a task as the default build task:

```json
{
  "label": "Build Project",
  "type": "boxlang",
  "command": "compile",
  "group": {
    "kind": "build",
    "isDefault": true
  }
}
```

Run it with `Ctrl+Shift+B` (`Cmd+Shift+B` on Mac).

### As a Test Task

Mark a task as the test task:

```json
{
  "label": "Test Project",
  "type": "boxlang",
  "command": "testbox run",
  "group": {
    "kind": "test",
    "isDefault": true
  }
}
```

Run it from **Tasks: Run Test Task**.

---

## Related Pages

{% content-ref url="../vscode/commands-reference.md" %}
{% endcontent-ref %}

{% content-ref url="../vscode/version-management.md" %}
{% endcontent-ref %}

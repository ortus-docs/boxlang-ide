---
description: >-
  How to debug BoxLang applications in VS Code — launch configurations,
  breakpoints, variable inspection, dump panel, and MiniServer debugging.
icon: bug
---

# Debugging

The BoxLang extension includes a built-in debugger that integrates with VS Code's debugging interface. It supports both script/class debugging and MiniServer web application debugging.

{% hint style="info" %}
The debugger uses the Java Debug Protocol (JDP) and communicates over a dynamically allocated port. No manual port configuration is needed for basic use.
{% endhint %}

---

## Quick Start

### Debug a Script or Class

1. Open a `.bxs` script file or a `.bx` class with a `main` method.
2. Right-click in the editor and select **BoxLang: Run File**.
3. Set breakpoints by clicking in the gutter next to line numbers.
4. The debugger pauses at breakpoints — inspect variables, step through code, and use the Debug Console.

Or use a `launch.json` configuration for more control (see below).

### Debug a MiniServer

1. Create a MiniServer in the **BoxLang Servers** tree view.
2. Start the server by clicking the ▶️ **Run** button.
3. Once running, click the 🐞 **Debug** button in the server's action bar.
4. The debugger attaches to the running server — set breakpoints in your application code and trigger them by navigating in the browser.

---

## Launch Configurations

Create a `.vscode/launch.json` file to configure debugging. The BoxLang debugger supports two request types:

### Launch

Starts a new BoxLang process and attaches the debugger.

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "boxlang",
      "request": "launch",
      "name": "Debug BoxLang Program",
      "program": "${workspaceFolder}/index.bx"
    }
  ]
}
```

### Attach

Attaches to an already-running BoxLang process.

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "boxlang",
      "request": "attach",
      "name": "Attach to BoxLang",
      "program": "${workspaceFolder}/index.bx",
      "serverPort": 8085
    }
  ]
}
```

### Configuration Properties

| Property | Required | Type | Description |
| --- | --- | --- | --- |
| `type` | Yes | `"boxlang"` | Must be `"boxlang"`. |
| `request` | Yes | `"launch"` or `"attach"` | Whether to start a new process or attach to an existing one. |
| `program` | Yes | `string` | The BoxLang file to debug. Supports `${workspaceFolder}` and other VS Code variables. |
| `serverPort` | No | `number` | For `attach` requests: the port to connect to. |

### VS Code Variables in launch.json

You can use standard VS Code variables in the `program` property:

| Variable | Expands to |
| --- | --- |
| `${workspaceFolder}` | Root of the open workspace |
| `${file}` | Currently active file |
| `${relativeFile}` | Currently active file relative to workspace |
| `${fileBasename}` | Filename without path |

---

## Breakpoints

Set breakpoints by clicking in the gutter (to the left of line numbers). Supported breakpoint types:

- **Line breakpoints** — Pause execution at a specific line. Click the gutter to toggle.
- **Conditional breakpoints** — Right-click the gutter and select **Add Conditional Breakpoint** to break only when an expression evaluates to `true`.
- **Logpoints** — Right-click the gutter and select **Add Logpoint** to log a message without pausing.

{% hint style="tip" %}
Breakpoints can be set before or during a debug session. The debugger will resolve them when the BoxLang runtime reaches the corresponding source lines.
{% endhint %}

---

## Variable Inspection

While paused at a breakpoint, use the **Variables** panel to inspect the current state:

- **Local variables** — Variables in the current function scope
- **Arguments** — Function parameters
- **Closure scope** — Variables captured by closures
- **Component fields** — Properties of the current component/class

Hover over variables in the editor to see their current values inline.

---

## Variable Dump

The **Dump Variable** feature provides a rich HTML visualization of BoxLang variables, similar to BoxLang's `writeDump()` function.

### How to Use

**From the Debug Variables panel:**
1. Pause at a breakpoint.
2. In the **Variables** panel, right-click any variable.
3. Select **Dump Variable**.

**From the editor (during debug):**
1. Pause at a breakpoint.
2. Right-click in the editor.
3. Select **BoxLang: Dump Variable**.

### Dump Panel Behavior

The dump panel is configurable via two settings:

| Setting | Description |
| --- | --- |
| `boxlang.dump.panelMode` | `replace` — each dump replaces the panel (default). `newTab` — each dump opens in a new tab. |
| `boxlang.dump.panelLocation` | Controls which editor column: `beside` (default), `active`, `one`, `two`, or `three`. |

---

## Debug Actions

While debugging, use the debug toolbar to control execution:

| Action | Description |
| --- | --- |
| **Continue** (F5) | Resume execution until the next breakpoint. |
| **Step Over** (F10) | Execute the current line and move to the next. |
| **Step Into** (F11) | Step into a function call. |
| **Step Out** (Shift+F11) | Run to the end of the current function. |
| **Restart** (Ctrl+Shift+F5) | Restart the debug session. |
| **Stop** (Shift+F5) | Terminate the debug session. |

---

## Debug Console

The **Debug Console** (accessible from the bottom panel during debugging) shows:

- `stdout` and `stderr` output from the running BoxLang process
- Error messages and stack traces
- Any `writeOutput()` or `console()` calls

---

## Debugger Modes

The extension supports two debugger implementations:

| Mode | Setting | Description |
| --- | --- | --- |
| **Legacy** | `boxlang.debugger.mode = "legacy"` | Built-in debugger from the BoxLang JAR (default). |
| **Module** | `boxlang.debugger.mode = "module"` | ForgeBox debugger module managed by version. Configure `boxlang.debugger.moduleName` and `boxlang.debugger.moduleVersion`. |

---

## Related Pages

{% content-ref url="settings-reference.md" %}
{% endcontent-ref %}

{% content-ref url="commands-reference.md" %}
{% endcontent-ref %}

{% content-ref url="miniserver.md" %}
{% endcontent-ref %}

{% content-ref url="version-management.md" %}
{% endcontent-ref %}

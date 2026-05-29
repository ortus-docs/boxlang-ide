---
description: >-
  How to debug BoxLang applications in IntelliJ IDEA — breakpoints, stepping,
  variable inspection, watch expressions, and expression evaluation.
icon: bug
---

# Debugging

The BoxLang IntelliJ plugin provides full debugging support through the Debug Adapter Protocol (DAP). Debug BoxLang scripts with breakpoints, stepping, variable inspection, and expression evaluation.

---

## Starting a Debug Session

### Method 1: Debug from Gutter Icon
1. Open a BoxLang file
2. Click the green play icon ▶️ in the gutter
3. Select **Debug 'filename'**

### Method 2: Debug from Run Configuration
1. Create or select a BoxLang run configuration
2. Click the **Debug** button (🐛) in the toolbar
3. Or press **Shift+F9**

### Method 3: Debug from Context Menu
1. Right-click a BoxLang file in the Project view
2. Select **Debug 'filename'**

---

## Breakpoints

### Setting Breakpoints

**Click in the gutter** next to a line number to set a breakpoint. A red dot appears.

**Keyboard shortcut:** Place cursor on the line and press **Cmd+F8** (Mac) or **Ctrl+F8** (Windows/Linux).

### Breakpoint Types

| Type | Description |
| --- | --- |
| **Line Breakpoint** | Pauses execution at a specific line |
| **Conditional Breakpoint** | Pauses only when a condition is true |
| **Logpoint** | Logs a message without pausing execution |

### Conditional Breakpoints

1. Right-click the breakpoint dot
2. Enter a condition in the **Condition** field
3. The breakpoint only triggers when the condition evaluates to `true`

Example conditions:
```javascript
i > 100
user.name == "admin"
arrayLen(items) > 50
```

### Logpoints

1. Right-click the breakpoint dot
2. Check **Log evaluated message**
3. Enter a message with expressions in `{}`
4. Uncheck **Suspend thread** to continue execution

Example log message:
```
Processing item {i} of {arrayLen(items)}: {item.name}
```

---

## Debug Toolbar

When paused at a breakpoint, use the debug toolbar to control execution:

| Button | Shortcut | Action |
| --- | --- | --- |
| **Resume** | F9 | Continue execution until next breakpoint |
| **Pause** | (none) | Pause execution at current line |
| **Stop** | Cmd+F2 / Ctrl+F2 | Terminate the debug session |
| **Step Over** | F8 | Execute current line, skip into functions |
| **Step Into** | F7 | Step into function calls |
| **Step Out** | Shift+F8 | Execute to end of current function |
| **Run to Cursor** | Alt+F9 | Execute to cursor position |
| **Drop Frame** | (none) | Pop current stack frame and re-execute |

---

## Variable Inspection

### Variables Panel

The **Variables** panel shows all variables in the current scope:

- **Local variables** — Variables in the current function
- **Arguments** — Function parameters
- **This** — Current object instance
- **Closure scope** — Variables captured by closures

Click the arrow next to a variable to expand nested values (structs, arrays, objects).

### Hover Inspection

Hover over any variable in the editor while paused to see its current value in a tooltip.

### Inline Values

Enable inline values in **Settings → Build, Execution, Deployment → Debugger → Async Stack Traces**:
- Check **Show variable values in editor**
- Variables display their values inline next to their declarations

---

## Watch Expressions

Add custom expressions to monitor during debugging:

1. Open the **Watches** panel (usually on the right side of Variables)
2. Click the **+** button
3. Enter an expression (e.g., `user.email`, `arrayLen(items)`)
4. The expression evaluates and updates on each pause

### Quick Evaluate

Select an expression in the editor and press **Alt+F8** (Option+F8 on Mac) to evaluate it immediately.

---

## Expression Evaluation

### Debug Console (REPL)

The **Debug Console** provides a REPL (Read-Eval-Print Loop) for evaluating BoxLang expressions:

1. Open the **Debug Console** tab at the bottom
2. Type any BoxLang expression
3. Press **Enter** to evaluate

Examples:
```javascript
// Evaluate variables
user.name
arrayLen(items)

// Call functions
now()
structKeyExists(user, "email")

// Modify state (affects running program)
user.status = "active"
```

### Evaluate Expression Dialog

1. Press **Alt+F8** (Option+F8 on Mac)
2. Enter an expression in the dialog
3. Click **Evaluate** to see the result

---

## Stack Frames

The **Frames** panel shows the call stack:

- Click a frame to switch to that context
- Variables update to show the selected frame's scope
- Double-click a frame to navigate to the source code

### Async Stack Traces

For asynchronous code (futures, callbacks), enable async stack traces:
- **Settings → Build, Execution, Deployment → Debugger → Async Stack Traces**
- Check **Capture async stack traces**

---

## Attach Debugging

Connect to a running BoxLang process:

1. Create a **BoxLang Attach** run configuration
2. Configure host, port, and path mappings
3. Click **Debug**

See [Run Configurations](run-configurations.md#boxlang-attach-configuration) for details.

---

## Debugging Tips

### Conditional Breakpoints for Loops
```javascript
// Break on iteration 50
i == 50

// Break when condition changes
oldValue != newValue
```

### Watch for State Changes
Add a watch expression that changes:
```javascript
user.lastLogin != previousLogin
```

### Use Logpoints for Tracing
Instead of adding `writeDump()` calls, use logpoints:
```
Entering processUser() with user={user.id}, name={user.name}
```

### Evaluate Complex Expressions
```javascript
// Filter and transform
items.filter((item) => item.active).map((item) => item.name)

// Query data
queryExecute("SELECT count(*) as total FROM users")
```

---

## Related Pages

- [Run Configurations](run-configurations.md)
- [TestBox Integration](testbox-integration.md)
- [Settings Reference](settings-reference.md)

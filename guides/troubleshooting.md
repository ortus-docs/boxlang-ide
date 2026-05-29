---
description: >-
  Troubleshooting common BoxLang extension issues — LSP problems, Java errors,
  version download failures, formatting issues, and how to get help.
icon: circle-exclamation
---

# Troubleshooting

Solutions for common issues with the BoxLang VS Code extension.

---

## Diagnostic Commands

Before troubleshooting, gather diagnostic information with these commands:

| Command | Purpose |
| --- | --- |
| **BoxLang: Output Version Info** | Shows extension version, Java version, component versions, and configuration. **Include this in bug reports.** |
| **BoxLang: Restart Language Server** | Restart the LSP if features stop working. |
| **BoxLang: Hard Reset Workspace Home** | Reset the workspace BoxLang Home to its initial state. |

### Check Logs

The extension writes logs to the **BoxLang** output channel:

1. Open the **Output** panel (`Ctrl+Shift+U` / `Cmd+Shift+U`).
2. Select **BoxLang** from the dropdown.
3. Review the log for errors.

Enable verbose LSP logging for more detail:

```json
{
  "boxlang.lsp.logLevel": "DEBUG"
}
```

---

## Common Issues

### LSP Won't Start or Keeps Crashing

**Symptoms:**
- No diagnostics, completions, or hover information
- "Starting BoxLang Language Server..." hangs
- LSP process exits immediately

**Solutions:**

1. **Check Java 21 is installed:**
   ```bash
   java -version
   ```
   Must show `21` or higher. If not, run **BoxLang: Download Java 21**.

2. **Verify Java path:**
   ```json
   {
     "boxlang.java.javaHome": "/path/to/jdk-21"
   }
   ```

3. **Check LSP version:**
   Run **BoxLang: Select LSP Version** and pick the latest.

4. **Increase heap size:**
   ```json
   {
     "boxlang.lsp.maxHeapSize": 1024
   }
   ```

5. **Check for conflicting Java installations:**
   ```bash
   echo $JAVA_HOME
   which java
   ```

---

### Java 21 Not Found

**Symptoms:**
- Error: "Java 21 or higher is required"
- Extension features don't work

**Solutions:**

1. Run **BoxLang: Download Java 21** to auto-install a compatible JRE.
2. Or install manually:
   ```bash
   # Ubuntu/Debian
   sudo apt install openjdk-21-jdk

   # macOS
   brew install openjdk@21
   ```
3. Set the path:
   ```json
   {
     "boxlang.java.javaHome": "/usr/lib/jvm/java-21-openjdk-amd64"
   }
   ```

---

### Version Download Failures

**Symptoms:**
- "Failed to download BoxLang version"
- Version selection list is empty

**Solutions:**

1. **Check internet connection:** Versions are downloaded from AWS S3.
2. **Check firewall/proxy:** Ensure outbound HTTPS connections are allowed.
3. **Run Check for Updates:** **BoxLang: Check for Updates** refreshes the available versions list.
4. **Try a different version:** Some versions may be unavailable. Try an older or newer version.

---

### Formatting Not Working

**Symptoms:**
- Format on save doesn't format BoxLang files
- **Format Document** has no effect

**Solutions:**

1. **Verify all four beta requirements** (see [Formatting](../language-tools/formatting.md)):
   - `.bxlint.json` has `formatting.experimental.enabled: true`
   - Format-on-save is enabled in settings
   - Latest BoxLang version is selected
   - Latest LSP version is selected

2. **Check BoxLang version:**
   ```bash
   boxlang format -h
   ```
   Formatting requires BoxLang 1.13.0+ and bx-lsp 1.10.0+.

3. **Verify settings:**
   ```json
   {
     "[boxlang]": {
       "editor.formatOnSave": true
     }
   }
   ```

---

### Diagnostics Not Appearing

**Symptoms:**
- No lint warnings or errors in BoxLang/CFML files
- Expected diagnostics are missing

**Solutions:**

1. **Check that linting is enabled:** `.bxlint.json` exists at workspace root.
2. **Check file filters:** `include` and `exclude` patterns may exclude your files.
3. **Check rule settings:** Specific rules may be disabled:
   ```json
   {
     "diagnostics": {
       "unusedVariable": { "enabled": false }
     }
   }
   ```
4. **Enable experimental diagnostics:**
   ```json
   {
     "boxlang.lsp.enableExperimentalDiagnostics": true
   }
   ```
5. **Restart the LSP:** **BoxLang: Restart Language Server**.

---

### Completions Not Working

**Symptoms:**
- No suggestions appear when typing
- Only basic word completions, no BoxLang-specific suggestions

**Solutions:**

1. **Check LSP is running:** Run **BoxLang: Output Version Info** and look for LSP status.
2. **Enable completions in settings:**
   ```json
   {
     "boxlang.cfml.suggest.enable": true
   }
   ```
3. **Check file type:** Ensure the file uses a recognized extension (`.bx`, `.bxs`, `.bxm`, `.cfc`, `.cfm`, `.cfml`, `.cfs`).
4. **Restart the LSP:** Sometimes required after settings changes.

---

### Debugger Won't Attach

**Symptoms:**
- Debug session starts but breakpoints are grayed out
- "Failed to attach debugger" error

**Solutions:**

1. **Check debugger mode:**
   ```json
   {
     "boxlang.debugger.mode": "legacy"
   }
   ```
2. **Verify the program path** in `launch.json`:
   ```json
   {
     "program": "${workspaceFolder}/index.bx"
   }
   ```
3. **For MiniServer debugging:** Start the server first, then click the Debug button.
4. **Check port conflicts:** Ensure no other process is using the debugger port.

---

### Extension Won't Activate

**Symptoms:**
- BoxLang sidebar doesn't appear
- Commands show "command not found"

**Solutions:**

1. **Check workspace contains BoxLang files:** The extension activates when `.bx`, `.bxm`, `.bxs`, `.cfm`, `.cfml`, or `.cfc` files are present.
2. **Reload the window:** `Ctrl+Shift+P` → **Developer: Reload Window**.
3. **Reinstall the extension:** Uninstall and reinstall from the Marketplace.
4. **Check VS Code version:** Requires VS Code 1.100.0+.

---

## Getting Help

If the solutions above don't resolve your issue:

1. **Run BoxLang: Output Version Info** and copy the output.
2. **Check the BoxLang output channel** for error messages.
3. **Report the issue:**
   - [BoxLang IDE Jira](https://ortussolutions.atlassian.net/browse/BLIDE) — Extension issues
   - [BoxLang Jira](https://ortussolutions.atlassian.net/browse/BL) — Language/runtime issues

**Community resources:**
- [Community Forum](https://community.ortussolutions.com/c/boxlang/42)
- [BoxTeam Slack](https://boxteam.ortussolutions.com)

---

## Related Pages

{% content-ref url="../vscode/settings-reference.md" %}
{% endcontent-ref %}

{% content-ref url="../vscode/commands-reference.md" %}
{% endcontent-ref %}

{% content-ref url="../vscode/debugging.md" %}
{% endcontent-ref %}

{% content-ref url="../language-tools/formatting.md" %}
{% endcontent-ref %}

{% content-ref url="../language-tools/linting.md" %}
{% endcontent-ref %}

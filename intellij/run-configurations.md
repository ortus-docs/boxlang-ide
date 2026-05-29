---
description: >-
  How to run BoxLang scripts in IntelliJ IDEA — run configurations, gutter icons,
  program arguments, environment variables, and attach configurations.
icon: play
---

# Run Configurations

The BoxLang IntelliJ plugin provides two types of run configurations: **BoxLang** for executing scripts directly, and **BoxLang Attach** for connecting to running BoxLang processes.

---

## BoxLang Run Configuration

Execute BoxLang scripts directly from the IDE with full control over the execution environment.

### Creating a Run Configuration

**Method 1: From Gutter Icon**
1. Open a BoxLang file (`.bx`, `.bxs`, `.cfc`, `.cfm`)
2. Click the green play icon ▶️ in the gutter next to the file or main method
3. Select **Run 'filename'**

**Method 2: From Run Menu**
1. Select **Run → Edit Configurations...**
2. Click the **+** button and select **BoxLang**
3. Configure the settings (see below)
4. Click **OK**

**Method 3: From Context Menu**
1. Right-click a BoxLang file in the Project view
2. Select **Run 'filename'**

### Configuration Options

| Field | Description |
| --- | --- |
| **Name** | Display name for the run configuration |
| **Script Path** | Path to the BoxLang script to execute. Use `$FilePath$` macro for current file |
| **Working Directory** | Directory where the script runs. Defaults to project root |
| **Program Arguments** | Command-line arguments passed to the script |
| **Environment Variables** | Environment variables set before execution (format: `KEY=value`) |
| **JVM Arguments** | Additional JVM arguments (e.g., `-Xmx512m`) |

### Example: Run Current File

```
Script Path: $FilePath$
Working Directory: $ProjectFileDir$
Program Arguments: (empty)
```

### Example: Run with Arguments

```
Script Path: /path/to/script.bxs
Working Directory: /path/to/project
Program Arguments: --input data.json --output result.json
Environment Variables: DEBUG=true
```

---

## BoxLang Attach Configuration

Connect the debugger to an already-running BoxLang process via JDWP (Java Debug Wire Protocol).

### Creating an Attach Configuration

1. Select **Run → Edit Configurations...**
2. Click the **+** button and select **BoxLang Attach**
3. Configure the settings (see below)
4. Click **OK**

### Configuration Options

| Field | Description |
| --- | --- |
| **Name** | Display name for the attach configuration |
| **Host** | Hostname or IP address of the running BoxLang process (default: `localhost`) |
| **JDWP Port** | Debug port the BoxLang process is listening on (default: `5005`) |
| **Local Root** | Local project root path for source mapping |
| **Remote Root** | Remote project root path (for remote debugging scenarios) |

### Starting a BoxLang Process with Debug Enabled

Before attaching, start your BoxLang process with JDWP enabled:

```bash
java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005 \
  -jar boxlang.jar your-script.bxs
```

Or use the BoxLang CLI:

```bash
boxlang --debug your-script.bxs
```

### Path Mapping for Remote Debugging

When debugging a BoxLang process running on a different machine or in a container:

```
Local Root: /Users/dev/myproject
Remote Root: /app/myproject
```

The debugger maps source file paths between local and remote locations.

---

## Run Line Markers

The plugin adds gutter icons for quick execution:

| Icon | Location | Action |
| --- | --- | --- |
| ▶️ | Next to file name | Run the entire file |
| ▶️ | Next to `main()` method | Run the main method |
| 🐛 | Next to file/method | Debug the file or method |

Click the icon to run or debug immediately. Right-click for additional options.

---

## Running from Terminal

You can also run BoxLang scripts from the integrated terminal:

```bash
# Run a script
boxlang script.bxs

# Run with arguments
boxlang script.bxs arg1 arg2

# Run with debug enabled
boxlang --debug script.bxs
```

---

## Related Pages

- [Debugging](debugging.md)
- [Settings Reference](settings-reference.md)
- [TestBox Integration](testbox-integration.md)

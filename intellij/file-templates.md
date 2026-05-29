---
description: >-
  How to create new BoxLang files in IntelliJ IDEA — file templates for classes,
  scripts, and templates with customizable content.
icon: file-plus
---

# File Templates

The BoxLang IntelliJ plugin provides file templates for quickly creating new BoxLang files. Templates are accessible from the **New** menu in the Project view.

---

## Creating a New BoxLang File

### Method 1: From Project View

1. Right-click in the Project view (or a specific folder)
2. Select **New → BoxLang File**
3. Choose the file type:
   - **BoxLang Class** (`.bx`)
   - **BoxLang Script** (`.bxs`)
   - **BoxLang Template** (`.bxm`)
4. Enter the file name (without extension)
5. Press **Enter**

### Method 2: From Menu

1. Select **File → New → BoxLang File**
2. Choose the file type
3. Enter the file name
4. Press **Enter**

### Method 3: Keyboard Shortcut

1. Press **Cmd+N** (Ctrl+N) in the Project view
2. Select **BoxLang File**
3. Choose the file type
4. Enter the file name

---

## File Template Types

### BoxLang Class (`.bx`)

Creates a new BoxLang class/component file:

```javascript
component {

    /**
     * Constructor
     */
    function init() {
        return this;
    }

}
```

**Use for:**
- Model classes
- Service classes
- DAO classes
- Any reusable component

### BoxLang Script (`.bxs`)

Creates a new BoxLang script file:

```javascript
// BoxLang Script

// Your code here

```

**Use for:**
- Standalone scripts
- Migration scripts
- Utility scripts
- Command-line tools

### BoxLang Template (`.bxm`)

Creates a new BoxLang markup template file:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Page Title</title>
</head>
<body>
    <h1>Hello BoxLang!</h1>

    <bx:output>
        #now()#
    </bx:output>
</body>
</html>
```

**Use for:**
- Web pages
- Email templates
- Report templates
- Any HTML-generating template

---

## Customizing Templates

You can customize the default templates or create your own:

### Edit Existing Templates

1. Open **Settings → Editor → File and Code Templates**
2. Select the **Templates** tab
3. Find the BoxLang template you want to edit:
   - **BoxLang Class**
   - **BoxLang Script**
   - **BoxLang Template**
4. Modify the template content
5. Click **Apply**

### Create Custom Templates

1. Open **Settings → Editor → File and Code Templates**
2. Click the **+** button
3. Enter a name (e.g., "BoxLang Service")
4. Set the extension (e.g., `bx`)
5. Enter the template content
6. Click **Apply**

### Template Variables

Templates support variables that are replaced when creating a file:

| Variable | Description | Example |
| --- | --- | --- |
| `${NAME}` | File name without extension | `UserService` |
| `${PACKAGE_NAME}` | Package/directory path | `models.services` |
| `${USER}` | Current system user | `john.doe` |
| `${DATE}` | Current date | `2026-05-29` |
| `${TIME}` | Current time | `14:30:00` |
| `${YEAR}` | Current year | `2026` |
| `${MONTH}` | Current month | `05` |
| `${DAY}` | Current day | `29` |

### Example: Custom Service Template

```javascript
/**
 * ${NAME} Service
 *
 * @author ${USER}
 * @created ${DATE}
 */
component singleton {

    /**
     * Constructor
     */
    function init() {
        return this;
    }

    /**
     * Get all ${NAME}s
     *
     * @return array
     */
    function getAll() {
        // TODO: Implement
        return [];
    }

    /**
     * Get ${NAME} by ID
     *
     * @id.hint The ${NAME} ID
     * @return struct
     */
    function get(required numeric id) {
        // TODO: Implement
        return {};
    }

    /**
     * Create a new ${NAME}
     *
     * @data.hint The ${NAME} data
     * @return struct
     */
    function create(required struct data) {
        // TODO: Implement
        return data;
    }

    /**
     * Update an existing ${NAME}
     *
     * @id.hint The ${NAME} ID
     * @data.hint The ${NAME} data
     * @return boolean
     */
    function update(required numeric id, required struct data) {
        // TODO: Implement
        return true;
    }

    /**
     * Delete a ${NAME}
     *
     * @id.hint The ${NAME} ID
     * @return boolean
     */
    function delete(required numeric id) {
        // TODO: Implement
        return true;
    }

}
```

---

## Template Best Practices

### Include Documentation

Always add Javadoc-style comments:

```javascript
/**
 * UserService
 *
 * Handles user authentication and management
 *
 * @author ${USER}
 * @version 1.0.0
 * @created ${DATE}
 */
```

### Use Type Hints

Add type hints for better IDE support:

```javascript
/**
 * Get user by ID
 *
 * @id.hint The user ID
 * @id.type numeric
 * @return User
 * @throws UserNotFoundException
 */
function getUser(required numeric id) {
    // Implementation
}
```

### Follow Naming Conventions

- **Classes:** PascalCase (`UserService`, `ProductDAO`)
- **Methods:** camelCase (`getUser`, `calculateTotal`)
- **Variables:** camelCase (`userName`, `orderTotal`)
- **Constants:** UPPER_SNAKE_CASE (`MAX_RETRIES`, `DEFAULT_TIMEOUT`)

---

## Live Templates

In addition to file templates, IntelliJ provides **Live Templates** for code snippets:

### Built-in Live Templates

| Abbreviation | Expands To |
| --- | --- |
| `sout` | `writeOutput()` |
| `soutv` | `writeOutput(variable)` |
| `for` | `for` loop |
| `fori` | `for` loop with index |
| `itere` | `for` loop over collection |
| `ifn` | `if (x == null)` |
| `inn` | `if (x != null)` |

### Creating Live Templates

1. Open **Settings → Editor → Live Templates**
2. Click **+** and select **Live Template**
3. Enter an abbreviation (e.g., `bxlog`)
4. Enter the template text:
   ```javascript
   writeLog("$MESSAGE$");$END$
   ```
5. Define variables (e.g., `MESSAGE` = `"Log message"`)
6. Set the context (BoxLang files)
7. Click **Apply**

### Using Live Templates

1. Type the abbreviation (e.g., `bxlog`)
2. Press **Tab** to expand
3. Fill in the variables
4. Press **Tab** to move to next variable or **Enter** to finish

---

## Related Pages

- [LSP Features](lsp-features.md)
- [Run Configurations](run-configurations.md)
- [Settings Reference](settings-reference.md)

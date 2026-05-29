---
description: >-
  How to run and debug TestBox tests in IntelliJ IDEA — gutter icons, test result
  tree, suite/spec filtering, and automatic TestBox detection.
icon: test-tube
---

# TestBox Integration

The BoxLang IntelliJ plugin provides first-class support for [TestBox](https://testbox.ortusbooks.com/), the BDD/TDD testing framework for BoxLang. Run and debug tests with gutter icons, view results in a tree structure, and filter by suites or specs.

---

## Features

| Feature | Description |
| --- | --- |
| **Gutter Icons** | Run or debug individual tests, suites, or entire test files |
| **Test Result Tree** | Visual tree showing pass/fail status for each test |
| **Suite Filtering** | Run only specific `describe()` blocks |
| **Spec Filtering** | Run only specific `it()` blocks |
| **Bundle Execution** | Run all tests in a test file |
| **Automatic Detection** | Detects TestBox installation and prompts to install if missing |
| **Debug Support** | Debug tests with breakpoints and variable inspection |

---

## Running Tests

### Method 1: Gutter Icons

TestBox test files show gutter icons for quick execution:

| Icon | Location | Action |
| --- | --- | --- |
| ▶️ | Next to `component` declaration | Run all tests in the file |
| ▶️ | Next to `describe()` block | Run only that test suite |
| ▶️ | Next to `it()` block | Run only that specific test |
| 🐛 | Next to any test element | Debug the test |

Click the icon to run or debug immediately.

### Method 2: Context Menu

1. Right-click a test file in the Project view
2. Select **Run 'TestBox: filename'** or **Debug 'TestBox: filename'**

### Method 3: Run Configuration

1. Select **Run → Edit Configurations...**
2. Click **+** and select **TestBox**
3. Configure the test scope (see below)
4. Click **OK**

---

## Test Configuration Options

| Field | Description |
| --- | --- |
| **Name** | Display name for the test configuration |
| **Test Scope** | What to run: `BUNDLE` (file), `SUITE` (describe block), or `SPEC` (it block) |
| **Bundle Path** | Dot-notation path to the test file (e.g., `tests.specs.UserServiceSpec`) |
| **Filter Suites** | Comma-separated list of suite names to run (for `SUITE` scope) |
| **Filter Specs** | Comma-separated list of spec names to run (for `SPEC` scope) |
| **Working Directory** | Directory where tests run. Defaults to project root |
| **Environment Variables** | Environment variables set before test execution |

### Example: Run Single Test

```
Test Scope: SPEC
Bundle Path: tests.specs.UserServiceSpec
Filter Specs: should create a new user
```

### Example: Run Test Suite

```
Test Scope: SUITE
Bundle Path: tests.specs.UserServiceSpec
Filter Suites: create()
```

### Example: Run All Tests in File

```
Test Scope: BUNDLE
Bundle Path: tests.specs.UserServiceSpec
```

---

## Test Result Tree

After running tests, the **Run** tool window shows a tree structure:

```
✅ UserServiceSpec
  ✅ create()
    ✅ should create a new user
    ✅ should validate email format
  ❌ update()
    ✅ should update user name
    ❌ should update user email
      Expected: "new@example.com"
      Actual: "old@example.com"
```

### Result Indicators

| Icon | Meaning |
| --- | --- |
| ✅ | Test passed |
| ❌ | Test failed |
| ⏭️ | Test skipped |
| ⏸️ | Test pending |

### Navigating Failures

- Click a failed test to see the error message and stack trace
- Double-click to navigate to the failing line in the test file
- Use the **Jump to Source** button (Cmd+F4 / Ctrl+F4) to open the test code

---

## TestBox Detection

The plugin automatically detects TestBox installations:

1. **On project open** — Checks for TestBox in `boxlang_modules/` or `modules/`
2. **On test execution** — Verifies TestBox is available before running tests
3. **Missing TestBox** — Shows a notification with option to install

### Installing TestBox

If TestBox is not detected:

1. Click **Install TestBox** in the notification
2. Or run manually: `box install testbox`
3. Restart the IDE or reload the project

---

## Debugging Tests

Debug tests the same way as regular BoxLang code:

1. Set breakpoints in your test file or application code
2. Click the debug icon 🐛 next to a test
3. The debugger pauses at breakpoints
4. Inspect variables, evaluate expressions, and step through code

### Debugging Tips

**Break on test failures:**
```javascript
// Add a conditional breakpoint that triggers on failure
expect(result).toBeTrue() // Break here when result is false
```

**Watch test state:**
Add watch expressions to monitor test variables:
```javascript
testData
mockService.callCount
```

**Evaluate during tests:**
Use the Debug Console to inspect test state:
```javascript
// Check mock calls
mockService.$callLog()

// Inspect test data
structKeyList(testData)
```

---

## Test File Structure

TestBox test files follow this structure:

```javascript
component extends="testbox.system.BaseSpec" {

    function run() {
        describe("UserService", () => {

            beforeEach(() => {
                variables.service = new models.UserService();
            });

            describe("create()", () => {

                it("should create a new user", () => {
                    var user = service.create({ name: "John" });
                    expect(user.id).toBeGT(0);
                });

                it("should validate email format", () => {
                    expect(() => {
                        service.create({ email: "invalid" });
                    }).toThrow();
                });
            });
        });
    }
}
```

The plugin recognizes:
- `component extends="testbox.system.BaseSpec"` — Test file marker
- `describe()` — Test suite
- `it()` — Individual test spec
- `beforeEach()`, `afterEach()` — Lifecycle methods

---

## Running Tests from Terminal

You can also run TestBox tests from the integrated terminal:

```bash
# Run all tests
box testbox run

# Run specific bundle
box testbox run bundles=tests.specs.UserServiceSpec

# Run with filtering
box testbox run bundles=tests.specs.UserServiceSpec filterSpecs="should create"

# Run with verbose output
box testbox run reporter=spec
```

---

## Related Pages

- [Run Configurations](run-configurations.md)
- [Debugging](debugging.md)
- [Settings Reference](settings-reference.md)

# Configuration

The langauge server is configured to look for .bxlint.json file in the root of your project. This file will automatically configure the running language server as soon as you update it. \
\
Through this file you can include/exclude files as well as control individual diagnostic rules.

### Example Configuration

```json
{
  // Optional: restrict analysis scope (workspace‑relative globs)
  "include": [ "src/**" ],
  "exclude": [ "coldbox/**", "modules/**" ],

  // Rule customization
  "diagnostics": {
    "unscopedVariable": {
      "enabled": true,
      "severity": "warning"
    },
    "unusedVariable": {
      "enabled": true,
      "severity": "hint"
    }
  }
}
```

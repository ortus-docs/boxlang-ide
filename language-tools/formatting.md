---
description: >-
  Experimental BoxLang formatting support, version requirements, and
  configuration files
icon: palette
---

# Formatting

Formatting support for BoxLang is currently experimental.

You must enable it in `.bxlint.json` before editor formatting becomes available.

{% hint style="warning" %}
Formatting requires **BoxLang `1.13.0` or higher** and **bx-lsp `1.10.0` or higher**.
{% endhint %}

### How formatting works

Formatting support is powered by the BoxLang CLI `format` command.

If your BoxLang version is new enough, run this command to inspect the available options:

```bash
boxlang format -h
```

This is the same formatting foundation used by the language tooling.

### Requirements

To use formatting, make sure all of the following are true:

* formatting is enabled in `.bxlint.json`
* BoxLang is `1.13.0` or newer
* bx-lsp is `1.10.0` or newer

If one of these requirements is missing, formatting may not appear or may fail to run.

### Formatter style

The BoxLang formatter is inspired by `cfformat` and `prettyprint`.

The goal is consistent, automatic formatting with minimal manual cleanup.

### Configuration files

The formatter introduces a BoxLang-native configuration file named `.bxformat.json`.

It is also compatible with `cfformat.json`.

That lets existing formatter configurations continue to work while giving BoxLang its own dedicated format going forward.

### When to use the CLI

The CLI is the fastest way to verify that your runtime supports formatting.

Use it when you need to:

* confirm the `format` command is available
* inspect supported formatter options
* validate your installed BoxLang version

### Related pages

For the broader language tooling stack, see [Language Tools overview](overview.md).

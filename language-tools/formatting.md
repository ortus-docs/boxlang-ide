---
description: >-
  Experimental BoxLang formatting support, version requirements, and
  configuration files
icon: palette
---

# Formatting

Formatting support for BoxLang is in its early stages and requires a few manual setup steps.

For full details on the BoxLang formatter itself — including all configuration options, rules, and `.bxformat.json` reference — see the [BoxLang Formatter documentation](https://boxlang.ortusbooks.com/getting-started/ide-tooling/boxlang-formatter).

{% hint style="warning" %}
Formatting requires **BoxLang `1.13.0` or higher** and **bx-lsp `1.10.0` or higher**.
{% endhint %}

## How formatting works

Formatting support is powered by the BoxLang CLI `format` command.

If your BoxLang version is new enough, run this command to inspect the available options:

```bash
boxlang format -h
```

This is the same formatting foundation used by the language tooling.

## Enabling formatting (beta)

There are **four** things you need to enable formatting during the beta period:

{% stepper %}
{% step %}

### Enable formatting in `.bxlint.json`

Add the following configuration to your workspace `.bxlint.json`:

```json
{
  "formatting": {
    "experimental": {
      "enabled": true
    }
  }
}
```

{% endstep %}

{% step %}

### Enable format-on-save in VSCode

Open your VSCode settings and add the format-on-save override for BoxLang:

{% tabs %}
{% tab title="settings.json" %}

```json
{
  "[boxlang]": {
    "editor.formatOnSave": true
  }
}
```

{% endtab %}

{% tab title="Settings UI" %}

1. Open **Preferences: Open Settings (JSON)** from the Command Palette
2. Add the `[boxlang]` block shown in the JSON tab
{% endtab %}
{% endtabs %}

You can also enable global format-on-save if you prefer:

```json
{
  "editor.formatOnSave": true
}
```

{% endstep %}

{% step %}

### Use the latest BoxLang version

Make sure you are on the latest BoxLang version available in VSCode:

1. Open the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Run **BoxLang: Select Default BoxLang Version**
3. Pick the newest version from the list
{% endstep %}

{% step %}

### Use the latest LSP version

Make sure you are on the latest LSP version:

1. Open the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Run **BoxLang: Select LSP Version**
3. Pick the newest version from the list

{% hint style="info" %}
You may need to run **Developer: Reload Window** from the Command Palette after switching LSP versions.
{% endhint %}
{% endstep %}
{% endstepper %}

Once all four steps are complete, formatting is active. Saving any `.bx`, `.bxs`, `.cfc`, or `.cfs` file will trigger the formatter.

### Formatter in action

The BoxLang formatter is inspired by `cfformat` and `prettyprint`. It enforces consistent style across your codebase with no manual effort.

**Before formatting:**

```js
class UserService{

function init( required name,  required email ){
variables.name=arguments.name
 variables.email = arguments.email
    return this
}

public function getUser( required id ) {
    if( arguments.id == 0 ) { throw( "Invalid ID" ) }
   return queryExecute( "SELECT * FROM users WHERE id = :id", { id : arguments.id } )
}

}
```

**After formatting:**

```js
class UserService {

	function init( required name, required email ){
		variables.name = arguments.name
		variables.email = arguments.email
		return this
	}

	public function getUser( required id ){
		if( arguments.id == 0 ){
			throw( "Invalid ID" )
		}
		return queryExecute(
			"SELECT * FROM users WHERE id = :id",
			{ id : arguments.id }
		)
	}

}
```

### Configuration files

The formatter uses a BoxLang-native configuration file named `.bxformat.json`.

It is also compatible with `cfformat.json`, so existing formatter configurations continue to work.

Place either file at the workspace root to customize formatting rules. See the [BoxLang Formatter documentation](https://boxlang.ortusbooks.com/getting-started/ide-tooling/boxlang-formatter) for the complete reference of available options.

### When to use the CLI

The CLI is the fastest way to verify that your runtime supports formatting.

Use it when you need to:

* confirm the `format` command is available
* inspect supported formatter options
* validate your installed BoxLang version

### Related pages

For the broader language tooling stack, see [Language Tools overview](overview.md).

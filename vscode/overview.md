---
description: A quick overview of our VSCode Extension for BoxLang
icon: crosshairs-simple
---

# Overview

### Features at a Glance

* Language server integration
  * Inline documentation
  * Language hints
  * Type information (experimental)
* Built-in debugger
* Mini BoxLang web server for quick development/testing
* Code Highlights and Introspection for supported grammars: Java, HTML, CSS, SQL, CFML

### Language Server

The extension bundles a language server based on the BoxLang runtime that gives VSCode access to the same information used when executing your sourcecode. This provides us the ability to display rich information right in the editor.

Some features provided by the language server are

#### Code outlines

<figure><img src="../.gitbook/assets/ide-tooling-outline.png" alt=""><figcaption></figcaption></figure>

#### Function definition

<figure><img src="../.gitbook/assets/ide-tooling-function-definition.png" alt=""><figcaption></figcaption></figure>

#### Type hinting (experimental - must configure in settings)

<figure><img src="../.gitbook/assets/ide-tooling-type-hinting.png" alt=""><figcaption></figcaption></figure>

A lot of functionality is still provided through the old JavaScript API. It is being converted to use the language server ASAP.

### Debugger

The [debugger](/broken/pages/wKeHIvqcYfxCQqnUc9ir) is implemented in Java using the JDP. It provides complete control over a running BoxLang application.

The extension provides quick ways to run your BoxLang programs. Simply right-click within a `.bxs` file or class (`.bx`) that implements a main method and select "BoxLang: Run File".

<figure><img src="../.gitbook/assets/ide-tooling-context-run.png" alt=""><figcaption></figcaption></figure>

You can use it to debug command line scripts or the built-in web server.

<figure><img src="../.gitbook/assets/ide-tooling-debug.png" alt=""><figcaption></figcaption></figure>

### Mini Web Server

The MinServer provides a lightweight web runtime powered by undertow. Simply hit `ctrl+shift+p` to bring up the command palette and select "BoxLang: Run Web Server". When you run the command it will open up the MinServer on the configured port (defaults to 8085) and open your browser.

<figure><img src="../.gitbook/assets/ide-tooling-context-minserver.png" alt=""><figcaption></figcaption></figure>

The web server will automatically be configured to use your projects directory as the web root. You will be prompted to select your web root if you have more than one folder open in your workspace.

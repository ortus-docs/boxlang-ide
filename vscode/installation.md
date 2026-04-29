---
description: >-
  We provide several different ways for you to install the BoxLang extension
  based on your needs.
icon: plug
---

# Installation

### VSCode Marketplace

* **Release Version: (**&#x6D;ajor.EVEN\_NUMBER.patch)\
  Search for "BoxLang" in the Extensions view and click "Install".
* **Pre-release Version: (**&#x6D;ajor.ODD\_NUMBER.patch)\
  On the extension page, select "Switch to Pre-Release" to install the latest beta.

We do our best to follow the official guidelines on pre-release development cycles for VSCode extensions. You can read about the recommended approach here \
[https://code.visualstudio.com/api/working-with-extensions/publishing-extension#prerelease-extensions](https://code.visualstudio.com/api/working-with-extensions/publishing-extension#prerelease-extensions)

The TLDR; of release/pre-release versioning is that as a user, you can select whichever version you would like to use. VSCode will do its best to always supply you with the latest version you have requested. For instance, if you prefer pre-release distributions it will always try to update you to the latest pre-release version.\
\
A version that includes an even number in the minor spot like `3.4.5` will be considered an official release. A version that includes an odd number in the minor spot like `2.7.2` will be considered a pre-release.

### OpenVSX

Visit [OpenVSX](https://open-vsx.org/) and search for "BoxLang" or go directly to the official [BoxLang Extension listing](https://open-vsx.org/extension/ortus-solutions/vscode-boxlang).<br>

There is a download button on the right-hand side of the page that will allow you to download/install the extension.

Once downloaded you can install via CLI

```
code --install-extension /path/to/boxlang.vsix
```

Or you can install through the UI by opening VSCode > sidebar extension menu > dot menu > Install from VSIX...

### &#x20;Manual Build & Install

*   Clone the repo:

    ```
    git clone https://github.com/ortus-solutions/vscode-boxlang.git
    cd vscode-boxlang
    ```
*   Install dependencies and build:

    ```
    npm install
    npm run build
    ```
*   Package and install:

    ```
    npm run package
    code --install-extension boxlang-*.vsix
    ```

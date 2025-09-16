---
icon: server
---

# MiniServer

The BoxLang MiniServer is a fast and convenient way to run a BoxLang web server. It is very powerful and integrates directly with VSCode.

This page primarily covers features specific to the VSCode extensions use of the MiniServer. To learn more about the MiniServer itself and other ways to use it refer to the [official MiniServer documentation](https://boxlang.ortusbooks.com/getting-started/running-boxlang/miniserver).

The MIniServer

* Is an undertow based ultralight web server
* Configurable through the VSCode UI
* Allows line debugging with the click of a button

### Creating a Server

You can create a MiniServer through the BoxLang panel and clicking "Create MiniServer" or using the "+" icon to the top right of the MiniServer panel.



<figure><img src="../.gitbook/assets/Screenshot 2025-04-29 at 1.28.11 AM.png" alt="" width="264"><figcaption></figcaption></figure>

Once you start creating a server you will be shown a series of prompts that allow you to name and configure different server properties.

### Managing a MiniServer

Once created MiniServers will appear in the panel and provide you with several options for managing their settings and interacting with them.

<figure><img src="../.gitbook/assets/image (4).png" alt="" width="264"><figcaption></figcaption></figure>

Some of the properties can be edited by hovering over them and clicking the pencil icon.\
\
In addition to being able to edit the server properties you can press the "play"  button to start the server.

### Running a Server

Once you have started a MiniServer your action items will change. You will gain new actions like

* Stop - shutdown the MiniServer
* Debug - start a debug session in VSCode and attach to the MiniServer
* Open - open the browser to the root of the server


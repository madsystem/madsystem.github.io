---
layout: post
title:  "Connect Visual Code to a Native Android App"
date:   2017-04-10 17:37 +0100
---

The last post was about getting gdb connected to a running Native Android Application. The gdb shell can be ok in most cases, but lacks convenience features. So I did some research and found [this](https://github.com/WebFreak001/code-debug) extension for Visual Code which I wanted to test.  
 
So first install the plugin via Visual Code extension manager. Then start the gdbserver on your device (see previous article). When this is done we need to open our project folder (for me this was the Atomic Age Engine root folder) and create an ```launch.json``` file. Mine looks like this:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "gdb",
            "request": "attach",
            "name": "Attach to gdbserver",
            "executable": "K:/code/androiddbg/gdb_client/sysroot/ad844a27d43/system/bin/app_process32",
            "remote": true,
            "target": ":5039",
            
            "cwd": "${workspaceRoot}",
            "gdbpath": "D:/Utils/Android/AndroidNDK/android-ndk-r10e/toolchains/arm-linux-androideabi-4.9/prebuilt/windows/bin/arm-linux-androideabi-gdb.exe",
            "autorun": [
                "set solib-search-path K:/code/androiddbg/gdb_client"
            ],
            "printCalls" : true
        }
    ]
}
```
So as you can see the ```executable``` is pointing to our process. The ```gdbpath``` to the installed NDK precompiled gdbclient. ```autorun``` is setting the solib-search-path to the folder where our native binary is located on the host system. As it turns out the extension is not 100% convenient either. Stepping is currently broken and breakpoints will only be send to the gdbserver if the application is paused. If I am doing something wrong just tell me :).
Happy debugging.

PS: I know absolute paths are not really an elegant solution but I have not found a way to use enviorment variable in VS Code configs. 

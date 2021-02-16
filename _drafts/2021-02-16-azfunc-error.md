---
layout: post
title:  "Azure Functions - "
category: Engineering
tags: Azure Functions Error
---

I've been building a queue reader with Azure Functions recently and ran into an exception that took me a while to fix. Hopefully this will help others sort-circuit the process :smile:

Here is the flow:

1. I'm using Visual Studio Code.
2. I have a simple function that is queue triggered and bound to an Azure Storage Queue.
3. In a PowerShell terminal I was start my function.
4. The function starts as expected but after a few seconds an exception is thrown.

![Visual Studio Code showing an exception message](/images/2021-02-16-vscode-azfun-error.png)
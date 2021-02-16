---
layout: post
title:  "Azure Functions - No such host is known"
category: Engineering
tags: Azure Functions Bug
---

I've been building a queue reader with [Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/functions-overview) recently and ran into an exception that took me a while to fix. Hopefully this will help others short-circuit the process :sunglasses:

Here is the flow:

1. I'm using [Visual Studio Code](https://code.visualstudio.com/).
2. I have a simple [queue triggered function](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-storage-queue-triggered-function) that is bound to an [Azure Queue Storage](https://docs.microsoft.com/en-gb/azure/storage/queues/storage-queues-introduction).
3. In a [PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.1) terminal I start my function.
4. The function starts as expected but __after a few seconds an exception is thrown__.

![Visual Studio Code showing an exception message](/images/2021-02-16-vscode-azfun-error.png)

The exception reads:

```
An unhandled exception has occurred. Host is shutting down.
Microsoft.WindowsAzure.Storage: No such host is known. System.Net.Http: No such host is known. System.Private.CoreLib: No such host is known.
```

The problem was with my _AZURE_STORAGE_CONNECTION_STRING_ variable. This is where my queue trigger function gets the connection string which it uses to bind to the queue storage.

I set the variable in my _settings.local.json_ file but as you can see in the screenshot above, the Azure Functions runtime notices that I have an Environment Variable with the same name and uses that instead.

![PowerShell terminal showing that the environment variable value is being used](/images/2021-02-16-vscode-psenv-skip.png)

Checking the environment variable in the terminal I can see that it's pointing to a storage account that doesn't exist! :beetle:

![PowerShell terminal showing the incorrect environment variable value](/images/2021-02-16-vscode-psenv-error.png)

Updating the environment variable with the correct connection string resolves the exception. :+1:
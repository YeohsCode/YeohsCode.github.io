---
layout: post
title:  "\"getaddrinfo ENOTFOUND\" error when debugging angular via VS Code"
date:   2022-07-04 10:48:01 +0800
image:  22.jpg
tags:   Frontend dev Angular node.js
---
### Symptom
I got an issue today when trying to debug a new Angular project, here's the details:

```
ApplicationInsights:CorrelationIdManager [
  Error: getaddrinfo ENOTFOUND dc.services.visualstudio.com
      at GetAddrInfoReqWrap.onlookup [as oncomplete] (node:dns:71:26)
      at GetAddrInfoReqWrap.callbackTrampoline (node:internal/async_hooks:130:17) {
    errno: -3008,
    code: 'ENOTFOUND',
    syscall: 'getaddrinfo',
    hostname: 'dc.services.visualstudio.com'
  }
]
```

### Analysis
I am totally new to Angular, after some googling, I found a solution here: [Node.js Error Message “getaddrinfo ENOTFOUND localhost” Solution](https://medium.com/swlh/node-js-error-message-getaddrinfo-enotfound-localhost-solution-9b2fa4f61a9c)

### Solution
1. Press win+R, enter drivers
    ![Step01](/images/2022/0704-01.png)
		
2. Go to drivers\etc
    ![Step02](/images/2022/0704-02.png)
		
	
3. Open hosts in notepad and add the highlight line:
    ```
    127.0.0.1       localhost
    ```

    ![Step03](/images/2022/0704-03.png)
---
id: doc5
title: Setup proxy
---

1. Create file /client/proxy.conf.json and past this code:
```
{
    "/api/*": {
        "target": "http://localhost:5000",
        "secure": false,
        "logLevel": "debug",
        "changeOrigin": true
    },
    "/uploads/": {
        "target": "http://localhost:5000",
        "secure": false,
        "logLevel": "debug",
        "changeOrigin": true
    }
}
```
2. Edit start script in file /client/package.json
```
...
"start": "ng serve --proxy-config proxy.conf.json",
...
```
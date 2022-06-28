# demo-pod
An example of 4 grouped services:

```mermaid
flowchart LR
    User--Makes a Request to-->main

    subgraph POD
        subgraph LR backendService[backendSidecar]
            backendPHP[php:backend]
            backendPHP--generates-->backendLogs
        end
        subgraph LR monitorService[monitorSidecar]
            monitorNginx[nginx:monitor]
            monitorNginx--serves-->monitorLogs
            monitorNginx--serves-->backendLogs
        end
        subgraph LR frontendService[frontendInit]
            frontendNPM[node+npm]
            frontendAssets[assets]
            frontendStatic[static]
            frontendNPM--generates-->frontendAssets
            frontendAssets--copied to-->frontendStatic
        end

        subgraph LR mainService[main]
            main[nginx:main]

            main--proxies-->monitorNginx
            main--proxies-->backendPHP
            main--serves-->frontendStatic
        end
    end
```

## Thanks to
- https://favicon.io/emoji-favicons/rabbit/
- https://github.com/twbs/bootstrap

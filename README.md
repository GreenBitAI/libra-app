# Libra

[English](./README.md) | [中文](./README.zh-CN.md)

## Overview
The biggest differentiating capability of Libra.app compared to other AI Agent products is **localization**. The specific features and dependencies are as follows:
* **Chat Mode**: All chats are sent to the local model, requiring the download of a low-bit LLM model optimized for macOS by GreenBitAI, approximately `2.5GB`.
* **Enhanced Mode**: Capable of autonomously performing complex tasks such as file searching, web browsing, programming, charting, and report generation. To better protect user's local data and environment, these operations run in an isolated container environment, requiring the download of a container runtime environment, approximately `1GB` in size.

## FAQ

### Notes on Starting Libra.app

* When starting Libra.app for the first time, it will need to download the model, Agent runtime environment dependencies, etc. These are completed automatically during the startup process and do not require manual configuration by default.
* Currently, the download of these dependencies comes with global CDN acceleration, so you do not need to use any VPN proxy software to make it work.
* It is also recommended not to enable any VPN proxy, as this may affect the normal operation of Libra.app.
* If you encounter similar abnormal situations as described below, you can try to resolve them yourself according to the FAQ instructions, or try to contact the Libra.app technical team via Slack, GitHub, email, etc. for support.



## Issue Descriptions

### Local Mode Cannot Be Used
Error message: `Loading Local Model`

![](docs/_images/loading-local-model.png)

* Confirm if the local model has been downloaded:
```
du -hd0 ~/.cache/huggingface/hub/models--GreenBitAI--Qwen3-4B-Instruct-2507-layer-mix-bpw-4.0-mlx
```

If you see the following content, it indicates the local model has been downloaded correctly:
```
2.5G    /Users/libra/.cache/huggingface/hub/models--GreenBitAI--Qwen3-4B-Instruct-2507-layer-mix-bpw-4.0-mlx
```

Before starting, make sure that the relevant VPN proxy software does not have TUN mode or global mode enabled. This may affect the internal process communication of Libra.app.

Or you need to manually configure `localhost`, `127.0.0.1` outside the rules in your VPN software.

If you find that the local model still has not started, you can try restarting Libra.app and wait, and check whether the model has been downloaded correctly.

Alternatively, you can execute the following command to manually download the model:

```
HF_ENDPOINT=https://hf-mirror.com /Applications/Libra.app/Contents/Resources/bin/gbx_lm.bin --model GreenBitAI/Qwen3-4B-Instruct-2507-layer-mix-bpw-4.0-mlx 
```


### Cannot Click Execute Button
Error message: `Execution Engine is not fully ready`

![](docs/_images/execution-engine-not-fully-ready.png)


### Unable to Parse Uploaded PDF Files

Error message: `The file content is either empty`

![](docs/_images/the-file-content-is-either-empty.png)


* Confirm if the container runtime environment is ready:
```
/Applications/Libra.app/Contents/Resources/bin/limactl shell libra nerdctl images
```

If you see the following content, it indicates proper initialization:
```
REPOSITORY                              TAG       IMAGE ID        CREATED         PLATFORM       SIZE       BLOB SIZE
ghcr.gnbt.io/greenbitai/libra-runner    v0.6.9    b5c04942e7ec    18 hours ago    linux/arm64    1.785GB    566.9MB
docker.gnbt.io/mcp/markitdown           latest    a93f01634ef9    19 hours ago    linux/arm64    990.8MB    355.6MB
```

If you cannot see two similar records as above, you can try exiting all VPN proxy software and then restarting Libra.app.



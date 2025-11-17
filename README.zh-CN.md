# Libra

[English](./README.md) | [中文](./README.zh-CN.md)

## 概述
由于Libra.app相比其他同类AI Agent产品来说，最大差异化能力在于**本地化**，具体的特性和其依赖说明如下：
* **Chat模式**: Chat都会发送到本地模型，因此需要下载由GreenBitAI针对macOS优化的低比特LLM模型，大约`2.5G`左右。
* **Enhanced模式**：能自主的进行文件查找、联网搜索、编程绘图、报告生成等复杂指令，为了更好保护用户本地数据和环境，这里通过容器运行环境进行了隔离，因此需要下载容器运行环境，大约`1G`大小。

## FAQ

### 启动Libra.app注意事项

* 首次启动Libra.app会需要下载模型、Agent运行环境依赖组件等，这些是启动过程自动完成的，默认情况下不需要手动配置。
* 目前这些依赖的下载已经自带全球CDN加速，所以不需要使用任何VPN代理软件即可工作。
* 而且也建议不要开启任何VPN代理，这可能会影响Libra.app的正常工作。
* 如果碰到类似如下异常情况，可以尝试按照FAQ中的说明自行解决，或者尝试通过 slack, github, mail等方式给Libra.app的技术团队留言以获取支持。


## 现象说明

### Local模式无法使用
错误提示：`Loading Local Model`

![](docs/_images/loading-local-model.png)

* 确认本地模式是否下载完成：
```
du -hd0 ~/.cache/huggingface/hub/models--GreenBitAI--Qwen3-4B-Instruct-2507-layer-mix-bpw-4.0-mlx
```

看到如下内容则表明本地模型已经正确下载：
```
2.5G    /Users/libra/.cache/huggingface/hub/models--GreenBitAI--Qwen3-4B-Instruct-2507-layer-mix-bpw-4.0-mlx
```

启动之前需要确保相关的VPN代理软件不要开启 TUN 模式 、以及 全局模式。这可能会影响Libra.app内部的进程通信。

或者需要手动在您的VPN软件中，将`localhost`, `127.0.0.1`配置在规则之外。

如果发现本地模型仍然没有启动，您可以尝试重启Libra.app然后等待，并检查模型是否有正确下载。

或者您也可以执行如下命令，进行手动下载模型。

```
HF_ENDPOINT=https://hf-mirror.com /Applications/Libra.app/Contents/Resources/bin/gbx_lm.bin --model GreenBitAI/Qwen3-4B-Instruct-2507-layer-mix-bpw-4.0-mlx 
```


### 无法点击Execute按钮
错误提示：`Execution Engine is not fully ready`

![](docs/_images/execution-engine-not-fully-ready.png)


### 上传pdf等文件后无法解析

错误提示：`The file content is either empty`

![](docs/_images/the-file-content-is-either-empty.png)


* 确认容器运行环境是否就绪：
```
/Applications/Libra.app/Contents/Resources/bin/limactl shell libra nerdctl images
```

看到如下内容则表明已经正确初始化：
```
REPOSITORY                              TAG       IMAGE ID        CREATED         PLATFORM       SIZE       BLOB SIZE
ghcr.gnbt.io/greenbitai/libra-runner    v0.6.9    b5c04942e7ec    18 hours ago    linux/arm64    1.785GB    566.9MB
docker.gnbt.io/mcp/markitdown           latest    a93f01634ef9    19 hours ago    linux/arm64    990.8MB    355.6MB
```

如果无法看到类似上面的两行记录，您可以尝试退出所有VPN代理软件后，重启Libra.app代理。




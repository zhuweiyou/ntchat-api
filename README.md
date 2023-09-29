# ntchat-api

Docker中运行的微信机器人API

> 本项目主要是为了没有Windows Server服务器的用户使用ntchat搭建微信机器人, 仅支持 `linux/amd64`(不支持arm), 其它系统不保证能运行

## 文档

### 运行

```bash
docker run -d \
  --privileged \
  --security-opt seccomp=unconfined \
  --hostname="$(hostname)" \
  --env="RDP_SERVER=yes" \
  --publish="3389:3389/tcp" \
  --publish="8000:8000/tcp" \
  zhuweiyou/ntchat-api:latest
```

### 远程

使用 `Microsoft Remote Desktop` 远程连接 `ip:3389` 用户名和密码均为 `wineuser`

打开桌面的`Home`文件夹, 找到 `ntchat@0.1.13/fastapi_example/main.py` <del>双击运行它</del>(如果不行,则右击打开方式选择Open With Python)

```bash
# 你也可以用终端运行, 但实测终端界面运行容易卡死, 建议上面的方式运行
# 打开终端后:
cd ntchat@0.1.13/fastapi_example
wine python main.py
```

或者安装 pm2 之类的, 你喜欢的工具来运行

### 开发

查看API文档 <http://ip:8000/docs>

用你的程序或Postman请求:

1. POST <http://ip:8000/client/create> 获得 `guid` 存下来, 后续所有请求都带上

2. POST <http://ip:8000/client/open> 此时远程界面应该会自动启动WeChat.exe(PC微信进程)

```json
{
  "guid": "第1步获得的guid",
  "smart": true
}
```

3. POST http://ip:8000/global/set_callback_url

```json
{
  "guid": "第1步获得的guid",
  "callback_url": "你的程序接收消息回调的地址"
}
```

![远程桌面截图](https://github.com/zhuweiyou/ntchat-api/assets/8413791/9397f9a2-b871-4aa1-86f4-fb1acff4dfad)




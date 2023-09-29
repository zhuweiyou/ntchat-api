# ntchat-api

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

使用 Microsoft Remote Desktop 远程连接 `ip:3389`, 用户名和密码均为 `wineuser`

打开文件夹找到 `ntchat@0.1.13/fastapi_example/main.py`, 双击运行它

### 开发

本机浏览器打开 http://ip:8000/docs 查看 API 文档

用你的程序或 Postman 请求:

1. POST http://ip:8000/client/create 获得 guid 存下来, 后续所有请求都带上 guid (此时远程界面应该会自动启动 WeChat.exe)

2. POST http://ip:8000/client/open

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


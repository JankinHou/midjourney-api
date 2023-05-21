# midjourney-api

基于 Discord 的 Midjourney API。

使用教程参考：[Midjourney｜如何集成到自己的平台](https://mp.weixin.qq.com/s?__biz=Mzg4MjkzMzc1Mg==&mid=2247484029&idx=1&sn=d3c458bba9459f19f05d13ab23f5f67e&chksm=cf4e68eaf839e1fc2db025bd9940d0f5e57862f1788c88215b4a66cb23f553a30c5f37ac3ae8&token=79614426&lang=zh_CN#rd)


## UML

```mermaid
sequenceDiagram
    participant ThirdServer
    participant APIServer
    participant DiscordAPI

    ThirdServer->>APIServer: 请求接口传入提示词
    APIServer->>DiscordAPI: 调接口触发绘画任务
    APIServer-->>ThirdServer: 返回是否触发成功

    DiscordAPI->>DiscordAPI: 触发Midjourney bot绘画任务
    DiscordAPI->>DiscordAPI: 监听MidJourney bot消息
    DiscordAPI-->>APIServer: 返回监听实时消息

	APIServer-->>ThirdServer: 回调，传输结果
```


## 安装启动

```bash
git clone
pip install -r requirements.txt
```

将文件`.env.template`重命名为`.env`，并填入参数值：

```
USER_TOKEN=用户token
BOT_TOKEN=机器人token
GUILD_ID=服务器ID
CHANNEL_ID=频道ID
CALLBACK_URL=回调地址，默认http post请求
```

### 直接启动

```bash
# 启动监听机器人
python task_bot.py
# 启动http服务
python server.py
```

### docker 启动

填写 [start.sh](./start.sh) 环境变量，启动：

```bash
# 构建镜像
sh build.sh
# 启动容器
sh start.sh
```

接口`swagger`文档：[http://127.0.0.1:8062/docs](http://127.0.0.1:8062/docs)

`midjourney-api` 提供接口：

1. `/v1/api/trigger/bot`：触发绘画任务，已完成
2. `/v1/api/upload`：上传图片，触发任务，待开发


## 功能

- [x] 文生图
- [x] upscale
- [x] variation
- [x] reset
- [ ] 图生图

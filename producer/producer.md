
# Producer AI API 使用

## Producer AI 简介

Producer AI 是一款个人 AI 音乐代理工具，能够将您的想象力转化为音乐。其主要功能包括：

- 根据歌词文本和音频提示创作音乐。
- 使用覆盖、替换或扩展工具重混音频。
- 使用 Stem Swap 更改人声或伴奏，同时保持其他部分不变。

---

## 接入 API 步骤

### 步骤一：注册账户

1. 访问 [TTAPI 官网](https://ttapi.io)。
2. 点击右上方的 **SIGN IN**。
3. 支持邮箱注册、GitHub 或 Google 登录。
4. 注册成功后，您将获得 30 积分，可免费生成 10 首音乐。

### 步骤二：查看 API 文档

请访问 [Producer AI API 文档](https://ttapi.io/docs) 以获取详细的接口说明和使用指南。

### 步骤三：获取 API KEY

在注册并登录后，您可以在账户设置中找到并复制您的 API 密钥。

### 步骤四：调用生成音乐接口

使用以下 Python 代码示例调用生成音乐接口：

```python
import requests

endpoint = "https://api.ttapi.io/producer/v1/music"
headers = {
    "TT-API-KEY": "your_key"  # 替换为实际 API 密钥
}

data = {
    "title": "your_title",  # 替换为实际标题
    "lyrics_text": "your_lyrics_text",  # 替换为实际歌词内容
    "sound_prompt": "your_sound_prompt"  # 替换为实际音频提示
}

response = requests.post(endpoint, headers=headers, json=data)

print(f"Status Code: {response.status_code}")

if response.status_code == 200:
    try:
        data = response.json()
        print(data)
    except ValueError:
        print("Response is not in JSON format")
else:
    print(f"Request failed with status code {response.status_code}")
    print("Error message:", response.text)
```

**成功响应示例**：

```json
{
    "status": "SUCCESS",
    "message": "",
    "data": {
        "jobId": "ed1a1b01-7d64-4c8a-acaa-71185d23a2f3"
    }
}
```

### 步骤五：查询音乐

使用以下 Python 代码示例查询生成的音乐：

```python
import requests

endpoint = "https://api.ttapi.io/producer/v1/fetch?jobId=your_job_id"
headers = {
    "TT-API-KEY": "your_key"
}

response = requests.get(endpoint, headers=headers)

print(f"Status Code: {response.status_code}")

if response.status_code == 200:
    try:
        data = response.json()
        print(data)
    except ValueError:
        print("Response is not in JSON format")
else:
    print(f"Failed to fetch data. Error code: {response.status_code}")
```

**成功响应示例**：

```json
{
    "status": "SUCCESS",
    "message": "success",
    "data": {
        "jobId": "ed1a1b01-7d64-4c8a-acaa-71185d23a2f3",
        "action": "music",
        "progress": "100%",
        "mv": "FUZZ-2.0",
        "quota": "3",
        "musics": [
            {
                "musicId": "989b625f-c691-45d0-8eca-05e9bb0b59ee",
                "title": "your title",
                "lyrics": "your lyrics",
                "imageUrl": "https://img_url",
                "audioUrl": "https://audio_url",
                "videoUrl": null,
                "imageId": "989b625f-c691-45d0-8eca-05e9bb0b59ee",
                "topic": null,
                "sound": "your sound",
                "seed": "1680274481",
                "durations": "199.13433106575962",
                "createdAt": "2025-10-17T13:38:31.542817Z"
            }
        ]
    }
}
```

---

## 结语

以上内容介绍了如何使用 Producer AI API 接口生成音乐并查询结果。欲了解更多功能和详细信息，请查阅 [API 文档](https://ttapi.io/docs)。

---

# OpenAI格式（支持各大原厂模型）

更新时间：2026-04-15

这是 ApiHalo 默认推荐、也是最稳的公开接入方式。

只要 SDK、客户端或第三方工具支持 `OpenAI`、`OpenAI Compatible` 或 `Custom OpenAI`，都建议优先按本页接入。

## 一、适用范围

- 文本与对话
- 代码生成
- 多模态理解
- 文件分析
- Embeddings
- 图像生成
- 音频识别与合成
- 视频生成

## 二、接入前准备

接入前只需要 3 项核心信息：

| 配置项 | 推荐值 |
| --- | --- |
| API Key | 控制台创建的 ApiHalo API Key |
| Base URL | `https://apihalo.com/v1` |
| 模型名称 | 先通过 `/v1/models` 获取 |

```text
# 基础配置
Base URL = "https://apihalo.com/v1"
API Key = "你的 ApiHalo API Key"
Model = "请替换为 /v1/models 返回的真实模型 ID"
```

## 三、快速接入流程

### 第 1 步：先获取可用模型

```bash
curl https://apihalo.com/v1/models \
  -H "Authorization: Bearer YOUR_API_KEY"
```

使用原则：

- 只使用返回结果中的 `data[].id`
- 不要直接照搬其他平台模型名
- 可用模型以当前 Key 的返回结果为准

### 第 2 步：发起标准对话请求

```bash
curl https://apihalo.com/v1/chat/completions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_MODEL_ID",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "你好，请做一个自我介绍"}
    ]
  }'
```

### 第 3 步：如果需要流式输出

```bash
curl -N https://apihalo.com/v1/chat/completions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_MODEL_ID",
    "messages": [
      {"role": "user", "content": "请分段输出一篇短文"}
    ],
    "stream": true
  }'
```

## 四、多模态理解

如果目标模型支持多模态输入，可以继续使用 `POST /v1/chat/completions`。

常见内容类型包括：

- `text`
- `image_url`
- `input_audio`
- `file`
- `video_url`

### 图片理解示例

```bash
curl https://apihalo.com/v1/chat/completions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_MULTIMODAL_MODEL",
    "messages": [
      {
        "role": "user",
        "content": [
          {"type": "text", "text": "请描述这张图片"},
          {
            "type": "image_url",
            "image_url": {
              "url": "https://example.com/demo.jpg"
            }
          }
        ]
      }
    ]
  }'
```

### PDF / 文件分析示例

```bash
curl https://apihalo.com/v1/chat/completions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_FILE_MODEL",
    "messages": [
      {
        "role": "user",
        "content": [
          {"type": "text", "text": "请总结这个 PDF 的重点"},
          {
            "type": "file",
            "file": {
              "filename": "report.pdf",
              "file_data": "BASE64_PDF_DATA"
            }
          }
        ]
      }
    ]
  }'
```

说明：

- 文件理解能力不等于开放 `/v1/files`
- 公开接入不要把 `/v1/files` 当作前提

## 五、专项能力接入示例

### 1. Embeddings

```bash
curl https://apihalo.com/v1/embeddings \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_EMBEDDING_MODEL",
    "input": "ApiHalo embedding test"
  }'
```

### 2. 图像生成

```bash
curl https://apihalo.com/v1/images/generations \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_IMAGE_MODEL",
    "prompt": "a futuristic city at sunrise"
  }'
```

### 3. 音频转写

```bash
curl https://apihalo.com/v1/audio/transcriptions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -F "model=YOUR_AUDIO_MODEL" \
  -F "file=@/path/to/demo.mp3"
```

### 4. 视频生成

```bash
curl https://apihalo.com/v1/videos \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -F "model=YOUR_VIDEO_MODEL" \
  -F "prompt=A panda riding a bicycle in the rain"
```

查询任务：

```bash
curl https://apihalo.com/v1/videos/YOUR_TASK_ID \
  -H "Authorization: Bearer YOUR_API_KEY"
```

获取视频内容：

```bash
curl -L https://apihalo.com/v1/videos/YOUR_TASK_ID/content \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## 六、SDK 示例

### Python

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_API_KEY",
    base_url="https://apihalo.com/v1",
)

resp = client.chat.completions.create(
    model="YOUR_MODEL_ID",
    messages=[{"role": "user", "content": "你好"}],
)

print(resp.choices[0].message.content)
```

### Node.js

```javascript
import OpenAI from "openai";

const client = new OpenAI({
  apiKey: "YOUR_API_KEY",
  baseURL: "https://apihalo.com/v1",
});

const resp = await client.chat.completions.create({
  model: "YOUR_MODEL_ID",
  messages: [{ role: "user", content: "你好" }],
});

console.log(resp.choices[0].message.content);
```

## 七、最重要的注意事项

- 默认优先使用 `chat/completions`
- 图片、文件、音频、视频理解也优先考虑 `chat/completions` 多模态输入
- 高级参数如 `tools`、`tool_choice`、`response_format`、`reasoning` 都是按模型开放
- 模型、能力、可见范围始终以 `/v1/models` 返回结果为准

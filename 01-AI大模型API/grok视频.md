# grok视频

更新时间：2026-04-15

如果你的账号中已开放 Grok 系列的视频能力，请优先按标准视频接口接入。

## 推荐地址

```text
POST https://apihalo.com/v1/videos
```

## 请求示例

```bash
curl https://apihalo.com/v1/videos \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -F "model=YOUR_GROK_VIDEO_MODEL" \
  -F "prompt=A neon-lit future city in the rain"
```

## 查询任务

```bash
curl https://apihalo.com/v1/videos/YOUR_TASK_ID \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## 说明

- 是否存在可用的 Grok 视频模型，以 `/v1/models` 返回结果为准
- 如果模型未出现在你的可用模型列表里，请不要直接照搬别处文档中的模型名

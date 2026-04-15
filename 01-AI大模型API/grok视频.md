# grok视频

更新时间：2026-04-15

如果当前 Key 已开放 Grok 系列的视频能力，优先按标准视频接口接入。

## 一、适用场景

- Grok 系列视频生成
- 标准 OpenAI 兼容视频入口

## 二、推荐地址

```text
POST https://apihalo.com/v1/videos
```

## 三、请求示例

```bash
curl https://apihalo.com/v1/videos \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -F "model=YOUR_GROK_VIDEO_MODEL" \
  -F "prompt=A neon-lit future city in the rain"
```

## 四、查询任务

```bash
curl https://apihalo.com/v1/videos/YOUR_TASK_ID \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## 五、说明

- 是否存在可用的 Grok 视频模型，以 `/v1/models` 返回结果为准
- 如果模型未出现在当前可用模型列表中，请不要直接照搬其他文档中的模型名

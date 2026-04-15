# flux系列

更新时间：2026-04-15

Flux 系列通常作为图片生成模型使用。

## 推荐地址

```text
POST https://apihalo.com/v1/images/generations
```

## 请求示例

```bash
curl https://apihalo.com/v1/images/generations \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_FLUX_MODEL",
    "prompt": "an editorial fashion portrait in natural light"
  }'
```

## 使用建议

- 先从 `/v1/models` 中确认具体 Flux 模型 ID
- 如果模型支持额外图像参数，再按你的账号开放能力追加
- 如果你只需要统一图片生成入口，本页就是默认接法

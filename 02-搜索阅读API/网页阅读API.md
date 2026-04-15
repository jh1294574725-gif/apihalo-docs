# 网页阅读API

更新时间：2026-04-15

网页阅读能力建议理解为“已开通网页阅读能力的模型，通过标准聊天接口完成网页内容理解”。

ApiHalo 对外不要求你使用单独的专有网页接口，优先仍按标准聊天接口接入。

## 推荐地址

```text
POST https://apihalo.com/v1/chat/completions
```

## 最稳的调用方式

把需要阅读的网页地址直接写进提示词里，让已开通网页阅读能力的模型处理。

```bash
curl https://apihalo.com/v1/chat/completions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_WEB_READING_MODEL",
    "messages": [
      {
        "role": "user",
        "content": "请阅读这个网页并总结重点：https://example.com/article"
      }
    ]
  }'
```

## 使用前提

- 该模型必须已经对你的账号开放网页阅读能力
- 是否可用，以 `/v1/models` 和账号能力为准

## 注意事项

- 不要默认所有聊天模型都具备网页阅读能力
- 如果你的业务必须读取实时网页内容，请先做一次最小请求验证

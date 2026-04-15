# NanoBanana

更新时间：2026-04-15

NanoBanana 页面用于说明这类专项模型如何判断接入方式。

由于不同账号实际开放的 NanoBanana 模型能力可能不同，是否走图片接口、聊天接口或多模态接口，必须以你的模型列表为准。

## 先做什么

先拉取模型列表：

```bash
curl https://apihalo.com/v1/models \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## 怎么判断该走哪个接口

建议按下面顺序判断：

1. 先看该模型是否出现在 `/v1/models`
2. 再看返回里的 `supported_endpoint_types`
3. 再决定走哪类接口

常见情况：

- 如果是对话/多模态模型，优先走 `POST /v1/chat/completions`
- 如果是图片生成模型，优先走 `POST /v1/images/generations`
- 如果是仅专项开放模型，以你的控制台开放说明为准

## 最稳的做法

如果你不确定该模型的最佳端点，请优先使用：

- [OpenAI格式（支持各大原厂模型）](OpenAI格式（支持各大原厂模型）.md)
- [Models（列出模型）](../03-进阶与系统接口/Models（列出模型）.md)
- [支持矩阵](../03-进阶与系统接口/支持矩阵.md)

## 结论

NanoBanana 这类专项模型不要写死接入方式，必须跟着 `/v1/models` 的真实开放结果走。

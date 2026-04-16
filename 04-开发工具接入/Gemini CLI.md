# Gemini CLI

更新时间：2026-04-16

官方 Gemini CLI 当前不作为 ApiHalo 的可保证直连接入方式。

如果你要稳定调用 ApiHalo 上开放的 Gemini 系列模型，请优先使用：

- [谷歌Gemini接口](../01-AI大模型API/谷歌Gemini接口.md)
- [OpenAI格式（支持各大原厂模型）](../01-AI大模型API/OpenAI格式（支持各大原厂模型）.md)

## 一、为什么本页不再提供直连配置

对于官方 Gemini CLI，公开可确认的稳定接入方式仍然是 Google 官方认证链路。

因此，面向客户的可保证文档里，不再把“把 ApiHalo Base URL 填进官方 Gemini CLI”作为标准接法。

## 二、可保证方案 A：直接调用 Gemini 原生 HTTP 接口

### 第 1 步：先列出可用模型

```bash
curl "https://apihalo.com/v1beta/models?key=YOUR_API_KEY"
```

### 第 2 步：发起最小请求

```bash
curl "https://apihalo.com/v1beta/models/YOUR_MODEL_ID:generateContent" \
  -H "x-goog-api-key: YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "contents": [
      {
        "parts": [
          {"text": "Reply with OK only."}
        ]
      }
    ]
  }'
```

## 三、可保证方案 B：改用支持自定义网关的客户端

如果你的目标是命令行代理、代码助手或多轮聊天工具，请改用支持以下任一方式的客户端：

- 自定义 OpenAI Compatible 网关
- 自定义 Anthropic 网关
- 原生 HTTP Request

这类工具可继续参考：

- [OpenAI格式（支持各大原厂模型）](../01-AI大模型API/OpenAI格式（支持各大原厂模型）.md)
- [Claude Code](Claude%20Code.md)
- [其他工具](其他工具.md)

## 四、最重要的结论

- 不建议把官方 Gemini CLI 当成 ApiHalo 的标准客户接入方式
- 如果要稳定接 Gemini 系列模型，优先直接调用 ApiHalo 的 Gemini 原生 HTTP 接口
- 如果需要终端工具体验，请改用明确支持自定义网关的客户端

## 五、后续更换上游是否受影响

不受影响。

只要客户继续调用：

- ApiHalo 的域名
- ApiHalo 的 API Key
- ApiHalo 返回的模型 ID

那么客户侧仍然是对接 ApiHalo，而不是感知你后面的上游渠道变化。

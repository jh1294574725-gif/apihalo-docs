# Gemini CLI

更新时间：2026-04-15

如果你的 Gemini CLI 支持自定义 OpenAI 兼容入口，可直接按 OpenAI 兼容方式接入。

## 一、接入前准备

- ApiHalo API Key
- ApiHalo Base URL：`https://apihalo.com/v1`
- 一个来自 `GET /v1/models` 的真实模型 ID

## 二、快速接入

### 第 1 步：先获取模型

```bash
curl https://apihalo.com/v1/models \
  -H "Authorization: Bearer YOUR_API_KEY"
```

### 第 2 步：推荐填写

- Base URL：`https://apihalo.com/v1`
- API Key：ApiHalo API Key
- Model：从 `/v1/models` 返回结果中选择

如果 CLI 会自动拼接 `/v1`，Base URL 改填：

```text
https://apihalo.com
```

### 第 3 步：完成一次简单测试

建议先发送一条最小请求，确认可以正常返回内容。

## 三、可选方式

如果你的 CLI 明确要求 Gemini 原生协议，可参考：

- [谷歌Gemini接口](../01-AI大模型API/谷歌Gemini接口.md)

默认仍然建议优先使用 OpenAI 兼容入口。

# Claude Code IDE

更新时间：2026-04-15

本页适用于支持自定义 OpenAI 网关的 IDE 插件版 Claude Code。

## 一、接入前准备

- ApiHalo API Key
- ApiHalo Base URL
- 一个来自 `GET /v1/models` 的真实模型 ID

## 二、快速接入

### 第 1 步：先获取模型

```bash
curl https://apihalo.com/v1/models \
  -H "Authorization: Bearer YOUR_API_KEY"
```

### 第 2 步：在插件设置中填写

```text
# 基础配置
Base URL = "https://apihalo.com/v1"
API Key = "你的 ApiHalo API Key"
Model = "请替换为 /v1/models 返回的真实模型 ID"
```

### 第 3 步：保存并测试

保存配置后，建议先发送一个短请求验证连通性，例如：

```text
Reply with OK only.
```

## 三、常见问题

- 如果插件会自动拼接 `/v1`，Base URL 只填 `https://apihalo.com`
- 如果插件只接受固定官方供应商，请不要强行照搬本页

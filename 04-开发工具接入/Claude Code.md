# Claude Code

更新时间：2026-04-15

本页仅适用于支持自定义 `OpenAI Compatible` 或 `Custom OpenAI` 网关的 Claude Code 版本。

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

请选择当前 Key 可见的模型 ID，不要直接照搬其他平台的模型名称。

### 第 2 步：填写连接信息

不同版本界面字段名称可能略有差异，但填写原则一致：

```text
# 基础配置
Provider = "OpenAI Compatible"
Base URL = "https://apihalo.com/v1"
API Key = "你的 ApiHalo API Key"
Model = "请替换为 /v1/models 返回的真实模型 ID"
```

如果当前版本显示的是 `Custom OpenAI`、`Compatible` 或其他近似名称，按同义字段填写即可。

如果客户端会自动拼接 `/v1`，Base URL 改填：

```text
https://apihalo.com
```

### 第 3 步：完成一次简单测试

建议在客户端中发送一条简单消息，例如：

```text
Say OK only.
```

如果能正常返回内容，说明接入完成。

## 三、常见问题

### 1. 为什么模型名不能手填

因为 Claude Code 中使用的模型，必须与当前 Key 的 `/v1/models` 返回结果一致。

### 2. 如果当前版本不支持自定义 OpenAI 网关怎么办

当前版本如果只允许固定官方供应商，就不能直接按本页方式接入。

### 3. 为什么建议优先走 OpenAI Compatible

- 如果只是为了稳定接入，优先选择 OpenAI 兼容模式
- 如果当前版本不支持自定义 OpenAI 网关，请改用支持 OpenAI Compatible 的客户端或适配层

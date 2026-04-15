# Cline

更新时间：2026-04-15

Cline 一般按 `OpenAI Compatible` 方式接入。

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

### 第 2 步：填写 Cline 配置

不同版本的字段名称可能不同，但填写逻辑一致：

- API Provider：`OpenAI Compatible`
- Base URL：`https://apihalo.com/v1`
- API Key：ApiHalo API Key
- Model ID：从 `/v1/models` 返回结果里选择

如果客户端会自动拼接 `/v1`，Base URL 改填：

```text
https://apihalo.com
```

### 第 3 步：先做一次对话测试

建议先发送一条简单消息验证连通性：

```text
Reply with OK only.
```

## 三、推荐做法

- 第一次接入时，先用普通文本模型验证连通性
- 连通后再切换到代码模型或多模态模型

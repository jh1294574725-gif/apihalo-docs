# Claude Code

更新时间：2026-04-16

本页适用于官方 Claude Code 通过 Anthropic 兼容网关接入 ApiHalo。

如果你使用的是官方 Claude Code，请不要寻找 `OpenAI Compatible` 或 `Custom OpenAI` 配置项。Claude Code 走的是 Anthropic 网关协议，接入时应使用 Anthropic 风格环境变量。

## 一、接入前准备

- ApiHalo API Key
- ApiHalo 网关根地址：`https://apihalo.com`
- 一个来自 `GET /v1/models` 的真实模型 ID

说明：

- Claude Code 会自行请求 `POST /v1/messages`
- 因此 `ANTHROPIC_BASE_URL` 应填写根地址 `https://apihalo.com`
- 不要写成 `https://apihalo.com/v1`

## 二、先获取模型

```bash
curl https://apihalo.com/v1/models \
  -H "x-api-key: YOUR_API_KEY" \
  -H "anthropic-version: 2023-06-01"
```

请选择当前 Key 可见的真实模型 ID，不要直接照搬其他平台的模型名。

## 三、设置环境变量

### macOS / Linux

```bash
export ANTHROPIC_BASE_URL="https://apihalo.com"
export ANTHROPIC_API_KEY="YOUR_API_KEY"
export ANTHROPIC_MODEL="YOUR_MODEL_ID"
```

### Windows PowerShell

```powershell
$env:ANTHROPIC_BASE_URL="https://apihalo.com"
$env:ANTHROPIC_API_KEY="YOUR_API_KEY"
$env:ANTHROPIC_MODEL="YOUR_MODEL_ID"
```

## 四、启动 Claude Code

```bash
claude
```

建议第一次启动后先发送一条最小测试消息，例如：

```text
Reply with OK only.
```

如果能正常返回内容，说明接入完成。

## 五、如需先做接口连通性测试

如果希望先验证网关是否可通，可直接测试 Anthropic Messages 接口：

```bash
curl https://apihalo.com/v1/messages \
  -H "x-api-key: YOUR_API_KEY" \
  -H "anthropic-version: 2023-06-01" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_MODEL_ID",
    "max_tokens": 64,
    "messages": [
      {"role": "user", "content": "Reply with OK only."}
    ]
  }'
```

## 六、常见问题

### 1. 为什么 `ANTHROPIC_BASE_URL` 不能写成 `https://apihalo.com/v1`

因为 Claude Code 会在 `ANTHROPIC_BASE_URL` 后继续请求 `/v1/messages`。如果手动把 `/v1` 写进去，最终路径容易变成重复拼接。

### 2. 为什么这里不是 `Bearer Token`

因为 Claude Code 走的是 Anthropic 协议网关。对于 ApiHalo 的 Anthropic 兼容入口，应使用 Anthropic 风格认证。

### 3. 为什么模型必须来自 `/v1/models`

因为真正可见、可调用的模型范围，取决于当前 Key 的权限和开放范围。始终以 ApiHalo 返回结果为准。

### 4. 后面如果更换上游，这套接法还有效吗

只要继续使用：

- ApiHalo 的域名
- ApiHalo 的 API Key
- ApiHalo 返回的模型 ID

那么客户侧接入方式不需要跟着上游渠道重写。

# Codex

更新时间：2026-04-15

Codex CLI 与 Codex IDE Extension 推荐通过 `config.toml` 配置自定义 Provider 接入 ApiHalo。

Codex 自定义 Provider 使用的是 `Responses API`，因此接入前应先完成一次 `/v1/responses` 连通性验证。

## 适用范围

- Codex CLI
- Codex IDE Extension

## 接入前准备

请先准备以下信息：

- ApiHalo 的 `Base URL`
- ApiHalo 的 `API Key`
- 一个已经验证可用于 `Responses API` 的模型 ID

默认地址：

```text
https://apihalo.com/v1
```

## 第一步：获取可用模型

先调用：

```bash
curl https://apihalo.com/v1/models \
  -H "Authorization: Bearer YOUR_API_KEY"
```

选择模型时，建议优先满足以下条件：

- 该模型在当前 Key 下可见
- 适合代码、推理或多轮代理式任务
- 能通过下文的 `/v1/responses` 连通性测试

如果 `/v1/models` 返回数据中包含 `supported_endpoint_types` 字段，优先选择包含 `openai-response` 的模型。

## 第二步：先测试 `Responses API`

在写入 Codex 配置前，先用候选模型做一次测试：

```bash
curl https://apihalo.com/v1/responses \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_MODEL_ID",
    "input": "Reply with OK only."
  }'
```

判断方式：

- 如果返回正常 JSON，并包含响应内容，说明该模型可用于 Codex
- 如果返回模型不可用、参数不支持或接口错误，请更换模型后重新测试

这一步很重要，因为并不是所有模型都适合 `Responses API` 场景。

## 第三步：找到 `config.toml`

Codex 官方文档说明，用户级配置文件路径为：

```text
~/.codex/config.toml
```

如果你在项目内单独配置，也可以使用：

```text
.codex/config.toml
```

如果你使用的是 Codex IDE Extension，也可以在设置里直接打开 `config.toml`。

## 第四步：写入 ApiHalo Provider

把下面内容写入 `config.toml`：

```toml
model = "YOUR_MODEL_ID"
model_provider = "apihalo"

[model_providers.apihalo]
name = "ApiHalo"
base_url = "https://apihalo.com/v1"
wire_api = "responses"
env_key = "APIHALO_API_KEY"
env_key_instructions = "Set APIHALO_API_KEY in your environment"
```

说明：

- `model`：替换为你从 `/v1/models` 获取到的真实模型 ID
- `model_provider`：这里固定写成自定义 provider 名称，例如 `apihalo`
- `base_url`：填写 ApiHalo 的接口根地址
- `wire_api = "responses"`：Codex 自定义 provider 使用 `Responses API`
- `env_key`：表示让 Codex 从环境变量读取 ApiHalo Key

## 第五步：设置环境变量

### macOS / Linux

```bash
export APIHALO_API_KEY="YOUR_API_KEY"
```

如果希望长期生效，可写入 `~/.zshrc` 或 `~/.bashrc`。

### Windows PowerShell

```powershell
$env:APIHALO_API_KEY="YOUR_API_KEY"
```

## 第六步：启动 Codex

完成配置后重新启动 Codex。

如果配置正确，Codex 会通过 `apihalo` 这个自定义 provider 调用 ApiHalo。

## 完整示例

```toml
model = "YOUR_MODEL_ID"
model_provider = "apihalo"

[model_providers.apihalo]
name = "ApiHalo"
base_url = "https://apihalo.com/v1"
wire_api = "responses"
env_key = "APIHALO_API_KEY"
env_key_instructions = "Set APIHALO_API_KEY in your environment"
```

## 常见问题

### 1. 为什么要先测试 `/v1/responses`

因为 Codex 自定义 Provider 走的是 `Responses API`。先完成一次接口测试，能避免模型已经上架但不适合 Codex 场景的情况。

### 2. 为什么不是直接填 OpenAI 官方地址

因为你在这里接入的是 ApiHalo，不是 OpenAI 原站。

### 3. 为什么 `base_url` 要写成 `https://apihalo.com/v1`

因为 Codex 会基于这个地址去请求 `Responses API`，所以这里应直接填写 ApiHalo 的 `v1` 根路径。

### 4. 为什么要用 `wire_api = "responses"`

Codex 自定义 provider 的 `wire_api` 应使用 `responses`。

### 5. 为什么不能随便写模型名

因为 Codex 里填的模型，必须是你的 ApiHalo Key 当前真实可用的模型。

### 6. 如果 `/v1/models` 里没有明显标注 `openai-response` 怎么办

直接对目标模型做一次 `/v1/responses` 测试。只要测试通过，就可以继续接入 Codex。

## 使用建议

- 代码场景优先选择代码模型或推理模型
- 模型是否可用，始终以 `/v1/models` 返回结果与 `/v1/responses` 实测结果为准
- 如果后续更换模型，只需要替换 `model` 字段，不需要重写整套 Codex 接入配置

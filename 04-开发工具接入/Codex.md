# Codex

更新时间：2026-04-15

Codex CLI 与 Codex IDE Extension 推荐通过 `config.toml` 配置自定义 Provider 接入 ApiHalo。

Codex 自定义 Provider 使用的是 `Responses API`，因此接入前应先完成一次 `/v1/responses` 连通性验证。

## 适用范围

- Codex CLI
- Codex IDE Extension

## 一、接入前准备

在开始配置前，请先准备以下 3 项核心信息：

- ApiHalo API Key
- ApiHalo Base URL：`https://apihalo.com/v1`
- 一个已经验证可用于 `Responses API` 的模型 ID

建议先通过 `GET /v1/models` 获取可用模型，再对目标模型做一次 `POST /v1/responses` 测试。

### 模型获取方式

```bash
curl https://apihalo.com/v1/models \
  -H "Authorization: Bearer YOUR_API_KEY"
```

选择模型时，建议优先满足以下条件：

- 该模型在当前 Key 下可见
- 适合代码、推理或多轮代理式任务
- 能通过下文的 `/v1/responses` 连通性测试

如果 `/v1/models` 返回数据中包含 `supported_endpoint_types` 字段，优先选择包含 `openai-response` 的模型。

### Responses API 连通性测试

```bash
curl https://apihalo.com/v1/responses \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_MODEL_ID",
    "input": "Reply with OK only."
  }'
```

如果返回正常 JSON，并包含响应内容，说明该模型可用于 Codex。

## 二、快速接入指南

### 第 1 步：安装 Codex CLI

如果本机还没有安装 Codex CLI，可先执行：

```bash
npm install -g @openai/codex
```

安装完成后，可用以下命令检查是否安装成功：

```bash
codex --version
```

### 第 2 步：找到或创建 `config.toml`

Codex 官方推荐通过 `config.toml` 配置自定义 Provider。

常见位置如下：

```text
macOS / Linux: ~/.codex/config.toml
Windows: C:\Users\你的用户名\.codex\config.toml
项目目录: .codex/config.toml
```

如果文件不存在，直接创建即可。

### 第 3 步：写入 ApiHalo Provider 配置

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

参数说明：

- `model`：替换为你从 `/v1/models` 获取到的真实模型 ID
- `model_provider`：这里固定写成自定义 provider 名称，例如 `apihalo`
- `base_url`：填写 ApiHalo 的接口根地址
- `wire_api = "responses"`：Codex 自定义 provider 使用 `Responses API`
- `env_key`：表示让 Codex 从环境变量读取 ApiHalo Key

完成标准接入只需要以上这些核心字段。网络上如果看到其他示例带有额外配置项，请以你当前 Codex 版本的实际要求为准；在没有明确要求时，不需要额外补写。

### 第 4 步：设置环境变量

### macOS / Linux

```bash
export APIHALO_API_KEY="YOUR_API_KEY"
```

如果希望长期生效，可写入 `~/.zshrc` 或 `~/.bashrc`。

### Windows PowerShell

```powershell
$env:APIHALO_API_KEY="YOUR_API_KEY"
```

如果希望持久写入当前用户环境变量，可使用：

```powershell
[System.Environment]::SetEnvironmentVariable("APIHALO_API_KEY", "YOUR_API_KEY", "User")
```

### 第 5 步：启动并测试 Codex

完成配置后重新启动 Codex。

在项目目录中运行：

```bash
codex
```

如果配置正确，Codex 会通过 `apihalo` 这个自定义 provider 调用 ApiHalo。

建议第一次启动后先输入一条最小测试指令，例如：

```text
请简要概述当前仓库的目录结构。
```

## 三、在 VS Code 中使用扩展

Codex CLI 与 Codex IDE Extension 共用同一套底层配置。

只要已经完成：

- `config.toml` 配置
- `APIHALO_API_KEY` 环境变量设置

那么在 VS Code 中安装 Codex 扩展后，也可以直接复用这套配置。

## 四、完整示例

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

## 五、常见问题

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

### 7. 启动后提示认证失败怎么办

- 确认环境变量名是否为 `APIHALO_API_KEY`
- 确认环境变量值中没有手动加 `Bearer ` 前缀
- 如果是 Windows 持久环境变量，写入后请重新打开终端

### 8. 启动后提示模型不存在怎么办

- 检查 `config.toml` 中的 `model` 是否来自 `GET /v1/models`
- 不要直接填写其他平台展示的模型名

### 9. 接通了，但体验不稳定怎么办

- 优先确认目标模型是否适合 `Responses API`
- 确认 `wire_api = "responses"` 没有写错
- 如果更换模型后恢复正常，说明原模型并不适合 Codex 场景

## 使用建议

- 代码场景优先选择代码模型或推理模型
- 模型是否可用，始终以 `/v1/models` 返回结果与 `/v1/responses` 实测结果为准
- 如果后续更换模型，只需要替换 `model` 字段，不需要重写整套 Codex 接入配置

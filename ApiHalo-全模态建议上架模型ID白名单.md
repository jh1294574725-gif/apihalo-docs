# ApiHalo 全模态建议上架模型 ID 白名单

更新时间：2026-04-15

这份清单用于帮助你理解 ApiHalo 当前建议优先开放的模型家族与模型 ID。

客户实际可用模型，以 `GET https://apihalo.com/v1/models` 返回结果为准。

## 接口口径

- 文本与对话、代码、多模态、工具调用、文件处理：建议走 `/v1/chat/completions` 或 `/v1/responses`
- Embedding 向量：走 `/v1/embeddings`
- 图像生成：走 `/v1/images/generations`
- 音频识别与合成：走 `/v1/audio/transcriptions`、`/v1/audio/translations`、`/v1/audio/speech`
- 视频生成：走 `/v1/videos`
- 文件处理能力指“模型支持 PDF/文件输入”，不是开放 `/v1/files` 文件管理接口

## 1. 文本与对话模型

- `openai/gpt-5.4`
- `openai/gpt-4.1`
- `openai/gpt-4o`
- `anthropic/claude-sonnet-4.6`
- `anthropic/claude-opus-4.6`
- `google/gemini-2.5-pro`
- `google/gemini-2.5-flash`
- `deepseek/deepseek-v3.2`
- `deepseek/deepseek-chat-v3.1`
- `qwen/qwen3-max`
- `qwen/qwen3-32b`
- `mistralai/mistral-large-2512`
- `x-ai/grok-4.20`
- `moonshotai/kimi-k2.5`
- `z-ai/glm-5.1`

## 2. 代码模型

- `openai/gpt-5-codex`
- `qwen/qwen3-coder`
- `qwen/qwen3-coder-plus`
- `qwen/qwen3-coder-flash`
- `qwen/qwen3-coder-next`
- `mistralai/codestral-2508`
- `mistralai/devstral-medium`
- `mistralai/devstral-small`
- `x-ai/grok-code-fast-1`

## 3. Embedding 向量模型

- `openai/text-embedding-3-large`
- `openai/text-embedding-3-small`
- `google/gemini-embedding-001`
- `qwen/qwen3-embedding-8b`
- `qwen/qwen3-embedding-4b`
- `baai/bge-m3`
- `mistralai/mistral-embed-2312`
- `mistralai/codestral-embed-2505`

## 4. 图像模型

### 图像生成

- `openai/gpt-5-image`
- `openai/gpt-5-image-mini`
- `google/gemini-2.5-flash-image`
- `black-forest-labs/flux.2-pro`
- `black-forest-labs/flux.2-max`
- `black-forest-labs/flux.2-flex`
- `black-forest-labs/flux.2-klein-4b`
- `bytedance-seed/seedream-4.5`

### 图像理解

- `openai/gpt-4o`
- `openai/gpt-4.1`
- `anthropic/claude-sonnet-4.6`
- `google/gemini-2.5-pro`
- `qwen/qwen3-vl-32b-instruct`
- `meta-llama/llama-4-maverick`

## 5. 音频模型

### 语音识别 / 音频理解

- `openai/gpt-audio`
- `openai/gpt-audio-mini`
- `mistralai/voxtral-small-24b-2507`
- `google/gemini-2.5-pro`
- `google/gemini-2.5-flash`
- `xiaomi/mimo-v2-omni`

### 语音合成 / 音频输出

- `openai/gpt-audio`
- `openai/gpt-audio-mini`

## 6. 视频模型

### 视频生成

- `openai/sora-2-pro`
- `google/veo-3.1`
- `bytedance/seedance-2.0`
- `bytedance/seedance-2.0-fast`
- `bytedance/seedance-1-5-pro`
- `alibaba/wan-2.7`
- `alibaba/wan-2.6`

### 视频理解

- `google/gemini-2.5-pro`
- `google/gemini-2.5-flash`
- `qwen/qwen3.6-plus`
- `z-ai/glm-5v-turbo`
- `google/gemma-4-31b-it`

## 7. 多模态模型

- `google/gemini-2.5-pro`
- `google/gemini-2.5-flash`
- `google/gemini-2.5-flash-lite`
- `google/gemini-2.0-flash-001`
- `google/gemini-2.0-flash-lite-001`
- `xiaomi/mimo-v2-omni`
- `x-ai/grok-4.20`
- `openai/gpt-5.4`

## 8. 工具调用与 Agent 模型

- `openai/gpt-5.4`
- `openai/o3`
- `openai/o4-mini`
- `anthropic/claude-sonnet-4.6`
- `google/gemini-2.5-pro`
- `deepseek/deepseek-v3.2`
- `qwen/qwen3-max`
- `qwen/qwen3-coder`
- `x-ai/grok-4.20`
- `moonshotai/kimi-k2.5`
- `z-ai/glm-5.1`
- `minimax/minimax-m2.7`

## 9. 文件处理与数据分析模型

- `openai/gpt-5.4`
- `openai/gpt-5.4-mini`
- `openai/gpt-4.1`
- `openai/gpt-4o`
- `openai/o3`
- `google/gemini-2.5-pro`
- `google/gemini-2.5-flash`
- `anthropic/claude-sonnet-4.5`
- `anthropic/claude-opus-4.5`
- `x-ai/grok-4.20`

## 使用说明

- 这份清单是“建议首批上架”的具体模型 ID 白名单，不是 OpenRouter 全量模型清单。
- 同一个模型可以同时出现在多个分类中，这是正常现象。
- 如果你后续更换上游，只要新上游仍兼容 OpenAI 路由，并且这些模型 ID 继续存在，这份分类口径仍然成立。
- 对客户侧文档，最稳的写法依然是：“可用模型以 `/v1/models` 返回结果为准”。

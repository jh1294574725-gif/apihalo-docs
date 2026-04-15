# OpenCode

更新时间：2026-04-15

如果你的 OpenCode 客户端支持自定义 OpenAI 兼容入口，可按下面配置。

## 填写方式

- Provider：`OpenAI` / `Compatible`
- Base URL：`https://apihalo.com/v1`
- API Key：你的 ApiHalo Key
- Model：从 `/v1/models` 返回结果中选择

## 注意事项

- 如果模型切换后不可用，请重新拉取一次 `/v1/models`
- 不要写死上游平台模型名

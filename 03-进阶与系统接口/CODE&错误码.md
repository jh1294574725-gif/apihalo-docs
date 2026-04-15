# CODE&错误码

更新时间：2026-04-15

## 通用错误结构

OpenAI 兼容接口通常返回：

```json
{
  "error": {
    "message": "错误信息",
    "type": "new_api_error",
    "code": "具体错误码"
  }
}
```

## 常见 HTTP 状态

### 400

通常表示请求参数错误、字段缺失、请求体格式不正确。

### 401

通常表示：

- Key 错误
- Key 无效
- 未携带鉴权头

### 403

通常表示：

- Key 没有权限访问该能力
- 当前分组无权限
- 账号或 Key 被禁用

### 404

通常表示：

- 路径写错
- Base URL 写错
- 你把具体接口路径误填成了 Base URL

### 429

通常表示：

- 请求频率过高
- 触发速率限制

### 500 / 502 / 503

通常表示：

- 服务内部错误
- 临时处理异常
- 临时不可用

## 常见错误码

- `model_not_found`
- `access_denied`
- `bad_request_body`
- `insufficient_user_quota`
- `read_request_body_failed`
- `rate_limit_check_failed`

## 最常见的排查顺序

1. 先检查 `API Key`
2. 再检查 Base URL
3. 再检查模型名是否来自 `/v1/models`
4. 再检查请求体字段是否符合当前接口
5. 最后再看是否触发了能力限制或限流

## 特别提醒

如果你看到 `model_not_found`，不要第一时间怀疑平台故障，先确认：

- 模型是不是来自 ApiHalo 的 `/v1/models`
- 这个 Key 是否确实有权限访问该模型

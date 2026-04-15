# API Key

更新时间：2026-04-15

ApiHalo 所有接口都需要使用你在控制台生成的 `API Key` 进行鉴权。

## 获取方式

1. 登录 `https://apihalo.com/`
2. 进入控制台
3. 创建新的 `API Key`
4. 复制并妥善保存

## 标准鉴权方式

绝大多数接口都使用标准 `Bearer Token`：

```http
Authorization: Bearer YOUR_API_KEY
```

常见搭配请求头：

```http
Content-Type: application/json
```

## 安全建议

- 不要把 Key 写进前端源码
- 不要把 Key 提交到 Git 仓库
- 不要把 Key 出现在公开截图里
- 建议不同项目、不同环境使用不同 Key

## Key 泄露后怎么处理

如果怀疑泄露，请直接：

1. 删除旧 Key
2. 创建新 Key
3. 把业务配置切换到新 Key

## 第三方工具里怎么填

如果工具支持 `OpenAI` 或 `OpenAI Compatible`：

- `API Key` 填你的 ApiHalo Key
- `Base URL` 填 ApiHalo 地址
- `Model` 用 `/v1/models` 返回的模型 ID

## 特殊格式说明

少数原生协议页会用到其他头名，例如：

- Anthropic 格式会用 `x-api-key`
- Gemini 格式会用 `x-goog-api-key`

但它们本质上仍然填写的是你的 ApiHalo Key，不是上游原站 Key。

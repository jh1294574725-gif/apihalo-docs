# API Key

更新时间：2026-04-15

ApiHalo 所有公开接口都需要使用控制台生成的 `API Key` 进行鉴权。

## 一、API Key 是什么

`API Key` 是调用 ApiHalo 接口的凭证。无论调用的是文本、代码、图像、音频、视频还是开发工具接入，只要是公开接口，都需要先准备一个可用 Key。

## 二、如何获取 API Key

1. 登录 `https://apihalo.com/`
2. 进入控制台
3. 创建新的 `API Key`
4. 复制并妥善保存

建议不同用途拆分不同 Key，例如：

- 本地开发环境
- 测试环境
- 生产环境
- 第三方工具调用

## 三、标准鉴权方式

绝大多数 OpenAI 兼容接口都使用标准 `Bearer Token`：

```http
Authorization: Bearer YOUR_API_KEY
```

常见搭配请求头：

```http
Content-Type: application/json
```

## 四、第三方工具里怎么填写

如果工具支持 `OpenAI`、`OpenAI Compatible` 或 `Custom OpenAI`：

- `API Key` 填 ApiHalo API Key
- `Base URL` 填 ApiHalo Base URL
- `Model` 使用 `/v1/models` 返回的模型 ID

## 五、不同协议下的头名说明

少数原生协议页会使用不同头名，例如：

| 协议 | 头名 |
| --- | --- |
| OpenAI 兼容 | `Authorization: Bearer YOUR_API_KEY` |
| Anthropic 格式 | `x-api-key: YOUR_API_KEY` |
| Gemini 格式 | `x-goog-api-key: YOUR_API_KEY` |

虽然头名不同，但本质上仍然填写的是同一个 ApiHalo API Key。

## 六、安全建议

- 不要把 Key 写进前端源码
- 不要把 Key 提交到 Git 仓库
- 不要把 Key 出现在公开截图里
- 建议不同项目、不同环境使用不同 Key

## 七、如果怀疑 Key 泄露

建议立即执行以下操作：

1. 删除旧 Key
2. 创建新 Key
3. 把业务配置切换到新 Key
4. 检查历史日志、脚本、截图、环境变量是否仍然残留旧 Key

## 八、常见问题

### 1. 为什么已经有其他平台的 Key 了，还不能直接用

因为调用方真正接入的是 ApiHalo，所以必须使用 ApiHalo 控制台生成的 Key。

### 2. 为什么返回 401

常见原因包括：

- Key 写错
- 请求头缺少 `Bearer `
- Key 已失效、已删除、已禁用
- 使用了其他平台的 Key

# Base URL

更新时间：2026-04-15

`Base URL` 用于确定调用入口。对于大多数 OpenAI 兼容 SDK、插件和第三方工具，ApiHalo 的默认填写方式如下。

## 一、默认地址

ApiHalo 默认 OpenAI 兼容地址是：

```text
https://apihalo.com/v1
```

## 二、什么时候只填域名

如果 SDK、插件或客户端会自动补 `/v1`，则填写：

```text
https://apihalo.com
```

## 三、最常见的填写方式

| 场景 | 推荐填写 |
| --- | --- |
| OpenAI SDK | `https://apihalo.com/v1` |
| OpenAI Compatible 工具 | `https://apihalo.com/v1` |
| 会自动补 `/v1` 的客户端 | `https://apihalo.com` |

## 四、常见错误写法

以下写法都不建议：

- `https://apihalo.com/v1/`
- `https://apihalo.com/v1/chat/completions`
- `https://openrouter.ai/api/v1`

原因如下：

- Base URL 只填网关根地址，不要直接填某个具体接口路径
- 不要在公开接入中直接填写上游地址
- 如果路径写到了具体接口，很多 SDK 会继续再拼一次接口，导致请求失败

## 五、常用完整接口示例

- `GET https://apihalo.com/v1/models`
- `POST https://apihalo.com/v1/chat/completions`
- `POST https://apihalo.com/v1/embeddings`
- `POST https://apihalo.com/v1/images/generations`
- `POST https://apihalo.com/v1/audio/transcriptions`
- `POST https://apihalo.com/v1/videos`

## 六、结论

不确定时，优先填写：

```text
https://apihalo.com/v1
```

如果客户端明确说明“会自动拼接 `/v1`”，再改填：

```text
https://apihalo.com
```

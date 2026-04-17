---
title: "Web Search"
---

# Web Search

更新时间：2026-04-15

Web Search 能力默认也建议走标准聊天接口。

## 一、推荐地址

```text
POST https://apihalo.com/v1/chat/completions
```

## 二、最小示例

```bash
curl https://apihalo.com/v1/chat/completions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_SEARCH_MODEL",
    "messages": [
      {
        "role": "user",
        "content": "请联网搜索今天关于 AI 网关的主要新闻，并给出摘要"
      }
    ]
  }'
```

## 三、如果模型已开放工具调用

当且仅当目标模型已明确开放 `tools` 能力时，才建议在业务里启用工具调用或搜索工具参数。

## 四、注意事项

- Web Search 是按模型开放能力，不是所有模型默认可用
- 对生产业务，建议先做小流量验证，再正式上线

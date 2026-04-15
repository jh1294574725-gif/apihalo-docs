# Rerank重排序模型

更新时间：2026-04-15

Rerank 适用于搜索召回后的二次排序，是检索系统、知识库、RAG 场景中常用的后处理能力。

## 一、适用场景

- 站内搜索
- RAG 召回后二次排序
- FAQ 命中结果重排

## 二、请求地址

```text
POST https://apihalo.com/v1/rerank
```

## 三、请求示例

```bash
curl https://apihalo.com/v1/rerank \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_RERANK_MODEL",
    "query": "如何接入 ApiHalo",
    "documents": [
      "ApiHalo 支持 OpenAI Compatible 接入",
      "Rerank 用于对候选文档重新排序",
      "视频生成使用异步任务接口"
    ],
    "top_n": 2
  }'
```

## 四、最重要的注意事项

- 只有 Rerank 模型才能走本接口
- 不要把普通聊天模型直接当作 Rerank 模型使用
- 模型是否可用，以 `/v1/models` 返回结果为准

# 文生音乐Suno

更新时间：2026-04-15

本页仅适用于已开通 Suno 音乐生成能力的账号。

## 常用地址

- 提交任务：`POST /suno/submit/{action}`
- 查询全部：`POST /suno/fetch`
- 查询单个：`GET /suno/fetch/{id}`

## 常用 action

- `generate`
- `textGenerate`

## 提交示例

```bash
curl https://apihalo.com/suno/submit/generate \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "a bright electronic pop song about sunrise",
    "title": "Sunrise",
    "tags": "pop,electronic",
    "make_instrumental": false
  }'
```

## 查询任务

```bash
curl https://apihalo.com/suno/fetch/YOUR_TASK_ID \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## 说明

- Suno 是专项能力，不属于 OpenAI 标准端点
- 如果你的账号没有开通，接口会不可用

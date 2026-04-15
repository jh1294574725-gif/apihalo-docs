# Midjourney格式

更新时间：2026-04-15

本页仅适用于已开通 Midjourney 能力的账号。

这组接口不是 OpenAI 标准接口，请在确实需要 Midjourney 工作流时再使用。

## 一、适用场景

- Midjourney 文生图工作流
- Midjourney 动作扩展
- Midjourney 专项任务查询

## 二、常用接口

- 提交绘图：`POST /mj/submit/imagine`
- 查询任务：`GET /mj/task/{id}/fetch`

## 三、提交文生图

```bash
curl https://apihalo.com/mj/submit/imagine \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "a cinematic cyberpunk street at night"
  }'
```

## 四、查询任务

```bash
curl https://apihalo.com/mj/task/YOUR_TASK_ID/fetch \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## 五、常见扩展动作

如果账号已开通，可继续使用：

- `POST /mj/submit/action`
- `POST /mj/submit/change`
- `POST /mj/submit/describe`
- `POST /mj/submit/blend`
- `POST /mj/submit/video`

## 六、说明

- Midjourney 能力通常按账号开放，不是所有 Key 都默认可用
- 如果只是普通图片生成，优先看 [OpenAI格式（支持各大原厂模型）](OpenAI格式（支持各大原厂模型）.md) 和 [flux系列](flux系列.md)

# 通用视频生成API

更新时间：2026-04-15

如果当前 Key 已开通 OpenAI 兼容视频能力，优先使用本页。

## 一、适用场景

- 标准 OpenAI 兼容视频模型
- 文生视频
- 图生视频

## 二、基本调用流程

视频生成通常是异步任务，推荐流程如下：

1. 提交任务
2. 获取 `task_id`
3. 查询任务状态
4. 成功后获取视频内容

## 三、提交任务

```bash
curl https://apihalo.com/v1/videos \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -F "model=YOUR_VIDEO_MODEL" \
  -F "prompt=A calm sunrise over the ocean"
```

如果模型支持图生视频，可继续传参考图：

```bash
curl https://apihalo.com/v1/videos \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -F "model=YOUR_VIDEO_MODEL" \
  -F "prompt=A robot walking through the snow" \
  -F "input_reference=@/path/to/reference.jpg"
```

## 四、查询任务状态

```bash
curl https://apihalo.com/v1/videos/YOUR_TASK_ID \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## 五、获取视频内容

```bash
curl -L https://apihalo.com/v1/videos/YOUR_TASK_ID/content \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## 六、使用建议

- 标准 OpenAI 兼容视频模型优先使用本页
- 如果调用的是豆包专项视频能力，再看 [豆包系列-视频生成](豆包系列-视频生成.md)
- 视频生成通常是异步任务，不要按聊天接口理解

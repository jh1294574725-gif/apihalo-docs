# 文档OCR解析API

更新时间：2026-04-15

文档 OCR、图片 OCR、PDF 解析，公开接入时统一优先走多模态聊天接口。

## 一、推荐地址

```text
POST https://apihalo.com/v1/chat/completions
```

## 二、图片 OCR 示例

```bash
curl https://apihalo.com/v1/chat/completions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_OCR_MODEL",
    "messages": [
      {
        "role": "user",
        "content": [
          {"type": "text", "text": "请识别图片中的全部文字"},
          {
            "type": "image_url",
            "image_url": {
              "url": "https://example.com/receipt.jpg"
            }
          }
        ]
      }
    ]
  }'
```

## 三、PDF / 文件 OCR 示例

```bash
curl https://apihalo.com/v1/chat/completions \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_OCR_MODEL",
    "messages": [
      {
        "role": "user",
        "content": [
          {"type": "text", "text": "请提取表格并输出成 JSON"},
          {
            "type": "file",
            "file": {
              "filename": "invoice.pdf",
              "file_data": "BASE64_PDF_DATA"
            }
          }
        ]
      }
    ]
  }'
```

## 四、说明

- 公开接入不要依赖 `/v1/files`
- 文档解析能力是否可用，以模型和账号开通情况为准

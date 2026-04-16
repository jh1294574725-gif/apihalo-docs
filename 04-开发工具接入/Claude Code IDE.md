# Claude Code IDE

更新时间：2026-04-16

本页适用于本机 IDE 中运行的 Claude Code 集成，前提是该集成复用本机 Claude Code 安装与环境变量。

如果你的 IDE 插件只接受固定官方登录，或不读取本机 Claude Code 配置，请不要套用本页。

## 一、先完成 Claude Code 主配置

先按 [Claude Code](Claude%20Code.md) 页面完成本机配置，确保以下三项已经可用：

- `ANTHROPIC_BASE_URL`
- `ANTHROPIC_API_KEY`
- `ANTHROPIC_MODEL`

并且已经能在终端里正常运行：

```bash
claude
```

## 二、让 IDE 读取同一套配置

推荐做法：

1. 先在终端里确认 `claude` 可正常调用 ApiHalo
2. 再从同一台机器打开 IDE
3. 使用本机 Claude Code 集成或扩展

如果 IDE 需要选择 Claude Code 可执行文件，请填写本机 `claude` 命令对应的安装路径。

## 三、第一次连接建议

建议首次在 IDE 中执行一个最小请求，例如：

```text
Reply with OK only.
```

如果可以正常返回内容，说明 IDE 集成已经复用本机 Claude Code 的配置。

## 四、常见问题

### 1. 为什么这里不再填写 `Base URL`、`API Key`、`Model`

因为可保证的方式不是在 IDE 面板里手填 OpenAI 风格字段，而是让 IDE 复用已经配置好的本机 Claude Code。

### 2. 如果 IDE 里连不上，但终端里可以连上怎么办

通常说明 IDE 进程没有读取到同一组环境变量。请优先检查：

- IDE 是否运行在本机环境中
- IDE 是否能读取 `ANTHROPIC_BASE_URL`
- IDE 是否能读取 `ANTHROPIC_API_KEY`
- IDE 是否能读取 `ANTHROPIC_MODEL`

### 3. 后面如果更换上游，这页还有效吗

有效。

只要客户继续使用：

- ApiHalo 的域名
- ApiHalo 的 API Key
- ApiHalo 返回的模型 ID

IDE 侧仍然只需要复用 Claude Code 的本地配置，不需要感知上游变化。

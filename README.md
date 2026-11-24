# 会议助手（AI 参会 · 实时转写 · 纪要）

> 英文文档：[README.en.md](./README.en.md)

对标 [ai-meeting-workstation](https://github.com/hufeide/ai-meeting-workstation) 的产品形态，以若道桌面端功能插件实现：

- **双录音通道**：麦克风（我方发言）+ 系统内录（线上会议对方声音），并行采集、分别转写。
- **双转写通道**：云端（若道「模型管理」STT 绑定，OpenAI 兼容）与本地（本地 whisper / FunASR 的 OpenAI 兼容服务，如 faster-whisper-server），可随时切换；本地通道不联网。
- **AI 参会**：随时邀请 AI 参谋基于最近发言发言，观点作为「AI 参谋」写回会议时间线。
- **会后纪要**：一键生成结构化 Markdown 纪要（概要 / 讨论内容 / 结论决议 / 待办 / 风险）。
- **会议持久化**：全部会议记录保存在本机 `~/.ruodao-meeting-assistant/`（JSON），可导出 Markdown、可删除。
- **文件转写**：已有录音直接上传转写（≤200MB），写入独立会议记录。

## 命令

| 命令 | 用途 |
| --- | --- |
| 环境自检 | ffmpeg、麦克风/内录设备、云端/本地转写、LLM 配置检查 |
| 创建 / 列出 / 查看 / 结束 / 删除会议 | 会议记录管理 |
| 录音转写一段 | 实时会议核心循环：并行录麦克风+内录 → 转写 → 写回时间线 |
| 邀请 AI 参会发言 | 基于最近上下文生成发言稿 + 要点 |
| 推荐快捷话术 | 结合会议标题/背景/最近发言推荐 6 条可填入输入框的指令，不写会议时间线 |
| 生成会议纪要 | LLM 生成结构化 Markdown 纪要 |
| 录音文件转写 | 本地文件 → 云端/本地 STT → 新会议记录 |
| 导出会议 Markdown | 逐字稿 + 纪要导出为 .md |

## 配置（环境变量 / 工作台配置项）

| 变量 | 说明 |
| --- | --- |
| `RUODAO_AUDIO_DEVICE` | 麦克风设备名（dshow，与自检列表完全一致） |
| `RUODAO_SYSTEM_AUDIO_DEVICE` | 系统内录设备名；Windows 需启用「立体声混音」或安装 virtual-audio-capturer |
| `RUODAO_CAPTURE_SECONDS` | 每轮录音时长，默认 12（3–120） |
| `RUODAO_STT_CHANNEL` | `cloud`（默认）/ `local` |
| `RUODAO_STT_*` | 云端转写，由宿主「转写模型绑定」自动注入，无需手填 |
| `RUODAO_LOCAL_STT_BASE_URL` / `_API_KEY` / `_MODEL` | 本地 OpenAI 兼容转写服务（Key 通常留空） |
| `RUODAO_LLM_*` | 对话模型，由宿主「文本模型绑定」自动注入 |
| `RUODAO_MEETING_CONTEXT` | 会议主题与背景，拼进 AI 提示词 |
| `RUODAO_MEETING_ROLE` | AI 参谋人设，默认「资深会议参谋」 |

依赖：Node ≥ 18、ffmpeg（PATH）。

## 隐私说明

会议数据只保存在本机数据目录；音频临时文件在转写后立即删除。云端通道会把转写文本发送到你配置的 STT/LLM 服务；本地通道全程不出本机。

## 本地验证

```
node bin/meeting-assistant.mjs doctor
node test/plugin.test.mjs
```
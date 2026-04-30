# Claudian OpenCode

> 将 [OpenCode](https://github.com/opencode-ai/opencode) 嵌入 Obsidian，让你的仓库成为 AI 编程代理的工作目录。

[English](README_EN.md) | **中文**

---

## 概述

**Claudian OpenCode** 是一款 Obsidian 桌面插件，将 AI 编程代理（OpenCode）直接集成到你的 Obsidian 仓库中。你的 Obsidian 仓库成为 AI 代理的工作目录，使其能够执行文件编辑、搜索、Shell 命令和多步骤工作流。

可选支持 [Codex](https://github.com/openai/codex) 作为备选 AI 提供商。

## 功能

- **AI 聊天面板** — 在 Obsidian 内与 AI 代理进行对话
- **多标签页会话** — 同时管理多个独立对话
- **工具调用可视化** — 实时查看 AI 执行的文件编辑、Shell 命令等操作
- **思考过程展示** — 展开/折叠 AI 的推理过程
- **文件上下文管理** — 将笔记作为上下文附加到对话中
- **图片附件** — 在对话中附加并预览图片
- **状态面板** — 实时查看待办事项和 Bash 输出
- **对话历史** — 保存、恢复和管理历史会话
- **内联编辑** — 在编辑器中直接请求 AI 修改选中文本
- **BangBash 模式** — 在输入框输入 `!` 直接执行 Shell 命令
- **MCP 服务器** — 配置和管理 MCP 工具服务器
- **环境变量管理** — 管理 API 密钥和其他环境变量
- **多提供商支持** — OpenCode 为主提供商，Codex 为可选项
- **国际化** — 支持多语言界面

## 安装

### 从 BRAT 安装（推荐）

1. 安装 [BRAT](https://obsidian.md/plugins?id=obsidian42-brat) 插件
2. 在 BRAT 设置中添加 `yudu-steven/Codian`
3. 启用 `Claudian OpenCode` 插件

### 手动安装

1. 从 [Releases](https://github.com/yudu-steven/Codian/releases) 下载 `main.js`、`manifest.json` 和 `styles.css`
2. 将文件放入 `<vault>/.obsidian/plugins/claudian/`
3. 在 Obsidian 设置中启用插件

## 前提条件

- **OpenCode**: 需要安装 [OpenCode CLI](https://github.com/opencode-ai/opencode)
- **Node.js**: OpenCode 依赖 Node.js 运行时

## 配置

在 Obsidian 设置中找到 **Claudian OpenCode** 选项卡：

### 基本设置

| 设置 | 说明 |
|------|------|
| 提供商 | 选择 AI 提供商（OpenCode / Codex） |
| 模型 | 选择 AI 模型 |
| 权限模式 | `yolo`（自动执行）/ `normal`（需要确认） |
| 思考预算 | 控制 AI 推理深度 |
| 努力级别 | 控制 AI 执行强度 |

### 环境变量

在 **环境变量** 区域配置 API 密钥：

```bash
ANTHROPIC_API_KEY=sk-ant-...
OPENAI_API_KEY=sk-...
OPENCODE_SERVER_PASSWORD=your-password
```

> **安全提示**: 敏感值（API 密钥、密码）存储在 `.claudian/claudian-settings.json` 中，并使用 AES-256-GCM 加密。加密密钥从仓库名称派生，储存在同一机器上的文件即使被同步到云端也无法解密。

### MCP 服务器

在 **MCP 服务器** 区域添加工具服务器：

- **stdio**: 本地命令（如 `docker exec -i mcp-server python -m src.server`）
- **SSE**: 服务器推送事件端点
- **HTTP**: HTTP 端点

## 使用

### 基本对话

1. 点击左侧功能区的新建聊天图标
2. 在输入框中输入消息，按 `Enter` 发送
3. AI 将执行工具操作并返回结果

### 快捷命令

| 命令 | 操作 |
|------|------|
| `/new` 或 `/clear` | 开始新对话 |
| `!`（空输入时） | 进入 BangBash Shell 模式 |
| `/add-dir <路径>` | 添加目录到上下文 |
| `/help` | 查看所有命令 |

### 内联编辑

1. 在编辑器中选中文本
2. 点击出现的编辑浮动按钮
3. 输入修改指令，AI 将展示差异对比
4. 一键接受或拒绝修改

### 键盘导航

| 按键 | 功能 |
|------|------|
| `w` / `s`（默认） | 消息列表上下滚动 |
| `i`（默认） | 聚焦到输入框 |
| `Escape` | 退出 BangBash 模式 / 关闭弹窗 |
| `Enter` | 发送消息 / 执行命令 |
| `Shift+Enter` | 输入框内换行 |

## 安全

本项目重视安全。关于已修复漏洞的详细信息，请参阅 [安全修复日志](https://github.com/yudu-steven/Codian/commits/main)。

### 已知的安全措施

- 敏感环境变量使用 AES-256-GCM 加密存储
- BangBash 模式增加了危险命令确认弹窗
- Diff HTML 输出经过脚本注入过滤
- 图片 MIME 类型白名单验证（拒绝 SVG）
- MCP 服务器命令有安全警告
- 临时会话数据在使用后自动清理

## 开发

```bash
# 构建（需要 TypeScript 源码）
npm install
npm run build
```

## 许可证

[MIT](LICENSE)

## 作者

- **Yishen Tu** — [GitHub](https://github.com/YishenTu)

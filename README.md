# yt-dlp-agent

🤖 **AI Agent 驱动的 YouTube 智能下载工具**

通过编写详细的 Agent SOP 文档（Standard Operating Procedures），让 AI 编码助手（Claude Code、Cursor、Windsurf 等）能够理解你的自然语言指令，自动完成 YouTube 视频下载、格式选择、文件管理等复杂任务。

**核心理念**：你只需说"下载这个视频"，AI Agent 会自动处理一切细节。

---

## ✨ 项目亮点

这个项目的核心**不是** yt-dlp 本身，而是：

1. **📝 精心设计的 Agent SOP 文档**（`CLAUDE.md`/`AGENTS.md`/`GEMINI.md`）
   - 定义了 AI Agent 的完整工作流程
   - 智能决策规则（格式选择、清理策略）
   - 最小交互原则（智能默认行为）

2. **🗣️ 自然语言操作**
   - 不需要记忆命令行参数
   - 不需要手动管理文件
   - 用人类语言描述需求即可

3. **🧠 AI 智能决策**
   - 自动判断内容类型（技术教程 vs 新闻娱乐）
   - 自动选择格式（MP4 视频 vs MP3 音频）
   - 自动清理同频道旧文件（保留当天下载）

---

## 🚀 快速开始

### 1. 克隆项目

```bash
git clone https://github.com/demon2036/yt-dlp-agent.git
cd yt-dlp-agent
```

### 2. 安装依赖

```bash
# 安装 yt-dlp
pip install yt-dlp

# 或使用系统包管理器
brew install yt-dlp  # macOS
sudo apt install yt-dlp  # Ubuntu/Debian
```

### 3. 配置 AI 编码助手

选择你喜欢的 AI 工具，按照下面的说明配置：

#### 🔹 Claude Code

1. 安装 [Claude Code](https://claude.ai/code)
2. 在项目根目录打开 Claude Code
3. **自动读取**：Claude Code 会自动识别 `CLAUDE.md` 文件
4. 直接用自然语言操作即可！

```bash
# 在项目目录下启动 Claude Code
cd yt-dlp-agent
claude-code
```

#### 🔹 Cursor

1. 安装 [Cursor](https://cursor.sh/)
2. 打开项目文件夹
3. 配置 `.cursorrules` 或在 Cursor 设置中添加：
   ```
   Read and follow the instructions in AGENTS.md for YouTube download operations.
   ```
4. 使用 Ctrl/Cmd + K 或 Chat 功能与 AI 交互

#### 🔹 Windsurf (Codeium)

1. 安装 [Windsurf](https://codeium.com/windsurf)
2. 打开项目
3. Windsurf 会自动读取项目中的 markdown 文档
4. 在 Chat 面板中输入指令

#### 🔹 Gemini Code Assist

1. 使用支持 Gemini 的编辑器（VS Code + Gemini 插件）
2. 打开项目
3. **手动引用**：在对话中提到 `GEMINI.md`
4. 或在 AI 配置中添加系统提示：
   ```
   Follow the instructions in GEMINI.md for YouTube download tasks.
   ```

---

## 💬 使用示例

配置好 AI 工具后，用自然语言操作：

### 示例 1：下载单个视频

```
你：下载这个视频：https://youtube.com/watch?v=xxxxx

AI：[自动分析]
    • 检测频道：新闻频道
    • 内容类型：新闻评论
    • 格式决策：MP3（音频）
    • 清理策略：删除该频道旧文件（保留今天下载的）

    [执行下载...]

    ✅ 完成！
    📁 新闻频道-NA/
       • 今日热点新闻解读.mp3 ✓ 新下载
       • [已清理 3 个旧文件]
```

### 示例 2：下载技术教程

```
你：下载这个 Docker 教程：https://youtube.com/watch?v=yyyyy

AI：检测到"Docker"关键词，判断为技术教程
    格式决策：MP4（视频，需要看操作演示）

    [执行下载...]

    ✅ 完成！
    📁 技术频道-NA/
       • Docker容器化实战教程.mp4 ✓ 新下载
```

### 示例 3：批量下载

```
你：下载这3个视频：
    https://youtube.com/watch?v=aaa
    https://youtube.com/watch?v=bbb
    https://youtube.com/watch?v=ccc

AI：[批量处理 3 个 URL...]
    [自动判断格式...]
    [执行下载...]
    [清理旧文件...]

    ✅ 完成！3 个视频已下载
```

### 示例 4：保留旧文件

```
你：下载这个，保留旧的

AI：收到，只下载新视频，不删除该频道的旧文件。
    [执行下载...]
```

---

## 🛠️ 支持的 AI 工具对比

| AI 工具 | SOP 文档 | 自动读取 | 配置难度 | 推荐度 |
|---------|---------|---------|---------|--------|
| **Claude Code** | `CLAUDE.md` | ✅ 自动 | ⭐ 简单 | ⭐⭐⭐⭐⭐ |
| **Cursor** | `AGENTS.md` | ⚠️ 需配置 `.cursorrules` | ⭐⭐ 中等 | ⭐⭐⭐⭐ |
| **Windsurf** | `AGENTS.md` | ✅ 自动 | ⭐ 简单 | ⭐⭐⭐⭐ |
| **Gemini** | `GEMINI.md` | ⚠️ 需手动引用 | ⭐⭐⭐ 较难 | ⭐⭐⭐ |

**推荐**：如果你有 Claude Code 访问权限，这是最佳选择（自动读取 SOP，零配置）。

---

## 📖 工作原理

### Agent SOP 文档

项目包含三个 SOP 文档（都指向同一内容）：

- **`CLAUDE.md`**：Claude Code 专用
- **`AGENTS.md`**：通用 AI Agent（Cursor、Windsurf 等）
- **`GEMINI.md`**：Google Gemini 专用

这些文档定义了：

1. **智能意图理解**
   - 预检 URL，获取频道和标题信息
   - 关键词匹配判断内容类型

2. **格式决策规则**
   ```python
   技术关键词 = ["Docker", "Kubernetes", "编程", "Code", "教程", "Python", ...]
   娱乐关键词 = ["新闻", "热线", "评论", "动漫", "电影", ...]

   if 标题包含技术关键词:
       格式 = MP4  # 需要看画面
   else:
       格式 = MP3  # 只需听
   ```

3. **清理策略**
   - ✅ 下载新视频时，自动清理同频道旧视频
   - ✅ **保留当天下载的所有文件**（按自然日判断）
   - ✅ 不同频道互不影响
   - ✅ 用户说"保留旧的"时不清理

4. **操作流程**
   ```
   步骤0: 预检URL → 获取频道/标题
   步骤1: 扫描当前文件
   步骤2: 通知用户即将做什么
   步骤3: 执行下载
   步骤4: 自动清理旧文件
   步骤5: 简洁报告结果
   ```

### 为什么这样设计？

**核心哲学**：智能默认 + 最小交互

> "最好的交互是没有交互。系统应该足够智能，理解用户真实意图。"

- **99% 的场景**：用户要新的，不要旧的 → 默认清理
- **1% 的场景**：用户要保留旧的 → 明确说"保留旧的"

避免每次都问用户一堆选择题，AI 应该自己做出合理决策。

---

## 🔧 手动使用（可选）

如果你不想用 AI Agent，也可以直接运行脚本：

```bash
# 下载音频（MP3）
python3 main2.py <YouTube_URL>

# 下载视频（MP4，含字幕）
python3 main2.py -v <YouTube_URL>

# 批量下载
python3 main2.py <URL1> <URL2> <URL3>

# 不使用代理
python3 main2.py --no-proxy <YouTube_URL>
```

但这样你需要：
- ❌ 手动决定下载音频还是视频
- ❌ 手动管理旧文件清理
- ❌ 记忆命令行参数

**建议**：使用 AI Agent，体验自动化的魅力！

---

## 📁 输出目录结构

```
yt_dlp/
├── 新闻频道-NA/
│   ├── 01 今日时事评论.mp3
│   ├── 02 热点新闻解读.mp3
│   └── ...
├── 技术频道-NA/
│   ├── 01 Docker容器化教程.mp4
│   ├── 02 Kubernetes实战.mp4
│   └── ...
└── 动漫频道-NA/
    ├── 01 第1471话.mp3
    └── ...
```

文件按**频道自动分类**，文件名包含**序号和标题**。

---

## ⚙️ 配置说明

### 代理配置

默认使用 `socks5://127.0.0.1:1089/`

修改 `main2.py` 第 39 行：

```python
cmd.append("--proxy socks5://YOUR_PROXY_HOST:PORT/")
```

### Cookie 认证

默认从 Firefox 读取 Cookie（用于访问需要登录的视频）

修改 `main2.py` 第 23 行：

```python
"--cookies-from-browser chrome"  # 或 edge, safari
```

### 下载路径模板

默认路径：`yt_dlp/频道名-NA/序号 标题.扩展名`

修改 `main2.py` 第 22 行自定义。

---

## 🧪 项目结构

```
.
├── README.md           # 项目文档（本文件）
├── CLAUDE.md           # Claude Code Agent SOP
├── AGENTS.md           # 通用 Agent SOP（→ CLAUDE.md）
├── GEMINI.md           # Gemini Agent SOP（→ CLAUDE.md）
├── main2.py            # 下载脚本
├── .gitignore          # Git 忽略配置
└── yt_dlp/             # 下载目录（不提交到 Git）
    ├── 频道A-NA/
    └── 频道B-NA/
```

---

## ❓ 常见问题

### Q: 我应该用哪个 AI 工具？

**A**: 推荐顺序：
1. **Claude Code**（最佳，自动读取 SOP，零配置）
2. **Windsurf**（次佳，自动读取文档）
3. **Cursor**（需要配置 `.cursorrules`）
4. **Gemini**（需要手动引用文档）

### Q: 如何让 AI 不删除旧文件？

**A**: 在指令中明确说明：
```
下载这个，保留旧的
```

或：
```
只下载不删除
```

### Q: 如何强制下载视频格式？

**A**: 在指令中提到 "mp4" 或 "视频"：
```
下载这个，要 mp4 格式
```

### Q: AI Agent 无法识别 SOP 文档？

**A**: 检查以下几点：
1. 确认 AI 工具在项目根目录运行
2. 确认对应的 `.md` 文件存在
3. 对于 Cursor，检查 `.cursorrules` 配置
4. 对于 Gemini，手动在对话中提到文档名

### Q: 如何查看 AI 的决策过程？

**A**: AI Agent 会输出决策信息：
```
🔎 智能判断
   • 内容类型：新闻评论
   • 格式决策：MP3（音频）
   • 清理策略：删除该频道旧文件（保留今天下载的）
```

### Q: 能否自定义关键词规则？

**A**: 可以！编辑 `CLAUDE.md`（或对应的 SOP 文档），修改关键词列表：

```python
TECH_KEYWORDS = [
    "Docker", "Kubernetes", "编程", ...
    # 添加你的自定义关键词
]
```

然后告诉 AI："重新读取 CLAUDE.md"。

---

## 🎯 设计哲学

本项目受 **Linus Torvalds** 的编程哲学启发：

1. **Good Taste（好品味）**
   - 让正确的事情自然发生
   - 通过良好的默认规则，消除特殊情况

2. **Pragmatism（实用主义）**
   - 为 99% 的场景优化默认行为
   - 1% 的特例用明确指令覆盖

3. **Simplicity（简洁性）**
   - 最好的交互是没有交互
   - 系统应该足够智能，理解用户意图

详见 `CLAUDE.md` 中的"哲学思考"章节。

---

## 🤝 贡献指南

欢迎贡献！你可以：

1. **改进 Agent SOP 文档**
   - 优化决策规则
   - 添加新的使用场景
   - 改进提示语

2. **支持更多 AI 工具**
   - 为其他 AI 编码助手编写配置指南
   - 测试兼容性

3. **增强下载功能**
   - 改进 `main2.py` 脚本
   - 添加新功能（字幕处理、画质选择等）

4. **报告问题**
   - 提交 Issue 描述 AI Agent 的异常行为
   - 分享你的使用经验

---

## 📄 许可证

MIT License

---

## 🙏 致谢

- [yt-dlp](https://github.com/yt-dlp/yt-dlp) - 强大的 YouTube 下载工具
- [Claude Code](https://claude.ai/code) - 启发了本项目的 AI Agent 设计
- [Cursor](https://cursor.sh/) - 优秀的 AI 编码工具
- [Windsurf](https://codeium.com/windsurf) - 创新的 AI 编程助手

---

## 📬 联系方式

如有问题或建议，欢迎提交 [Issue](https://github.com/demon2036/yt-dlp-agent/issues)。

---

**记住**：这不是一个简单的下载脚本，而是一个展示 **AI Agent 自动化能力** 的示例项目。通过精心设计的 SOP 文档，让 AI 成为你的智能助手！

# YouTube 智能下载工具

基于 `yt-dlp` 的智能 YouTube 视频下载工具，支持音频/视频批量下载，并集成了 AI Agent 自动化管理。

## 功能特性

- **智能格式选择**：根据内容类型自动选择 MP3（音频）或 MP4（视频）
- **批量下载**：支持同时下载多个视频
- **代理支持**：内置 SOCKS5 代理配置
- **自动分类**：按频道自动组织下载文件
- **智能清理**：自动清理同频道旧文件（保留当天下载）
- **AI Agent 集成**：通过 Claude Code 实现自动化操作

## 安装要求

### 依赖软件

```bash
# 安装 yt-dlp
pip install yt-dlp

# 或使用系统包管理器
# Ubuntu/Debian
sudo apt install yt-dlp

# macOS
brew install yt-dlp
```

### 可选依赖

- **Firefox**：用于 Cookie 认证（访问需要登录的视频）
- **SOCKS5 代理**：如需翻墙访问（默认 127.0.0.1:1089）

## 使用方法

### 基本用法

```bash
# 下载音频（MP3 格式）
python3 main2.py <YouTube_URL>

# 下载多个视频的音频
python3 main2.py <URL1> <URL2> <URL3>

# 下载视频（MP4 格式，含字幕）
python3 main2.py -v <YouTube_URL>

# 不使用代理
python3 main2.py --no-proxy <YouTube_URL>
```

### 命令行参数

| 参数 | 说明 |
|------|------|
| `urls` | 一个或多个视频 URL（必需） |
| `-v, --video` | 下载视频格式（默认下载音频） |
| `--no-proxy` | 不使用代理（默认使用 SOCKS5 代理） |

### 输出目录结构

```
yt_dlp/
├── 频道名称-NA/
│   ├── 01 视频标题1.mp3
│   ├── 02 视频标题2.mp3
│   └── ...
└── 另一个频道-NA/
    ├── 01 视频标题A.mp4
    └── ...
```

## AI Agent 集成

本项目集成了智能 AI Agent 自动化流程，支持通过 **Claude Code** 进行智能操作。

### 特性

1. **智能意图理解**：自动识别内容类型（技术教程 vs 娱乐新闻）
2. **自动格式决策**：
   - 技术类内容 → MP4（需要看画面）
   - 新闻/娱乐类 → MP3（只需听）
3. **自动清理策略**：下载新视频时自动清理同频道旧文件（保留当天下载）
4. **最小交互原则**：智能默认行为，减少用户决策负担

### Agent 使用方式

在 Claude Code 中直接使用自然语言：

```
# 示例 1：下载新闻类视频
"下载这个视频：<URL>"
→ AI 自动判断为新闻类，下载 MP3，清理旧文件

# 示例 2：下载技术教程
"下载这个 Docker 教程：<URL>"
→ AI 识别为技术类，下载 MP4

# 示例 3：保留旧文件
"下载这个，保留旧的"
→ 只下载，不清理

# 示例 4：批量下载
"下载这 3 个视频：<URL1> <URL2> <URL3>"
→ 批量下载，自动清理
```

详细的 Agent SOP 请参考 [CLAUDE.md](./CLAUDE.md)

## 配置说明

### 代理配置

默认代理地址：`socks5://127.0.0.1:1089/`

修改代理地址：编辑 `main2.py` 第 39 行

```python
cmd.append("--proxy socks5://YOUR_PROXY_HOST:PORT/")
```

### Cookie 认证

默认从 Firefox 浏览器读取 Cookie。如需使用其他浏览器：

```python
# Chrome
"--cookies-from-browser chrome"

# Edge
"--cookies-from-browser edge"
```

### 下载路径模板

默认路径模板（第 22 行）：

```python
'yt_dlp/%(uploader)s-%(playlist).20s/%(playlist_index)02d %(title).60s.%(ext)s'
```

格式说明：
- `%(uploader)s`：上传者（频道名）
- `%(playlist).20s`：播放列表（截取 20 字符）
- `%(playlist_index)02d`：播放列表序号（2 位数字）
- `%(title).60s`：视频标题（截取 60 字符）
- `%(ext)s`：文件扩展名

## 项目结构

```
.
├── README.md           # 项目说明文档
├── CLAUDE.md           # AI Agent 操作流程（SOP）
├── main2.py            # 主程序
└── yt_dlp/             # 下载目录
    ├── 频道A-NA/
    └── 频道B-NA/
```

## 常见问题

### Q: 下载速度慢？

A: 尝试以下方法：
1. 使用更快的代理服务器
2. 增加并发下载数（修改 `-N` 参数）
3. 使用 `--no-proxy`（如果不需要翻墙）

### Q: 无法下载需要登录的视频？

A: 确保已在 Firefox 浏览器中登录 YouTube，程序会自动读取 Cookie。

### Q: 如何只下载播放列表的部分视频？

A: 在 URL 后添加播放列表范围参数：

```bash
python3 main2.py "https://youtube.com/playlist?list=XXX&start=1&end=10"
```

### Q: 如何下载最高画质？

A: 修改 `main2.py`，在视频模式下添加 `-f bestvideo+bestaudio` 参数。

## 许可证

MIT License

## 致谢

- [yt-dlp](https://github.com/yt-dlp/yt-dlp) - 强大的 YouTube 下载工具
- [Claude Code](https://claude.ai/code) - AI 智能助手集成

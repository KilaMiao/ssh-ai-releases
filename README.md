<div align="center">

<img src="https://kiramiao.site:447/images/ssh_ai/icon.png" alt="SSH-AI" width="96">

# SSH-AI

**用自然语言管理你的服务器**

一款桌面应用，将 AI 能力嵌入 SSH 远程管理。你只需要用中文描述需求，AI 会自动规划、生成并执行对应的 Linux 命令。

[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey)]()
[![AI](https://img.shields.io/badge/AI-DeepSeek%20%7C%20OpenAI%20%7C%20兼容模型-000000)]()

</div>

---

![主界面](https://kiramiao.site:447/images/ssh_ai/screenshot-main.png)

## 为什么需要 SSH-AI

管理 Linux 服务器时，你是否遇到过这些问题：

- 不记得某个命令的参数怎么写
- 不确定一条命令会不会搞坏服务器
- 需要连续执行多条命令，但记不住完整流程
- 想快速完成一件事，却要先花 10 分钟搜教程

SSH-AI 让你**用说人话的方式管理服务器**。你告诉它你想做什么，它帮你把事情办了——而且会在执行危险操作前先问你。

---

## 功能一览

### 智能对话

用自然语言描述需求，AI 自动拆解为多个步骤逐步执行。你可以实时看到它的思考过程，也可以随时取消。

![AI 对话](https://kiramiao.site:447/images/ssh_ai/screenshot-ai-chat.png)

**示例：**

```
你: 帮我看下哪些进程占内存最多

AI: 正在分析服务器内存使用情况...
    → 执行: ps aux --sort=-%mem | head -10

    内存占用 Top 5：
    1. mysql    — 2.3 GB
    2. java     — 1.8 GB
    3. nginx    — 120 MB
    ...

    MySQL 占用了最多内存，如果需要可以进一步分析其配置。
```

```
你: 帮我清理 docker 垃圾

AI: 即将执行清理操作：
    - docker container prune  （删除已停止的容器）
    - docker image prune -a   （删除未使用的镜像）

    ⚠️ 这会删除所有未被使用的镜像，操作不可逆。
    [取消]  [确认执行]
```

### 安全防护

AI 生成的每一条命令都会经过安全检测。系统内置了 30+ 条危险命令识别规则：

| 风险等级 | 说明 | 处理方式 |
|----------|------|----------|
| 低 | 查看信息类命令 | 自动执行 |
| 中 | 可能有副作用的操作 | 弹窗提示，确认后执行 |
| 高 | 删除文件、修改权限等 | 详细风险说明 + 明确确认 |
| 极高 | 格式化磁盘、清空数据库等 | 预览影响 + 二次确认 |

所有密码和 API Key 均使用系统级加密存储，不会明文保存。

### 终端 + 文件管理

- 内置完整终端，支持所有 Shell 交互操作
- 可视化文件管理器，浏览、上传、下载远程文件
- 终端与文件管理器一键切换

![终端与文件管理](https://kiramiao.site:447/images/ssh_ai/screenshot-terminal.png)

### 多模型支持

支持多个 AI 服务商，可在对话中随时切换：

| 服务商 | 推荐模型 |
|--------|----------|
| DeepSeek | DeepSeek V3、V4 Flash |
| OpenAI | GPT-4o、GPT-4o-mini |
| 通义千问 | Qwen-Max、Qwen-Plus |
| Kimi | Moonshot-v1-128k |
| 智谱 AI | GLM-4 |
| Ollama | 本地部署的模型（无需 API Key） |
| 其他 | 任何兼容 OpenAI 接口格式的服务 |

### 联网搜索（可选）

开启后，AI 可以在回答你的问题时搜索互联网，获取最新的技术文档和解决方案。

### 更多

- **Token 用量统计** — 查看每次对话的 Token 消耗和每日趋势
- **对话历史** — 多会话管理，随时切换和回顾
- **记忆系统** — AI 记住你的服务器环境和偏好
- **多主题** — 内置多套界面主题，一键切换

---

## 安装

### Windows

1. 下载 `.exe` 安装包
2. 双击运行安装程序
3. 按向导完成安装

### macOS

1. 下载 `.zip` 文件
2. 解压后将 SSH-AI 拖入「应用程序」文件夹
3. 首次打开时，系统可能会提示"无法验证开发者"，前往「系统设置 → 隐私与安全性」点击「仍要打开」

### Linux

**Debian / Ubuntu：**
```bash
sudo dpkg -i ssh-ai_*.deb
```

**Fedora / RHEL：**
```bash
sudo rpm -i ssh-ai_*.rpm
```

---

## 快速上手

### 第一步：配置 AI 模型

1. 启动 SSH-AI
2. 点击左下角齿轮图标，进入「设置」
3. 在「AI 配置」页面，点击「+」添加模型
4. 选择服务商（如 DeepSeek），填入 API Key
5. 点击「测试连接」确认配置正确
6. 保存

![AI 配置](https://kiramiao.site:447/images/ssh_ai/screenshot-settings-ai.png)

> **没有 API Key？**
> - DeepSeek：前往 [platform.deepseek.com](https://platform.deepseek.com) 注册获取
> - OpenAI：前往 [platform.openai.com](https://platform.openai.com) 注册获取
> - Ollama：本地部署无需 Key，详见 [ollama.com](https://ollama.com)

### 第二步：连接服务器

1. 点击界面中的「新建连接」按钮
2. 填写以下信息：
   - **连接名称** — 给这台服务器起个名字（如"生产服务器"）
   - **主机地址** — 服务器 IP 或域名
   - **端口** — 默认 22，如有修改请填写实际端口
   - **用户名** — 如 `root`
   - **认证方式** — 选择「密码」或「密钥」
3. 点击「保存并连接」

### 第三步：开始对话

连接成功后，在右侧对话框中输入你想做的事情：

- `查看服务器磁盘使用情况`
- `帮我检查 nginx 是否在运行`
- `找出 /var/log 下超过 100MB 的日志文件`
- `安装 Docker 并启动`
- `备份 MySQL 数据库到 /backup 目录`

AI 会自动分析你的需求，生成命令并执行。如果涉及危险操作，会先弹窗请你确认。

---

## 使用技巧

### 让 AI 做更多

- **描述越具体，结果越准确**：`查看磁盘使用` vs `查看 /data 分区的使用率，如果超过 80% 告诉我`
- **可以要求 AI 解释命令**：`systemctl status nginx 这个命令是什么意思？`
- **可以要求 AI 做多步操作**：`先备份 nginx 配置，然后修改 worker_processes 为 4，最后重启 nginx`

### 管理多台服务器

- 左侧边栏可以保存多个服务器连接
- 点击服务器 Tab 快速切换
- 每台服务器有独立的对话历史

### 安全建议

- 首次使用时，建议先在测试服务器上熟悉 AI 的行为
- 对于生产环境的高风险操作（删除数据、修改配置等），即使 AI 给出了命令，也建议先在终端手动验证
- 可以在设置中管理「白名单」，将确认过的安全命令加入白名单以减少弹窗

---

## 常见问题

**Q: 连接服务器失败怎么办？**
A: 检查以下几点：
- 服务器地址和端口是否正确
- SSH 服务是否已启动（`systemctl status sshd`）
- 防火墙是否放行了 22 端口
- 用户名和密码/密钥是否正确

**Q: AI 生成的命令我不确定是否安全怎么办？**
A: SSH-AI 内置了安全检测，会自动标记高风险命令并弹窗确认。如果你仍然不确定，可以点击「取消」，然后在终端中手动执行 `命令 --help` 查看命令说明。

**Q: 支持哪些 Linux 发行版？**
A: 支持所有主流发行版，包括 Ubuntu、Debian、CentOS、Fedora、Rocky Linux、AlmaLinux、Arch Linux 等。只要服务器开启了 SSH 服务即可连接。

**Q: 数据存储在哪里？**
A: 所有数据存储在本地计算机上：
- Windows：`%APPDATA%/ssh-ai/`
- macOS：`~/Library/Application Support/ssh-ai/`
- Linux：`~/.config/ssh-ai/`

**Q: 如何更新到最新版本？**
A: 下载最新版安装包覆盖安装即可，配置和连接信息会自动保留。

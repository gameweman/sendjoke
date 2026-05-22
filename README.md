# 每日笑话推送 (Daily Joke Sender)

自动每天在指定时间获取20个中文笑话（包含10个冷笑话），并发送到你的邮箱。

## 功能特性

✨ **主要特性：**
- 📥 自动从多个API源获取20个中文笑话
- ❄️ 智能识别和分类10个冷笑话
- 📧 通过Outlook邮件发送格式化的笑话
- ⏰ 每日定时发送（默认9点）
- 🔄 自动重试机制
- 📊 详细的日志输出

## 安装

### 1. 克隆仓库
```bash
git clone https://github.com/gameweman/sendjoke.git
cd sendjoke
```

### 2. 安装依赖
```bash
pip install -r requirements.txt
```

### 3. 配置环境变量

复制 `.env.example` 为 `.env`：
```bash
cp .env.example .env
```

编辑 `.env` 文件并填入你的信息：
```env
# Outlook邮箱配置
SENDER_EMAIL=your_email@outlook.com
SENDER_PASSWORD=your_app_password
RECIPIENT_EMAIL=gameweman168@outlook.com

# 发送时间 (24小时格式)
SCHEDULE_TIME=09:00
```

### 4. 获取Outlook应用密码

由于Outlook启用了两步验证，你需要创建一个"应用密码"：

1. 访问 https://account.microsoft.com/account/security
2. 点击 "高级安全选项"
3. 转到 "应用密码"
4. 为 "邮件" 和 "Windows设备" 创建应用密码
5. 将生成的16字符密码复制到 `.env` 文件中的 `SENDER_PASSWORD`

## 使用

### 直接运行

```bash
python main.py
```

程序会在后台运行，每天在指定时间发送笑话。

### 一次性发送

如果只想测试一次，可以运行：

```bash
python fetch_jokes.py  # 测试获取笑话
python email_sender.py  # 测试发送邮件
```

## 使用云服务部署

### GitHub Actions (推荐)

已包含 `.github/workflows/send-jokes.yml` 文件，可以自动运行。

1. 在GitHub仓库中添加Secrets：
   - `SENDER_EMAIL`
   - `SENDER_PASSWORD`
   - `RECIPIENT_EMAIL`

2. 工作流会自动每天运行

### 其他云服务选项

- **Heroku**: 使用 `Procfile` 和 scheduler
- **AWS Lambda**: 使用CloudWatch Events触发
- **Google Cloud Functions**: 使用Cloud Scheduler触发
- **本地服务器**: 使用 cron 任务或 systemd 定时器

## 项目结构

```
sendjoke/
├── main.py                 # 主程序和调度器
├── fetch_jokes.py          # 笑话获取模块
├── email_sender.py         # 邮件发送模块
├── requirements.txt        # Python依赖
├── .env.example           # 环境变量模板
└── README.md              # 本文件
```

## 文件说明

### main.py
- 主程序入口
- 实现每日定时发送逻辑
- 处理错误和日志

### fetch_jokes.py
- 从多个API源获取笑话
- 智能识别和分类冷笑话
- 去重处理

### email_sender.py
- 使用SMTP发送邮件
- 格式化HTML邮件内容
- 支持Outlook邮箱

## 支持的笑话API

当前支持的API源：
1. **shadiao.io** - 随机笑话API
2. **jikipai.com** - Jikipai笑话API

如果某个API不可用，程序会自动尝试其他源。

## 冷笑话识别

冷笑话通过关键词匹配识别，包括：
- 冷、尴尬、无语、笑不出来
- 没意思、生硬、生冷、冷笑
- 呵呵、一言难尽、醉了

## 故障排除

### 邮件无法发送

1. **检查SENDER_PASSWORD是否正确**
   - 确保使用的是应用密码（16字符），不是账户密码
   - 访问 https://account.microsoft.com/account/security 验证

2. **检查SENDER_EMAIL**
   - 确保使用的是@outlook.com邮箱
   - 如果使用@hotmail.com，改为相应的outlook邮箱

3. **检查网络连接**
   - 确保可以连接到 smtp-mail.outlook.com:587

### 无法获取笑话

1. 检查网络连接
2. 检查API是否可用
3. 查看日志输出获取更多信息

### 定时任务未执行

1. 确保程序一直在运行
2. 检查SCHEDULE_TIME格式是否正确（应为HH:MM）
3. 查看程序日志

## 日志

程序会输出详细的日志信息，显示：
- 笑话获取进度
- 冷笑话识别结果
- 邮件发送状态
- 错误信息

## 许可证

MIT License

## 贡献

欢迎提交Issue和Pull Request！

## 联系

如有问题，请通过以下方式联系：
- 📧 Email: gameweman168@outlook.com
- 🐙 GitHub: https://github.com/gameweman

---

**祝你每天都能收到开心的笑话！😂**

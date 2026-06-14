# 资源站,影视资源站与采集站聚集和收集平台，包含视频源，播放源，json，xml等等格式，支持libretv，moontvplus，maccms等等

一个自动监测 [ziyuanzu.com](https://www.ziyuanzu.com/) 影视资源站可用性的开源工具，通过 GitHub Actions 定时运行，生成静态监控页面并通过 GitHub Pages 发布。
## 功能特性

- **定时监测**：每 2 小时自动抓取并检测所有资源站状态
- **实时数据**：HTTP 状态码、响应时间、在线/离线状态
- **静态页面**：自动生成美观的暗色主题监控面板
- **历史存档**：每次监测结果保存为 JSON，支持历史对比
- **GitHub Pages**：零成本部署，自动更新

## 项目结构

```
ziyuanzu-monitor/
├── .github/
│   └── workflows/
│       └── monitor.yml      # GitHub Actions 定时工作流
├── docs/
│   └── index.html           # 生成的监控页面（GitHub Pages 源）
├── data/
│   ├── latest.json          # 最新监测数据
│   └── monitor_*.json       # 历史数据存档
├── monitor.py               # 核心监测脚本
├── requirements.txt         # Python 依赖
└── README.md                # 项目说明
```

## 快速开始

### 1. Fork 本项目

点击右上角 **Fork** 按钮，将本项目复制到你的 GitHub 账号下。

### 2. 启用 GitHub Pages

1. 进入你 Fork 后的仓库
2. 点击 **Settings** → **Pages**
3. **Source** 选择 **Deploy from a branch**
4. **Branch** 选择 `main`，文件夹选择 `/docs`
5. 点击 **Save**

等待几分钟后，你的监控页面将发布在：
```
https://你的用户名.github.io/ziyuanzu-monitor/
```

### 3. 启用 GitHub Actions

1. 进入仓库的 **Actions** 标签页
2. 点击 **I understand my workflows, go ahead and enable them**
3. 工作流将自动按照 cron 计划每 2 小时运行一次

### 4. 手动触发（可选）

进入 **Actions** → **Monitor ziyuanzu.com Resources** → **Run workflow**，可以立即手动运行一次监测。

## 本地运行

```bash
# 克隆仓库
git clone https://github.com/你的用户名/ziyuanzu-monitor.git
cd ziyuanzu-monitor

# 安装依赖
pip install -r requirements.txt

# 运行监测脚本
python monitor.py

# 查看生成的页面
open docs/index.html
```

## 自定义配置

### 修改监测频率

编辑 `.github/workflows/monitor.yml` 中的 cron 表达式：

```yaml
schedule:
  - cron: '0 */2 * * *'   # 每2小时（默认）
  - cron: '0 */6 * * *'   # 每6小时
  - cron: '0 0 * * *'     # 每天0点
```

### 修改超时时间

编辑 `monitor.py` 中的 `TIMEOUT` 变量：

```python
TIMEOUT = 15  # 秒
```

## 数据来源

- 资源站列表：[ziyuanzu.com](https://www.ziyuanzu.com/)
- 监测方式：HTTP HEAD 请求检测可用性

## 免责声明

本项目为第三方开源监测工具，与 ziyuanzu.com 官方无关。仅供学习和技术交流使用。

## License

MIT License

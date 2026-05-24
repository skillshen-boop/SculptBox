# SculptBox V1.0

**3D 资产管理工具 — 让笔刷库随取随用。**

---

[English](README.md) · 中文 · [日本語](README.ja.md) · [한국어](README.ko.md)

---

## 📥 下载

| 版本 | 下载 | 说明 |
|:----|:----|:------|
| macOS V1.0 | [⬇️ GitHub Releases](https://github.com/skillshen-boop/SculptBox/releases/latest) | 直接下载 |
| macOS V1.0 | [☁️ 百度网盘](https://pan.baidu.com/s/1BeFZfMoCmqbfOQDEYJQdSg?pwd=tayr) | 提取码: tayr |

---

## ⚠️ 首次安装

macOS 可能提示 **"SculptBox 已损坏，无法打开"**。不是文件坏了，执行：

```bash
sudo xattr -rd com.apple.quarantine /Applications/SculptBox.app
```

或 **系统设置 → 隐私与安全性 → 仍然打开**。

---

## 🚀 快速开始

1. 下载 DMG，拖入 Applications
2. 如果报错，执行上面的命令
3. 启动 SculptBox
4. Settings → Plugin Status → Install 一键部署桥接
5. 重启 ZBrush

---

## ✨ 功能介绍

### 笔刷管理

<img src="promo/assets/screenshot_main.png" width="700" alt="主界面"/>

SculptBox 自动索引你的全部笔刷目录。几千个笔刷，几秒加载完成。

- **搜索** — 输入关键词，实时过滤
- **标签** — 10 个自动标签（雕刻/曲线/插入/工具...）+ 自定义标签
- **收藏夹** — 星标收藏，一键切换
- **分类** — 按目录浏览，按类型筛选

### 缩略图预览

<img src="promo/assets/screenshot_thumbnail_s.png" width="300" alt="小缩略图"/> <img src="promo/assets/screenshot_thumbnail_l.png" width="300" alt="大缩略图"/>

每个笔刷实时显示真实缩略图，不用再靠文件名猜。原生 ZBP 解析，50ms 一个。支持 S/M/L 三级缩放。

### Send to ZBrush

<img src="promo/assets/screenshot_send.png" width="400" alt="发送到 ZBrush"/>

任意笔刷上右键 → Send to ZBrush，通过 IPC 桥接实时加载。不用再在 ZBrush 里翻文件夹了。

### 批量操作

<img src="promo/assets/screenshot_batch.png" width="700" alt="批量多选"/>

多选笔刷 → 批量发送到 ZBrush、批量导出缩略图、批量打标签。

### 多语言

内置 4 种语言：中文、English、日本語、한국어，在 Settings 随时切换。

### 桥接状态一键查看

<img src="promo/assets/screenshot_plugin_status.png" width="600" alt="桥接状态"/>

Settings → Plugin Status 一目了然：
- ZBrush 是否安装
- 桥接脚本是否部署
- IPC 目录是否就绪
- LaunchAgent 状态

点击 **Install**，1 分钟完成部署，不需要终端。

---

## 📖 使用说明

### 添加笔刷目录

1. 打开 SculptBox
2. 点击右上角齿轮图标设置
3. 进入 **扫描目录** → **添加**
4. 选择放笔刷的文件夹（.ZBP / .ZBR / .MNU）
5. 等待扫描完成

### 搜索笔刷

在顶栏搜索框输入关键词，结果实时过滤。右侧标签面板按分类筛选。

### 发送到 ZBrush

1. 确保 ZBrush 正在运行
2. 右键点击任意笔刷
3. 选择 **Send to ZBrush**
4. 笔刷自动出现在 ZBrush 中

### 批量发送

1. 按住 Shift/Cmd 多选笔刷
2. 右键 → Send to ZBrush
3. SculptBox 通过 IPC 桥接逐个发送

### 管理标签

- 自动标签从文件名检测生成
- 点击标签按分类筛选
- 支持自定义标签，跨会话持久化

---

## 系统要求

- macOS 10.15+
- ZBrush 2026+（Send to ZBrush 功能需要）
- Python 3.9+（开发用）

---

## 🔗 链接

- 官网：[sculptbox.net](https://sculptbox.net)
- 下载：[GitHub Releases](https://github.com/skillshen-boop/SculptBox/releases)
- 反馈：[Issues](https://github.com/skillshen-boop/SculptBox/issues)

---

*SculptBox — 3D 资产管理工具*

# SculptBox V017 Beta — 交接文档

## 快速上手

```bash
# 启动桌面端
python3 run_viewer.py          # 终端
open dist/SculptBox.app            # 或双击 .app

# ZBrush 桥接
# Ctrl+, → 插件 → Deploy Plugin
# 然后双击 ZBrush.app 即可（LaunchAgent 自动加载）
```

## 版本分支

| 分支 | 说明 |
|:----:|:------|
| `v016` ★ | **当前分支（V014→V017 全部功能）** |

## 启动命令

```bash
make run         # 启动桌面端
make build       # 构建 .app
make dmg         # 构建 DMG
```

## 语言支持

| 语言 | 代码 | 文件 | 状态 |
|:----|:----:|:----|:----:|
| 🇨🇳 中文 | `zh` | `zh.json` | ✅ 138 条 |
| 🇺🇸 English | `en` | `en.json` | ✅ 138 条，默认 |
| 🇯🇵 日本語 | `ja` | `ja.json` | ✅ 138 条 |
| 🇰🇷 한국어 | `ko` | `ko.json` | ✅ 138 条 |

切换语言：`Ctrl+,` → ZBrush 设置 → Language 下拉

## 功能清单

| 模块 | 说明 |
|:----:|:------|
| 🖼️ 缩略图预览 | ZBP 提取 + PSD 3层解码 + 占位符 |
| 🔍 搜索 + 关键词 | 搜索框 + 快捷芯片，热度排序 Top 10 |
| ⭐ 收藏 + 🏷️ Tags | 星标切换 + 预定义/自定义标签 |
| 🔄 排序 | 按钮式 Name/Date/Size/Format/Hot/Fav |
| 📂 目录树 | SQLite 驱动 |
| 🔌 ZBrush 桥接 | Deploy 插件 + LaunchAgent 自动加载 |
| 🔗 双击/发送图标 | 双击发送 → 右下角 ↗ 一键发送 |
| ⌨️ 快捷键管理 | 全局/单独配置 |
| 🌐 4 语言 | 中/英/日/韩 |
| 📦 DMG 构建 | `make build && make dmg` |

## 关键路径

| 路径 | 说明 |
|:-----|:------|
| `~/Library/.../ZBrush4/SculptBox/plugin/SculptBox_bridge.py` | 桥接脚本 |
| `~/Library/.../SculptBox/ipc/` | IPC 目录 |
| `~/Library/LaunchAgents/com.SculptBox.bridge.plist` | LaunchAgent |
| `project/SculptBox_cache/` | SQLite + 缩略图缓存 |
| `project/SculptBox_cache/settings.json` | 设置 + 关键词 + 快捷键 + 语言 |
| `src/i18n/*.json` | 4 语言翻译文件 |

## 给新开发者的建议

1. 先读 `PROJECT_STATUS.md`
2. 分支在 `v016`
3. 添加新语言 → 在 `src/i18n/` 下新建 `xx.json`
4. 打包 → `make build && make dmg`

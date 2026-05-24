# SculptBox — ZBrush 桥接部署指南

## 核心架构

```
桌面端 (PySide6)                  ZBrush 2026
     │                               │
     │ 写入 JSON 命令文件              │  xmd_bridge.py 轮询读取
     │ ─────────────────→  IPC/       │
     │                    cmd_*.json  │
     │                               │  执行 zbrush.commands API
     │                               │  ↓
     │                               │  ZBrush 内加载笔刷/Alpha等
```

## 启动要求

**关键**: ZBrush 必须通过特定方式启动才能加载桥接。

### ✅ 正确方式（从终端启动）

```bash
cd /Users/skillshen/CodeBuddy/SculptBox
bash launch_zbrush_bridge.sh
```

这个脚本会自动设置 `ZBRUSH_PLUGIN_PATH` 环境变量，ZBrush 启动时加载桥接。

### ❌ 错误方式（从 Finder 启动）

直接双击 `ZBrush.app` 或 `open /Applications/Maxon\ ZBrush\ 2026/ZBrush.app` → **桥接不会加载**。

因为 Finder 启动的 App 不继承 `~/.zshenv` 中的环境变量。

## 环境变量

| 变量 | 值 | 用途 |
|------|-----|------|
| `ZBRUSH_PLUGIN_PATH` | `~/Library/Application Support/ZBrush4/SculptBox/plugin` | 告诉 ZBrush 在哪里找 Python 桥接脚本 |

### 为什么不能永久设置

`launchctl setenv` 可以永久设置全局环境变量（Finder 启动也生效），但**当前环境无权限**（Sandbox 限制）。用户登录到自己的终端执行可以，但这需要一次性操作。

## 关键路径

| 路径 | 说明 |
|------|------|
| `~/Library/Application Support/ZBrush4/SculptBox/plugin/xmd_bridge.py` | **桥接脚本** — 运行在 ZBrush 内部 |
| `~/Library/Application Support/ZBrush4/SculptBox/ipc/` | **IPC 共享目录** — 桌面端写 JSON，桥接读取 |
| `~/Library/Application Support/ZBrush4/SculptBox/bridge.log` | **桥接运行时日志** |
| `~/.zshenv` | Shell 环境变量配置（仅终端启动有效） |

## 部署方式

通过桌面端 Settings → 🔌 ZBrush Plugin → **📦 Deploy Plugin** 一键部署。

### 部署内容

1. 复制 `src/installer/xmd_bridge.py` → `~/Library/.../SculptBox/plugin/xmd_bridge.py`
2. 创建 IPC 目录 → `~/Library/.../SculptBox/ipc/`
3. 写入 `~/.zshenv` 设置 `ZBRUSH_PLUGIN_PATH`

### 卸载

通过 Settings → 🔌 ZBrush Plugin → **🗑 Remove Plugin**。

安全策略：
- 只删除安装清单中的已知文件
- 路径必须在白名单内（`~/Library/.../SculptBox/` 或 `/Applications/Maxon ZBrush 2026/ZData/ZPlugs64/`）
- 文件被占用时跳过，不强制删除
- 不使用 `shutil.rmtree` 或 `rm -rf`

## 验证桥接是否加载

```bash
# 检查桥接日志
cat ~/Library/Application\ Support/ZBrush4/SculptBox/bridge.log
```

成功加载应看到：
```
[HH:MM:SS] === SculptBox Bridge (macOS) starting ===
[HH:MM:SS] zbrush.commands imported OK
[HH:MM:SS] Bridge UI ready. IPC dir: .../ipc
[HH:MM:SS] === SculptBox Bridge initialized ===
```

## IPC 测试

桌面端右键笔刷 → **Send to ZBrush**

1. 桌面端 `ipc_sender.py` 写入 JSON 到 IPC 目录
2. ZBrush 端点击 **Poll** 按钮（或按 `Ctrl+Shift+Alt+8`）
3. 桥接读取 JSON 并执行
4. 笔刷在 ZBrush 中加载

## 常见问题

| 问题 | 原因 | 解决 |
|------|------|------|
| ZBrush 启动但无 "SculptBox Bridge" 面板 | 从 Finder 启动了，环境变量未设置 | 用 `bash launch_zbrush_bridge.sh` 启动 |
| `bridge.log` 不存在 | 桥接从未被加载过 | 重新部署 + 正确方式启动 ZBrush |
| 发送笔刷后 ZBrush 无反应 | 未点击 Poll 按钮 | 在 ZBrush 中点击 Poll 或按快捷键 |
| ZBrush 启动时 MEMORY ERROR | ZBrush 内部 VMEM 损坏 | `rm -rf "/Applications/Maxon ZBrush 2026/ZBrush.app/Contents/ZVMEM_"` |

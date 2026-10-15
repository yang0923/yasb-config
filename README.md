# yasb-config

个人 [YASB](https://github.com/amnweb/yasb)（Yet Another Status Bar）配置仓库。基于 Catppuccin Mocha 配色，深度集成 GlazeWM，配合 Windows 平铺工作流使用。

## ✨ 特性

- 🎨 **Catppuccin Mocha** 主题，所有颜色与间距通过 CSS 变量集中管理
- 🪟 **GlazeWM 深度集成**：工作区切换、绑定模式指示、平铺方向
- 📊 **系统监控**：CPU、GPU、内存、磁盘、网络流量
- 🎵 **媒体控制**：媒体信息显示、播放控制、缩略图
- 🔔 **通知中心**：统一管理 Windows 通知
- 📅 **时钟日历**：中文 locale，支持周数显示
- 🖼️ **毛玻璃弹窗**：所有菜单/日历/媒体面板统一模糊效果

## 📁 目录结构

```
yasb-config/
├── config.yaml              # 主配置：任务栏布局、widget 选项
├── styles.css               # 样式入口（@import 各 widget CSS）
└── widgets/                 # 各 widget 的独立样式
    ├── base.css             # CSS 变量 + 全局 reset
    ├── recycle_bin.css
    ├── glazewm_binding_mode.css
    ├── glazewm_tiling_direction.css
    ├── glazewm_workspaces.css
    ├── active_window.css
    ├── cpu.css
    ├── gpu.css
    ├── memory.css
    ├── disk.css
    ├── traffic.css
    ├── media.css
    ├── brightness.css
    ├── volume.css
    ├── clock.css
    └── notifications.css
```

## 🖥️ 任务栏布局

| 区域 | Widget |
|---|---|
| **左侧** | 回收站 · GlazeWM 绑定模式 · 平铺方向 · 工作区切换器 · 活动窗口标题 |
| **中间** | CPU · GPU · 内存 · 磁盘 · 网络流量 |
| **右侧** | 媒体 · 亮度 · 音量 · 时钟 · 通知中心 |

## 🚀 安装

### 前置条件

- Windows 10/11
- [YASB](https://github.com/amnweb/yasb) v2.0.0 或更高
- [GlazeWM](https://github.com/glzr-io/glazewm)（用于工作区相关 widget）
- 字体：[JetBrainsMono Nerd Font](https://www.nerdfonts.com/font-downloads)

### 安装步骤

1. 克隆仓库到 YASB 配置目录：

   ```powershell
   git clone https://github.com/yang0923/yasb-config.git "$env:USERPROFILE\.config\yasb"
   ```

   如果 `~/.config/yasb` 已存在，先备份：

   ```powershell
   Move-Item "$env:USERPROFILE\.config\yasb" "$env:USERPROFILE\.config\yasb.bak"
   ```

2. 确认 `config.yaml` 顶部的路径与用户名正确。

3. 启动或重启 YASB：

   ```powershell
   yasbc restart
   ```

## 🎨 主题定制

所有颜色、间距、字号等设计 token 集中在 `widgets/base.css` 的 `:root` 中。修改一处即可全局生效。

### Catppuccin Mocha 色板

```css
--base / --mantle / --crust           /* 三层背景 */
--surface0 / --surface1 / --surface2  /* 表面层级 */
--overlay0 / --overlay1 / --overlay2  /* 次级文字 */
--text / --subtext0 / --subtext1      /* 主/次文字 */
--blue / --mauve / --green / --red ... /* 强调色 */
```

### 设计 token

```css
--widget-padding: 0 5px      /* 所有 widget 统一内边距 */
--widget-radius: 8px         /* widget 圆角 */
--icon-size: 13px            /* 图标字号 */
--label-size: 13px           /* 标签字号 */
--menu-bg: #181825e6         /* 弹窗背景 */
--menu-radius: 10px          /* 弹窗圆角 */
```

### 状态色阈值

CPU、内存、GPU 采用统一的阈值方案：

```css
--status-low: var(--green)      /* < 50% */
--status-medium: var(--yellow)  /* 50-75% */
--status-high: var(--peach)     /* 75-90% */
--status-critical: var(--red)   /* >= 90% */
```

## ⌨️ 快捷键

部分 widget 支持全局热键（由 YASB 原生注册）：

| 快捷键 | 功能 |
|---|---|
| `Win + Del` | 清空回收站 |
| `Win + Alt + Space` | 播放/暂停媒体 |
| `Win + Alt + .` | 下一曲 |
| `Win + Alt + ,` | 上一曲 |
| `Win + Alt + C` | 打开日历 |
| `Win + Alt + M` | 静音切换 |

> 具体键位以 `config.yaml` 中各 widget 的 `keybindings` 配置为准。

## 🔧 常用操作

### 修改 widget 更新频率

在 `config.yaml` 中对应 widget 的 `options.update_interval` 调整。参考值：

| Widget | 建议值 | 说明 |
|---|---|---|
| CPU / GPU | 3000ms | 降低轮询频率，减少系统负担 |
| 内存 | 5000ms | 变化较慢 |
| 磁盘 | 60s | 几乎不变 |
| 网络流量 | 2000ms | 平衡实时性与开销 |
| 时钟 | 1000ms | 秒针需要每秒刷新 |

### 换配色

把 `widgets/base.css` 的 `:root` 色板替换为其他 Catppuccin flavor（Latte / Frappé / Macchiato），或直接换成任意配色方案。

### 调整弹窗样式

各 widget 的弹窗配置在 `config.yaml` 的 `menu` / `calendar` / `media_menu` 等字段中，统一支持：

```yaml
blur: true                     # 毛玻璃
round_corners: true            # 圆角
round_corners_type: "normal"   # normal / small
border_color: "system"         # 跟随系统
alignment: "right"             # 弹出方向
direction: "down"
offset_top: 6
```

## 📤 更新配置

修改后提交：

```bash
git add .
git commit -m "update yasb config"
git push
```

如果本仓库作为 [desktop-configs](https://github.com/yang0923/desktop-configs) 的子模块使用，需要在主仓库同步更新：

```bash
cd desktop-configs
git submodule update --remote yasb-config
git add yasb-config
git commit -m "update yasb-config"
git push
```

## 🐛 故障排查

### YASB 启动失败

查看日志：

```powershell
Get-Content $env:TEMP\yasb.log -Tail 100
```

### Widget 显示 "unknown type"

说明 `config.yaml` 中该 widget 的 `type` 字段与实际安装的版本不匹配。对照 [YASB 官方文档](https://github.com/amnweb/yasb) 检查 widget 名称。

### GlazeWM 相关 widget 显示离线

确认 GlazeWM 正在运行，且 `config.yaml` 顶部的 `glazewm.start_command` 路径正确。

### 字体图标显示为方块

安装 [JetBrainsMono Nerd Font](https://www.nerdfonts.com/font-downloads)，重启 YASB。

## 🔗 相关链接

- [YASB 官方仓库](https://github.com/amnweb/yasb)
- [YASB 文档](https://github.com/amnweb/yasb/wiki)
- [GlazeWM](https://github.com/glzr-io/glazewm)
- [Catppuccin 配色方案](https://github.com/catppuccin/catppuccin)
- [Nerd Fonts](https://www.nerdfonts.com/)

## 📄 许可

个人配置文件，自由取用。

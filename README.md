# yasb-config

个人 [YASB Reborn](https://github.com/amnweb/yasb) 配置：Catppuccin Mocha 配色 + GlazeWM 集成，用于 Windows 11 平铺工作流。

当前版本：YASB Reborn v2.0.7，单屏 2560×1440。

## ✨ 特性

- 🎨 **Catppuccin Mocha**：颜色、间距、字号全部集中在 `widgets/tokens.css`
- 🪟 **GlazeWM 集成**：工作区、绑定模式、平铺方向、活动窗口
- 📊 **系统监控**：CPU / GPU / 内存 / 磁盘 / 网络流量，按阈值变色
- 🎵 **媒体控制**：标题滚动、缩略图、播放控制、按音源着色的弹窗
- 🔔 **通知中心**：统一接管 Windows 通知
- 📅 **时钟日历**：中文 locale，含周数
- 🖼️ **毛玻璃**：任务栏与所有弹窗统一模糊 + 圆角

## 📁 目录结构

```
yasb-config/
├── config.yaml              # 布局 + widget 选项
├── styles.css               # 样式入口（按顺序 @import）
└── widgets/
    ├── tokens.css           # 设计 token：色板 / 间距 / 字号 / 弹窗 / 状态色
    ├── base.css             # reset + 通用组件（弹窗骨架、滚动条、tooltip、右键菜单）
    ├── active_window.css
    ├── glazewm_binding_mode.css
    ├── glazewm_tiling_direction.css
    ├── glazewm_workspaces.css
    ├── recycle_bin.css
    ├── cpu.css  gpu.css  memory.css  disk.css  traffic.css
    ├── media.css
    ├── brightness.css  volume.css  audio.css
    ├── clock.css
    └── notification.css
```

## 🖥️ 任务栏布局

| 区域 | Widget |
|---|---|
| **左** | 回收站 · 绑定模式 · 平铺方向 · 工作区 · 活动窗口 |
| **中** | CPU · GPU · 内存 · 磁盘 · 流量 |
| **右** | 媒体 · 亮度 · 音量 · 时钟 · 通知 |

顶栏高 36px，不启用 `windows_app_bar`：窗口让位交给 GlazeWM 的 `outer_gap.top: 42px`（栏高 36 + 6 间距）。改栏高时同步改这个 gap。

## 🖱️ 交互约定

统一为 **左键主操作 / 右键菜单 / 中键无**：

| Widget | 左键 | 右键 | 其他 |
|---|---|---|---|
| 回收站 | 打开回收站 | 清空（带确认） | `Win + Del` 清空 |
| CPU / GPU / 内存 / 磁盘 | 切换 label / label_alt | 打开图表菜单 | CPU 中键开任务管理器 |
| 流量 | 切换 label | 打开流量菜单 | |
| 媒体 | 切换 label | 打开媒体菜单 | 中键打开来源应用 |
| 音量 | 打开音量菜单 | 静音切换 | 滚轮调音量 |
| 亮度 | 切换 label | 打开亮度菜单 | |
| 时钟 | 切换 label | 打开日历 | |
| 通知 | 打开通知中心 | 切换 label | |

## 🎨 设计 token

全部在 `widgets/tokens.css`，其余文件只引用变量。

```css
/* 色板：Catppuccin Mocha 全色 */
--base --mantle --crust --surface0~2 --overlay0~2
--text --subtext0~1 --lavender --blue ... --red

/* 间距：4px 网格 */
--space-1: 4px  --space-2: 8px  --space-3: 12px
--widget-padding: 0 4px          /* widget 外边距 */
--container-padding: 2px 8px     /* widget-container 内边距 */
--widget-radius: 8px  --btn-radius: 6px

/* 字号 */
--icon-size: 16px  --label-size: 13px  --label-weight: 500

/* 交互底色 */
--hover-bg  --active-bg  --focus-bg   /* lavender 低透明度 */

/* 弹窗 */
--menu-bg: rgba(24,24,37,.9)  --menu-border  --menu-radius: 12px
```

配色语义：**窗口管理 = lavender，系统监控 = blue，系统外设 = overlay2**；监控数字只在超过阈值时才着色。

### 状态阈值

| Widget | 正常 | 黄 | 橙 | 红 |
|---|---|---|---|---|
| CPU / GPU | < 50% | 50–75% | 75–90% | > 90% |
| 内存 | < 70% | 70–85% | 85–95% | > 95% |
| 磁盘（已用） | < 70% | 70–85% | 85–95% | > 95% |

## ⏱️ 刷新频率

| Widget | 值 | 说明 |
|---|---|---|
| 时钟 | 1000ms | 需要秒 |
| 流量 | 2000ms | 实时性与开销的折中 |
| CPU / GPU | 3000ms | 再快意义不大 |
| 内存 | 5000ms | 变化慢 |
| 磁盘 | 60s | 几乎不变 |

## 🔧 常用操作

```powershell
yasbc reload          # 改完配置/样式手动重载（默认 watch_config 会自动重载）
yasbc log             # 实时日志
yasbc config-dir      # 打开配置目录
yasbc migrate-config  # 自动迁移被弃用的配置项
```

- **换配色**：只改 `tokens.css` 的 `:root`，换成 Latte / Frappé / Macchiato 均可。
- **改弹窗**：`config.yaml` 里各 widget 的 `menu` / `calendar` / `media_menu` 支持 `blur`、`round_corners`、`border_color`、`alignment`、`direction`、`offset_top`。
- **加 widget**：先在 `widgets:` 下定义，再挂到 `bars.yasb-bar.widgets` 的某个区域；样式文件记得在 `styles.css` 里 `@import`。

## 🐛 故障排查

- **日志**：`~/.config/yasb/yasb.log`（不是 `%TEMP%`）。
- **widget 显示 unknown type**：`type` 与安装版本不匹配，对照 [官方 widget 文档](https://github.com/amnweb/yasb/wiki)。
- **图标显示成方块**：安装 [JetBrainsMono Nerd Font](https://www.nerdfonts.com/font-downloads) 并重启 YASB。
- **GlazeWM 相关 widget 显示离线**：确认 GlazeWM 在运行；本配置由 GlazeWM 的 `startup_commands` 拉起 YASB。
- **日志里 `Error creating corner mask`**：缩略图圆角半径大于缩略图尺寸，调小 `thumbnail_corner_radius`。

## 🔗 相关链接

- [YASB](https://github.com/amnweb/yasb) · [文档](https://github.com/amnweb/yasb/wiki)
- [GlazeWM](https://github.com/glzr-io/glazewm)
- [Catppuccin](https://github.com/catppuccin/catppuccin) · [Nerd Fonts](https://www.nerdfonts.com/)

## 📄 许可

个人配置文件，自由取用。

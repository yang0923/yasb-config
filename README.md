# windhawk-config

个人 Windhawk 配置备份仓库。通过 Git 管理 mod 的 JSON 设置，便于在多台设备间同步、版本追踪和一键恢复。

## 📋 已包含的 Mod 配置

| Mod ID | 说明 |
|---|---|
| `taskbar-clock-customization` | 任务栏时钟自定义（格式、字体、布局） |
| `taskbar-dock-animation` | 任务栏 Dock 风格动画效果 |
| `windows-11-notification-center-styler` | 通知中心样式（当前主题：WindowGlass） |
| `windows-11-start-menu-styler` | 开始菜单样式定制 |
| `windows-11-taskbar-styler` | 任务栏样式定制（颜色、圆角、间距等） |

## 📁 目录结构

```
windhawk-config/
├── README.md
└── mods/
    ├── taskbar-clock-customization.json
    ├── taskbar-dock-animation.json
    ├── windows-11-notification-center-styler.json
    ├── windows-11-start-menu-styler.json
    └── windows-11-taskbar-styler.json
```

每个 JSON 文件对应一个 Windhawk mod 的完整设置。

## 🚀 使用方法

### 前置条件

- 已安装 [Windhawk](https://windhawk.net/)
- 已安装对应的 mod（在 Windhawk 中搜索 mod 名称并安装）

### 单 Mod 导入

1. 打开 Windhawk，进入目标 mod 的详情页
2. 切换到 **Advanced** 标签页
3. 将对应 JSON 文件的**全部内容**复制到 "Mod settings" 文本框中
4. 点击 **Save settings** 保存

### 批量导入

目前 Windhawk 没有官方的批量导入功能，需要逐个 mod 手动导入。如果 mod 数量较多，建议使用社区工具 [Windhawk Backup Manager](https://github.com/osmanonurkoc/Windhawk-Backup-Manager) 进行选择性恢复。


## ⚙️ Windhawk 配置存储说明

Windhawk 有两种存储模式：

| 模式 | 存储位置 | 说明 |
|---|---|---|
| 系统模式（默认） | Windows 注册表 `HKLM\SOFTWARE\Windhawk` | 标准安装 |
| 便携模式 | 安装目录下的 `settings.ini` | 便携安装，不写注册表 |

本仓库通过 **mod 的 JSON 设置**进行备份，与存储模式无关，两种模式下均可使用。

## 📤 更新配置

当你在 Windhawk 中修改了某个 mod 的设置后：

1. 进入该 mod 的 **Advanced** 标签页
2. 复制 "Mod settings" 中的 JSON 内容
3. 覆盖仓库中对应的 `mods/<mod-id>.json` 文件
4. 提交更改

## ⚠️ 注意事项

- **先安装 mod，再导入设置**。设置导入前需确保对应的 mod 已安装，否则设置无法关联。
- **JSON 格式校验**。手动编辑 JSON 时注意保持格式正确，否则导入可能失败。建议使用 VS Code 等编辑器并开启 JSON 格式化。
- **版本兼容性**。不同 Windhawk 版本的 mod 设置字段可能略有差异，导入前确认 mod 版本一致。
- **主题变更**。如 `windows-11-notification-center-styler` 当前使用 `WindowGlass` 主题，更换主题时需同步更新 JSON 文件。

## 🔗 相关链接

- [Windhawk 官网](https://windhawk.net/)
- [Windhawk GitHub](https://github.com/ramensoftware/windhawk)
- [Windhawk Backup Manager](https://github.com/osmanonurkoc/Windhawk-Backup-Manager)
- [Windows 11 Taskbar Styling Guide](https://github.com/ramensoftware/windows-11-taskbar-styling-guide)

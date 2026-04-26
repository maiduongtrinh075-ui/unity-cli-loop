# Unity CLI Loop (uloop) 中文说明

Unity Editor 自动化 CLI 工具集，包含 18 个 Claude Code 技能。

## 功能概述

**uloop** 提供 18 个 Unity Editor 自动化技能：

| 分类 | 技能 |
|------|------|
| **编辑器控制** | `launch`, `compile`, `control-play-mode`, `clear-console`, `focus-window` |
| **检查** | `get-hierarchy`, `find-game-objects`, `get-logs`, `screenshot` |
| **测试** | `run-tests` |
| **动态代码** | `execute-dynamic-code`, `execute-menu-item` |
| **输入模拟** | `simulate-mouse-ui`, `simulate-mouse-input`, `simulate-keyboard` |
| **录制** | `record-input`, `replay-input` |

## 安装

### 前置条件

1. **uloop CLI** - 先安装 CLI 工具
2. **Unity Editor** - 目标 Unity 项目必须打开
3. **Input System** - 输入模拟技能需要（包：`com.unity.inputsystem`）

### 技能安装

克隆或复制到 Claude Code skills 目录：

```
skills/
└── unity-cli-loop/
    ├── SKILL.md                    # 包概述
    ├── uloop-compile/
    ├── uloop-control-play-mode/
    ├── uloop-screenshot/
    ├── uloop-execute-dynamic-code/
    │   ├── SKILL.md
    │   └── references/
    │       ├── prefab-operations.md
    │       ├── scene-operations.md
    │       └── ...
    └── ...
```

## 技能参考

### 编辑器控制

#### uloop-launch
启动 Unity Editor（自动匹配版本）。

```bash
uloop launch [项目路径] [-r] [-p Android]
```

#### uloop-compile
编译 Unity 项目，报告错误/警告。

```bash
uloop compile [--force-recompile] [--wait-for-domain-reload]
```

#### uloop-control-play-mode
控制 Unity Editor 播放模式。

```bash
uloop control-play-mode --action Play
uloop control-play-mode --action Stop
uloop control-play-mode --action Pause
```

### 检查

#### uloop-get-hierarchy
获取 Unity 场景层级树结构。

```bash
uloop get-hierarchy [--root-path "Canvas/UI"] [--max-depth 2]
```

#### uloop-screenshot
捕获 Unity Editor 窗口截图。

```bash
uloop screenshot                              # Game View
uloop screenshot --capture-mode rendering     # 游戏渲染（PlayMode）
uloop screenshot --window-name Scene          # Scene View
```

#### uloop-get-logs
获取 Unity Console 日志。

```bash
uloop get-logs [--filter-type error|warning|log]
```

### 测试

#### uloop-run-tests
执行 Unity Test Runner。

```bash
uloop run-tests                              # EditMode 测试
uloop run-tests --test-mode PlayMode         # PlayMode 测试
uloop run-tests --filter-type exact --filter-value "MyTest"
```

### 动态代码执行

#### uloop-execute-dynamic-code
在 Unity Editor 中动态执行 C# 代码（Roslyn）。

```bash
uloop execute-dynamic-code --code 'using UnityEngine; return Mathf.PI;'
```

参考文档见 `references/` 目录：
- `prefab-operations.md` - 预制体创建、实例化、添加组件
- `scene-operations.md` - 创建 GameObject、连接引用
- `playmode-inspection.md` - 运行时状态检查
- `playmode-automation-zsh.md` / `powershell.md` - PlayMode 自动化

### 输入模拟

#### uloop-simulate-mouse-ui
模拟 UI 元素的鼠标交互（EventSystem）。

```bash
uloop simulate-mouse-ui --action Click --x 400 --y 300
uloop simulate-mouse-ui --action Drag --from-x 100 --from-y 200 --x 400 --y 300
```

#### uloop-simulate-mouse-input
通过 Input System 模拟鼠标输入（游戏逻辑）。

```bash
uloop simulate-mouse-input --action Click --x 400 --y 300
uloop simulate-mouse-input --action Scroll --scroll-y 120
```

#### uloop-simulate-keyboard
模拟键盘输入。

```bash
uloop simulate-keyboard --action Press --key Space
```

### 录制与回放

#### uloop-record-input
录制 PlayMode 期间的键盘和鼠标输入。

```bash
uloop record-input --action Start
uloop record-input --action Stop --output-path my-recording.json
```

#### uloop-replay-input
回放录制的输入，用于确定性测试。

```bash
uloop replay-input --input-path my-recording.json
```

## 常用工作流

### 编译并测试

```bash
uloop compile
uloop run-tests
```

### PlayMode Bug 诊断

```bash
uloop control-play-mode --action Play
uloop screenshot --capture-mode rendering
uloop simulate-mouse-ui --action Click --x 400 --y 300
uloop screenshot --capture-mode rendering
uloop get-logs
uloop control-play-mode --action Stop
```

### 输入录制用于 E2E 测试

```bash
uloop control-play-mode --action Play
uloop record-input --action Start
# ... 手动游戏操作 ...
uloop record-input --action Stop
uloop control-play-mode --action Stop

# 之后：回放
uloop control-play-mode --action Play
uloop replay-input --input-path recording.json
uloop screenshot --capture-mode rendering
```

### 动态代码探针

```bash
# 检查运行时状态
uloop execute-dynamic-code --code '
using UnityEngine;
var controller = Object.FindObjectOfType<GameController>();
return $"Phase: {controller.phase}, Locked: {controller.inputLocked}";
'
```

## 依赖关系

此包被以下项目使用：
- **unity-validation-router** - Unity 变更的验证路由技能

## 版本

当前版本：**1.0.0**

版本历史见 [CHANGELOG.md](CHANGELOG.md)。

## 许可证

MIT License - 见 [LICENSE](LICENSE) 文件。
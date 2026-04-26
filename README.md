# Unity CLI Loop (uloop)

A collection of Claude Code skills for Unity Editor automation via CLI.

## Overview

**uloop** provides 18 skills for Unity Editor automation:

| Category | Skills |
|----------|--------|
| **Editor Control** | `launch`, `compile`, `control-play-mode`, `clear-console`, `focus-window` |
| **Inspection** | `get-hierarchy`, `find-game-objects`, `get-logs`, `screenshot` |
| **Testing** | `run-tests` |
| **Dynamic Code** | `execute-dynamic-code`, `execute-menu-item` |
| **Input Simulation** | `simulate-mouse-ui`, `simulate-mouse-input`, `simulate-keyboard` |
| **Recording** | `record-input`, `replay-input` |

## Installation

### Prerequisites

1. **uloop CLI** - Install the CLI tool first
2. **Unity Editor** - Target Unity project must be open
3. **Input System** - Required for input simulation skills (package: `com.unity.inputsystem`)

### Skill Setup

Clone or copy this directory to your Claude Code skills folder:

```
skills/
└── unity-cli-loop/
    ├── SKILL.md                    # Package overview
    ├── uloop-compile/
    ├── uloop-control-play-mode/
    ├── uloop-screenshot/
    ├── uloop-execute-dynamic-code/
    │   ├── SKILL.md
    │   └── references/
    │       ├── prefab-operations.md
    │       ├── scene-operations.md
    │       ├── playmode-inspection.md
    │       └── ...
    └── ...
```

## Skills Reference

### Editor Control

#### uloop-launch
Launch Unity Editor with the correct version for a project.

```bash
uloop launch [project-path] [-r] [-p Android]
```

#### uloop-compile
Compile Unity project and report errors/warnings.

```bash
uloop compile [--force-recompile] [--wait-for-domain-reload]
```

#### uloop-control-play-mode
Control Unity Editor play mode (play/stop/pause).

```bash
uloop control-play-mode --action Play
uloop control-play-mode --action Stop
uloop control-play-mode --action Pause
```

### Inspection

#### uloop-get-hierarchy
Get Unity scene hierarchy as a structured tree.

```bash
uloop get-hierarchy [--root-path "Canvas/UI"] [--max-depth 2]
```

#### uloop-screenshot
Capture screenshots of Unity Editor windows.

```bash
uloop screenshot                              # Game View
uloop screenshot --capture-mode rendering     # Game rendering (PlayMode)
uloop screenshot --window-name Scene          # Scene View
```

#### uloop-get-logs
Get Unity Console logs.

```bash
uloop get-logs [--filter-type error|warning|log]
```

### Testing

#### uloop-run-tests
Execute Unity Test Runner.

```bash
uloop run-tests                              # EditMode tests
uloop run-tests --test-mode PlayMode         # PlayMode tests
uloop run-tests --filter-type exact --filter-value "MyTest"
```

### Dynamic Code Execution

#### uloop-execute-dynamic-code
Execute C# code dynamically in Unity Editor (Roslyn).

```bash
uloop execute-dynamic-code --code 'using UnityEngine; return Mathf.PI;'
```

See `references/` folder for code examples:
- `prefab-operations.md` - Create prefabs, instantiate, add components
- `scene-operations.md` - Create GameObjects, wire references
- `playmode-inspection.md` - Runtime state inspection
- `playmode-automation-zsh.md` / `powershell.md` - PlayMode automation

### Input Simulation

#### uloop-simulate-mouse-ui
Simulate mouse interaction on UI elements (EventSystem).

```bash
uloop simulate-mouse-ui --action Click --x 400 --y 300
uloop simulate-mouse-ui --action Drag --from-x 100 --from-y 200 --x 400 --y 300
```

#### uloop-simulate-mouse-input
Simulate mouse input via Input System (game logic).

```bash
uloop simulate-mouse-input --action Click --x 400 --y 300
uloop simulate-mouse-input --action Scroll --scroll-y 120
```

#### uloop-simulate-keyboard
Simulate keyboard input.

```bash
uloop simulate-keyboard --action Press --key Space
```

### Recording & Replay

#### uloop-record-input
Record keyboard and mouse input during PlayMode.

```bash
uloop record-input --action Start
uloop record-input --action Stop --output-path my-recording.json
```

#### uloop-replay-input
Replay recorded input for deterministic testing.

```bash
uloop replay-input --input-path my-recording.json
```

## Common Workflows

### Compile and Test

```bash
uloop compile
uloop run-tests
```

### PlayMode Bug Diagnosis

```bash
uloop control-play-mode --action Play
uloop screenshot --capture-mode rendering
uloop simulate-mouse-ui --action Click --x 400 --y 300
uloop screenshot --capture-mode rendering
uloop get-logs
uloop control-play-mode --action Stop
```

### Input Recording for E2E Testing

```bash
uloop control-play-mode --action Play
uloop record-input --action Start
# ... manual gameplay ...
uloop record-input --action Stop
uloop control-play-mode --action Stop

# Later: replay
uloop control-play-mode --action Play
uloop replay-input --input-path recording.json
uloop screenshot --capture-mode rendering
```

### Dynamic Code Probe

```bash
# Check runtime state
uloop execute-dynamic-code --code '
using UnityEngine;
var controller = Object.FindObjectOfType<GameController>();
return $"Phase: {controller.phase}, Locked: {controller.inputLocked}";
'
```

## Dependencies

This package is used by:
- **unity-validation-router** - Validation routing skill for Unity changes

## Version

Current version: **1.0.0**

See [CHANGELOG.md](CHANGELOG.md) for version history.

## License

MIT License - see [LICENSE](LICENSE) file.
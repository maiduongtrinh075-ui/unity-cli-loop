---
name: unity-cli-loop
version: "1.0.0"
description: "Unity Editor automation via uloop CLI. Provides skills for: compilation, play mode control, scene inspection, screenshot capture, test execution, dynamic C# code execution, input simulation (mouse/keyboard), and input recording/replay. Requires uloop CLI tool and Unity Editor."
---

# Unity CLI Loop (uloop)

This package provides Claude Code skills for Unity Editor automation via the uloop CLI tool.

## Skills Included

| Skill | Description |
|-------|-------------|
| `uloop-launch` | Launch Unity Editor with correct version |
| `uloop-compile` | Compile project, report errors/warnings |
| `uloop-control-play-mode` | Play/stop/pause Unity Editor |
| `uloop-clear-console` | Clear Unity Console |
| `uloop-focus-window` | Focus specific EditorWindow |
| `uloop-get-hierarchy` | Get scene hierarchy tree |
| `uloop-find-game-objects` | Find GameObjects by criteria |
| `uloop-get-logs` | Get Console logs |
| `uloop-screenshot` | Capture screenshots |
| `uloop-run-tests` | Execute Unity Test Runner |
| `uloop-execute-dynamic-code` | Dynamic C# execution (Roslyn) |
| `uloop-execute-menu-item` | Execute Unity menu items |
| `uloop-simulate-mouse-ui` | UI mouse simulation (EventSystem) |
| `uloop-simulate-mouse-input` | Gameplay mouse input (Input System) |
| `uloop-simulate-keyboard` | Keyboard input simulation |
| `uloop-record-input` | Record input during PlayMode |
| `uloop-replay-input` | Replay recorded input |

## Prerequisites

- **uloop CLI** - Must be installed and available in PATH
- **Unity Editor** - Target project must be open
- **Input System** - Required for input simulation (`com.unity.inputsystem`)

## Usage

Invoke individual skills via `$skill-name`:

```
Use $uloop-compile to check compilation
Use $uloop-screenshot to capture Game View
Use $uloop-execute-dynamic-code to inspect runtime state
```

## Full Documentation

See [README.md](README.md) for complete usage guide.
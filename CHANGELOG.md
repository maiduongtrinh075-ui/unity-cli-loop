# Changelog

All notable changes to this skill package will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-04-26

### Added
- Initial release with 18 skills:
  - `uloop-launch` - Launch Unity Editor with correct version
  - `uloop-compile` - Compile Unity project
  - `uloop-control-play-mode` - Control play/stop/pause
  - `uloop-clear-console` - Clear Unity Console
  - `uloop-focus-window` - Focus EditorWindow
  - `uloop-get-hierarchy` - Get scene hierarchy tree
  - `uloop-find-game-objects` - Find GameObjects by criteria
  - `uloop-get-logs` - Get Console logs
  - `uloop-screenshot` - Capture Editor window screenshots
  - `uloop-run-tests` - Execute Unity Test Runner
  - `uloop-execute-dynamic-code` - Dynamic C# execution (Roslyn)
  - `uloop-execute-menu-item` - Execute Unity menu items
  - `uloop-simulate-mouse-ui` - UI mouse simulation (EventSystem)
  - `uloop-simulate-mouse-input` - Gameplay mouse input (Input System)
  - `uloop-simulate-keyboard` - Keyboard input simulation
  - `uloop-record-input` - Record input during PlayMode
  - `uloop-replay-input` - Replay recorded input
- Reference documentation for `execute-dynamic-code`:
  - `prefab-operations.md` - Prefab creation and modification
  - `scene-operations.md` - Scene and GameObject operations
  - `material-operations.md` - Material operations
  - `asset-operations.md` - Asset search and management
  - `scriptableobject.md` - ScriptableObject operations
  - `batch-operations.md` - Bulk operations
  - `cleanup-operations.md` - Cleanup broken references
  - `undo-operations.md` - Undo-aware operations
  - `selection-operations.md` - Selection management
  - `playmode-inspection.md` - Runtime state inspection
  - `playmode-automation-zsh.md` - PlayMode automation (zsh)
  - `playmode-automation-powershell.md` - PlayMode automation (PowerShell)
  - `playmode-ui-controls.md` - UI control simulation
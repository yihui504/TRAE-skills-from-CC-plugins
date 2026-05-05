# 其他环境 Tool Mapping

Skills use TRAE IDE tool names. When you encounter these in a skill, use your platform equivalent:

| Skill references | 其他环境 equivalent |
|-----------------|----------------------|
| `Read` (file reading) | `read_file` |
| `Write` (file creation) | `write_file` |
| `Edit` (file editing) | `replace` |
| `Bash` (run commands) | `run_shell_command` |
| `Grep` (search file content) | `grep_search` |
| `Glob` (search files by name) | `glob` |
| `TodoWrite` (task tracking) | `write_todos` |
| `Skill` tool (invoke a skill) | `activate_skill` |
| `WebSearch` | `google_web_search` |
| `WebFetch` | `web_fetch` |
| 智能体调用 (调用 智能体) | No equivalent — 其他环境 does not support 智能体 |

## No 智能体 support

其他环境 has no equivalent to TRAE IDE's 智能体调用. Skills that rely on 智能体 dispatch (`subagent-driven-development`, `dispatching-parallel-agents`) will fall back to single-session execution via `executing-plans`.

## Additional 其他环境 tools

These tools are available in 其他环境 but have no TRAE IDE equivalent:

| Tool | Purpose |
|------|---------|
| `list_directory` | List files and subdirectories |
| `save_memory` | Persist facts to 项目规则文件 across sessions |
| `ask_user` | Request structured input from the user |
| `tracker_create_task` | Rich task management (create, update, list, visualize) |
| `enter_plan_mode` / `exit_plan_mode` | Switch to read-only research mode before making changes |

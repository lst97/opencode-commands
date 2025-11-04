# OpenCode Commands Documentation

This repository contains personal documentation and configurations for **OpenCode** - an open-source AI coding assistant that works directly in your terminal.

## What is OpenCode?

OpenCode is an open-source AI coding agent built from the ground up for the terminal. It provides a powerful, interactive experience that allows developers to integrate AI assistance directly into their workflow. With OpenCode, you can type commands like `opencode fix error in main.go` and the AI will instantly read your code, identify problems, and suggest solutions.

### Key Features

- **Terminal-based AI assistant** - Works directly in your command line
- **Context-aware** - Understands your codebase and current work
- **Custom commands** - Create reusable workflows and prompts
- **Multiple tools** - File operations, web fetching, shell commands, and more
- **Agent system** - Configure different AI agents for specific tasks

## Installation

```bash
pnpm install -g opencode-ai
```

## Basic Usage

### Interactive Mode

```bash
opencode
```

Starts the OpenCode TUI (Terminal User Interface) for interactive sessions.

### One-shot Mode

```bash
opencode run "Explain the most common uses of the 'awk' command with examples"
```

Execute commands without entering the interactive TUI.

## Custom Commands

Custom commands allow you to create reusable prompts and workflows. Commands can be defined in two ways:

### 1. Configuration File

Add commands to your OpenCode config using the `command` option:

```json
{
  "commands": {
    "test": {
      "template": "Run tests and check for any failures",
      "description": "Run test suite"
    }
  }
}
```

### 2. Markdown Files

Create markdown files in the `command/` directory:

- Global: `~/.config/opencode/command/`
- Per-project: `.opencode/command/`

Example `.opencode/command/test.md`:

```markdown
---
template: "Run tests and check for any failures"
description: "Run test suite"
---

Run tests and check for any failures
```

### Command Features

#### Arguments

Use placeholders to pass arguments:

- `$ARGUMENTS` - All arguments
- `$1`, `$2`, `$3` - Positional arguments

#### Shell Output

Inject shell command output with `!command`:

```markdown
Check test coverage: !npm run test:coverage
```

#### File References

Include files with `@filename`:

```markdown
Review this file: @src/main.js
```

## Available Tools

OpenCode provides built-in tools that the AI can use:

### File Operations

- **read** - Read file contents
- **write** - Create or overwrite files
- **edit** - Modify existing files with precise replacements
- **list** - List directory contents
- **glob** - Find files by pattern matching
- **grep** - Search file contents with regex
- **patch** - Apply patches to files

### Development Tools

- **bash** - Execute shell commands
- **webfetch** - Fetch and read web content
- **todowrite/todoread** - Manage task lists

### Configuration

Tools can be configured globally or per-agent, with options to:

- Enable/disable specific tools
- Set permissions for tool usage
- Configure wildcards for bulk tool management

## Built-in Commands

OpenCode includes several built-in commands:

- `/init` - Initialize project
- `/undo` - Undo last action
- `/redo` - Redo last action
- `/share` - Share session
- `/help` - Show help

Custom commands with the same name will override built-in commands.

## Project Structure

This repository is organized for personal OpenCode configurations and documentation:

```bash
.
├── README.md                 # This file
├── .opencode/               # Project-specific OpenCode config
│   ├── command/             # Custom commands
│   └── config.json          # OpenCode configuration
└── docs/                    # Additional documentation
```

## Configuration

OpenCode can be configured through:

- Global config: `~/.config/opencode/config.json`
- Project config: `.opencode/config.json`

### Example Configuration

```json
{
  "model": "claude-3-5-sonnet-20241022",
  "tools": {
    "bash": true,
    "write": true,
    "edit": true,
    "read": true,
    "webfetch": true
  },
  "agents": {
    "plan": {
      "model": "claude-3-haiku-20240307",
      "tools": {
        "write": false,
        "bash": false
      }
    }
  },
  "commands": {
    "review": {
      "template": "Review the current code for improvements",
      "description": "Code review"
    }
  }
}
```

## Resources

- [Official OpenCode Documentation](https://opencode.ai/docs/)
- [GitHub Repository](https://github.com/sst/opencode)
- [Commands Documentation](https://opencode.ai/docs/commands/)
- [Tools Documentation](https://opencode.ai/docs/tools/)

## Contributing

This is a personal documentation repository for OpenCode configurations and custom commands. Feel free to adapt the configurations and commands for your own use cases.

## License

See [LICENSE](LICENSE) file for details.

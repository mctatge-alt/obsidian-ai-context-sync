# AI Context Sync for Obsidian

[![GitHub release](https://img.shields.io/github/v/release/mitchelltatge/obsidian-ai-context-sync)](https://github.com/mitchelltatge/obsidian-ai-context-sync/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**One source of truth for all your AI coding assistants.**

Tired of maintaining separate context files for Claude, Cursor, GitHub Copilot, and other AI tools? This Obsidian plugin lets you write your project context once and sync it everywhere.

![AI Context Sync Demo](./assets/demo.gif)

## The Problem

Modern AI coding assistants use different context files:
- **Claude Code** → `CLAUDE.md`
- **Cursor** → `.cursor/rules/*.md` (works with GPT, Claude, Gemini, DeepSeek, etc.)
- **GitHub Copilot** → `.github/copilot-instructions.md`
- **Windsurf/Codeium** → `.windsurfrules`
- **Continue.dev** → `.continuerules`
- **Sourcegraph Cody** → `.cody/instructions.md`
- **OpenAI Codex CLI** → `AGENTS.md`
- **DeepSeek Coder** → `DEEPSEEK.md`
- **Google Gemini** → `.gemini/context.md`
- **Amazon Q** → `.amazonq/rules.md`
- **Zed AI** → `.zed/assistant/context.md`
- **Aider** → `.aider.conf.yml`
- **ChatGPT** → Manual memory export
- **AGENTS.md** → Universal standard (emerging)

When you work primarily with one tool (like Claude) but occasionally switch to others (like Cursor with GPT), your carefully crafted context doesn't transfer. You end up maintaining multiple files or getting subpar assistance.

## The Solution

Write your AI context once in Obsidian, sync to all your tools automatically.

```
                    ┌─────────────────────┐
                    │   Obsidian Note     │
                    │   "AI Context.md"   │
                    └─────────┬───────────┘
                              │
                              ▼
                        ┌───────────┐
                        │ AI Context│
                        │   Sync    │
                        └─────┬─────┘
                              │
       ┌──────────┬───────────┼───────────┬──────────┐
       ▼          ▼           ▼           ▼          ▼
   ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐
   │CLAUDE  │ │AGENTS  │ │.cursor/│ │.windsurf│ │.github/│
   │.md     │ │.md     │ │rules/  │ │rules    │ │copilot │
   └────────┘ └────────┘ └────────┘ └────────┘ └────────┘
       │          │           │           │          │
       ▼          ▼           ▼           ▼          ▼
    Claude    DeepSeek     Cursor      Windsurf   Copilot
              Codex CLI   (any model)  Codeium
              Gemini
              ChatGPT*
```
*ChatGPT export is for manual copy/paste into memory

## Features

- 🔄 **Auto-sync** - Syncs automatically when you save your source note
- 🎯 **Multi-target** - Sync to Claude, Cursor, Copilot, AGENTS.md, and more
- 📁 **Multi-project** - Sync to multiple project directories at once
- 📝 **Templates** - Customizable output templates per target
- ⚡ **Commands** - Quick commands for manual sync and configuration
- 📊 **Status bar** - See sync status at a glance

## Installation

### From Obsidian Community Plugins (Recommended)

1. Open Obsidian Settings
2. Go to Community Plugins → Browse
3. Search for "AI Context Sync"
4. Click Install, then Enable

### Manual Installation

1. Download the latest release from [GitHub Releases](https://github.com/mitchelltatge/obsidian-ai-context-sync/releases)
2. Extract to your vault's `.obsidian/plugins/ai-context-sync/` folder
3. Reload Obsidian
4. Enable the plugin in Settings → Community Plugins

### From Source

```bash
git clone https://github.com/mitchelltatge/obsidian-ai-context-sync.git
cd obsidian-ai-context-sync
npm install
npm run build
```

Copy `main.js`, `manifest.json`, and `styles.css` to your vault's `.obsidian/plugins/ai-context-sync/` folder.

## Quick Start

1. **Create your context note** - Use the command `AI Context Sync: Create AI context template note` to get started with a template, or use any existing note

2. **Set as source** - Open your context note and run `AI Context Sync: Set current note as AI context source`

3. **Add project paths** - Run `AI Context Sync: Add project path` to add your project directories

4. **Sync!** - Click the sync icon in the ribbon or run `AI Context Sync: Sync AI context to all targets`

## Configuration

### Settings

| Setting | Description |
|---------|-------------|
| Source note | The Obsidian note containing your AI context |
| Auto-sync on save | Automatically sync when source note is modified |
| Show status bar | Display sync status in Obsidian's status bar |
| Include timestamp | Add timestamp comments to synced files |
| Custom header | Header comment added to all synced files |

### Sync Targets

Enable/disable specific targets in settings:

| Target | Output Path | Description |
|--------|-------------|-------------|
| Claude Code | `CLAUDE.md` | Claude Code's context file |
| AGENTS.md | `AGENTS.md` | Universal standard (Codex, DeepSeek, etc.) |
| Cursor Rules | `.cursor/rules/ai-context.md` | Works with ALL Cursor models |
| GitHub Copilot | `.github/copilot-instructions.md` | Copilot custom instructions |
| Windsurf | `.windsurfrules` | Windsurf/Codeium rules |
| Continue.dev | `.continuerules` | Continue for VS Code/JetBrains |
| Sourcegraph Cody | `.cody/instructions.md` | Cody context instructions |
| OpenAI Codex CLI | `AGENTS.md` | Codex CLI reads AGENTS.md |
| ChatGPT | `.chatgpt/project-context.md` | Export for manual memory |
| DeepSeek Coder | `DEEPSEEK.md` | DeepSeek context file |
| Google Gemini | `.gemini/context.md` | Gemini/AI Studio context |
| Amazon Q | `.amazonq/rules.md` | Amazon Q Developer rules |
| Zed AI | `.zed/assistant/context.md` | Zed editor AI assistant |
| Aider | `.aider.conf.yml` | Aider configuration |

### Project Paths

Add multiple project directories to sync your context to all your codebases:

- `/Users/you/projects/my-app`
- `/Users/you/projects/another-project`
- `/Users/you/work/client-project`

## Commands

| Command | Description |
|---------|-------------|
| Sync AI context to all targets | Sync to all enabled targets |
| Sync AI context to specific target | Choose a specific target to sync |
| Set current note as AI context source | Set the open note as the source |
| Add project path | Add a project directory for syncing |
| Create AI context template note | Create a starter template |

## Template Variables

Use these variables in custom templates:

| Variable | Description |
|----------|-------------|
| `{{CONTENT}}` | The content of your source note |
| `{{HEADER}}` | The configured header comment |
| `{{TIMESTAMP}}` | Current ISO timestamp |
| `{{SOURCE}}` | Path to the source note |

## Example Context Note

```markdown
# AI Context

## Project Overview
A React + TypeScript web application for task management.

## Tech Stack
- Frontend: React 18, TypeScript, TailwindCSS
- Backend: Node.js, Express, PostgreSQL
- Testing: Vitest, Playwright

## Coding Conventions
- Use functional components with hooks
- Prefer named exports
- Use `const` by default, `let` only when reassignment is needed
- Error handling: Always use try/catch with proper error types

## File Organization
- `src/components/` - React components
- `src/hooks/` - Custom hooks
- `src/utils/` - Utility functions
- `src/types/` - TypeScript type definitions

## Important Patterns
- State management via Zustand
- API calls through custom `useQuery` hook
- Form handling with React Hook Form + Zod

## Things to Avoid
- Don't use `any` type
- Don't use default exports (except for pages)
- Don't mutate state directly
```

## Why Obsidian?

Obsidian is the perfect home for AI context because:

1. **Already in your workflow** - If you use Obsidian for notes, your context is always accessible
2. **Markdown native** - Perfect format for AI context files
3. **Linking** - Link your context to other notes, documentation, decisions
4. **Version history** - Track changes to your context over time
5. **Cross-platform** - Access and edit from any device

## Roadmap

- [ ] Import existing CLAUDE.md/AGENTS.md back into Obsidian
- [ ] Template library for common project types
- [ ] Git integration (auto-commit synced files)
- [ ] Selective section sync (sync only parts of a note)
- [ ] VS Code extension companion

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

MIT License - see [LICENSE](LICENSE) for details.

## Acknowledgments

- Inspired by the fragmentation of AI context files across different tools
- Built with the [Obsidian Plugin API](https://docs.obsidian.md/Plugins/Getting+started/Build+a+plugin)
- Thanks to the Obsidian community for plugin development resources

---

**Found this useful?** Give it a ⭐ on [GitHub](https://github.com/mitchelltatge/obsidian-ai-context-sync)!

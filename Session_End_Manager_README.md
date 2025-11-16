# Session-End Manager Agent for Claude Code

Automate end-of-session documentation, git commits, and multi-AI context synchronization with a single "wrap up" command.

## What It Does

The Session-End Manager is a Claude Code agent that executes comprehensive end-of-session workflows automatically:

- ✅ **Documentation**: Updates CLAUDE.md, AGENTS.md, GEMINI.md with session insights
- ✅ **Git Operations**: Creates meaningful commit messages, stages changes, commits with co-authorship
- ✅ **Session Summaries**: Generates searchable markdown summaries with decisions, artifacts, and next steps
- ✅ **Context Syncing**: Synchronizes context across multiple AI assistants for seamless handoffs
- ✅ **README Updates**: Keeps project documentation current with session changes

**Time saved per session**: 25-30 minutes (documentation + git operations + context prep for next session)

## Why Use This?

**Before Session-End Manager**:
- Manual documentation: 10-15 min
- Git commit messages: 5-10 min
- Context switching prep: 10 min
- Forgotten decisions and lost context

**After Session-End Manager**:
- Single command: "wrap up"
- 3 minutes automated execution
- Comprehensive, searchable session history
- Perfect context preservation for next session

## Prerequisites

- [Claude Code](https://claude.ai/code) installed and configured
- Git repository initialized in your project
- Project uses modular documentation structure (CLAUDE.md, AGENTS.md, GEMINI.md)

## Installation

1. **Download the agent file**: Save `session-end-manager.md` to your project's `.claude/agents/` directory

2. **Verify structure**:
   ```bash
   .claude/
   └── agents/
       └── session-end-manager.md
   ```

3. **Restart Claude Code** (if already running) to load the agent

## Usage

### Basic Usage

At the end of any coding session, simply run:

```
wrap up
```

Claude Code will invoke the session-end-manager agent and execute the full workflow.

### What Gets Created

**1. Session Summary** (in `Claude/sessions/YYYY-MM/`):
```markdown
SESSION_SUMMARY_YYYYMMDD_TOPIC.md

## Session Summary
**Date**: 2025-11-15
**Focus**: Social media automation - image generation integration

**Key Decisions**:
- Caddy dual-route architecture (internal http:// for Docker, external https:// for testing)
- getBinaryDataBuffer() for n8n filesystem compatibility

**Artifacts Created**:
- Social_Media_Image_Gen_and_Post workflow (n8n)
- Caddy configuration for /media serving

**Next Session**: Test end-to-end posting with NocoDB migration
```

**2. Updated Context Files**:
- `CLAUDE.md`: Current Focus section updated
- `AGENTS.md`: Synced from CLAUDE.md
- `GEMINI.md`: Synced from CLAUDE.md

**3. Git Commit**:
```bash
Session end: [Brief description of session work]

🤖 Generated with Claude Code (https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>
```

### Advanced Usage

**Customize for your workflow**:

Edit `.claude/agents/session-end-manager.md` to adjust:
- Documentation structure (add/remove context files)
- Session summary format
- Git commit message style
- Additional automation steps

## Example Output

After running "wrap up", you'll see:

```
✅ Session summary created: Claude/sessions/2025-11/SESSION_SUMMARY_20251115_SOCIAL_MEDIA_AUTOMATION.md
✅ CLAUDE.md updated (Current Focus section)
✅ Synced: CLAUDE.md → AGENTS.md, GEMINI.md
✅ Git commit created: 8e8a5e6
✅ Changes pushed to main

Session wrapped successfully!
```

## Integration with Other AI Tools

The Session-End Manager maintains context across multiple AI assistants:

- **CLAUDE.md**: Primary context for Claude Code
- **AGENTS.md**: Shared context for specialized agents
- **GEMINI.md**: Research context for Gemini (headless mode)

When you start a new session with any AI, they have full context from the previous session without manual handoff.

## Modular Documentation Structure

This agent works best with a modular documentation setup:

```
project/
├── CLAUDE.md               # Lightweight index (~250 lines)
├── AGENTS.md               # Synced copy for agents
├── GEMINI.md               # Synced copy for Gemini
├── docs/
│   ├── architecture/       # Detailed architecture docs
│   ├── patterns/           # Workflow patterns
│   └── troubleshooting/    # Issue resolution guides
└── Claude/
    └── sessions/
        └── 2025-11/        # Monthly session summaries
```

See [modular documentation guide](link-to-guide) for setup details.

## Troubleshooting

### Agent not found

**Symptom**: Claude Code says "I don't have a session-end-manager agent"

**Fix**:
1. Verify file is at `.claude/agents/session-end-manager.md`
2. Restart Claude Code
3. Try: `claude code --list-agents` to confirm it's loaded

### Git commit fails

**Symptom**: Error during git operations

**Fix**:
1. Ensure git is initialized: `git status`
2. Ensure you have staged changes
3. Check git config: `git config user.name` and `git config user.email`

### Context files not syncing

**Symptom**: AGENTS.md or GEMINI.md not updated

**Fix**:
1. Verify files exist in project root
2. Check file permissions (must be writable)
3. Review session summary for sync confirmation

## ROI

**Time investment**:
- Setup: 10 minutes (one-time)
- Per session: 3 minutes (automated)

**Time saved**:
- Per session: 25-30 minutes
- Per month (20 sessions): 8-10 hours
- Per year: 100+ hours

**Value beyond time**:
- Searchable decision history (find "why we did X" in seconds)
- Perfect context preservation (no "what was I working on?" moments)
- Compounding automation patterns (session summaries become reusable templates)

## Credits

Created as part of a multi-AI orchestration workflow combining Claude Code, Gemini (headless mode), and n8n MCP integration.

Inspired by NetworkChuck's [Claude Code tutorial](https://youtu.be/MsQACpcuTkU).

## License

MIT License - feel free to adapt for your workflow.

## Contributing

Found a way to improve the session-end workflow? Open an issue or submit a PR!

## Related Resources

- [Claude Code Documentation](https://claude.ai/code)
- [Modular Documentation Structure Guide](link-to-guide)
- [Multi-AI Orchestration Setup](link-to-article)

---

**Last Updated**: 2025-11-15
**Version**: 1.0
**Tested with**: Claude Code (claude-sonnet-4-5), Git 2.x

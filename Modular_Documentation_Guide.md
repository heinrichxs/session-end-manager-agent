# Modular Documentation Guide for AI-Assisted Development

A lightweight documentation structure optimized for AI assistants with context limits and multi-AI workflows.

## Table of Contents
- [The Problem](#the-problem)
- [The Solution: Modular Documentation](#the-solution-modular-documentation)
- [Structure Overview](#structure-overview)
- [Implementation Guide](#implementation-guide)
- [Multi-AI Synchronization](#multi-ai-synchronization)
- [Session Summaries](#session-summaries)
- [Best Practices](#best-practices)
- [Examples](#examples)

---

## The Problem

**Traditional documentation fails with AI assistants**:

1. **Context Limits**: Large README/CLAUDE.md files (500+ lines) consume 15-25% of AI context windows, leaving less room for actual code and conversation
2. **Maintenance Overhead**: Monolithic docs become stale quickly - updating one section requires reviewing the entire file
3. **Multi-AI Chaos**: Using Claude Code + Gemini + other AIs means maintaining separate context files manually
4. **Lost History**: Critical decisions buried in git commits or forgotten conversations

**Symptoms you need modular documentation**:
- Your CLAUDE.md or README is 500+ lines
- You frequently say "I mentioned this earlier" to AI assistants
- Context switching between AIs requires re-explaining everything
- You can't remember why you made a decision 2 weeks ago

---

## The Solution: Modular Documentation

**Core Principle**: Lightweight index files + detailed content in organized folders + automated session summaries

**Benefits**:
- ✅ **Small Context Footprint**: CLAUDE.md stays ~200-250 lines, leaving 95%+ of context for code
- ✅ **Easy Maintenance**: Update only relevant docs/ files, not massive monoliths
- ✅ **Perfect Multi-AI Sync**: Automated syncing across CLAUDE.md → AGENTS.md → GEMINI.md
- ✅ **Searchable History**: Session summaries capture decisions, searchable by keyword
- ✅ **Scalable**: Add new docs without bloating index files

---

## Structure Overview

```
project/
├── CLAUDE.md                      # Lightweight index (~200-250 lines)
├── AGENTS.md                      # Synced copy for Claude agents
├── GEMINI.md                      # Synced copy for Gemini (headless mode)
├── README.md                      # Public-facing project documentation
│
├── docs/                          # Detailed documentation folders
│   ├── architecture/
│   │   ├── overview.md            # System architecture
│   │   ├── service-stack.md       # Infrastructure details
│   │   └── data-flow.md           # Data flow diagrams
│   ├── patterns/
│   │   ├── n8n-patterns.md        # Workflow patterns
│   │   ├── api-patterns.md        # API integration patterns
│   │   └── deployment-patterns.md # Deployment best practices
│   ├── troubleshooting/
│   │   ├── n8n-issues.md          # n8n troubleshooting
│   │   ├── linkedin-api.md        # LinkedIn API issues
│   │   └── infrastructure.md      # Infrastructure problems
│   └── deployment/
│       ├── common-commands.md     # Operational commands
│       └── backup-restore.md      # Backup procedures
│
└── Claude/                        # AI session management
    └── sessions/
        ├── 2025-11/               # Monthly session summaries
        │   ├── SESSION_SUMMARY_20251115_TOPIC.md
        │   ├── SESSION_SUMMARY_20251114_TOPIC.md
        │   └── ...
        └── 2025-12/
            └── ...
```

---

## Implementation Guide

### Step 1: Create the Lightweight Index (CLAUDE.md)

**Goal**: Keep CLAUDE.md under 250 lines - it's a navigation file, not a knowledge base.

**Template Structure**:
```markdown
# CLAUDE.md - Quick Reference & Navigation

## Quick Navigation

### Documentation
- [Architecture Overview](docs/architecture/overview.md)
- [n8n Patterns](docs/patterns/n8n-patterns.md)
- [Troubleshooting](docs/troubleshooting/)
- [Common Commands](docs/deployment/common-commands.md)

### Recent Work
- [Session Summaries](Claude/sessions/2025-11/)
- [Latest Session](Claude/sessions/2025-11/SESSION_SUMMARY_20251115_TOPIC.md)

## Current Focus (Date)

**Status**: [Current work status in 1-2 sentences]

**Next Steps**:
1. [Immediate next task]
2. [Following task]
3. [Third task]

**Known Issues**:
- [Critical issue 1]
- [Critical issue 2]

## Top 10 Critical Patterns

[Quick reference patterns - 1-2 lines each with link to full docs]

## Quick Start Commands

```bash
# Start services
command here

# View logs
command here
```

## Project Overview

[2-3 paragraph summary - link to docs/architecture/overview.md for details]

## Key Decisions & Context

[Recent major decisions - 1 line each with date, link to session summary]

## Lessons Learned

[Latest lessons - 1-2 lines each with date, link to full docs]

---

**Last Updated**: YYYY-MM-DD
**Documentation Structure**: Modular (CLAUDE.md ~XXX lines, detailed content in docs/)
**Status**: Active Development - [Current Phase]
```

**Rules**:
- ✅ Only update "Current Focus" and "Recent Work" sections regularly
- ✅ Link to detailed docs/ files, don't duplicate content
- ✅ Keep total under 250 lines
- ✅ Use session-end-manager to automate updates

### Step 2: Create docs/ Folders

**Organize by concern**:

**docs/architecture/** - "How is this built?"
- System design, service stacks, data flow
- Infrastructure diagrams
- Component relationships

**docs/patterns/** - "How do we solve recurring problems?"
- Workflow patterns (n8n, API, deployment)
- Code patterns
- Integration patterns

**docs/troubleshooting/** - "What breaks and how do we fix it?"
- Known issues by component
- Error messages and solutions
- Debugging guides

**docs/deployment/** - "How do we operate this?"
- Common commands
- Backup/restore procedures
- Monitoring setup

**Example docs/patterns/n8n-patterns.md**:
```markdown
# n8n Workflow Patterns

Production-tested patterns for n8n automation.

## Pattern 1: HTTP Request Data Loss

**Problem**: HTTP Request nodes strip all upstream data

**Solution**:
```javascript
const originalData = $('Previous Node').first().json;
return [{ json: { ...originalData, newField: value } }];
```

**When to Use**: Any HTTP Request node that needs to preserve upstream context

**Related**: See troubleshooting/n8n-issues.md for debugging
```

### Step 3: Set Up Session Summaries

**Create Claude/sessions/ structure**:
```bash
mkdir -p Claude/sessions/$(date +"%Y-%m")
```

**Session summary template** (automated by session-end-manager):
```markdown
# Session Summary - YYYY-MM-DD - [Topic]

**Date**: YYYY-MM-DD
**Focus**: [1 sentence describing session focus]
**Duration**: ~X hours

## Accomplishments

1. [Major accomplishment 1]
2. [Major accomplishment 2]
3. [Major accomplishment 3]

## Key Decisions

**Decision 1**: [What was decided]
- **Context**: [Why it mattered]
- **Rationale**: [Why this approach]
- **Alternative Considered**: [What was rejected and why]

## Technical Details

**Files Modified**:
- `path/to/file.ext` - [What changed and why]
- `another/file.ext` - [What changed and why]

**New Patterns Discovered**:
- [Pattern name]: [Brief description, link to docs/patterns/]

**Issues Encountered**:
- [Issue]: [How it was resolved]

## Artifacts Created

- [File/workflow/config created]
- [Documentation added]

## Next Session Priorities

1. [Top priority task]
2. [Second priority]
3. [Third priority]

## Lessons Learned

**What Worked**:
- [Approach that succeeded]

**What Didn't**:
- [Approach that failed and why]

**Would Do Differently**:
- [Hindsight improvements]

---

**Documentation Updated**: CLAUDE.md, [other files]
**Git Commit**: [commit hash]
```

### Step 4: Multi-AI Synchronization

**Create sync copies**:
```bash
cp CLAUDE.md AGENTS.md
cp CLAUDE.md GEMINI.md
```

**Purpose**:
- **CLAUDE.md**: Primary context for Claude Code
- **AGENTS.md**: Context for specialized Claude agents
- **GEMINI.md**: Context for Gemini research (headless mode)

**Automation** (via session-end-manager):
```bash
# In session-end-manager agent
cp CLAUDE.md AGENTS.md
cp CLAUDE.md GEMINI.md
echo "✅ Synced: CLAUDE.md → AGENTS.md, GEMINI.md"
```

**When to sync**:
- ✅ After every session (via session-end-manager)
- ✅ When updating "Current Focus" in CLAUDE.md
- ✅ When adding major decisions or lessons learned

---

## Multi-AI Synchronization

### Why Sync Matters

**Without syncing**:
- Claude Code knows about a pattern from yesterday
- Gemini doesn't, requires manual re-explanation
- Agents start from scratch each invocation

**With syncing**:
- Single source of truth (CLAUDE.md)
- All AIs read from synced copies
- Perfect context handoffs between sessions

### Sync Workflow

```
Session work
     ↓
Update CLAUDE.md (Current Focus, Recent Work)
     ↓
session-end-manager runs "wrap up"
     ↓
Auto-sync: CLAUDE.md → AGENTS.md, GEMINI.md
     ↓
Git commit with synced files
     ↓
Next session: All AIs have current context
```

### What Gets Synced

**Always synced** (identical across all three files):
- Quick Navigation
- Current Focus
- Top 10 Critical Patterns
- Quick Start Commands
- Project Overview
- Key Decisions & Context
- Lessons Learned

**AI-specific additions** (optional):
- AGENTS.md: Agent-specific instructions
- GEMINI.md: Research focus areas, API preferences

---

## Session Summaries

### Why Session Summaries Matter

**Searchable decision history**:
```bash
# Find why you chose a specific approach
grep -r "Caddy configuration" Claude/sessions/

# Result: Claude/sessions/2025-11/SESSION_SUMMARY_20251112_CADDY.md
# Decision: Dual-route architecture (internal http:// for performance)
```

**Compounding knowledge**:
- Session 1: Discover pattern
- Session 2: Document pattern in docs/patterns/
- Session 3: Reuse pattern without research
- Result: Faster implementation each time

**Onboarding acceleration**:
- New team member reads last 5 session summaries
- Understands current state in 30 minutes
- No "tribal knowledge" loss

### Automation with Session-End Manager

**Manual process** (before automation):
1. Recall what you did (5-10 min)
2. Write summary (10-15 min)
3. Update CLAUDE.md (5 min)
4. Git commit with message (5 min)
5. Total: 25-35 minutes

**Automated process** (with session-end-manager):
1. Run "wrap up" command
2. Agent generates summary, updates CLAUDE.md, creates commit
3. Total: 3 minutes

**ROI**: 20-30 minutes saved per session × 20 sessions/month = 6-10 hours/month saved

---

## Best Practices

### DO ✅

1. **Keep CLAUDE.md under 250 lines**
   - Link to detailed docs, don't duplicate
   - Treat it as a navigation index, not a knowledge base

2. **Update "Current Focus" every session**
   - What you're working on (1-2 sentences)
   - Next 3 steps
   - Known blockers

3. **Use session-end-manager for automation**
   - Eliminates manual sync errors
   - Ensures consistent format
   - Saves 25+ min per session

4. **Search session summaries before re-researching**
   - `grep -r "keyword" Claude/sessions/`
   - Often finds solutions in 30 seconds vs 30 minutes

5. **Link between documents**
   - CLAUDE.md → docs/patterns/pattern-name.md
   - docs/troubleshooting/issue.md → session summary with solution
   - Creates knowledge graph

### DON'T ❌

1. **Don't duplicate content across files**
   - CLAUDE.md: Brief summary + link
   - docs/: Full details
   - Duplication causes sync issues

2. **Don't skip session summaries**
   - "I'll remember this" → You won't
   - Skipping breaks searchable history
   - Use session-end-manager to make it effortless

3. **Don't let CLAUDE.md grow unbounded**
   - When it hits 250 lines, move details to docs/
   - Keep only essential navigation in CLAUDE.md

4. **Don't manually sync AGENTS.md/GEMINI.md**
   - Manual syncing causes drift
   - Use session-end-manager automation

5. **Don't forget to commit synced files together**
   - Commit CLAUDE.md + AGENTS.md + GEMINI.md as one unit
   - Prevents version mismatches

---

## Examples

### Example 1: Minimal Setup (1-person project)

```
project/
├── CLAUDE.md           # 150 lines - navigation only
├── README.md           # Public docs
└── Claude/
    └── sessions/
        └── 2025-11/
            └── SESSION_SUMMARY_20251115_FEATURE_X.md
```

**Good for**: Solo developers, small projects, getting started

### Example 2: Multi-AI Setup (this project)

```
project/
├── CLAUDE.md           # 232 lines
├── AGENTS.md           # Synced copy
├── GEMINI.md           # Synced copy
├── docs/
│   ├── architecture/
│   ├── patterns/
│   └── troubleshooting/
└── Claude/
    └── sessions/
        ├── 2025-11/    # 5 session summaries
        └── 2025-12/
```

**Good for**: Multi-AI workflows, complex projects, team collaboration

### Example 3: Enterprise Setup

```
project/
├── CLAUDE.md
├── AGENTS.md
├── GEMINI.md
├── COPILOT.md          # For GitHub Copilot context
├── docs/
│   ├── architecture/
│   ├── patterns/
│   ├── troubleshooting/
│   ├── deployment/
│   ├── api/
│   └── security/
└── Claude/
    ├── sessions/
    │   └── 2025-11/
    └── decisions/      # ADRs (Architecture Decision Records)
        └── 001-use-modular-docs.md
```

**Good for**: Large teams, compliance requirements, complex systems

---

## Migration Guide

### From Monolithic README to Modular Docs

**Step 1: Analyze current README**
```bash
wc -l README.md
# If > 300 lines, modular structure will help
```

**Step 2: Create CLAUDE.md**
- Copy "Quick Start" section from README
- Add navigation links (to be created)
- Keep under 250 lines

**Step 3: Extract content to docs/**
- Architecture section → docs/architecture/overview.md
- API docs → docs/api/endpoints.md
- Troubleshooting → docs/troubleshooting/
- Patterns → docs/patterns/

**Step 4: Update CLAUDE.md with links**
```markdown
## Documentation
- [Architecture](docs/architecture/overview.md) - System design
- [API Reference](docs/api/endpoints.md) - API documentation
```

**Step 5: Set up session-end-manager**
- Install session-end-manager agent
- Run first "wrap up" to test
- Verify AGENTS.md and GEMINI.md sync

**Step 6: Start using**
- End each session with "wrap up"
- Search session summaries when debugging
- Keep CLAUDE.md updated (automated)

---

## Tools & Automation

### Session-End Manager Agent

**Install**: [session-end-manager](https://github.com/heinrichxs/session-end-manager-agent)

**What it automates**:
- Session summary generation
- CLAUDE.md updates (Current Focus section)
- Multi-AI syncing (CLAUDE.md → AGENTS.md, GEMINI.md)
- Git commits with meaningful messages

**Usage**:
```
wrap up
```

### Search Helper Script

```bash
#!/bin/bash
# search-sessions.sh - Search session summaries

QUERY="$1"
SESSIONS_DIR="Claude/sessions"

if [ -z "$QUERY" ]; then
    echo "Usage: ./search-sessions.sh 'search term'"
    exit 1
fi

echo "Searching for: $QUERY"
echo "---"
grep -r -n -i "$QUERY" "$SESSIONS_DIR" --color=always
```

**Usage**:
```bash
./search-sessions.sh "Caddy configuration"
./search-sessions.sh "LinkedIn API"
```

---

## FAQ

### Q: How often should I update CLAUDE.md?

**A**: Use session-end-manager at the end of every session (automated). Manual updates only for urgent "Current Focus" changes mid-session.

### Q: What if my CLAUDE.md grows past 250 lines?

**A**: Extract details to docs/ folders. Keep only navigation and current focus in CLAUDE.md. Examples:
- "Critical Patterns" → docs/patterns/critical-patterns.md (link in CLAUDE.md)
- "Lessons Learned" → Keep latest 5, move old to docs/lessons-learned/YYYY-MM.md

### Q: Do I need all three files (CLAUDE.md, AGENTS.md, GEMINI.md)?

**A**: Depends on your workflow:
- Solo with Claude Code only: Just CLAUDE.md
- Claude Code + agents: CLAUDE.md + AGENTS.md
- Claude Code + Gemini: CLAUDE.md + GEMINI.md
- Full multi-AI: All three

### Q: Can I use this with GitHub Copilot, Cursor, etc.?

**A**: Yes! Create COPILOT.md or CURSOR.md as sync targets. Adapt session-end-manager to sync to those files.

### Q: How do I search session summaries?

**A**:
```bash
# Basic search
grep -r "search term" Claude/sessions/

# With line numbers and context
grep -r -n -C 2 "search term" Claude/sessions/

# Case-insensitive
grep -r -i "search term" Claude/sessions/
```

---

## Related Resources

- [Session-End Manager Agent](https://github.com/heinrichxs/session-end-manager-agent)
- [Claude Code Documentation](https://claude.ai/code)

---

**Version**: 1.0
**Last Updated**: 2025-11-15
**License**: MIT
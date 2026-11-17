@AGENTS.md

## Claude Code Execution Directives

- **Source of Truth**: Follow `@AGENTS.md` strictly for all architectural, multi-tenancy, and database rules.
- **Token Efficiency & Brevity**:
  - Keep responses concise, direct, and free of conversational padding.
  - Read only the specific sections, lines, or files required; avoid reading entire multi-thousand-line schema definitions unless necessary.
  - Emit focused, contextual diffs rather than recreating complete documents.
- **Quality Gates**:
  - Verify SQLite database integrity when modifying database files (`sqlite3 fattura-facile.sqlite "PRAGMA integrity_check;"`).
  - Verify all internal Markdown links and Mermaid diagram syntax when editing documentation.
- **Worktree Discipline**:
  - Use isolated git worktrees for multi-step tasks and remove them cleanly when finished.

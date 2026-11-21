@AGENTS.md

- Claude override: read targeted file sections/lines (avoid full multi-thousand-line ER files unless required) and emit concise contextual diffs.
- Use isolated git worktrees only for multi-step tasks and remove them immediately after merging into `dev`.

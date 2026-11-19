# CAP teaching slides
Use .agents/skills/frontend-slides/SKILL.md and .agents/skills/frontend-design/SKILL.md.
Persian RTL, light minimalist design, embedded Vazirmatn font. Keep 1920x1080 fixed stage.
Reserve the bottom-right square (320x320, right 80, bottom 60) for the presenter on every slide.
Use VibeFarsi via https://vibefarsi.ir/mcp; project MCP config is .codex/config.toml.
Original fetched components are in references/vibefarsi/source. HTML adaptations preserve their tokens and behavior.
Never describe CA as an option that survives arbitrary network partitions with both C and A.
C is linearizability. A means eventual successful responses at every non-failing node, not HTTP error or a latency SLA.

Use .agents/skills/humanizer/SKILL.md to edit prose while preserving technical meaning.

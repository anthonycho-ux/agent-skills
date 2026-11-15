# agent-skills

Agent skills (SKILL.md files) for AI agents — portable, agent-agnostic procedures any agent can load and follow.

## Skills

- **[deal-scan](deal-scan/SKILL.md)** — verify a benchmark price is the best available deal before buying anything. Pins the exact variant, scans local + online vendors in parallel, recomputes comparisons in code, and reports verdict-first. Works with subagents if available, sequential web search if not.

## Use

Copy a skill's directory into your agent's skills folder, or point your agent at the `SKILL.md` directly:

```
~/.hermes/skills/<category>/<skill-name>/SKILL.md     # Hermes
~/.config/magpie/library/skills/<skill-name>/         # Magpie library
```

Most agents discover skills by scanning for `SKILL.md` files with YAML frontmatter — no other wiring needed.

## Contributing

Skills here are kept deliberately agent-agnostic: no host-specific paths, no tool names that aren't universal ("web search", "subagents"), procedures any agent can execute. Open an issue or PR if a skill doesn't work in your agent.

MIT licensed — see [LICENSE](LICENSE).

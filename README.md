# Claude Skill: C++20

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill that provides guidelines for writing modern C++20 code.

## What This Skill Does

When installed, this skill instructs Claude to follow a consistent set of C++20 coding standards drawn from:

- [C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines) by Bjarne Stroustrup and Herb Sutter
- [Better Code](https://sean-parent.stlab.cc/papers-and-presentations/) series by Sean Parent
- Rust-style naming and formatting conventions, enforced via clang-format

## Key Conventions

- **C++20** language standard
- **Rust-style naming**: `UpperCamelCase` for types, `snake_case` for functions and variables, `SCREAMING_SNAKE_CASE` for constants
- **Rust-style formatting**: 4-space indent, K&R braces, 100 character line limit
- **`.hpp`/`.cpp` file extensions** with every header having a corresponding source file
- **`#pragma once`** for all headers
- **Value semantics** by default, RAII for resource management, no owning raw pointers
- **No raw loops** — prefer `<algorithm>` and C++20 ranges
- **Concepts** over SFINAE for template constraints

## Installation

Add this skill to your Claude Code project by including it in your `.claude/settings.json`:

```json
{
  "skills": [
    "https://github.com/<owner>/claude_skill_cpp"
  ]
}
```

## Contents

| File | Purpose |
|---|---|
| `SKILL.md` | Full coding guidelines consumed by Claude |
| `.clang-format` | Formatting configuration (requires clang-format 16+) |

## License

MIT

# Unreal Best Practices

A reusable Codex skill for Unreal Engine C++, reflected APIs, API documentation,
Blueprint authoring, and gameplay testing.

The full guidance is public and readable without installing Codex. Start with
[SKILL.md](SKILL.md), then read the reference relevant to your task:

- [C++ style and documentation](references/cpp-style.md)
- [Unreal design](references/unreal-design.md)
- [Testing](references/testing.md)
- [Blueprint authoring](references/blueprint-authoring.md)

## Install and use

The repository root is the skill directory. Clone it into your personal Codex
skills directory as `unreal-best-practices`:

```sh
git clone https://github.com/GuyPaddock/skill-unreal-best-practices.git ~/.codex/skills/unreal-best-practices
```

If that directory already exists, preserve your local changes and compare the
contents before replacing or updating it.

Invoke the skill with `$unreal-best-practices`. Automatic discovery is enabled
for relevant Unreal work through [the skill metadata](agents/openai.yaml).

## Project conventions

The skill provides shared defaults and asks about unresolved conflicts with
project instructions, formatters, or established conventions. It preserves
framework-required contracts and prior resolutions rather than silently choosing
between competing rules. Keep project-specific exceptions in the project's own
instructions.

To reference an exact version from a contributor guide, use a GitHub permalink
to `SKILL.md` at the selected commit. All detailed references use relative links
within the same repository revision.

## License

[MIT](LICENSE), copyright 2026 Guy Elsmore-Paddock.

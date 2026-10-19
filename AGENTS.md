# Purpose

- Maintain the public `unreal-best-practices` Codex skill and its readable references.
- The canonical repository is https://github.com/GuyPaddock/skill-unreal-best-practices.

# Ownership

- The repository root owns the skill entrypoint, UI metadata, references, README,
  license, and repository instructions. No child instruction files are required.
- `SKILL.md` routes tasks to the focused documents in `references/`.
- `agents/openai.yaml` owns discovery and UI metadata.

# Local Contracts

- Keep the repository root installable as the skill directory.
- Keep guidance self-contained, with relative reference links and no dependency
  on private projects, personal paths, assets, credentials, or optional plugins.
- Preserve the user's resolved style choices and project-conflict process in
  `SKILL.md`. Ask before changing those choices or broadening their scope.
- Keep automatic discovery enabled unless the user requests otherwise.
- Record durable changes in the owning guidance and update these instructions
  when repository responsibilities or verification change.

# Work Guidance

- Keep shared guidance in one place and link to conditional references.
- Use focused feature branches and Conventional Commits for subsequent changes.
- Keep project-specific exceptions in their owning projects rather than making
  them universal skill requirements.
- Preserve MIT licensing and keep publication free of local validation artifacts.

# Verification

- Run the skill-creator validator against the repository root when available.
- Verify frontmatter, UI metadata, relative Markdown links, and `git diff --check`.
- Review changed guidance against the user's selected rules. Formatting examples
  may be checked with in-memory probes without modifying project source files.

# Child DOX Index

- None. The root instructions own the complete skill package.

---
name: unreal-best-practices
description: Apply when implementing or reviewing Unreal Engine C++, reflected APIs, API documentation, Blueprint authoring, or related gameplay tests. Combine consistent C++ style with Unreal module, reflection, networking, and authoring practices. Ask about unresolved conflicts with project rules, formatters, or established conventions.
---

# Unreal Best Practices

Apply these rules to new code and the work in scope. Preserve public contracts and framework-required signatures. Keep style changes focused on touched code; a style task does not authorize architecture changes, asset edits, dependency installation, or unrelated cleanup.

## Establish the project contract

- Read applicable `AGENTS.md` files, project style guides, module guidance, formatter settings, and representative nearby code before applying the relevant reference.
- Compare the skill's rules with explicit project instructions, formatter behavior, and established local conventions. For an unresolved conflict, identify the competing rules and ask the user which to use before making the affected edit. Continue independent work when possible.
- Honor a resolution already supplied for the same conflict and scope. Do not repeatedly ask settled questions or silently extend a project-specific exception to other projects.
- Preserve framework-required contracts. If a requested style conflicts with Unreal reflection, an override, generated code, a public API, or supported engine/compiler constraints, explain the constraint and ask about an alternative without breaking the contract.
- Treat formatter behavior as an implementation detail to check, not authority to silently override a resolved written rule. Do not rewrite formatter settings as a side effect.
- Use Unreal idioms and the nearest established pattern for matters these instructions leave unspecified. Ask before spreading a new convention across a project.

## Read the relevant guidance

- For C++ implementation, review, or API documentation, read [C++ style and documentation](references/cpp-style.md).
- For modules, reflected interfaces, editor APIs, logging, or gameplay authority and replication, read [Unreal design](references/unreal-design.md).
- When changing gameplay behavior or authoring tests, read [Testing](references/testing.md).
- For Blueprint graphs, descriptions, layout, or asset authoring, read [Blueprint authoring](references/blueprint-authoring.md). For native Blueprint-facing APIs, also read the C++ and design references.

Read only the references relevant to the task. These instructions are self-contained; source projects and optional editor plugins are not required dependencies.

## Resolved style defaults

The references define the details of these user-selected defaults:

- Use tabs of width four, a 120-character soft limit, next-line opening braces, and braces around every control-statement body.
- Allow readable short lambdas on one line when they fit the 120-character soft limit. Keep longer lambdas multiline.
- Prefer shared-type, vertically aligned local declarations. Preserve separate declarations when complex initializers would obscure the grouping.
- Follow the written wrapped-parameter and closing-parenthesis layout even when a formatter cannot reproduce it exactly. Review and correct the output after any conflict with mandatory project formatting checks has been resolved.
- Use angle brackets for engine headers and quotes for project headers. Ask when a project's conventions conflict.
- Document every member field and enum value. Introduce documented APIs and Blueprint descriptions with one or two sentences explaining their role before mechanics.

Carry these defaults into new projects. In existing projects, use the conflict process above rather than silently overriding either set of instructions.

## Finish the work

Verify the relevant behavioral change with the project's existing checks. Review touched code for the selected style and documentation rules, including formatting that automated tools cannot express. Report checks actually run, unresolved conflicts, and any verification limits. Preserve existing user work, comments, valid suppressions, and assets outside the requested scope.

# C++ Style and Documentation

Use this reference for Unreal C++ changes and reviews. Resolve project conflicts through the process in `SKILL.md` before applying a competing convention.

## Whitespace and control flow

- Use tabs for indentation, displayed at width four.
- Prefer lines of 120 characters or fewer. Allow longer lines when materially clearer or when a literal cannot be wrapped cleanly.
- Put opening braces on the next line for classes, structs, functions, control flow, namespaces, and lambdas.
- Allow readable short lambdas on one line when they fit the 120-character soft limit. Keep longer lambdas multiline.
- Give every control-statement body a braced compound statement, including single-statement `if`, `else`, `for`, `while`, and `do` bodies.
- Attach pointer and reference symbols to the type: `UObject* Object` and `const FString& Name`.
- Group related assignments, calls, and mixed setup/use sequences into short logical paragraphs. Prefer a blank line between an assignment paragraph and a call paragraph, except when they form one tight responsibility.
- Align assignment operators within a paragraph when alignment improves scanning without awkward wrapping.
- Keep short, simple value-choice ternaries on one line. Wrap ternaries when aligning their branches makes differences easier to compare, such as mirrored coordinates, visibility, or alignment choices.

## Wrapping

- Break at a higher syntactic level before splitting nested expressions: assignment, argument list, conditional header, or chained-call boundary.
- In compound conditions, parenthesize operands containing binary expressions when that makes grouping explicit. Avoid redundant parentheses around a standalone comparison, unary expression, or function call with no precedence ambiguity.
- Wrap long Unreal annotations across lines. Omit spaces around `=` within annotation metadata, as in `meta=(...)`, `Category="..."`, and `DisplayName="..."`.
- For a wrapped declaration or definition, keep the return type and function name on the first line where practical. Put every parameter on its own following line, indented one additional level, and vertically align parameter names. Put the closing parenthesis on its own line aligned with the declaration start.
- For a wrapped standalone call, place the arguments on following lines and the closing parenthesis on its own line aligned with the call expression's start.
- Match established alignment for wrapped constructor initializer lists and spacing inside control-flow parentheses, subject to the skill's conflict process.

For example, wrapped parameters use this layout:

```cpp
void SetPlaybackRange(
	const float StartTime,
	const float EndTime
)
{
	this->UpdatePlaybackRange(
		StartTime,
		EndTime
	);
}
```

- Prefer an `if` initializer when its variable is used only by that conditional. Keep the header on one line when it fits.
- If the header must wrap, put the initializer on its own line inside the parentheses. Put the condition on the next line with the initializer's leading indent plus four spaces.
- Move initialization outside the conditional when the value is reused afterward or the wrapped header becomes awkward.

### Formatter limitations

Review formatter output against the written layout. A formatter may move the first parameter next to the function name, attach `)` to the final argument, or change a shared declaration's alignment. Correct affected output manually after resolving any conflict with required project formatting checks. Do not claim formatter compliance alone proves style compliance or change the project's formatter configuration without authorization.

## Includes and file structure

- Preserve required project file headers. Keep `#pragma once` at the beginning of header code, before includes.
- Group includes by directory, separated by blank lines. Order engine groups before project groups; keep the generated header include last in every reflected Unreal header.
- Use angle brackets for engine headers and quotes for project headers.
- Prefer forward declarations when a complete definition is unnecessary. Keep implementation-only includes in `.cpp` files and avoid unnecessary transitive dependencies.
- Preserve useful section banners and comment structure. Use banners in large files or between materially different responsibilities.
- Arrange header content as file-level documentation, includes, forward declarations, delegates/enums/supporting types, then the class declaration.
- Use a dedicated `Forward Declarations (to minimize header dependencies)` section when needed, followed by a dedicated heading such as `Delegates` for standalone event declarations.
- In C++ section banners, put content directly after the heading without a blank line. This rule concerns source-code sections, not Markdown heading spacing.
- Keep section headers in headers rather than mirroring them in implementation files.
- Preserve valid existing diagnostic suppressions. When a suppression is necessary, prefer a narrow, single-use suppression over disabling a check for an entire file.

## Naming and member organization

- Follow Unreal type prefixes `U`, `A`, `F`, `E`, `I`, and `T` according to the kind of type. Retain the project's own prefixes where applicable.
- Use the `b` prefix for Boolean fields and descriptive predicate names that communicate the state or decision. Use descriptive PascalCase names for constants, pin names, and similar identifiers.
- Prefer descriptive names to abbreviations unless the abbreviation is established in that domain. Name methods for their actions and types for their responsibilities.
- Declare nested types before fields, then fields before methods.
- Within the field group, use `public`, `protected`, `private` order; use the same visibility order within the method group.
- Within each visibility level's methods, declare and implement overrides before other methods. Group overrides in header-only subsections naming the overridden parent type.
- Order overrides according to where they are introduced in the parent hierarchy.
- Implement methods in header declaration order. For a true getter/setter pair, declare and implement the getter first.
- Use `this->` consistently within non-static member bodies. It clarifies member access; it does not prevent shadowing or replace compiler diagnostics.
- Use explicit `nullptr` comparisons for object-pointer checks.

## Local declarations and method shape

- Prefer local declarations near the top of their block, including small anonymous blocks, with the scoped `if` initializer exception above.
- Initialize at declaration unless initialization is materially expensive or the correct value depends on intervening work.
- For consecutive same-type variables declared together, write the type once and put each variable on its own aligned line. If the type changes, start a new declaration. A logical paragraph may contain several types.
- Keep separate declarations when long or complex initializers make a shared declaration harder to read. Preserve each variable's actual type and qualification; a pointer/reference declarator may need its own symbol on each variable.

For example:

```cpp
const float StartTime = 0.0f,
			EndTime   = 1.0f;
```

- Name significant behavioral, layout, and policy constants. Document what the value means and why it matters. Obvious literals such as zero, one, and straightforward geometry fractions need no extraction unless a name improves clarity.
- Prefer short methods with one or two responsibilities. Extract smaller units when doing so improves readability, isolation, or testability without obscuring control flow.
- Prefer `const` for unchanged locals and parameters when compatible with the intended implementation.
- Treat top-level `const` on by-value parameters as an implementation choice. It may be omitted in a header declaration; prefer it in a definition when the value is unchanged. Do not add it when intentionally moving from the parameter.
- Prefer one entry and one exit when readable. Use early returns for exceptional validation, clear guards, and cheap no-op cases when these avoid less readable nesting.
- Keep template operations small and readable. Prefer returning a new value over mutating inputs when that suits the contract; preserve mutation where it is the natural Unreal pattern.
- Reserve container capacity before filling it when the size is known. Use descriptive lambda parameter names that expose each value's role.

## Documentation

- Use Doxygen-style blocks for public APIs, documented types and delegates, and non-obvious internal operations.
- Lead each documented type, field, method, event, and enum value with one or two sentences describing what it represents and why callers use it. Establish its role before storage, execution order, restrictions, or side effects.
- After a blank line, add short paragraphs only where behavior, usage, preconditions, ownership, units, failure conditions, or side effects need explanation.
- Use `@param`, `@return`, and `@tparam` when applicable to explain the callable or template contract.
- Document every member field, including private state and nested-type fields, and every enum value.
- Do not duplicate inherited override documentation unless behavior differs meaningfully or project-specific context is needed.
- Use inline comments for non-obvious behavior, engine quirks, multiplayer constraints, and design decisions. Preserve still-valid diagnostic notes and explanations.
- Apply the same role-first introductory rule to Blueprint descriptions and tooltips. Explain what the feature is before describing callback order or lifecycle restrictions.

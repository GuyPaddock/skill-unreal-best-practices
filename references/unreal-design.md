# Unreal Design

Use the sections relevant to the change. Networking and ability-system guidance applies when those systems participate in the behavior; ordinary style changes do not require introducing them.

## Modules and public contracts

- Keep reusable runtime code, editor support, custom Blueprint nodes, tests, and project-specific sample policy in their owning modules.
- Use `Public/` for exposed APIs and `Private/` for implementation details. Group related subsystems in the existing module structure.
- Preserve public API shape unless an intentional contract change is part of the task. Prefer interfaces at system boundaries and for replaceable components.
- Keep headers lightweight and keep editor-only dependencies outside runtime modules.

## Reflection and interfaces

- Use `UCLASS`, `USTRUCT`, and reflected members where reflection is required. Apply `BlueprintType` where the type needs that exposure.
- Give reflected fields and methods meaningful metadata. Match `BlueprintCallable`, `BlueprintAssignable`, `BlueprintReadOnly`, categories, and other exposure to the actual API contract.
- Apply `Transient`, replication, clamp, and editor metadata according to property semantics rather than copying annotations blindly.
- For an Unreal interface, prefer a minimal reflected wrapper using `UINTERFACE(MinimalAPI, ...)` when sufficient, and put the module API macro on the native `I...` interface exposing callable methods.
- Use `meta=(CannotImplementInterfaceInBlueprint)` when the interface contract requires native implementation. Preserve the intended native/Blueprint extension boundary.
- Follow established explicit event-object and multicast-delegate patterns when exposing interface events to Blueprint.
- Mark constructors `explicit` where appropriate. Use `mutable` only for a clear contract such as an established lazy cache or event object.

## Gameplay authority, replication, and GAS

Treat ownership, authority, lifecycle, and replication as architectural concerns. Before changing them, trace who mutates state, when initialization happens, what replicates, and what remote clients can observe.

- Preserve server and client initialization paths. Possession-time and controller-replication callbacks may both be necessary; verify their roles before combining or removing them.
- Preserve authority checks unless the intended network behavior and its verification justify a change.
- Keep replicated properties, lifetime replication declarations, `OnRep_...` callbacks, and event broadcasts consistent.
- Mutate replicated collections through their owning APIs so replication and notifications remain synchronized.
- Use existing ability-system interfaces and wrappers. Do not bypass them for a local shortcut.
- Treat ASC actor-info initialization, refresh, passive effects, dynamic tags, attribute sets, and queued gameplay operations as coordinated behavior.
- Preserve instance ownership and class-default-object isolation for event objects and state. Do not replace deliberate lazy allocation with constructor allocation without checking lifecycle and multiplayer effects.
- Verify changed ownership, initialization timing, ability application, and event delivery on the server and affected clients. Use the [testing guidance](testing.md) to choose relevant scenarios.

## Localization and diagnostics

- Localize editor node titles, tooltips, and menu categories through the project's existing localization pattern.
- In `.cpp` files that define localized editor text with `LOCTEXT`, define `LOCTEXT_NAMESPACE` and undefine it at the end of the file.
- Use existing module log categories and logging facilities. Include enough object or world context to identify the event.
- Follow local severity conventions. `VeryVerbose` suits routine lifecycle tracing; `Warning` suits recoverable issues when consistent with the project.
- Avoid duplicate lifecycle logs and noisy messages without diagnostic context.

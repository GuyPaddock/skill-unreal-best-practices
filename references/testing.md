# Unreal Testing

Use the project's existing build and test framework. Scale verification to changed behavior rather than introducing a new test system or running multiplayer scenarios for formatting-only edits.

## Behavioral coverage

- Add or update automation coverage for changed gameplay logic, reusable calculations, attributes, and library behavior when existing tests do not establish the new contract.
- Assert observable results, state transitions, events, and side effects. Avoid tests that merely compare source code, documentation wording, or implementation structure.
- Use clear scenario names and assertion labels. Match established namespacing, file suffixes, and test organization.
- Reuse existing test base classes, world setup, actors, fixtures, and asset-loading facilities. Use specs with setup, teardown, and descriptive cases when that is the project's established framework.
- For Blueprint-backed behavior, load the relevant test assets through existing facilities and exercise the resulting behavior. Keep world, delegate, and timer cleanup complete enough to avoid leaking state between cases.

## Choose checks for the change

- For native changes, build the relevant target and run affected automation tests according to project instructions. Include reflected declarations in the normal Unreal build path so header-tool issues are caught.
- For authority, replication, or ability-lifecycle changes, check the relevant server and client paths, initialization/refresh callbacks, replicated state, and event delivery. Test ownership transitions or repeated initialization when the behavior depends on them.
- For Blueprint authoring, compile affected Blueprints, inspect the graph, and run the affected gameplay flow. A successful compilation does not establish correct execution connections or defaults.
- For formatting-only edits, use the relevant existing formatting/build checks without inventing behavior-mirroring tests. Inspect wrapping and shared declarations manually when the formatter cannot express the resolved rules.
- Preserve existing public contracts and API metadata in verification. If a required target, engine, asset, or test environment is unavailable, report what was checked and what remains unverified.

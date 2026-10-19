# Blueprint Authoring

Use this reference for graph organization, Blueprint descriptions, and deliberate asset-authoring operations. Editing native Blueprint-facing APIs also uses the C++ style and Unreal design references.

## Descriptions and API exposure

- Introduce types, properties, events, and functions with one or two sentences explaining their role and why the author uses them. Explain lifecycle restrictions or execution mechanics afterward.
- Keep categories, display names, pin descriptions, defaults, and reflected metadata consistent with the subsystem and native API contract.
- Preserve native-only implementation restrictions and existing interface/delegate patterns rather than changing the extension model during a presentation edit.

## Graph readability

- Organize related execution flows into readable event blocks and functions according to the project's existing graph conventions. Keep synchronous operations in functions when that remains their contract.
- Make execution direction easy to follow, leave space for input data nodes, and route wires so connections remain understandable. Choose a consistent column or flow layout suited to the graph.
- Preserve node comments, explanatory text, and authored enclosing comment groups. Moving nodes without their comment boxes can detach explanations from the behavior they describe.
- Wrap long explanatory notes so comment bubbles do not force connected logic far apart.
- Review graph overviews and individual functions. Large graphs need inspection by section; a single overview can conceal unreadable details.

## Asset edits and verification

- Treat graph formatting as an explicit asset-writing operation within the requested task. Use an explicit set of owned assets, preserve unrelated user edits, and follow the project's backup and save process.
- Check whether Blueprint Assist is installed for the project's engine version. When installed and available in the editor, use it to format the nodes added or changed by the task.
- Select only the affected nodes and use selection-scoped formatting. Do not format the entire graph or use commands that expand formatting to unrelated connected nodes. Preserve unrelated node positions and existing comment groups.
- If formatting cannot be restricted to the affected nodes, arrange those nodes manually instead of widening the scope. If Blueprint Assist is unavailable, use manual layout; this skill does not authorize installing the plugin.
- For layout-only edits, preserve authored node identities where the tool supports them, pin defaults, and logical terminal connections. Routing nodes can change, so compare their ultimate endpoints rather than treating every reroute edit as a behavioral change.
- Keep layout edits separate from deliberate logic changes such as removing unreachable nodes or duplicating pure calculations. Verify the intended semantic change before formatting it.
- Avoid saving over unrelated dirty packages or racing another editor that holds the same assets open. Follow the project's supported authoring workflow.
- Compile every affected Blueprint before accepting the result, inspect the saved layout, and run the relevant behavior checks. Use [testing guidance](testing.md) for the verification appropriate to the change.

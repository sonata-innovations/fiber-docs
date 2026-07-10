# Fiber Documentation

Fiber is a system for building and rendering data-collection forms. Builders (FBT, FBTL) author a JSON document called a Flow; the render engine (FBRE) renders it and returns collected data (FlowData). All libraries are standard React components published on npm.

> **This repository is a mirror.** It is generated from the Fiber source repo and updated automatically. Do not open pull requests here — the source of truth is the `docs/` tree in the private Fiber repo.

## Packages

All packages are published to the public npm registry under the `@sonata-innovations` scope.

| Package | What it is |
|---|---|
| [`@sonata-innovations/fiber-fbre`](https://www.npmjs.com/package/@sonata-innovations/fiber-fbre) | Render engine — consumes a Flow, renders the form, returns FlowData |
| [`@sonata-innovations/fiber-fbt`](https://www.npmjs.com/package/@sonata-innovations/fiber-fbt) | Full drag-and-drop builder for power users |
| [`@sonata-innovations/fiber-fbtl`](https://www.npmjs.com/package/@sonata-innovations/fiber-fbtl) | Lite builder for non-technical end users |
| [`@sonata-innovations/fiber-theme-editor`](https://www.npmjs.com/package/@sonata-innovations/fiber-theme-editor) | Visual theme editor widget |
| [`@sonata-innovations/fiber-types`](https://www.npmjs.com/package/@sonata-innovations/fiber-types) | Schema types, and the canonical JSON Schema |
| [`@sonata-innovations/fiber-shared`](https://www.npmjs.com/package/@sonata-innovations/fiber-shared) | Condition, validation, markup, and formula engines |

Every package also ships these docs inside its own tarball, under `node_modules/<package>/docs/`, alongside an `AGENTS.md` routing guide. **Those copies always match the version you installed** — prefer them over this mirror when you have the package installed.

## Using these docs with an AI assistant

- [`llms.txt`](https://raw.githubusercontent.com/sonata-innovations/fiber-docs/main/llms.txt) — a link index, per the [llmstxt.org](https://llmstxt.org) convention
- [`llms-full.txt`](https://raw.githubusercontent.com/sonata-innovations/fiber-docs/main/llms-full.txt) — every document concatenated into one file, for pasting into a context window

Validate a Flow you generated against the schema:

```bash
npx ajv-cli validate --spec=draft2020 \
  -s https://raw.githubusercontent.com/sonata-innovations/fiber-docs/main/schema/flow-schema.json \
  -d my-flow.json
```

## Start here

- [Fiber Concepts](fiber-concepts.md) — First contact with Fiber: the Flow/Screen/Component model, FlowData, builders vs render engine, conditions/validation/calculations concepts.

## Integration guides

Embedding a Fiber package in a parent application.

- [FBRE Integration Guide](integration/fbre.md) — Embedding the render engine in a parent app: props and modes, onFlowComplete contract, confirmation screen, store access, events, theming, pre-populating data.
- [FBT Integration Guide](integration/fbt.md) — Embedding the full builder in a parent app: getting the Flow out, composable layout, custom presets and templates.
- [FBTL Integration Guide](integration/fbtl.md) — Embedding the lite builder in a parent app: controlled-component contract, scope, save lifecycle, normalizing generator-authored flows.
- [Theme Editor Integration Guide](integration/theme-editor.md) — Embedding the plug-and-play theming widget: controlled value contract, knob sets, defaults, modal pattern, passing the theme to FBRE/FBT/FBTL.

## Schema reference

The Flow (input) and FlowData (output) contracts, in prose and as JSON Schema.

- [FlowData Schema](schema/flow-data-schema.md) — Consuming FlowData output from FBRE: structure, per-type value shapes, exclusion rules, containers, calculations.
- [Flow JSON Quick Reference](schema/flow-quick-reference.md) — Constructing or interpreting Flow JSON: structure, component types and value types, options, conditions, validation, widths, inline markup. For exhaustive per-property detail, use flow-schema.md instead.
- [Flow JSON Schema Reference](schema/flow-schema.md) — Exhaustive per-property reference for Flow JSON: every component type, property, condition, validation rule, calculation, and config field. For a compact overview use flow-quick-reference.md.

## Feature guides

Deep dives on individual capabilities.

- [Confirmation ("Thank You") Screen](features/confirmation-screen.md) — Configuring the post-submit thank-you screen: config.confirmation, dynamic ${...} content, and the onFlowComplete return contract.
- [Custom Presets & Templates (FBT)](features/custom-presets-and-templates.md) — Extending FBT's pool with custom presets/templates: data-based vs factory definitions, icon catalog, collision rules, server-stored definitions.
- [FBRE Theming Guide](features/fbre-theming.md) — Theming FBRE-rendered forms: colorScheme presets, palette knobs, raw --fbre-* token overrides, precedence model, full token catalog.

## Machine-readable schema

| File | Purpose |
|---|---|
| [`schema/flow-schema.json`](schema/flow-schema.json) | JSON Schema (draft 2020-12) for a Flow — the input to the render engine |
| [`schema/flow-data-schema.json`](schema/flow-data-schema.json) | JSON Schema for FlowData — the output |

## License

See [LICENSE](LICENSE).

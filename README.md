# Fiber Documentation

Fiber is a system for building and rendering data-collection forms. Builders (FBT, FBTL) author a JSON document called a Flow; the render engine (FBRE) renders it and returns collected data (FlowData). All libraries are standard React components published on npm.

## Quick start

Render a form in about two minutes. Install the render engine:

```bash
npm install @sonata-innovations/fiber-fbre
```

A **Flow** is plain JSON — screens of components, each with a uuid, a type, and properties:

```ts
const flow = {
  uuid: "11111111-1111-4111-8111-111111111111",
  metadata: { name: "Contact" },
  screens: [
    {
      uuid: "22222222-2222-4222-8222-222222222222",
      label: "About you",
      components: [
        {
          uuid: "33333333-3333-4333-8333-333333333333",
          type: "inputText",
          properties: {
            label: "Your name",
            validation: { rules: [{ type: "required" }] },
          },
        },
        {
          uuid: "44444444-4444-4444-8444-444444444444",
          type: "yesNo",
          properties: { label: "Subscribe to updates?" },
        },
      ],
    },
  ],
};
```

Hand it to `<FBRE />`. When the user finishes, you get the collected **FlowData** back:

```tsx
import { FBRE } from "@sonata-innovations/fiber-fbre";
import "@sonata-innovations/fiber-fbre/styles"; // required — styles are not bundled with the JS

export default function App() {
  return <FBRE flow={flow} onFlowComplete={(data) => console.log(data)} />;
}
```

That's the whole loop: **a Flow goes in, FlowData comes out.** Conditional logic, validation, and screen transitions are handled for you, declared in the JSON rather than written in your components.

Next: [Fiber Concepts](fiber-concepts.md) for the mental model, or the [FBRE integration guide](integration/fbre.md) for the full API. To let people *author* flows instead of hand-writing JSON, add a builder — [FBT](integration/fbt.md) for developers and form designers, [FBTL](integration/fbtl.md) for non-technical end users.

## Using these docs with an AI assistant

Point your assistant at [`llms.txt`](https://raw.githubusercontent.com/sonata-innovations/fiber-docs/main/llms.txt) — a titled, described index of every document, per the [llmstxt.org](https://llmstxt.org) convention — and it will fetch only the pages it needs. For a single paste into a context window, use [`llms-full.txt`](https://raw.githubusercontent.com/sonata-innovations/fiber-docs/main/llms-full.txt) (the entire corpus in one file).

Flow JSON is machine-validatable at a stable URL, with no install and no auth. Validate anything you generate rather than trusting it by inspection:

```bash
npx ajv-cli validate --spec=draft2020 \
  -s https://raw.githubusercontent.com/sonata-innovations/fiber-docs/main/schema/flow-schema.json \
  -d my-flow.json
```

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

Every package also ships these docs inside its own tarball, under `node_modules/<package>/docs/`, alongside an `AGENTS.md` routing guide. **Those copies always match the version you installed** — prefer them over this mirror once you have the package.

## Core concepts

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

## About this repository

This is a **generated mirror**, published from the `docs/` tree of the Fiber source repo and updated automatically on every change. Please don't open pull requests here — they can't be merged upstream. Corrections and questions are welcome as [issues](https://github.com/sonata-innovations/fiber-docs/issues).

## License

See [LICENSE](LICENSE).

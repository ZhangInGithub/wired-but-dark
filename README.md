# Wired but Dark

Field notes on the POC-to-production gap in **small-model agent harnesses** — two failure modes that pass every demo and quietly die under real traffic.

- **Trap 01 — The wired stub.** A persistence layer that saves perfectly and reads back nothing: the write path fills the store, but the read-side transform is stubbed to `return []`, so every turn starts blind. All the infrastructure is present; the one severed hop has no side effect to monitor.
- **Trap 02 — The text-JSON detour.** Tool calls parsed out of prose with a regex instead of using native function calling. It works in the demo and misses silently the moment the model wraps the JSON, emits two blocks, or trails a comma — and a missed parse looks exactly like "the model chose not to call a tool."

Plus a sibling failure at the wire boundary (streamed `tool_calls` with explicit `null` name/id overwriting a good value → `unknown tool ""`), a comparison table of maintained harness/memory libraries, and four smoke tests that catch a hollow pillar.

> The page uses custom CSS, theming, and hand-authored SVG diagrams, so GitHub's README/Gist sanitizer strips the design. **View it rendered via GitHub Pages** (link in the repo's About / Pages settings), or open `index.html` locally.

Patterns are generalized from a real audit; identifiers are illustrative. Single self-contained HTML file, no build step.

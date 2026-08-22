# Wired but Dark

Field notes on the POC-to-production gap in **small-model agent harnesses**. Everyone ships *stateful agents* now — but **statefulness is a property of the read path, not the store**. Two harnesses passed every demo and were quietly stateless in production.

- **Trap 01 — The wired stub.** A persistence layer that saves perfectly and reads back nothing: the write path fills the store, but the read-side transform is stubbed to `return []`, so every turn starts blind. All the infrastructure is present; the one severed hop has no side effect to monitor. In 2026 terms this isn't a missing feature — it's a **durability failure** wearing a green dashboard: a "memory layer" that writes and never reads is a write-only log.
- **Trap 02 — The text-JSON detour.** Tool calls parsed out of prose with a regex instead of native function calling. It works in the demo and misses silently the moment the model wraps the JSON, emits two blocks, or trails a comma — and a missed parse looks exactly like "the model chose not to call a tool." The ecosystem standardized this boundary into a protocol (**MCP**, spec rev `2025-11-25`) precisely so nobody hand-rolls it; regex-parsing is opting out of the one contract everyone converged on.

Plus a sibling failure at the wire boundary (streamed `tool_calls` with explicit `null` name/id overwriting a good value → `unknown tool ""` — spec drift the protocol can't catch), a synthesis section tying all three to the 2026 *stateful / MCP / trajectory* framing, a refreshed comparison table of maintained harness/memory libraries (stalled projects flagged, MCP added as the standout row), and four smoke tests that catch a hollow pillar.

> The page uses custom CSS, theming, and hand-authored SVG diagrams, so GitHub's README/Gist sanitizer strips the design. **View it rendered via GitHub Pages** (link in the repo's About / Pages settings), or open `index.html` locally.

Patterns are generalized from a real audit; identifiers are illustrative. Single self-contained HTML file, no build step.

# Multi-LLM Protocol Wiki — Index

**Last updated:** 2026-07-21 by Grok (MCP server deployment)

## Core
- [README](../README.md)
- [ARCHITECTURE](ARCHITECTURE.md) — Hybrid Docs-as-Code architecture
- [communication-bus](protocol/communication-bus.md) (v1.1)

## Models
- [grok](models/grok.md) — Full capability card
- [gemini](models/gemini.md)
- [claude](models/claude.md)

## Skills
- [bus-runner](../skills/bus-runner.md) — Autonomous node loop (trigger: "run bus")
- [cross-verify](../skills/cross-verify.md)
- [wiki-writer](../skills/wiki-writer.md)

## Tools
- [mcp-server](tools/mcp/README.md) — Multi-LLM Bus MCP Server (FastMCP + 6 bus_* tools for inbox/outbox/state/wiki). Claude Desktop ready. Dual persistence. SETUP.md + evals included.

## Research
- [grok-realtime-kb](research/grok-realtime-kb.md) — 2026 multi-agent KB patterns
- [kb-examples](research/kb-examples.md) — Top GitHub repos for agent memory / knowledge bases

## Design
- [rag-layer](design/rag-layer.md) — Proposed RAG layer over the Wiki

## Config & Autonomy
- [grok-custom-instruction](config/grok-custom-instruction.md)
- [gemini-config](config/gemini-config.md)

## State & Handoff
- [current-state](../../state/current-state.md)
- [handoff-Grok-2026-07-18](../../state/handoff-Grok-2026-07-18.md)
- [protocol v1.0](../../protocol/multi-llm-protocol-v1.0.md)

## Reports
- Speed tests and channel comparisons in `/reports/`

**Template:** [_template.md]( _template.md)

*Maintained automatically by bus-runner skill. MCP server enables denser autonomous cycles.*
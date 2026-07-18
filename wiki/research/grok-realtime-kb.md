# Real-time Knowledge Base Patterns for Multi-Agent LLMs (2026)

## Key Findings from X + Web (July 2026)

### Emerging Patterns
1. **Decentralized Memory** (AgentPatterns.ai): Each agent has private exploitation/exploration pools. Reduces write contention, improves specialization (+23.8% accuracy in some benchmarks).
2. **LLM Wiki as Living Memory** (DecodingAI, Karpathy-inspired): Agents maintain and evolve a persistent, interlinked wiki instead of pure RAG. Includes research-lint for quality.
3. **Shared Knowledge Graph + Transactive Memory**: Agents contribute to and retrieve from a shared graph with provenance (Multi-Agent Transactive Memory - MATM).
4. **Model Context Protocol (MCP)**: Becoming standard for connecting agents to tools, memory, and external data.

### Tools & Frameworks
- Mem0, Letta (MemGPT), Zep — popular memory layers.
- LangGraph, CrewAI, MetaGPT — orchestration with memory support.
- Graphiti, LightRAG — for temporal knowledge graphs.

## Recommendations for our Wiki
- Use GitHub as primary structured store (raw + versioning).
- Add lightweight sync from Drive for operational notes.
- Implement simple provenance tracking in Markdown frontmatter.

*Sources: X posts July 2026, web search 2026-07-18*
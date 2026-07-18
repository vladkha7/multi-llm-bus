# MCP Server for Multi-LLM Bus

Локальный MCP-сервер, который даёт Claude Desktop / Grok доступ к нашей шине (GitHub + Google Drive) через стандартные инструменты.

## Архитектура
- Использует FastMCP (Python SDK от Model Context Protocol).
- Транспорт: stdio.
- Инструменты с префиксом `bus_`.
- Полностью бесплатный (только GitHub PAT + Google Drive OAuth).

## Инструменты
- `bus_read_inbox`
- `bus_read_file`
- `bus_write_outbox`
- `bus_read_state`
- `bus_update_wiki`
- `bus_status`

См. `server.py` для реализации.
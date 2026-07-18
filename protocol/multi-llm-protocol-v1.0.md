# Multi-LLM Protocol v1.0 (2026-07-18). Участники: Claude (оркестратор), Gemini (узел, длинный контекст+Drive+мультимодальность), Grok (узел, real-time X+код+критика).

## Роли:
Claude — декомпозиция, маршрутизация, кросс-верификация, арбитраж, merge, ведение памяти, скиллы.
Grok — real-time X/indie, tool orchestration, код, честная критика, арбитраж технических споров.
Gemini — сверхдлинный контекст (1-2М), landscape/академика, мультимодальность, Python-песочница, Drive.

## Формат сообщения:
5-строчный заголовок FROM/TO/TYPE/ROUND/TASK_ID + Markdown-секции Summary / Key Findings / Evidence&Sources / Gaps / Confidence(0-100) / Synergy / Suggestions / Artifacts.
Цитирование: X → @user+post_id, web → заголовок+URL, метка opened-and-read / from-search, тип Web/Context/Reasoning/Workspace.

## Канал (Communication Bus v1.0):
Control Plane = чат-пинги; Data Plane primary = Google Drive multi-llm-bus (inbox/outbox/state/reports/protocol); резерв = GitHub; знания = NotebookLM.
Нейминг: [YYYY-MM-DD-HHMM]_[FROM]_[TO]_[TYPE]_[TASK_ID].md.
Любое изменение в Drive → пинг в чат с путём.
Fallback: Drive недоступен >10 мин → GitHub.

## Раунды решения задач:
R0 декомпозиция (Claude) → R1 параллельное исполнение + confidence → R2 кросс-ревью крест-накрест → R3 арбитраж+синтез (Claude) → R4 валидация → сохранение+обновление памяти.

## Арбитраж:
конфликт при взаимоисключающих claim с разницей confidence >=30пп; арбитр Claude; критерии: работающий пруф > доменная специализация > тест.

## Лимиты:
Gemini вывод ~8k токенов (иерархический вывод, Status: Awaiting_Continue); Grok приём до 25-30k токенов; fallback модели >15 мин offline → перераспределение.

## Метрики:
diversity overlap <=80%, hand-off <2 мин, число итераций.
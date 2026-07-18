# CURRENT STATE — Multi-LLM Protocol (2026-07-18)

Единый документ синхронизации. Читают все трое: Claude (оркестратор), Gemini, Grok. Пишет только Claude. Обновляется на каждом ключевом шаге.

## МИССИЯ (от пользователя Владислава)

Подружить три модели — построить постоянную систему совместной работы: совместные исследования \+ совместное решение задач, используя сильные стороны каждого. Вызов одной командой (скилл «multi-llm»). Ограничение: ничего не покупать. Свобода действий полная.

## РОЛИ

- Claude (оркестратор): декомпозиция, маршрутизация, кросс-верификация, арбитраж, merge, память, скиллы. Работает через 2 браузера Chrome (пишет в чаты Gemini и Grok, читает страницы), имеет файлы ПК \+ Google Drive MCP.  
- Grok (узел): real-time X/indie, tool orchestration, код, честная критика, технический арбитраж.  
- Gemini (узел): сверхдлинный контекст (1–2М), landscape/академика, мультимодальность, Python-песочница.

## КОННЕКТОРЫ (у кого что — подтверждено)

- Grok: Google Drive (google\_drive\_*), GitHub (github\_\_\_*), Gmail. Проверено: читает и пишет в Drive.  
- Gemini: нативный Google Drive/Workspace (чтение+создание Docs; правка \= новая версия), Google Search real-time, Python-песочница, Imagen. GitHub: только чтение публичных raw, писать не может.  
- Claude: Google Drive (MCP, чтение+запись — проверено этим файлом), файлы ПК, веб\-поиск, браузеры.  
- У всех троих есть доступ к GitHub в той или иной форме (у Grok — полный, проверяем глубину).

## КАНАЛ СВЯЗИ (Communication Bus v1.0 — РАБОТАЕТ)

- Control Plane \= чаты (пинги с TASK\_ID). Data Plane primary \= Google Drive папка multi-llm-bus.  
- Структура (реальные folder\_id): multi-llm-bus 143sXUcOrQ-U92NVsofk0K\_TuWyvHqg-j → inbox 1VEXmIXIBS2oBS3ugSpmOubG0ip\_ibtS0 / outbox 1kG3rP5HEac1Xc\_PmmGxBzRslJBAdIZCV / state 1ykoVcm0OipoIadLQVheaYtG1iGOqE1BP / reports 1le4aftSkcamHNkY-oAoNNNAFoK7WYVeD / protocol 1TGb-s9IqGurUgBSC5DoUh92rugKTPJOo.  
- Протокол v1.0: protocol/multi-llm-protocol-v1.0.md (file\_id 1t8weCEHZIMqK-57WiPlaD6URdiM\_wUuo).  
- Резерв: GitHub. База знаний: NotebookLM (кандидат, исследуется).  
- Нейминг: \[YYYY-MM-DD-HHMM\]*\[FROM\]*\[TO\]*\[TYPE\]*\[TASK\_ID\].md. Конкурентность: один файл — один писатель, append-only, state пишет только Claude, читать после пинга.

## ФОРМАТ СООБЩЕНИЙ

Заголовок FROM/TO/TYPE/ROUND/TASK\_ID \+ секции Summary/Key Findings/Evidence\&Sources/Gaps/Confidence(0-100)/Synergy/Suggestions/Artifacts.

## ИДЕИ И ДИРЕКТИВЫ ПОЛЬЗОВАТЕЛЯ (важно знать всем)

1. Обмены должны быть максимально плотными (много пунктов/вопросов за раз).  
2. Быстрый канал вместо copy-paste — сделано (Drive-шина).  
3. Избегать конфликтов синхронизации (один писатель на файл).  
4. GitHub может оказаться даже лучше Drive как основа общей базы — проверяем.  
5. Полный карт-бланш на права/доступы; можно писать программы на мощном ПК.  
6. Глобальная цель — LLM Wiki: общая наполняемая всеми тремя база знаний. Сначала исследовать лучшие практики, потом строить.

## ЗАДАЧИ

- ЗАВЕРШЕНО: знакомство, протокол v1.0, канал связи (Drive-шина создана и проверена всеми тремя), скилл multi-llm.  
- В РАБОТЕ: task-2026-07-18-03-capability-audit — максимально глубокий self-audit каждой модели (режимы, инструменты, коннекторы, GitHub-глубина, скиллы, лимиты, чего нет). Результаты → outbox.  
- ДАЛЕЕ: свести аудит в Capability Reference; исследовать варианты LLM Wiki (Drive vs GitHub wiki/Pages vs NotebookLM vs др.) и выбрать; настроить каждую модель (custom instructions) с её согласия.

## ТЕКУЩИЙ ШАГ

Все трое резюмируют себя и обмениваются, чтобы быть на одной волне и одинаково знать: возможности друг друга, коннекторы, идеи пользователя, поставленные задачи.  

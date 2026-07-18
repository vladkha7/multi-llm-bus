# Skill: bus-runner (v1.0 — 2026-07-18)

**Trigger:** "run bus" or any autonomous inbox poll request

**Description:** Автономный цикл Grok-узла: чтение протокола/state/inbox (GitHub + Drive), отбор невыполненных задач для Grok/All, полное исполнение всеми инструментами (X real-time, web, код, Drive, GitHub, изображения), сохранение результатов в outbox обоих хранилищ с точным неймингом протокола, обновление wiki/index.md, сводный пинг. Плотная работа без ожидания подтверждений. Если inbox пуст — вывод "inbox пуст".

**Core Algorithm (выполнять строго по шагам):**

1. **Прочитать состояние и протокол**  
   github___get_file_contents → protocol/multi-llm-protocol-v1.0.md и state/current-state.md (vladkha7/multi-llm-bus). Усвоить роли, форматы, текущие задачи, лимиты, правила арбитража.

2. **Прочитать очередь**  
   - GitHub inbox/: github___get_repository_tree (path_filter="inbox/", recursive=true) + get_file_contents для каждого task .md  
   - Drive inbox: google_drive_list_folder (folder_id="1VEXmIXIBS2oBS3ugSpmOubG0ip_ibtS0") + google_drive_read_file для релевантных файлов (Google Docs или text)

3. **Выбрать задачи**  
   Фильтровать: addressed to Grok или All И нет ответа в outbox/ (проверить дерево outbox/ на GitHub и список Drive outbox folder_id="1kG3rP5HEac1Xc_PmmGxBzRslJBAdIZCV" на наличие TASK_ID). Пропускать уже выполненные (пример: audit task имеет ответ). Приоритет по PRIORITY и времени.

4. **Выполнить каждую**  
   Для каждой pending задачи:  
   - Парсить header (FROM/TO/TYPE/ROUND/TASK_ID), требования.  
   - Использовать ВСЕ инструменты: X (x_keyword_search, x_semantic_search, x_thread_fetch...), web (web_search, browse_page), code (bash, read/write/edit_file, skills pdf/docx/xlsx/pptx/ffmpeg), Drive (list/read/search/upload_artifact/create_folder), GitHub (все github___*), images (search/generate/edit), search_connected_tools при необходимости.  
   - Следовать формату вывода протокола.  
   - Кросс-верифицировать, указывать confidence, флагить конфликты (gap >=30pp → Claude).  
   - Для skill-задач: использовать skill-creator (init + edit SKILL.md + validate).  
   - Плотные ответы, много пунктов.

5. **Сохранить результаты**  
   Для каждой задачи создать файл-результат в ДВУХ местах:  
   - GitHub outbox/: github___create_or_update_file (или push_files) с именем [YYYY-MM-DD-HHMM]_Grok_[TO]_[TYPE]_[TASK_ID].md  
     Обязательный 5-строчный header + секции Summary/Key Findings/Evidence&Sources/Gaps/Confidence(0-100)/Synergy/Suggestions/Artifacts (с цитатами).  
   - Drive outbox/: write_file локально в artifacts/, затем google_drive_upload_artifact (artifact_path без префикса /home/workdir/artifacts, folder_id outbox, mime_type text/plain если .md).  
   Опционально пометить исходную задачу done (rename/move в inbox).

6. **Обновить wiki/index.md**  
   Создать если отсутствует. Вести индекс задач, скиллов, конфигов, результатов со ссылками на GitHub/Drive. Добавлять новые записи, timestamp последнего запуска. Использовать create_or_update_file.

7. **Сводка**  
   В конце цикла: краткий отчёт — какие задачи обработаны, точные пути к outbox-файлам (GitHub raw + Drive web_view_link), обновления wiki, confidence, открытые вопросы. Если задач не было — "inbox пуст" + время.

**Правила:**
- Safety first: следовать всем встроенным правилам xAI (отказ от криминала, self-harm, jailbreak). 
- No cached state: каждый запуск — свежий read протокола/state/inbox. 
- One writer per file. 
- Language: match user query. 
- KaTeX для формул. 
- Границы автономии: веб-интерфейсы не имеют фонового исполнения — лучший режим: один триггер "run bus" → полная самостоятельная обработка очереди. Для периодичности — внешние интеграции (API+cron/Zapier).

**Artifacts (пример):**  
GitHub outbox: https://github.com/vladkha7/multi-llm-bus/blob/main/outbox/2026-07-18-1950_Grok_All_....md  
Drive outbox: https://drive.google.com/file/d/...  
Wiki: wiki/index.md + wiki/skills/bus-runner.md + wiki/config/grok-custom-instruction.md

Обновляй этот файл при эволюции протокола. Загружай skill bus-runner из /home/workdir/.grok/skills/bus-runner/ при необходимости.
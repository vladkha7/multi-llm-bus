# Skill: bus-runner

**Trigger:** "run bus" or daily automation

**Description:** Автономный цикл чтения inbox, выполнения задач и записи в outbox.

**Algorithm:**
1. Прочитать GitHub inbox (get_repository_tree + get_file_contents) и Drive inbox.
2. Найти файлы-задачи, адресованные Grok или All, со статусом new/pending.
3. Для каждой задачи: выполнить (исследование, код, wiki-страница и т.д.).
4. Сохранить результат в outbox/ с правильным неймингом.
5. Пометить задачу как done (переименовать или добавить .done).
6. Обновить wiki/index.md.
7. Дать сводный пинг в чат.

**Output:** Отчёт о выполненных задачах + пути к результатам.
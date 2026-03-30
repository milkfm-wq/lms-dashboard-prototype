# Dashboard Prototype Pack

Цель этой папки:
- быстро согласовать UI дашбордов с наставником на мокапе (без БД);
- зафиксировать требования так, чтобы потом безболезненно подключить реальные данные.

## Что внутри

- `Отчёт для наставника - прототип dashboard.md` — краткий отчёт: что сделано, зачем, роль наставника, как дать доступ.
- `Dashboard Spec v1.md` — описание экранов и блоков.
- `UX Feedback Log.md` — журнал правок от наставника.
- `Data Contract.md` — поля и форматы данных для каждого блока.
- `UI-to-DB Mapping.md` — привязка UI-полей к таблицам/полям БД.
- `API Contract.md` — контракты endpoint для блоков.
- `Definition of Done - Dashboard.md` — критерии готовности.
- `Role Visibility Matrix.md` — что видит mentor/assistant/student.

## Как использовать

1. Рисуем/показываем мокап.
2. Все комментарии фиксируем в `UX Feedback Log.md` по ID блока.
3. Финализируем `Dashboard Spec v1.md`.
4. Заполняем `Data Contract.md` и `API Contract.md`.
5. Связываем с базой через `UI-to-DB Mapping.md`.
6. Проверяем готовность по `Definition of Done - Dashboard.md`.

## Prototype v01 (web)

- Файл прототипа: `index.html`
- Открыть локально: двойной клик или через VS Code Live Server.
- Внутри прототипа:
  - у каждого блока есть `Вопрос` и `Комментарий`;
  - сохранение в `localStorage`;
  - экспорт:
    - `Export JSON`
    - `Export Markdown`
- Имя файлов экспорта генерируется автоматически по timestamp:
  - `dashboard-feedback-YYYY-MM-DD_HH-MM-SS.json`
  - `dashboard-feedback-YYYY-MM-DD_HH-MM-SS.md`
- Номер итерации ведётся отдельно в документах (`UX Feedback Log`, `Dashboard Spec`).

Рекомендуемая папка для входящих ответов от наставника:
- `reports/dashboard-prototype/feedback/`

## GitHub Pages (без ручного хостинга)

Минимальный процесс:

1. Создать отдельный репозиторий (например `lms-dashboard-prototype`).
2. Загрузить в него содержимое этой папки (`index.html` + docs).
3. В GitHub открыть `Settings -> Pages`.
4. Выбрать:
   - `Deploy from a branch`
   - `Branch: main`
   - `Folder: / (root)`
5. Получить постоянную ссылку вида:
   - `https://<github-user>.github.io/lms-dashboard-prototype/`

После этого для обновления прототипа достаточно commit/push в тот же repo.

## Правило ID блоков

Используем стабильные идентификаторы:
- `M*` — metric cards
- `C*` — charts
- `T*` — tables
- `S*` — student card sections
- `F*` — filters

Пример:
- `M1` Общий прогресс группы
- `C1` Динамика прогресса по неделям
- `T1` Таблица участников

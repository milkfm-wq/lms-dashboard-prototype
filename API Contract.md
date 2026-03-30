# API Contract

Контракты endpoint для обеспечения данных дашборда.

## Формат

| Endpoint | Назначение | Params | Основные поля ответа | Ошибки | Статус |
|---|---|---|---|---|---|
| GET /api/programs/:id/dashboard/mentor | Главный дашборд mentor | period, week, status, q, page, limit | cards, charts, studentsTable, selectedStudent, meta | 400/401/403/500 | Proposed |
| GET /api/programs/:id/dashboard/student | Личный дашборд student | period, week | cards, charts, myTasks, myPenalties, meta | 400/401/403/500 | Proposed |
| GET /api/programs/:id/dashboard/assistant | Облегчённый дашборд assistant | period, week, status, q, page, limit | cards, charts, studentsTable, meta | 400/401/403/500 | Proposed |

## Endpoint details (заполняется)

### GET /api/programs/:id/dashboard/mentor

- Query params:
  - `period`: `7d|30d|90d|current_program` (default `30d`)
  - `week`: `all|w1..w9` (default `all`)
  - `status`: `all|active|withdrawn` (default `active`)
  - `q`: строка поиска по имени/проекту (optional)
  - `page`: integer (default `1`)
  - `limit`: integer (default `25`)
- Response schema (high level):
  - `cards`: `{M1,M2,M3,M4}`
  - `charts`: `{C1,C2}`
  - `studentsTable[]`: `T1 rows`
  - `selectedStudent`: `S1` (optional, если передан `programMemberId`)
  - `meta`
- Empty behavior:
  - возвращать пустые массивы/нули без 500
- Error behavior:
  - `400` invalid query
  - `401` auth required
  - `403` role forbidden
  - `500` internal

### GET /api/programs/:id/dashboard/student

- Query params:
  - `period`
  - `week`
- Response schema:
  - только собственные данные (`S1 + личные KPI + история`)
- Ограничения видимости:
  - никаких чужих внутренних полей
  - только разрешённая групповая информация по режиму видимости потока

### GET /api/programs/:id/dashboard/assistant

- Query params:
  - как у mentor, кроме выбора `selectedStudent` с restricted полями
- Response schema:
  - `cards`, `charts`, `studentsTable`, `meta`
- Ограничения видимости:
  - read-only
  - без write-операций и без внутренних mentor-комментариев

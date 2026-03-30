# Data Contract

Документ описывает входные данные для каждого UI-блока.

## Формат записи

| Block ID | Поле UI | Тип | Обяз. | Nullable | Формат/единицы | Пример |
|---|---|---|---|---|---|---|
| M1 | groupProgressPercent | number | yes | no | 0..100 (%) | 68.4 |

## Разделы

### M* Metric Cards

| Block ID | Поле UI | Тип | Обяз. | Nullable | Формат/единицы | Пример |
|---|---|---|---|---|---|---|
| M1 | groupProgressPercent | number | yes | no | 0..100 (%) | 68.4 |
| M1 | deltaVsPrevWeek | number | yes | no | -100..100 (pp) | +2.3 |
| M2 | averageRating | number | yes | no | 0..100 | 72.1 |
| M2 | ratingTrend | string | yes | no | up/down/flat | up |
| M3 | riskStudentsCount | number | yes | no | integer | 4 |
| M3 | riskSharePercent | number | yes | no | 0..100 (%) | 21.0 |
| M4 | leadersCount | number | yes | no | integer | 3 |
| M4 | leadersTopNames | string[] | no | yes | max 3 names | ["Иван","Мария","Олег"] |

### C* Charts

| Block ID | Поле UI | Тип | Обяз. | Nullable | Формат/единицы | Пример |
|---|---|---|---|---|---|---|
| C1 | series[].periodLabel | string | yes | no | week/day label | "W3" |
| C1 | series[].progressPercent | number | yes | no | 0..100 (%) | 64.2 |
| C2 | series[].periodLabel | string | yes | no | week label | "W3" |
| C2 | series[].disciplineScore | number | yes | no | 0..100 | 76.0 |
| C2 | series[].violationsCount | number | yes | no | integer | 5 |

### T* Tables

| Block ID | Поле UI | Тип | Обяз. | Nullable | Формат/единицы | Пример |
|---|---|---|---|---|---|---|
| T1 | rows[].programMemberId | uuid | yes | no | UUID | "cae01d75-..." |
| T1 | rows[].studentFullName | string | yes | no | text | "Иван Петров" |
| T1 | rows[].projectName | string | no | yes | text | "Маркетплейс X" |
| T1 | rows[].progressPercent | number | yes | no | 0..100 (%) | 63.0 |
| T1 | rows[].rating | number | yes | no | 0..100 | 71.0 |
| T1 | rows[].disciplineScore | number | yes | no | 0..100 | 80.0 |
| T1 | rows[].riskStatus | string | yes | no | normal/risk | "risk" |
| T1 | rows[].leaderStatus | boolean | yes | no | true/false | false |
| T1 | rows[].isActive | boolean | yes | no | true/false | true |

### S* Student Card

| Block ID | Поле UI | Тип | Обяз. | Nullable | Формат/единицы | Пример |
|---|---|---|---|---|---|---|
| S1 | student.programMemberId | uuid | yes | no | UUID | "cae01d75-..." |
| S1 | student.fullName | string | yes | no | text | "Иван Петров" |
| S1 | student.projectName | string | no | yes | text | "Маркетплейс X" |
| S1 | student.pointA | string | no | yes | text | "0 клиентов" |
| S1 | student.pointB | string | no | yes | text | "20 клиентов/мес" |
| S1 | student.progressPercent | number | yes | no | 0..100 (%) | 63.0 |
| S1 | student.rating | number | yes | no | 0..100 | 71.0 |
| S1 | student.disciplineScore | number | yes | no | 0..100 | 80.0 |
| S1 | student.openTasksCount | number | yes | no | integer | 2 |
| S1 | student.unpaidPenaltiesAmount | number | yes | no | money | 3500 |
| S1 | student.weeklyHistory[] | object[] | no | yes | week snapshots | [{"week":"W3","progressPercent":63}] |

## Фильтры (F*)

| Block ID | Поле UI | Тип | Обяз. | Nullable | Формат/единицы | Пример |
|---|---|---|---|---|---|---|
| F1 | period | string | yes | no | 7d/30d/90d/current_program | "30d" |
| F2 | week | string | no | yes | all/w1..w9 | "w3" |
| F3 | participantStatus | string | no | yes | all/active/withdrawn | "active" |

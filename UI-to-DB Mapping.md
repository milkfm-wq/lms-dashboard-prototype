# UI-to-DB Mapping

Связка UI-полей с источниками в БД и/или вычислениями.

| Block ID | Поле UI | Источник (таблица.поле) | Тип трансформации | Формула/правило | Примечание |
|---|---|---|---|---|---|
| M1 | groupProgressPercent | group_metrics.progress_percent | direct | — | если готов агрегат |
| M1 | groupProgressPercent | participant_metrics.* | aggregate | avg(progress_percent) | fallback |
| M1 | deltaVsPrevWeek | group_metrics.progress_percent | derived | current_week - previous_week | если есть weeks |
| M2 | averageRating | group_metrics.average_rating | direct | — | предпочтительный источник |
| M2 | averageRating | participant_metrics.rating | aggregate | avg(rating) | fallback |
| M3 | riskStudentsCount | participant_metrics.risk_status | aggregate | count(where risk_status='risk') | для активных |
| M3 | riskSharePercent | participant_metrics.risk_status + program_members.is_active | derived | risk_count / active_count * 100 | % риска |
| M4 | leadersCount | participant_metrics.leader_week_flag | aggregate | count(where leader_week_flag=true) | текущая неделя |
| M4 | leadersTopNames | participant_metrics + program_members + users | aggregate | top 3 by ranking_score | имена лидеров |
| C1 | series[].progressPercent | group_metrics.progress_percent_by_week | direct | — | или материализованный агрегат |
| C2 | series[].disciplineScore | group_metrics.discipline_score_by_week | direct | — | для графика дисциплины |
| C2 | series[].violationsCount | session_tracking (count fields) | aggregate | sum(late_count + missed_count + overdue_count + buddy_missed_count) | по неделе |
| T1 | rows[].studentFullName | users.full_name | direct | join via program_members.user_id | таблица участников |
| T1 | rows[].projectName | project_descriptions.project_name | direct | left join by program_member_id | nullable |
| T1 | rows[].progressPercent | participant_metrics.progress_percent | direct | latest week snapshot | |
| T1 | rows[].rating | participant_metrics.rating | direct | latest week snapshot | |
| T1 | rows[].disciplineScore | participant_metrics.discipline_score | direct | latest week snapshot | |
| T1 | rows[].riskStatus | participant_metrics.risk_status | direct | latest week snapshot | normal/risk |
| T1 | rows[].leaderStatus | participant_metrics.leader_week_flag | direct | selected week | boolean |
| T1 | rows[].isActive | program_members.is_active | direct | — | active/withdrawn |
| S1 | student.pointA | student_goals.point_a | direct | latest | nullable |
| S1 | student.pointB | student_goals.point_b | direct | latest | nullable |
| S1 | student.openTasksCount | tasks.status | aggregate | count(where status in todo/in_progress) | by program_member_id |
| S1 | student.unpaidPenaltiesAmount | penalties.amount + penalties.payment_status | aggregate | sum(amount where payment_status='unpaid' and status='confirmed') | debt |
| S1 | student.weeklyHistory[] | participant_metrics + program_weeks | direct | ordered by week_number | history |

## Типы трансформации

- `direct`: прямое поле из БД.
- `aggregate`: агрегат (avg/sum/count/rank).
- `derived`: вычисление на уровне API.
- `manual`: ввод/корректировка наставником.

## Проверка готовности привязки

- для каждого поля в UI есть источник или правило вычисления;
- нет полей со статусом "непонятно откуда брать";
- все manual-поля помечены отдельно.

## Поля, требующие подтверждения

- Точная формула `rating`.
- Порог/формула `risk_status`.
- Правила присвоения `leader_week_flag`.

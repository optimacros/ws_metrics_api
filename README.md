#  Документация по сервису метрик Optimacros

ИС Optimacros предоставляет доступ к сервису метрик основных параметров приложения по протоколу HTTP (для использования в системах Prometheus, Zabbix и т.п.).

Сервис метрик доступен по следующим точкам доступа:
- **/api/v1/metrics** (предоставляет метрики в формате [**JSON**](#metrics-json))
- **/api/v1/metrics/prometheus** (предоставляет метрики в формате [**Prometheus**](#metrics-prometheus))

Основные метрики приложения:
- системные (system)
  - **system_cpu_load** - степень загруженности процессора в процентах от 0 до 100
  - **system_memory_used** - размер использованной памяти
- ворскспейс (workspace)
  - **workspace_memory_allocated** - размер занятой памяти
  - **workspace_memory_allowance** - размер максимально занятой памяти
  - **workspace_memory_total** - размер общедоступной памяти
  - **workspace_users_total** - количество всех пользователей
  - **workspace_users_active** - количество активных (залогиненных) пользователей
  - **workspace_users_modeler** - количество пользователей-моделеров
  - **workspace_users_non_modeler** - количество обычных пользователей
  - **workspace_backups_count** - количество созданных бэкапов
  - **workspace_backups_size** - размер созданных бэкапов
  - **workspace_backups_size_limit** - лимит пространства для бэкапов
  - **workspace_backups_tasks_failed** - количество провальных задач бекапирования в системе
- запросы (requests)
  - **requests_number** - количество запросов (мгновенное значение (RPS))
  - **requests_history_number** - общее количество запросов (по истории)
  - **requests_history_time_minimum** - минимальное время выполнения запросов
  - **requests_history_time_maximum** - максимальное время выполнения запросов
  - **requests_history_time_average** - среднее время выполнения запросов
  - **requests_history_time_median** - медиана времени выполнения запросов
- модели (models)
  - **models_counter_total** - общее количество моделей в системе
  - **models_counter_online** - количество доступных моделей (online)
  - **models_counter_offline** - количество недоступных моделей (offline)

## Метрики в формате JSON <a name="metrics-json"></a>

Следующая точка доступа **/api/v1/metrics** предоставляет метрики в формате <a href="https://habr.com/ru/articles/554274/#json_object">**JSON**</a>.

Пример метрик в формате JSON:<br>
![Metrics JSON](./pics/metrics_json.png)

## Метрики в формате Prometheus <a name="metrics-prometheus"></a>

Следующая точка доступа **/api/v1/metrics** предоставляет метрики в формате <a href="https://habr.com/ru/articles/554274/#json_object">**JSON**</a>.

Пример метрик в формате <a href="https://prometheus.io/docs/instrumenting/exposition_formats/">Prometheus</a>:<br>
![Metrics Prometheus](./pics/metrics_prometheus.png)

## Глоссарий

**JSON** — текстовый формат обмена данными, <a href="https://habr.com/ru/articles/554274/#json_object">основанный</a> на JavaScript.

**Ворскспейс (workspace)** – приложение, на котором пользователи размещают свои модели и проводят работу с данными.

**Запрос (request)** – процесс обращения пользователя через систему Оптимакрос к определенному функционалу системы.

**Модель** – совокупность структур данных, связанных между собой, в виде мастер-данных, форм ввода, отчетов и визуализации, ограниченных конкретной областью (физической и логической (предметной)).

**Prometheus** - это система мониторинга и оповещений, хранящая и обрабатывающая метрики, собираемые из экспортеров в Time Series Database (TSDB). Prometheus сам собирает метрики, опрашивая необходимые сайты, предоставляющие метрики.

**Zabbix** - это программное обеспечение для мониторинга многочисленных параметров сети, жизнеспособности и целостности серверов, приложений, сервисов. Zabbix использует гибкий механизм оповещений, что позволяет пользователям настраивать уведомления основанные на e-mail практически на любое событие.


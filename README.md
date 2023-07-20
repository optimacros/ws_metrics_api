#  Документация по сервису метрик Optimacros

ИС Optimacros предоставляет доступ к сервису метрик основных параметров приложения по протоколу HTTP (для использования в системах Prometheus, Zabbix и т.п.).

Сервис метрик доступен по следующим точкам доступа:
- **/api/v1/metrics** (предоставляет метрики в формате [**JSON**](#metrics-json))
- **/api/v1/metrics/prometheus** (предоставляет метрики в формате [**Prometheus**](#metrics-prometheus))

Основные метрики приложения:
- системные (system)
  - [**system_cpu_load**](#metrics_system_cpu_load) - степень загруженности процессора в процентах от 0 до 100
  - [**system_memory_used**](#metrics_system_memory_used) - размер использованной памяти
- ворскспейс (workspace)
  - [**workspace_memory_allocated**](#metrics_workspace_memory_allocated) - размер занятой памяти
  - [**workspace_memory_allowance**](#metrics_workspace_memory_allowance) - размер максимально занятой памяти
  - [**workspace_memory_total**](#metrics_workspace_memory_total) - размер общедоступной памяти
  - [**workspace_users_total**](#metrics_workspace_users_total) - количество всех пользователей
  - [**workspace_users_active**](#metrics_workspace_users_active) - количество активных (залогиненных) пользователей
  - [**workspace_users_modeler**](#metrics_workspace_users_modeler) - количество пользователей-моделеров
  - [**workspace_users_non_modeler**](#metrics_workspace_users_non_modeler) - количество обычных пользователей
  - [**workspace_backups_count**](#metrics_workspace_backups_count) - количество созданных бэкапов
  - [**workspace_backups_size**](#metrics_workspace_backups_size) - размер созданных бэкапов
  - [**workspace_backups_size_limit**](#metrics_workspace_backups_size_limit) - лимит пространства для бэкапов
  - [**workspace_backups_tasks_failed**](#metrics_workspace_backups_tasks_failed) - количество провальных задач бекапирования в системе
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

Следующая точка доступа **/api/v1/metrics/prometheus** предоставляет метрики в формате <a href="https://prometheus.io/docs/instrumenting/exposition_formats/">**Prometheus**</a>.

Пример метрик в формате Prometheus:<br>
![Metrics Prometheus](./pics/metrics_prometheus.png)

## Детали метрик

### Системные метрики

#### system_cpu_load <a name="metrics_system_cpu_load"></a>

Данная метрика предоставляет информацию о загруженности процессора компьютера, на котором работает воркспейс.
<br>Метрика представлена целым числом от 0 (минимальное значение) до 100 (максимальное значение).

#### system_memory_used <a name="metrics_system_memory_used"></a>

Данная метрика предоставляет информацию об использованной оперативной памяти компьютера, на котором работает воркспейс.
<br>Метрика представлена целым числом и показывает размер использованной памяти в байтах.

### Метрики воркспейс

#### workspace_memory_allocated <a name="metrics_workspace_memory_allocated"></a>

Данная метрика предоставляет информацию об использованной дисковой памяти на компьютере, где работает воркспейс. Т.е. отображает размер дисковой памяти, занимаемый всеми моделями, хранящимися на воркспейсе.
<br>Метрика представлена целым числом и показывает размер использованной памяти в байтах.
<br>Данная картинка показывает пример использованной дисковой памяти и связанные метрики:
<br>![Workspace Memory](./pics/workspace_memory.png)

#### workspace_memory_allowance <a name="metrics_workspace_memory_allowance"></a>

Данная метрика предоставляет информацию об лимите дисковой памяти на компьютере, где работает воркспейс. 
<br>Метрика представлена целым числом и показывает размер памяти в байтах.
<br>Приближение использованной дисковой памяти к данному лимиту указывает на увеличение размера воркспейс, возможно следует задуматься об удалении некоторых моделей или об увеличении дискового пространства на компьютере.

#### workspace_memory_total <a name="metrics_workspace_memory_total"></a>

Данная метрика предоставляет информацию о размере общей доступной дисковой памяти на компьютере, где работает воркспейс. 
<br>Метрика представлена целым числом и показывает размер памяти в байтах.
<br>Использованная дисковая память физически не может быть больше доступной дисковой памяти.

#### workspace_users_total <a name="metrics_workspace_users_total"></a>

Данная метрика предоставляет информацию об общем количестве пользователей, **зарегистрированных** в воркспейс.
<br>Метрика представлена целым числом.

#### workspace_users_active <a name="metrics_workspace_users_active"></a>

Данная метрика предоставляет информацию о количестве пользователей, которые **залогинены** в воркспейс.
<br>Метрика представлена целым числом.

#### workspace_users_modeler <a name="metrics_workspace_users_modeler"></a>

Данная метрика предоставляет информацию об общем количестве **пользователей-моделеров**, зарегистрированных в воркспейс.
<br>Метрика представлена целым числом.

#### workspace_users_non_modeler <a name="metrics_workspace_users_non_modeler"></a>

Данная метрика предоставляет информацию об общем количестве **обычных** пользователей (не моделеров), зарегистрированных в воркспейс.
<br>Метрика представлена целым числом.

#### workspace_backups_count <a name="metrics_workspace_backups_count"></a>

Данная метрика предоставляет информацию об общем количестве созданных бэкапов моделей.
<br>Метрика представлена целым числом.

#### workspace_backups_size <a name="metrics_workspace_backups_size"></a>

Данная метрика предоставляет информацию о размере дисковой памяти на компьютере, которую занимают все созданные бэкапы моделей.
<br>Метрика представлена целым числом и показывает размер памяти в байтах.

#### workspace_backups_size_limit <a name="metrics_workspace_backups_size_limit"></a>

Данная метрика предоставляет информацию об лимите дисковой памяти на компьютере, которую занимают все созданные бэкапы моделей. 
<br>Метрика представлена целым числом и показывает размер памяти в байтах.
<br>Приближение использованной дисковой памяти, занятой созданными бэкапами моделей, к данному лимиту указывает на возможные проблемы с созданием бэкапов моделей, возможно следует задуматься об удалении бэкапов моделей или об увеличении дискового пространства на компьютере.

#### workspace_backups_tasks_failed <a name="metrics_workspace_backups_count"></a>

Данная метрика предоставляет информацию об общем количестве провальных задач создания бэкапов моделей в системе.
<br>Метрика представлена целым числом.


## Глоссарий

**JSON** — текстовый формат обмена данными, <a href="https://habr.com/ru/articles/554274/#json_object">основанный</a> на JavaScript.

**Ворскспейс (workspace)** – приложение (ПО «Оптимакрос»), на котором пользователи размещают свои модели и проводят работу с данными.

**Модель** – совокупность структур данных, связанных между собой, в виде мастер-данных, форм ввода, отчетов и визуализации, ограниченных конкретной областью (физической и логической (предметной)).

**Моделер** - продвинутый пользователь ПО «Оптимакрос», который имеет доступ к инструментам и механизмам бизнес-моделировани ПО «Оптимакрос».

**Запрос (request)** – процесс обращения пользователя через систему ПО «Оптимакрос» к определенному функционалу системы.

**Бэкап (backup)** – резервная копия модели.

**Prometheus** - это система мониторинга и оповещений, хранящая и обрабатывающая метрики, собираемые из экспортеров в Time Series Database (TSDB). Prometheus сам собирает метрики, опрашивая необходимые сайты, предоставляющие метрики.

**Zabbix** - это программное обеспечение для мониторинга многочисленных параметров сети, жизнеспособности и целостности серверов, приложений, сервисов. Zabbix использует гибкий механизм оповещений, что позволяет пользователям настраивать уведомления основанные на e-mail практически на любое событие.


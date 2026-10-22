# DataOps Zero to Hero

**Data Contracts · Качество · Dataset Versions · Lineage · Orchestration · Эксплуатация данных**

## Навигация

| Раздел | Название |
| --- | --- |
| 1 | [Фундамент DataOps и эксплуатационная модель data-продукта](#section-01) |
| 2 | [Среды, доступы и доставка изменений данных](#section-02) |
| 3 | [Data contracts, качество и data observability](#section-03) |
| 4 | [Версионирование datasets и воспроизводимость](#section-04) |
| 5 | [Lineage, каталог, governance и privacy](#section-05) |
| 6 | [Оркестрация: Airflow, Dagster и Prefect](#section-06) |
| 7 | [Надёжная эксплуатация pipelines, backfill и поддержка MLOps](#section-07) |
| 8 | [Практические проекты и критерии готовности DataOps](#section-08) |

## Содержание

<a id="section-01"></a>

<details>
<summary>

### 1. Фундамент DataOps и эксплуатационная модель data-продукта

</summary>

- **Предмет DataOps**
  - Доставка изменений в data-продуктах
  - Воспроизводимость и контроль operational state
  - Ответственность producer, consumer и platform team
  - Связь DataOps, Data Engineering и MLOps
  - Потребительский контракт вместо внутренней реализации ETL

- **Жизненный цикл data-продукта**
  - Development, validation, release и production
  - Версии кода, конфигурации и входных snapshots
  - Ownership, service catalog и документация
  - Условия принятия данных downstream-потребителем
  - Deprecation и миграция consumers

- **Эксплуатационная модель**
  - Freshness, completeness и delivery deadlines
  - Инциденты данных и технические инциденты
  - Регламент остановки публикации неверных данных
  - Исправление, повторная публикация и consumer notification
  - Аудит ручных корректировок

- **Границы справочника**
  - Платформенные guarantees для batch и streaming jobs
  - Эксплуатация orchestrators и metadata services
  - Контракты storage и вычислительных платформ
  - Передача требований к ML datasets и features
  - Ссылка на отдельное изучение SQL, ETL и вычислительных движков

</details>

<a id="section-02"></a>

<details>
<summary>

### 2. Среды, доступы и доставка изменений данных

</summary>

- **Среды и доступ**
  - Изоляция research и production datasets
  - Маскированные, синтетические и ограниченные test datasets
  - Минимальные read/write permissions
  - Временные sandboxes и cleanup
  - Доступ внешних подрядчиков и аннотаторов

- **Доставка изменений**
  - CI для contracts и operational metadata
  - Promotion проверенных pipeline definitions
  - Совместимость schema changes
  - Проверка downstream impact до rollout
  - Release manifest data-продукта

- **Изменения и миграции**
  - Schema compatibility и staged rollout
  - Dual-run старой и новой версии
  - Shadow comparison результатов
  - Rollforward при невозможности возврата state
  - Миграция scheduler или compute backend

- **Изоляция и безопасность**
  - Раздельные identities producer и consumer
  - Ограничение write scope каждого pipeline
  - Secrets и приватный доступ к источникам
  - Защита test runs от production outputs
  - Auditable ручные операции с данными

</details>

<a id="section-03"></a>

<details>
<summary>

### 3. Data contracts, качество и data observability

</summary>

- **Data contracts**
  - Schema, semantics, ownership и SLA
  - Required, optional и nullable поля
  - Units, categories, time zones и identifier semantics
  - Versioning и правила breaking changes
  - Проверки producer и consumer на границе

- **Измерения качества**
  - Completeness, validity, uniqueness и consistency
  - Freshness, volume и distribution checks
  - Referential integrity и reconciliation totals
  - Accuracy и необходимость внешнего ground truth
  - Различие технической валидности и бизнес-корректности

- **Quality gates**
  - Great Expectations, Soda и аналогичные проверки
  - Проверки перед публикацией dataset
  - Severity, quarantine и fail-open/fail-closed
  - Baselines, dynamic thresholds и сезонность
  - Учет стоимости full scan и sampling

- **Data observability**
  - Метрики datasets, partitions и critical columns
  - Volume anomalies и задержка обновления
  - Lineage-aware impact analysis
  - Корреляция изменений producer с деградацией ML
  - Dashboards и alerts для владельцев данных

- **Работа с нарушениями**
  - Карантин партии или диапазона
  - Ограничение распространения некорректных данных
  - Поиск затронутых datasets, features и моделей
  - Recompute, replay и controlled backfill
  - Проверка качества после исправления

- **Сопровождение контрактов**
  - Contract registry и code review
  - Consumer inventory и migration windows
  - Documented exceptions с expiry
  - Метрики нарушения контрактов
  - Contract tests в CI обеих сторон

</details>

<a id="section-04"></a>

<details>
<summary>

### 4. Версионирование datasets и воспроизводимость

</summary>

- **Идентичность dataset**
  - Dataset name, version и immutable snapshot
  - Files, partitions, manifest и checksum
  - Data cutoff и границы включённых событий
  - Составной dataset из нескольких источников
  - Ссылки на dataset вместо копирования в Git

- **Управление версиями**
  - DVC, lakeFS и storage-native snapshots
  - Branching, tagging и promotion datasets
  - Content addressing и дедупликация
  - Atomic publication и видимость завершённой версии
  - Retention и защита используемых snapshots от удаления

- **Проверяемая воспроизводимость**
  - Dataset version вместе с кодом и окружением
  - Повторное получение snapshot из manifest
  - Проверка целостности при восстановлении
  - Разделение reproducibility и битовой идентичности результата
  - Политика недоступного или отозванного источника

</details>

<a id="section-05"></a>

<details>
<summary>

### 5. Lineage, каталог, governance и privacy

</summary>

- **Lineage**
  - Source–dataset–feature–run–model–deployment
  - OpenLineage, Marquez и metadata integrations
  - Column-level и dataset-level lineage
  - Provenance внешних и размеченных данных
  - Impact analysis при отзыве источника

- **Каталог и governance**
  - Owners, stewards и классификация данных
  - DataHub, OpenMetadata и каталоги
  - Discoverability и бизнес-описание
  - Политики доступа и audit trail
  - Срок хранения и legal retention по требованиям

- **Privacy operations**
  - Consent, purpose limitation и минимизация
  - PII detection, masking и tokenization
  - Права доступа на уровне строки и колонки
  - Удаление данных и зависимые snapshots
  - Учет производных features и обученных моделей

</details>

<a id="section-06"></a>

<details>
<summary>

### 6. Оркестрация: Airflow, Dagster и Prefect

</summary>

- **Модель workflow**
  - DAG, task, run и execution state
  - Dependencies, parameters и artifacts
  - Scheduled, event-driven и manual triggers
  - Idempotent tasks и внешние побочные эффекты
  - Разделение orchestration и compute execution

- **Airflow**
  - Scheduler, executor, workers и metadata database
  - DAG parsing и нагрузка control plane
  - Logical date, data intervals и time zones
  - Pools, concurrency, retries и deferrable tasks
  - Assets/datasets и API выбранной версии

- **Dagster и Prefect**
  - Asset-centric и task/flow-centric модели
  - Resources, deployments и execution environments
  - Partitions, schedules и sensors
  - Workers, agents и job execution по версии продукта
  - Operational metadata и доступ к логам

- **Надёжность orchestrator**
  - HA scheduler и отказ metadata backend
  - Heartbeats, zombie tasks и потерянные workers
  - Credential rotation и secret delivery
  - Upgrades и metadata migrations
  - Backup definitions, metadata и конфигурации

- **Масштабирование исполнения**
  - Kubernetes executors и удалённые jobs
  - Очереди, pools и приоритеты команд
  - Контроль global и per-tenant concurrency
  - Вынос больших payload в artifact storage
  - Разделение CPU, GPU и I/O workloads

- **Наблюдаемость workflows**
  - Queue delay, execution time и end-to-end deadline
  - Task retries, failures и skipped dependencies
  - Корреляция run ID с внешними compute jobs
  - Alert на просроченный результат, а не только failed task
  - Runbooks зависшего scheduler и массового backfill

</details>

<a id="section-07"></a>

<details>
<summary>

### 7. Надёжная эксплуатация pipelines, backfill и поддержка MLOps

</summary>

- **Повторный запуск и восстановление**
  - Checkpoints и границы подтверждённого прогресса
  - Idempotency внешних writes
  - Retry classification и permanent errors
  - Poison records, quarantine и DLQ
  - Replay с контролем повторных эффектов

- **Backfill**
  - Диапазон, snapshot и ожидаемый результат
  - Разделение live processing и backfill capacity
  - Rate limits и приоритет текущих данных
  - Dry run и проверка затронутых consumers
  - Reconciliation результата с исходным состоянием

- **Эксплуатационные SLO**
  - Freshness, completeness и completion deadline
  - Queue delay и backlog age
  - Capacity для catch-up после простоя
  - Dependency readiness и degraded sources
  - Business impact при частичной публикации

- **Поддержка MLOps**
  - Dataset readiness перед training
  - Публикация feature snapshots по контракту
  - Запрет training на непроверенной партии
  - Lineage от источника до serving deployment
  - Совместное расследование data и model incidents

</details>

<a id="section-08"></a>

<details>
<summary>

### 8. Практические проекты и критерии готовности DataOps

</summary>

- **DataOps-контур**
  - Версионировать contract и dataset manifest
  - Запустить quality gates перед publication
  - Собрать lineage до ML consumer
  - Отработать bad data quarantine и backfill
  - Подтвердить freshness и completeness после восстановления

- **Безопасное изменение data contract**
  - Составить producer/consumer inventory и правила совместимости
  - Проверить изменение в CI обеих сторон контракта
  - Провести dual-run и reconciliation результатов
  - Выполнить controlled cutover с согласованными потребителями
  - Подтвердить freshness, completeness и готовность downstream

- **Инцидент данных и восстановление**
  - Обнаружить нарушение качества до публикации ML-потребителю
  - Ограничить распространение неверного snapshot
  - Найти затронутые artifacts и модели через lineage
  - Выполнить bounded backfill без вытеснения live processing
  - Восстановить согласованный dataset и зафиксировать evidence

- **Проверка самостоятельности DataOps**
  - Определить владельца, контракт и операционные SLO data-продукта
  - Воспроизвести публикацию по версии кода, конфигурации и dataset
  - Различить ошибку orchestrator, доступа и содержимого данных
  - Доказать корректность повторного запуска и очистки ресурсов
  - Подготовить runbook изменения, карантина и восстановления

</details>

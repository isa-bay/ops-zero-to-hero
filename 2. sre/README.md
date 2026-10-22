# SRE Zero to Hero

**Надёжность · Observability · SLO · On-call · Incidents · Performance · Disaster Recovery**

## Навигация

| Раздел | Название |
| --- | --- |
| 1 | [Фундамент SRE и гарантии распределённых систем](#section-01) |
| 2 | [Архитектура надёжных сервисов](#section-02) |
| 3 | [Наблюдаемость и OpenTelemetry](#section-03) |
| 4 | [Метрики, Prometheus, PromQL и Grafana](#section-04) |
| 5 | [Логи, distributed tracing и profiling](#section-05) |
| 6 | [SLI, SLO, SLA и error budgets](#section-06) |
| 7 | [Alerting, on-call, runbooks и управление toil](#section-07) |
| 8 | [Инциденты, troubleshooting и postmortems](#section-08) |
| 9 | [Производительность, нагрузочные тесты и capacity planning](#section-09) |
| 10 | [Disaster recovery, chaos engineering и resilience](#section-10) |
| 11 | [Практические проекты и критерии готовности SRE](#section-11) |

## Содержание

<a id="section-01"></a>

<details>
<summary>

### 1. Фундамент SRE и гарантии распределённых систем

</summary>

- **Роль SRE и работа с риском**
  - Надёжность как свойство пользовательского пути
  - Доступность, корректность и своевременность результата
  - Приоритизация риска по влиянию на пользователей
  - Партнёрство SRE, продукта и владельцев сервисов
  - Инженерная работа, дежурство и уменьшение toil

- **Жизненный цикл надёжного сервиса**
  - Service ownership и границы ответственности зависимостей
  - Production readiness review до первого релиза
  - Эксплуатационные контракты и документированные ограничения
  - Проверка готовности к дежурству и эскалации
  - Пересмотр надёжности при росте трафика и изменении продукта

- **Модель отказов**
  - Частичные отказы и ненадёжная сеть
  - Crash, pause и недоступность зависимости
  - Неопределённый результат операции после timeout
  - Fail-stop, Byzantine failures и границы модели
  - Коррелированные отказы и общие зависимости

- **Время и порядок**
  - Wall clock, monotonic clock и clock skew
  - Happens-before и частичный порядок событий
  - Lamport clocks и vector clocks на уровне принципов
  - Leases и опасность длительной паузы процесса
  - Event time, processing time и задержка доставки

- **Консистентность**
  - Linearizability, serializability и eventual consistency
  - Read-your-writes и monotonic reads
  - CAP и корректная интерпретация network partition
  - PACELC и компромисс latency–consistency
  - Quorum reads/writes и ограничения quorum-арифметики

- **Координация**
  - Leader election и split brain
  - Consensus и назначение Raft/Paxos
  - etcd, ZooKeeper и распределённые metadata stores
  - Distributed locks и fencing tokens
  - Service discovery и динамическое членство

- **Доставка и внешние эффекты**
  - At-most-once и at-least-once delivery
  - Exactly-once в пределах конкретной системы
  - Idempotency keys, deduplication и replay
  - Transactional outbox, inbox и change notifications
  - Sagas, компенсации и ограничения распределённой транзакции

- **Проектирование контрактов**
  - Versioned API и backward compatibility
  - Retry-safe операции и bounded concurrency
  - Проверка инвариантов при конкуренции
  - Устойчивость к дубликатам и переупорядочиванию
  - Явное описание границ гарантий системы

</details>

<a id="section-02"></a>

<details>
<summary>

### 2. Архитектура надёжных сервисов

</summary>

- **Декомпозиция системы**
  - Monolith, modular monolith и microservices
  - Control plane и data plane
  - Stateless compute и управление состоянием
  - Синхронные и асинхронные зависимости
  - Критический путь запроса и карта отказов

- **Изоляция отказов**
  - Bulkheads, cells и shuffle sharding
  - Tenant isolation и noisy neighbour
  - Connection pools и ограниченные очереди
  - Ограничение fan-out и amplification
  - Локализация отказа без глобального restart

- **Работа с перегрузкой**
  - Admission control и backpressure
  - Bounded queues и отказ от бесконечного буфера
  - Load shedding по приоритетам
  - Graceful degradation и fallback
  - Retry storms и положительная обратная связь

- **Кеширование**
  - Cache-aside, read-through и write-through
  - TTL, eviction и invalidation
  - Cache stampede, hot keys и negative caching
  - Stale-while-revalidate и допустимая свежесть
  - Корректность при смене модели и preprocessing

- **Высокая доступность**
  - Replication, redundancy и independent failure domains
  - Active-active и active-passive
  - Failover, failback и защита от split brain
  - Dependency SLO и составная доступность
  - Доступность при недоступном control plane

- **Эволюция архитектуры**
  - API compatibility и consumer-driven contracts
  - Strangler pattern и поэтапная миграция
  - Dual write, shadow read и reconciliation
  - Service deprecation и удаление зависимостей
  - Выбор минимально достаточной архитектуры

</details>

<a id="section-03"></a>

<details>
<summary>

### 3. Наблюдаемость и OpenTelemetry

</summary>

- **Модель наблюдаемости**
  - Вопросы о поведении системы и необходимые сигналы
  - Metrics, logs, traces, profiles и events
  - Monitoring, observability и debugging
  - RED, USE и golden signals
  - Пользовательский путь и внутренняя telemetry

- **Инструментирование**
  - Автоматическое и ручное instrumenting
  - Resource attributes и semantic conventions
  - Service name, version и deployment environment
  - Correlation IDs и trace context propagation
  - Измерение ошибок, latency и отменённых запросов

- **OpenTelemetry**
  - API, SDK и Collector
  - Receivers, processors и exporters
  - OTLP и выбор транспортного протокола
  - Agent и gateway deployment patterns
  - Совместимость SDK, Collector и backend

- **Обработка telemetry**
  - Batching, retries и persistent queues
  - Head sampling и tail sampling
  - Filtering, redaction и attribute limits
  - Cardinality budgets и sampling bias
  - Управление потерями при перегрузке pipeline

- **Архитектура telemetry-платформы**
  - Локальный сбор и центральная агрегация
  - Multi-tenant ingest и изоляция доступа
  - Retention, downsampling и object storage
  - Региональный сбор и требования к размещению данных
  - Cost attribution по сервису и владельцу

- **Надёжность наблюдаемости**
  - Monitoring самого monitoring
  - Потеря exporter, Collector или backend
  - Backpressure telemetry и влияние на приложение
  - Независимые black-box probes
  - Проверка качества и полноты поступающих сигналов

</details>

<a id="section-04"></a>

<details>
<summary>

### 4. Метрики, Prometheus, PromQL и Grafana

</summary>

- **Модель метрик**
  - Counter, gauge, histogram и summary
  - Labels, time series и cardinality
  - Classic и native histograms с учётом поддержки
  - Buckets и точность вычисления quantiles
  - Exemplars и переход от метрики к trace

- **Сбор Prometheus**
  - Pull model, scrape interval и timeout
  - Service discovery и relabeling
  - Exporters для nodes, приложений и GPU
  - Recording rules и evaluation interval
  - Pushgateway и ограничения lifecycle batch-задач

- **PromQL**
  - Instant vectors, range vectors и selectors
  - rate, increase и resets counters
  - Aggregation, joins и vector matching
  - histogram_quantile и агрегирование latency
  - Absent series, stale samples и корректные знаменатели

- **Dashboards**
  - Обзор сервиса, зависимости и детализация
  - SLO, error rate, saturation и capacity
  - Deployment annotations и сравнение версий
  - Variables, links и controlled dashboard provisioning
  - Антипаттерны средних значений и декоративных графиков

- **Масштабирование хранения**
  - TSDB, WAL, blocks и compaction
  - Remote write и remote read
  - HA pairs, deduplication и federation
  - Thanos, Mimir и VictoriaMetrics: архитектурные варианты
  - Retention, query cost и cardinality control

- **Эксплуатация**
  - Scrape failures и пропуски данных
  - Медленные queries и высокие расходы памяти
  - Rule evaluation failures и alert delays
  - Backup конфигурации и миграция dashboards
  - Проверка метрик synthetic traffic и контролируемым отказом

</details>

<a id="section-05"></a>

<details>
<summary>

### 5. Логи, distributed tracing и profiling

</summary>

- **Структурированные логи**
  - Timestamp, severity и event name
  - Service, version, tenant и request correlation
  - JSON logs и стабильная схема полей
  - Stack traces и многострочные события
  - Исключение credentials, PII и payload по умолчанию

- **Log pipelines**
  - Fluent Bit, Vector и OpenTelemetry Collector
  - Parsing, enrichment и redaction
  - Backpressure, buffering и доставка при перезапуске
  - Loki, OpenSearch/Elasticsearch и другие backends
  - Indexing, retention и стоимость high-cardinality fields

- **Distributed tracing**
  - Trace, span, parent и links
  - Сквозной context в HTTP, gRPC и очередях
  - Асинхронные задачи и длительные ML pipelines
  - Sampling и корректная интерпретация выборки
  - Jaeger, Tempo и trace search

- **Profiling**
  - CPU, wall time и allocation profiles
  - Continuous profiling и overhead
  - Flame graphs и off-CPU анализ
  - perf, eBPF и системные bottlenecks
  - GPU profiling и связь с приложением

- **Связывание сигналов**
  - Metrics-to-traces через exemplars
  - Logs-to-traces через trace ID
  - Deployment markers и изменения конфигурации
  - Сопоставление host, container, Pod и model version
  - Временная шкала пользовательской деградации

- **Диагностика telemetry**
  - Потерянный context и разорванные traces
  - Clock skew и отрицательные durations
  - Дублированные logs и неверный timestamp
  - Слишком дорогой sampling и profiling
  - Безопасный доступ к debug endpoints

</details>

<a id="section-06"></a>

<details>
<summary>

### 6. SLI, SLO, SLA и error budgets

</summary>

- **Модель надёжности**
  - Пользовательская потребность и критический путь
  - SLI как измеряемая доля успешных событий
  - SLO как целевое значение в окне
  - SLA как договор и последствия нарушения
  - Различие reliability target и внутреннего alert threshold

- **Проектирование SLI**
  - Availability, latency и correctness
  - Freshness, completeness и durability
  - Good events и valid events
  - Граница измерения и исключённые события
  - Black-box и server-side измерение

- **Вычисление SLO**
  - Request-based и window-based показатели
  - Rolling и calendar windows
  - Percentiles, thresholds и корректное агрегирование
  - Малый трафик и недостаток наблюдений
  - Зависимость результата от sampling и потери telemetry

- **Error budget**
  - Допустимая доля плохих событий
  - Budget remaining и burn rate
  - Multi-window, multi-burn-rate alerts
  - Политика релизов при исчерпании бюджета
  - Баланс feature work и reliability work

- **SLO для ML и данных**
  - Prediction availability и end-to-end latency
  - Data freshness и feature availability
  - Batch completion до бизнес-дедлайна
  - Качество предсказаний при задержанной разметке
  - Раздельные service SLO и model quality objectives

- **Управление SLO**
  - Выбор реалистичного первого target
  - Согласование с владельцами продукта
  - Dependency budgets и shared services
  - Пересмотр при изменении поведения пользователей
  - SLO review и действия по фактическому риску

</details>

<a id="section-07"></a>

<details>
<summary>

### 7. Alerting, on-call, runbooks и управление toil

</summary>

- **Дизайн alert**
  - Симптом пользователя и техническая причина
  - Page, ticket и информационное уведомление
  - Severity, urgency и правила маршрутизации
  - Actionable alert с владельцем и runbook
  - Проверка полезности на реальном сценарии

- **Alertmanager и доставка**
  - Grouping, deduplication и inhibition
  - Routing tree и escalation policies
  - Silence, maintenance windows и audit
  - HA и отказ внешнего notification provider
  - Тестовый alert и проверка доставки

- **Организация on-call**
  - Primary, secondary и incident escalation
  - Handover и контекст текущих изменений
  - Подготовка инженера к самостоятельному дежурству
  - Доступы, break-glass и экстренные инструкции
  - Устойчивая нагрузка и предотвращение выгорания

- **Alert quality**
  - Precision, recall и missed incidents
  - False positives и flapping
  - Alert storms и shared dependency failures
  - Настройка порогов на основе SLO
  - Регулярное удаление бесполезных alerts

- **Toil**
  - Повторяемая ручная работа и её измерение
  - Отличие toil от необходимой инженерной работы
  - Приоритизация автоматизации по затратам и риску
  - Self-service вместо повторяющихся запросов
  - Проверка эффекта автоматизации

- **Runbooks**
  - Симптом, проверка и безопасная первая реакция
  - Диагностические команды с контекстом и ограничениями
  - Decision points и условия эскалации
  - Проверка восстановления и отмена временных мер
  - Владение, актуальность и регулярная репетиция

</details>

<a id="section-08"></a>

<details>
<summary>

### 8. Инциденты, troubleshooting и postmortems

</summary>

- **Управление инцидентом**
  - Detection, triage и объявление severity
  - Incident commander, operations и communications
  - Единая временная шкала и журнал решений
  - Ограничение параллельных несогласованных изменений
  - Escalation и привлечение владельцев зависимостей

- **Системная диагностика**
  - Формулировка симптома и границ проблемы
  - Гипотезы, наблюдения и опровержения
  - Изменения перед началом деградации
  - Divide and conquer по слоям системы
  - Проверка эффекта каждого вмешательства

- **Восстановление сервиса**
  - Mitigation перед долгим поиском причины
  - Rollback, traffic shift и отключение feature
  - Load shedding и временное ограничение нагрузки
  - Защита state при аварийных действиях
  - Подтверждение recovery через пользовательские SLI

- **Коммуникация**
  - Регулярные status updates и известные факты
  - Работа с неопределённостью без ложных обещаний
  - Внутренние и внешние каналы информирования
  - Контакт с провайдером и evidence package
  - Передача инцидента между сменами

- **Postmortem**
  - Blameless анализ и проверяемая chronology
  - Trigger, contributing factors и systemic causes
  - Customer impact и фактическая длительность
  - Корректирующие действия с владельцами
  - Проверка исполнения и эффективности действий

- **ML-специфичные инциденты**
  - HTTP 200 при неверных предсказаниях
  - Повреждённый model artifact или feature snapshot
  - Резкое изменение input distribution
  - GPU hang, training stall и рост serving latency
  - Остановка retraining и карантин заражённых артефактов

</details>

<a id="section-09"></a>

<details>
<summary>

### 9. Производительность, нагрузочные тесты и capacity planning

</summary>

- **Ресурсная модель**
  - Latency, throughput, concurrency и utilization
  - Little's Law и оценка числа запросов в системе
  - Queueing delay и насыщение ресурсов
  - Amdahl's Law и ограничение масштабирования
  - Headroom, bursts и резерв на отказ

- **Методика измерения**
  - Baseline и репрезентативный workload
  - Open-loop и closed-loop load generation
  - Coordinated omission и смещённые результаты
  - Warmup, cold start и steady state
  - p50, p95, p99 и хвостовые задержки

- **Нагрузочные проверки**
  - Load, stress, spike и soak tests
  - k6, Locust, JMeter и выбор инструмента
  - Реалистичные payload sizes и request mix
  - Тестирование overload и graceful degradation
  - Критерии остановки и защита соседних систем

- **Поиск bottleneck**
  - CPU, RAM, disk, network и GPU saturation
  - Thread pools, connection pools и queues
  - Locks, serialization и лишние data copies
  - Критический путь и fan-out amplification
  - Изменение одной гипотезы и повторное измерение

- **Планирование capacity**
  - Forecast трафика, datasets и количества моделей
  - Capacity на пике и при потере зоны
  - Резервирование дефицитных GPU
  - Autoscaling delay и необходимый buffer
  - Capacity model с измеренными предположениями

- **Управление performance**
  - Performance budgets и release gates
  - Regression tracking по версиям
  - Сравнение cost/performance вариантов
  - Отделение оптимизации latency от throughput
  - Документирование результата и ограничений benchmark

</details>

<a id="section-10"></a>

<details>
<summary>

### 10. Disaster recovery, chaos engineering и resilience

</summary>

- **Цели восстановления**
  - Business impact analysis
  - RTO, RPO и максимальная допустимая потеря
  - Топология зависимостей и порядок восстановления
  - Классификация state по критичности
  - Recovery priority для online и batch workloads

- **Backup architecture**
  - Политика нескольких копий и независимых failure domains
  - Immutable backups и защита от ransomware
  - Application-consistent backup нескольких компонентов
  - Encryption keys и доступность credentials при disaster
  - Retention, restore time и стоимость хранения

- **Disaster recovery**
  - Cold, warm и hot standby
  - Backup–restore, pilot light и regional failover
  - DNS, routes и переключение клиентского трафика
  - Failback и reconciliation накопленных изменений
  - Проверка целостности после восстановления

- **Chaos engineering**
  - Steady-state hypothesis и ограниченный эксперимент
  - Fault injection на уровне process, node и network
  - Потеря зоны и недоступность dependency
  - Задержки, packet loss и throttling
  - Abort conditions и контролируемый blast radius

- **Game days**
  - Tabletop exercise и практический drill
  - Неизвестный заранее сценарий отказа
  - Проверка runbooks, доступа и коммуникации
  - Измерение фактических RTO/RPO
  - Исправление выявленных gaps и повторный drill

- **ML-платформа при disaster**
  - Registry, metadata, dataset и artifact consistency
  - Восстановление feature store и online state
  - Потеря checkpoints и возобновление обучения
  - Резервный inference без основного GPU-пула
  - Работа serving при недоступном training control plane

</details>

<a id="section-11"></a>

<details>
<summary>

### 11. Практические проекты и критерии готовности SRE

</summary>

- **SRE-контур сервиса**
  - Определить пользовательские SLI и SLO
  - Настроить dashboards и burn-rate alerts
  - Провести load и overload tests
  - Отработать incident и написать postmortem
  - Измерить recovery и подтвердить corrective action

- **Stateful recovery drill**
  - Сделать согласованный backup metadata и artifacts
  - Потерять исходный стенд в учебном окружении
  - Восстановить сервис в новом окружении
  - Проверить доступ, целостность и dependencies
  - Сопоставить фактические RTO/RPO с целевыми

- **Проверка самостоятельности SRE**
  - Обосновать SLI, target SLO и политику error budget
  - Найти причину деградации по нескольким видам telemetry
  - Организовать mitigation, коммуникацию и подтверждение recovery
  - Измерить фактические RTO/RPO в recovery drill
  - Устранить повторяющуюся причину сбоя и проверить эффект изменения

</details>

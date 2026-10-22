# MLOps & LLMOps Zero to Hero

**ML Lifecycle · GPU Infrastructure · Training · Serving · Model Monitoring · LLMOps · RAG · AgentOps**

## Навигация

| Раздел | Название |
| --- | --- |
| 1 | [Архитектура ML-систем, рабочие окружения и воспроизводимость](#section-01) |
| 2 | [Experiment tracking, model registry и metadata](#section-02) |
| 3 | [Training pipelines, continuous training и HPO workloads](#section-03) |
| 4 | [Feature platforms, feature stores и training-serving consistency](#section-04) |
| 5 | [Тестирование ML-систем и release gates](#section-05) |
| 6 | [GPU, ускорители и инфраструктура вычислений](#section-06) |
| 7 | [Распределённое обучение и управление GPU-кластерами](#section-07) |
| 8 | [Архитектуры inference и serving frameworks](#section-08) |
| 9 | [Производительность inference, доставка моделей и rollback](#section-09) |
| 10 | [Мониторинг моделей, drift, feedback и переобучение](#section-10) |
| 11 | [Model governance, privacy, безопасность и ML supply chain](#section-11) |
| 12 | [LLMOps: lifecycle, prompts, evaluation, safety и observability](#section-12) |
| 13 | [Self-hosted LLM serving и эффективность GPU](#section-13) |
| 14 | [RAG: retrieval, индексы и end-to-end эксплуатация](#section-14) |
| 15 | [AgentOps и эксплуатация систем с инструментами](#section-15) |
| 16 | [Managed ML, переносимость, edge и offline inference](#section-16) |
| 17 | [Многопользовательская ML-платформа: проектирование и эксплуатация](#section-17) |
| 18 | [System design, архитектурные разборы и экономика ML](#section-18) |
| 19 | [Сквозные проекты, портфолио и критерии senior MLOps](#section-19) |

## Содержание

<a id="section-01"></a>

<details>
<summary>

### 1. Архитектура ML-систем, рабочие окружения и воспроизводимость

</summary>

- **ML-система как продукт**
  - Бизнес-решение и роль предсказания
  - Потребитель модели и контракт результата
  - Online, batch, streaming и embedded inference
  - Стоимость ошибок и требования к объяснимости
  - Обоснование ML относительно простого baseline

- **Компоненты жизненного цикла**
  - Data readiness и подготовленный dataset
  - Experiment, training run и evaluation
  - Model registration и release approval
  - Deployment, monitoring и feedback
  - Retraining, retirement и удаление артефактов

- **Производственные контракты**
  - Input schema, output schema и model signature
  - Feature definitions и preprocessing version
  - Dataset snapshot и training configuration
  - Runtime dependencies и hardware requirements
  - Quality thresholds, SLO и fallback policy

- **Архитектурные границы**
  - Research environment и production runtime
  - Training plane и serving plane
  - Control plane и compute workers
  - Online state и offline artifacts
  - Общие и выделенные компоненты платформы

- **Технический долг ML**
  - Undeclared consumers и hidden dependencies
  - Training-serving skew и feedback loops
  - Data dependencies и configuration debt
  - Pipeline glue и невоспроизводимые notebooks
  - Entanglement нескольких моделей и shared features

- **Ownership и зрелость**
  - RACI для DS, ML, platform и data teams
  - Ручной процесс и automated training pipeline
  - CI/CD/CT как разные механизмы
  - Launch review и production acceptance
  - План эксплуатации до первого релиза

- **Research workspace**
  - Notebooks, IDE и remote development
  - Изолированные environments для разных проектов
  - GPU access, quotas и idle shutdown
  - Persistent user storage и ephemeral compute
  - Доступ только к разрешённым datasets

- **Воспроизводимое окружение**
  - Lockfile, container digest и системные зависимости
  - Driver, CUDA runtime и framework compatibility
  - CPU architecture и accelerator architecture
  - Environment manifest вместе с experiment
  - Проверка запуска в чистом окружении

- **Воспроизводимость запуска**
  - Git commit, parameters и dataset snapshot
  - Random seeds и границы их гарантий
  - Недетерминизм GPU и распределённого выполнения
  - Порядок входных данных и внешние зависимости
  - Уровни воспроизводимости и допустимые отклонения

- **От notebook к pipeline**
  - Чистый запуск без скрытого состояния
  - Явные inputs, outputs и parameters
  - Пакетирование подготовленного кода без обучения языку
  - Удаление интерактивных действий и локальных путей
  - Проверка orchestration на маленьком dataset

- **Совместная работа**
  - Общие базовые images и templates
  - Разделение user credentials и workload identity
  - Experiment naming и metadata conventions
  - Review изменений pipeline и environment
  - Сохранение результатов при выключении workspace

- **Эксплуатация workspace-платформы**
  - JupyterHub и многопользовательские notebooks
  - SSO, session lifecycle и tenant isolation
  - Resource profiles и GPU node pools
  - Upgrade notebook images и совместимость storage
  - Аудит доступа и очистка заброшенных окружений

</details>

<a id="section-02"></a>

<details>
<summary>

### 2. Experiment tracking, model registry и metadata

</summary>

- **Модель experiment tracking**
  - Experiment, run, nested run и trial
  - Parameters, metrics, artifacts и tags
  - Run status и обработка аварийного завершения
  - Сравнение результатов и корректность metadata
  - Связь run с dataset, кодом и environment

- **MLflow и альтернативы**
  - Tracking client, server и storage backends
  - MLflow, Weights & Biases и ClearML: выбор подхода
  - Autologging и явный контракт логирования
  - Offline runs и последующая синхронизация
  - Ограничения объёма metrics и artifacts

- **Model registry**
  - Registered model и immutable model version
  - Aliases, tags и promotion workflows
  - Signature, input example и dependency manifest
  - Доступность модели и её approval status
  - Различие registry state и фактического deployment

- **Release bundle**
  - Weights, preprocessing и postprocessing
  - Feature schema, tokenizer и vocabulary
  - Environment digest и hardware constraints
  - Evaluation report и model card
  - Bundle checksum, signature и provenance

- **Metadata graph**
  - Dataset–run–artifact–model–deployment lineage
  - Immutable evidence и изменяемые labels
  - ML metadata stores и поиск происхождения
  - Внешние эксперименты и imported models
  - Проверка полноты metadata перед promotion

- **Эксплуатация registry**
  - Database и artifact storage как отдельные компоненты
  - SSO, authorization и разграничение проектов
  - Backup, restore и миграции схемы
  - Retention без удаления deployed versions
  - Consistency checks и orphaned artifacts

</details>

<a id="section-03"></a>

<details>
<summary>

### 3. Training pipelines, continuous training и HPO workloads

</summary>

- **Контракт training pipeline**
  - Versioned pipeline definition и component interfaces
  - Dataset validation и readiness gates
  - Training, evaluation и registration stages
  - Явные artifacts между шагами
  - Cancellation и сохранение partial results

- **Оркестрация ML workflow**
  - Kubeflow Pipelines, Argo Workflows и managed pipelines
  - Airflow/Dagster для межсистемных зависимостей
  - Caching по входам, коду и окружению
  - Артефакты вместо больших inline payload
  - Выбор workflow engine по operational requirements

- **Continuous training**
  - Schedule, data event и quality trigger
  - Deduplication и debounce triggers
  - Data cutoff и воспроизводимый snapshot
  - Защита от бесконечного retraining loop
  - Отдельные решения retrain, register и deploy

- **Hyperparameter search как workload**
  - Trials, parallelism и resource profiles
  - Budget по времени, деньгам и GPU-hours
  - Optuna, Ray Tune и managed tuning
  - Early stopping, cancellation и cleanup
  - Метаданные trials и выбор утверждённого результата

- **Надёжность обучения**
  - Retry policy для transient infrastructure failures
  - Distinction code error, data error и resource failure
  - Checkpointing и resume с согласованным состоянием
  - Timeout, heartbeat и detection stalled jobs
  - Validation результата до публикации

- **Управление выпуском pipeline**
  - CI pipeline definition и компонентов
  - Smoke training на ограниченном dataset
  - Versioned parameters и schema migration
  - Promotion одинаковой реализации между окружениями
  - Аудит ручных overrides и повторных запусков

</details>

<a id="section-04"></a>

<details>
<summary>

### 4. Feature platforms, feature stores и training-serving consistency

</summary>

- **Назначение feature platform**
  - Online и offline consumers
  - Feature definitions и registry
  - Entity keys, timestamps и feature views
  - Feature store или простой versioned dataset
  - Граница ответственности MLOps и Data Engineering

- **Point-in-time correctness**
  - Event timestamp и available-at timestamp
  - Историческая доступность значения на момент предсказания
  - Late-arriving data и corrections
  - TTL и допустимая свежесть feature
  - Проверки предотвращения temporal leakage

- **Offline и online stores**
  - Historical retrieval и reproducible snapshots
  - Materialization и incremental publishing
  - Online lookup, batching и caching
  - Consistency expectations и lag между stores
  - Feast и managed feature stores

- **Training-serving consistency**
  - Одинаковые feature contracts и transformations
  - Проверка типов, defaults и missing values
  - Версионирование preprocessing и feature sets
  - Сравнение offline и online значений
  - Совместимый rollout features и моделей

- **Serving features**
  - Latency budget и fan-out lookups
  - Online freshness и update lag
  - Hot entities, skew и cache behavior
  - Fallback при missing или stale features
  - Изоляция tenant и row-level authorization

- **Эксплуатация feature platform**
  - SLO retrieval и materialization
  - Backfill исторических features
  - Schema evolution и consumer inventory
  - Backup online state и восстановление
  - Feature deprecation и удаление зависимостей

</details>

<a id="section-05"></a>

<details>
<summary>

### 5. Тестирование ML-систем и release gates

</summary>

- **Уровни проверок**
  - Code, data, features и model artifacts
  - Component, integration и end-to-end contracts
  - Малый deterministic smoke workload
  - Golden inputs и expected outputs с tolerances
  - Проверка ошибок, границ и fallback

- **Data и feature tests**
  - Input schema и допустимые значения
  - Dataset split metadata и отсутствие пересечений
  - Point-in-time invariants и leakage checks
  - Training-serving feature parity
  - Missing values, stale data и unseen categories

- **Проверка модели как артефакта**
  - Загрузка в чистой целевой среде
  - Model signature и output schema
  - Численная стабильность и invalid outputs
  - Совместимость preprocessing и weights
  - Security checks формата и provenance

- **Quality gates**
  - Evaluation dataset и versioned baseline
  - Требования по сегментам и критичным сценариям
  - Confidence intervals и ограничения малого sample
  - Quality–latency–cost tradeoff
  - Review исключений и документированное approval

- **Serving tests**
  - API contract и backward compatibility
  - Batch boundaries, concurrency и cancellation
  - Warmup, cold start и длительная нагрузка
  - Resource limits и поведение при OOM
  - Fallback при недоступном feature store

- **Проверка жизненного цикла**
  - Training–registry–deployment integration
  - Rollback совместимого release bundle
  - Отказ во время promotion и повтор операции
  - Retraining trigger и запрет плохого candidate
  - Сохранение evidence для каждого release

</details>

<a id="section-06"></a>

<details>
<summary>

### 6. GPU, ускорители и инфраструктура вычислений

</summary>

- **Устройство ускорителя**
  - GPU memory, compute units и memory bandwidth
  - Host memory, device memory и data transfer
  - PCIe, NVLink/NVSwitch и topology
  - NUMA locality и размещение CPU workloads
  - GPU, TPU и другие accelerators: operational различия

- **Software compatibility**
  - Kernel driver, runtime и toolkit
  - CUDA, cuDNN и зависимости framework
  - Driver compatibility и поддерживаемые combinations
  - NVIDIA Container Toolkit и device access
  - Firmware и проверка после обновления

- **GPU в Kubernetes**
  - Device plugin и extended resources
  - NVIDIA GPU Operator и node configuration
  - Node Feature Discovery и GPU labels
  - Resource requests, taints и dedicated pools
  - Startup validation и smoke workload на каждом узле

- **Совместное использование**
  - MIG и аппаратные partitions
  - Time-slicing и его ограничения изоляции
  - MPS и compatibility constraints
  - GPU memory oversubscription и contention
  - Выбор shared или dedicated GPU по SLO

- **Наблюдаемость и диагностика**
  - nvidia-smi, DCGM и exporter
  - Utilization, memory, temperature и power
  - ECC, Xid errors и degraded devices
  - Thermal throttling и power limits
  - GPU health checks и автоматический quarantine узла

- **Высокопроизводительная сеть**
  - InfiniBand, RoCE и RDMA
  - NIC–GPU affinity и GPUDirect
  - NCCL topology и collective communication
  - Network Operator и совместимость драйверов
  - Проверка bandwidth, latency и стабильности межузлового обмена

- **Альтернативные accelerators**
  - AMD ROCm и compatibility matrix
  - TPU topology и managed execution environments
  - AWS Trainium/Inferentia и Neuron runtime
  - CPU vector instructions и optimized inference libraries
  - Переносимость artifacts и проверка качества на другом hardware

</details>

<a id="section-07"></a>

<details>
<summary>

### 7. Распределённое обучение и управление GPU-кластерами

</summary>

- **Модель distributed workload**
  - Workers, ranks, world size и rendezvous
  - Data, tensor и pipeline parallelism как требования инфраструктуры
  - Synchronous и asynchronous coordination
  - Gang scheduling и совместный старт workers
  - Topology-aware placement и communication overhead

- **Kubernetes training workloads**
  - Kubeflow Trainer/Training Operator по выбранной версии
  - Job templates и набор worker roles
  - Kueue/Volcano для queues и admission
  - Приоритеты, quotas и fair sharing
  - Cleanup failed jobs и зависших ресурсов

- **Ray infrastructure**
  - Head node, workers и control services
  - KubeRay, RayCluster и RayJob
  - Logical resources и фактические resource limits
  - Autoscaling, object spilling и shared memory
  - Network isolation и защита Ray control plane

- **Slurm infrastructure**
  - Partitions, nodes, jobs и reservations
  - sbatch, srun, squeue и sacct
  - GRES для GPU и resource accounting
  - Fair-share, preemption и wall-time limits
  - Сопоставление Slurm jobs с ML metadata

- **Checkpoint и recovery**
  - Model, optimizer и execution state как единый checkpoint
  - Atomic publication и проверка завершённости записи
  - Sharded checkpoints и составной manifest
  - Resume после потери worker или spot node
  - Частота checkpoint: стоимость записи и потерянные вычисления
  - Изменение world size и ограничения framework

- **Диагностика обучения**
  - Training hang, straggler и desynchronization
  - NCCL timeouts и network failures
  - Data loading starvation и storage bottleneck
  - GPU memory OOM и fragmentation
  - Метрики time-to-train, throughput и полезных GPU-hours

- **Очереди и справедливое распределение**
  - Local queues, shared quotas и cluster admission
  - Borrowing capacity и правила возврата ресурсов
  - Reservations для production-critical workloads
  - Preemption, starvation и fairness между командами
  - Admission checks для доступности datasets и network topology
  - JobSet/LeaderWorkerSet как building blocks сложных jobs

</details>

<a id="section-08"></a>

<details>
<summary>

### 8. Архитектуры inference и serving frameworks

</summary>

- **Режимы inference**
  - Synchronous online prediction
  - Asynchronous request–job–result
  - Batch scoring с дедлайном публикации
  - Streaming inference и stateful consumers
  - Edge и embedded execution

- **Контракт prediction service**
  - Input/output schemas и model version
  - Preprocessing и postprocessing как часть release
  - Limits payload size и batch size
  - Idempotency, cancellation и request deadlines
  - Error codes и partial batch failures

- **Жизненный цикл model server**
  - Download, integrity check и load
  - Warmup и readiness после подготовки
  - Healthcheck процесса и работоспособность модели
  - Graceful shutdown и завершение in-flight requests
  - Cache eviction и unload моделей

- **Stateful зависимости**
  - Feature lookup и latency budget
  - Retrieval, tokenization и external API calls
  - Cache key с моделью и preprocessing version
  - Fallback при missing dependencies
  - Согласованность release bundle в нескольких replicas

- **Batch и async serving**
  - Queue admission и backpressure
  - Chunking, checkpoints и partial results
  - Deterministic result identifiers и дедупликация
  - Result storage, retention и авторизация
  - Retry-safe publication и completion manifests

- **Надёжность serving**
  - Model load failure и quarantine candidate
  - CPU/GPU fallback и допустимое качество
  - Isolation разных моделей и tenants
  - Multi-zone replicas и topology constraints
  - Serving при недоступном registry или control plane

- **Критерии выбора**
  - Тип модели и поддерживаемый runtime
  - Batch, real-time и generative workloads
  - Kubernetes integration и managed options
  - Multi-model serving и tenant isolation
  - Стоимость сопровождения и переносимость artifacts

- **KServe**
  - Control plane, data plane и custom resources
  - Predictive и generative serving по версии
  - Model storage и download identity
  - Autoscaling, routing и health management
  - Upgrade платформы без одновременной миграции всех моделей

- **NVIDIA Triton Inference Server**
  - Model repository и model configuration
  - Backends и поддерживаемые форматы
  - Dynamic batching и instance groups
  - Ensemble execution и dependency lifecycle
  - Метрики, tracing и performance analysis

- **Ray Serve и BentoML**
  - Deployment graph и зависимости компонентов
  - Replicas, concurrency и request queues
  - Runtime environments и model packaging
  - Autoscaling и GPU resource placement
  - Failure recovery и upgrade сервиса

- **Другие подходы**
  - Seldon Core и его ecosystem по версии
  - MLflow Serving для ограниченного контура
  - Собственный HTTP/gRPC wrapper вокруг runtime
  - Managed endpoints облачной ML-платформы
  - Поддерживаемый проект против устаревающей зависимости

- **Эксплуатационное сравнение**
  - Один model bundle в двух serving backends
  - Сравнение cold start, latency и throughput
  - Проверка rollout и rollback
  - Проверка OOM, node loss и dependency outage
  - ADR выбора с ограничениями и migration path

</details>

<a id="section-09"></a>

<details>
<summary>

### 9. Производительность inference, доставка моделей и rollback

</summary>

- **Модель производительности**
  - End-to-end latency и время model execution
  - CPU preprocessing и GPU compute
  - Host–device transfer и serialization
  - Queue delay и saturation
  - Throughput, tail latency и ресурсный headroom

- **Batching**
  - Static и dynamic batching
  - Max batch size и queue delay budget
  - Разные размеры inputs и padding overhead
  - Приоритеты online и batch requests
  - Проверка качества при изменении execution mode

- **Runtime optimization**
  - ONNX Runtime, TensorRT и runtime-specific engines
  - Compilation и hardware-specific artifacts
  - Precision changes и quantization validation
  - Версия optimization profile и target GPU
  - Корректность outputs после преобразования

- **Memory и model placement**
  - Model weights, activations и temporary buffers
  - Memory fragmentation и allocator behavior
  - Multi-model loading и cache eviction
  - GPU partitions и конкуренция workloads
  - CPU offload и цена дополнительной задержки

- **Autoscaling**
  - RPS, concurrency и queue depth
  - GPU utilization как неполный scaling signal
  - Model load time и pre-warmed replicas
  - Scale-to-zero и cold-start SLO
  - Coordination workload scaling и node provisioning

- **Performance engineering**
  - Benchmark по реальному input distribution
  - Batch size–latency–cost curves
  - Cold и warm measurements
  - Capacity при потере GPU node
  - Проверка regression budget перед release

- **Единица release**
  - Model, features, preprocessing и serving image
  - Immutable deployment manifest
  - Dataset и evaluation evidence
  - Policy checks и approvals
  - Проверка наличия всех артефактов перед rollout

- **Стратегии rollout**
  - Blue-green и rolling model replacement
  - Canary по трафику и пользовательскому cohort
  - Shadow inference без внешних эффектов
  - Champion/challenger и controlled comparison
  - Multi-armed experiments как отдельный управляемый контур

- **Online experimentation**
  - Unit of randomization и stable assignment
  - Exposure logging и experiment version
  - Sample ratio mismatch и потерянные события
  - Guardrail metrics и stop conditions
  - Связь product experiment и model deployment

- **Совместимость**
  - Новые features до включения новой модели
  - Dual support input/output contracts
  - Доступность старого preprocessing после rollout
  - Online state и несовместимые feature changes
  - Проверка совместного существования model versions

- **Решение о promotion**
  - Infrastructure health и model quality
  - Достаточность трафика и задержка labels
  - Автоматическое продолжение и human review
  - Защита от выбора по случайному улучшению
  - Аудит данных и метрик решения

- **Rollback**
  - Trigger по SLO, quality или security event
  - Возврат полного совместимого release bundle
  - Сохранение старых artifacts и feature versions
  - Проверка трафика, cache и replicas после возврата
  - Forward fix при необратимом изменении state

</details>

<a id="section-10"></a>

<details>
<summary>

### 10. Мониторинг моделей, drift, feedback и переобучение

</summary>

- **Уровни мониторинга**
  - Infrastructure health и serving SLI
  - Input/output contracts и feature quality
  - Prediction distribution и confidence signals
  - Model quality по ground truth
  - Business outcome и cost of errors

- **Drift**
  - Data drift, concept drift и label shift
  - Training baseline и recent production baseline
  - PSI, KS и другие сигналы с ограничениями
  - Сезонность, segmentation и multiple comparisons
  - Отличие drift signal от доказанного падения качества

- **Ground truth**
  - Delayed labels и окна созревания результата
  - Prediction–label join через устойчивый identifier
  - Пропущенная и selective разметка
  - Sampling bias и coverage labels
  - Backfill метрик после поступления результатов

- **Анализ качества**
  - Метрики, выбранные владельцем модели
  - Quality по сегментам, регионам и версиям
  - Rare events и малые выборки
  - Confidence intervals и practical significance
  - Сравнение baseline, candidate и business guardrails

- **Monitoring pipeline**
  - Prediction logging с privacy controls
  - Sampling и cost-aware collection
  - Batch evaluation и near-real-time checks
  - Evidently, WhyLabs и альтернативные инструменты
  - Версионирование monitoring configuration

- **Реакция на деградацию**
  - Alert, triage и подтверждение причины
  - Data incident против model incident
  - Fallback, traffic reduction и rollback
  - Retraining как проверяемая гипотеза
  - Закрытие инцидента после проверки качества

- **Источники обратной связи**
  - Явная пользовательская оценка
  - Бизнес-результат и delayed outcome
  - Экспертная разметка и adjudication
  - Поведенческие proxies и ограничения интерпретации
  - Prediction logging и consent requirements

- **Annotation operations**
  - Task queues и versioned labeling instructions
  - Access control для внутренних и внешних annotators
  - Inter-annotator agreement и gold tasks
  - Review спорных примеров и исправление labels
  - Provenance, dataset version и lineage разметки

- **Управление feedback loop**
  - Selective labels и selection bias
  - Влияние предсказания на последующие данные
  - Human-in-the-loop и ручные overrides
  - Delayed feedback и stale decisions
  - Разделение training feedback и независимого evaluation

- **Retraining policies**
  - Calendar, data volume и quality triggers
  - Minimum new data и cooldown period
  - Eligibility источников и quality gates
  - Budget, priority и resource allocation
  - Ограничение числа одновременных candidates

- **Проверка результата**
  - Сопоставимый baseline и актуальный evaluation snapshot
  - Проверки по критичным cohorts
  - Evidence полноты, качества и стоимости
  - Separate approval для register и deploy
  - Сохранение failed candidates для расследования

- **Управление жизненным циклом**
  - Обновление модели и прекращение retraining
  - Sunset policy для старых deployments
  - Удаление зависимостей features и datasets
  - Retention labels, artifacts и audit evidence
  - Измерение пользы retraining относительно затрат

</details>

<a id="section-11"></a>

<details>
<summary>

### 11. Model governance, privacy, безопасность и ML supply chain

</summary>

- **Инвентаризация моделей**
  - Model owner и business owner
  - Назначение, пользователи и запрещённые применения
  - Risk classification по последствиям ошибки
  - Внешняя модель и сторонние поставщики
  - Зависимости datasets, features и infrastructure

- **Документация release**
  - Model card и dataset documentation
  - Ограничения и known failure modes
  - Evaluation methodology и coverage
  - Human oversight и escalation path
  - Полная история approvals и deployments

- **Responsible AI operations**
  - Выбранные fairness criteria и проверяемые сегменты
  - Объяснения и доступность для потребителей
  - Safety tests по области применения
  - Обработка жалоб и оспаривание результата
  - Ответственный владелец решения о выпуске

- **Privacy lifecycle**
  - Purpose limitation и минимизация данных
  - Access controls для datasets и predictions
  - PII в artifacts, logs и traces
  - Retention, deletion и downstream impact
  - Проверка влияния удаления данных на model lifecycle

- **Audit и policy**
  - Evidence source–data–model–deployment
  - Separation of duties и approvals по риску
  - Policy as code и documented exceptions
  - Vendor due diligence и license compatibility
  - Сопоставление требований организации и применимых правил

- **Операционная реализация**
  - Risk register и план mitigations
  - Periodic review и revalidation
  - Отзыв модели и emergency disable
  - Доказательства воспроизводимости для аудита
  - Governance без превращения каждого изменения в ручной процесс

- **Threat model ML-системы**
  - Dataset, pipeline, registry и serving boundaries
  - Research users и production privileges
  - Внешние модели, packages и публичные repositories
  - Credentials training jobs и доступ к datasets
  - Impact compromise на соседние tenants

- **Безопасность model artifacts**
  - Небезопасная десериализация и executable formats
  - Pickle-подобные artifacts как недоверенный код
  - Safe tensor formats и ограничения формата
  - Контроль remote code при загрузке внешней модели
  - Integrity, signatures и verified provenance
  - Quarantine внешней модели перед загрузкой

- **Data и model integrity**
  - Poisoning и contamination как классы риска
  - Provenance источников и контроль публикации
  - Read-only dataset snapshots для training
  - Подпись training outputs доверенной identity
  - Контроль несанкционированной замены registry aliases

- **Безопасность inference**
  - Authentication и authorization на model endpoint
  - Input validation и resource exhaustion limits
  - Rate limits, quotas и abuse detection
  - Leakage через prediction logs и debug endpoints
  - Изоляция preprocessing и внешних adapters

- **Безопасность вычислительной платформы**
  - Sandbox для research и imported code
  - Network egress и защита metadata service
  - GPU sharing и отсутствие гарантированной security isolation
  - Доступ к Ray, notebooks и scheduler APIs
  - Секреты при checkpoint, crash и artifact upload

- **Реагирование**
  - Отзыв model release и блокировка serving
  - Поиск затронутых runs через lineage
  - Ротация identities и пересборка окружения
  - Проверка datasets и artifacts после компрометации
  - Recovery из последнего доверенного release

</details>

<a id="section-12"></a>

<details>
<summary>

### 12. LLMOps: lifecycle, prompts, evaluation, safety и observability

</summary>

- **Модель LLM-приложения**
  - Model endpoint, prompt и runtime configuration
  - Retrieval, tools и conversation state
  - Hosted API и self-hosted inference
  - Text, multimodal и structured outputs
  - Product quality и ограничения выбранного model family

- **Release bundle LLM-приложения**
  - Model version и provider identifier
  - Prompt template, system policy и parameters
  - Tokenizer и chat template для self-hosted модели
  - Retrieval configuration и tool schemas
  - Evaluation snapshot и compatibility manifest

- **Model gateway**
  - Единый API и provider adapters
  - Authentication, tenant quotas и budgets
  - Routing, fallback и regional availability
  - Retry policy с учётом повторного списания
  - Сравнимость outputs разных providers

- **Provider operations**
  - Rate limits и token-based quotas
  - Version pinning и model deprecation
  - Data retention и обработка запросов поставщиком
  - Private endpoints и региональная доступность
  - План migration при изменении API или качества

- **Fine-tuning как pipeline**
  - Подготовленный dataset и разрешение на использование
  - Job submission и resource budget
  - Checkpoint, adapter и base model lineage
  - Evaluation и compatibility gates
  - Регистрация результата без повторения теории обучения

- **Производственная эксплуатация**
  - Token accounting и cost attribution
  - Latency, availability и error taxonomy
  - Streaming cancellation и client disconnect
  - Контроль context size и output limits
  - Fallback mode при недоступности model provider

- **Управление prompts**
  - Prompt registry и immutable versions
  - Parameters, templates и input validation
  - Prompt–model–tool compatibility
  - Review, promotion и rollout
  - Rollback полного release bundle

- **Evaluation datasets**
  - Golden set и реальные пользовательские сценарии
  - Coverage языков, domains и редких ошибок
  - Dataset provenance и contamination checks
  - Synthetic examples и экспертная проверка
  - Версионирование и ограничение доступа к evaluation data

- **Методы оценки**
  - Exact checks для structured outputs
  - Task success и domain-specific rubrics
  - Human evaluation и согласованность annotators
  - LLM-as-judge, bias и calibration
  - Повторные прогоны и stochastic variance

- **Safety и защита**
  - Prompt injection и недоверенный retrieved content
  - Output validation и policy checks
  - Sensitive data leakage и redaction
  - Content safety по назначению продукта
  - Ограничения guardrails и остаточный риск

- **LLM observability**
  - Trace prompt, retrieval, generation и tools
  - Model version, prompt version и experiment ID
  - Latency, tokens, cost и error categories
  - Payload sampling с privacy controls
  - Langfuse, MLflow и OpenTelemetry integrations

- **Production feedback и gates**
  - Online quality sampling и human review
  - Guardrail failure rate и false positives
  - Quality–cost–latency regression checks
  - Canary releases и stop conditions
  - Incident review с воспроизводимым trace

</details>

<a id="section-13"></a>

<details>
<summary>

### 13. Self-hosted LLM serving и эффективность GPU

</summary>

- **Runtime и совместимость**
  - vLLM, SGLang и TensorRT-LLM как варианты
  - Supported architectures и model format
  - Tokenizer, chat template и generation settings
  - Driver, runtime и GPU compatibility
  - Проверка запуска конкретной модели на целевом hardware

- **Память и scheduling**
  - Model weights и KV cache
  - Context length и output token budget
  - Continuous batching и request admission
  - Paged KV management и fragmentation
  - Ограничение одновременных длинных запросов

- **Оптимизация**
  - Prefix caching и cache invalidation
  - Quantized artifacts и проверка качества
  - Speculative decoding и operational constraints
  - CPU offload и дополнительные transfers
  - Compilation и kernel warmup

- **Масштабирование**
  - Tensor/pipeline/data parallel deployment requirements
  - Multi-node topology и communication bandwidth
  - Prefill/decode disaggregation
  - Shared cache transfer и цена сети
  - Autoscaling по очереди и token throughput

- **Измерения**
  - Time to first token
  - Inter-token latency и time per output token
  - End-to-end latency по длине запросов
  - Input/output tokens per second
  - Goodput при заданных latency и quality objectives

- **Надёжность и изоляция**
  - OOM, worker crash и потеря одного shard
  - Graceful drain длительных generations
  - Tenant boundaries для prefix caches
  - Cancellation, orphaned requests и resource cleanup
  - Capacity при reload модели и потере GPU

</details>

<a id="section-14"></a>

<details>
<summary>

### 14. RAG: retrieval, индексы и end-to-end эксплуатация

</summary>

- **Контракт RAG-системы**
  - Корпус, индекс, retrieval и generation
  - Corpus version и document provenance
  - Embedding model version и index compatibility
  - Chunking configuration как versioned artifact
  - Граница ingestion pipeline и retrieval platform

- **Жизненный цикл индекса**
  - Build, validate, publish и serve
  - Incremental updates и delete propagation
  - Blue-green index и atomic alias switch
  - Re-embedding при смене модели
  - Rollback index и согласованный corpus snapshot

- **Retrieval infrastructure**
  - Vector storage, lexical search и hybrid retrieval
  - Qdrant, Milvus, pgvector и search engines
  - Shards, replicas и index memory
  - Tenant filtering и authorization-aware retrieval
  - Backup, restore и восстановление индекса из источника

- **Производительность**
  - Retrieval latency и candidate count
  - Search parameters и recall–latency tradeoff
  - Reranking cost и отдельный resource pool
  - Caching с учётом пользователя и прав доступа
  - Capacity при росте корпуса и update rate

- **Freshness и correctness**
  - Document readiness и publication lag
  - Stale index и deleted documents
  - Проверка citation consistency
  - ACL changes и немедленное ограничение доступа
  - Reconciliation источника и опубликованного индекса

- **Evaluation и release**
  - Versioned query set и expected evidence
  - Retrieval recall и ranking quality
  - End-to-end answer quality
  - Проверка доступа и отказов dependencies
  - Совместный rollout prompt, retrieval config и index

</details>

<a id="section-15"></a>

<details>
<summary>

### 15. AgentOps и эксплуатация систем с инструментами

</summary>

- **Модель агентного workflow**
  - Planner, model, tools и execution state
  - Детерминированный workflow и autonomous loop
  - State machine и явные terminal states
  - Session, conversation и task identity
  - Версионирование graph, prompts и tool contracts

- **Контракты инструментов**
  - Typed inputs, outputs и schema validation
  - Timeout, retry и cancellation
  - Idempotency keys для внешних эффектов
  - Read-only и mutating operations
  - MCP servers и protocol version compatibility

- **Полномочия и безопасность**
  - User identity и delegated workload identity
  - Least privilege и resource-scoped credentials
  - Подтверждение действий по заранее заданной политике
  - Sandbox для code execution и file access
  - Защита от prompt injection через tool outputs

- **Ограничение ресурсов**
  - Максимум steps, tokens, времени и стоимости
  - Tool concurrency и bounded fan-out
  - Loop detection и повторяющиеся ошибки
  - Circuit breakers внешних tools
  - Budget isolation по tenant и task

- **Надёжность исполнения**
  - Durable execution и checkpoints workflow
  - Resume после process crash
  - Повторная доставка events без повторного внешнего эффекта
  - Compensation и частично выполненный план
  - Human handoff и безопасное завершение task

- **Проверка и наблюдаемость**
  - Task success и correctness внешних эффектов
  - Тестовые tools и безопасные replay environments
  - Сквозные traces решений и вызовов
  - Версионирование evidence без раскрытия secrets
  - Rollback workflow и отзыв опасного tool

</details>

<a id="section-16"></a>

<details>
<summary>

### 16. Managed ML, переносимость, edge и offline inference

</summary>

- **Выбор managed подхода**
  - Область ответственности провайдера
  - Training, registry, features и endpoints
  - Ограничения regional availability и quotas
  - Private networking и enterprise identities
  - Vendor lock-in и exit requirements

- **AWS ML-контур**
  - SageMaker AI training и processing jobs
  - Pipelines, experiments и model registry
  - Real-time, asynchronous и batch inference
  - Security, encryption и VPC integration
  - Статус поддержки monitoring-компонентов перед выбором

- **Google Cloud ML-контур**
  - Gemini Enterprise Agent Platform и Vertex AI Inference
  - Managed training и pipeline orchestration
  - Model registry и inference endpoints
  - Experiment metadata и model monitoring
  - IAM, private connectivity и regional constraints

- **Azure ML-контур**
  - Workspaces, compute и managed identities
  - Jobs, components и pipelines
  - Environments, data assets и model registry
  - Managed online и batch endpoints
  - Monitoring, network isolation и deployment policies

- **Переносимый контракт**
  - OCI images и model bundle
  - Dataset manifests и external artifact storage
  - Pipeline inputs/outputs без provider-specific leakage
  - Экспорт metadata, evaluation и lineage
  - Независимые serving APIs и observability

- **Миграция и проверка**
  - Inventory зависимостей и provider capabilities
  - Parallel runs и comparison evidence
  - Data transfer, encryption keys и egress cost
  - Cutover, rollback и DNS/client compatibility
  - Удаление ресурсов и отзыв прежних identities

- **Условия применения**
  - On-device latency и отсутствие постоянной сети
  - Private data и локальная обработка
  - Mobile, embedded и industrial environments
  - Ограниченные power, memory и storage
  - Отличие fleet management от облачного serving

- **Упаковка**
  - Целевая architecture и runtime compatibility
  - Optimized model artifacts и quality validation
  - Signed bundle с preprocessing и metadata
  - Model storage budget и несколько release slots
  - Проверка hardware capability перед установкой

- **Доставка в fleet**
  - Device identity и secure channel
  - OTA updates и staged rollout
  - Resume interrupted download и integrity checks
  - Rollback после startup или health failure
  - Revocation и недопустимые model versions

- **Offline execution**
  - Локальный cache inputs и результатов
  - Backpressure при ограниченном storage
  - Конфликты и синхронизация после reconnect
  - Временные метки и clock drift
  - Graceful degradation при недоступном accelerator

- **Fleet observability**
  - Device cohorts и version inventory
  - Отложенная отправка telemetry
  - Sampling и bandwidth budgets
  - Drift по устройствам и условиям эксплуатации
  - Privacy и минимизация передаваемых payload

- **Эксплуатационные компромиссы**
  - Устройство как отдельный failure domain
  - Невозможность мгновенного глобального rollback
  - Remote diagnostics и безопасный support access
  - Vendor runtime lifecycle и аппаратные ограничения
  - Критерии выбора edge или cloud inference

</details>

<a id="section-17"></a>

<details>
<summary>

### 17. Многопользовательская ML-платформа: проектирование и эксплуатация

</summary>

- **Платформенные домены**
  - Workspaces и project lifecycle
  - Training, tuning и batch execution
  - Registry, artifacts и metadata
  - Feature access и model serving
  - Identity, governance и cost management

- **Control plane**
  - Public platform API и resource model
  - Async operations и durable state machine
  - Idempotency и reconciliation
  - Provider adapters и versioned contracts
  - Event audit и восстановление незавершённых операций

- **Tenant isolation**
  - Проект, команда и организационная граница
  - Shared clusters, dedicated clusters и node pools
  - Storage, network и identity isolation
  - Quotas, priorities и fair sharing
  - Ограничение noisy neighbour без голодания других команд

- **Self-service ML**
  - Project templates и golden paths
  - Resource profiles CPU/GPU
  - Одобренные base images и pipeline components
  - Стандартный model release contract
  - Документация и понятная диагностика для DS

- **Service reliability**
  - SLO control plane и data plane
  - Работа inference при отказе management services
  - Backup metadata и artifacts
  - Multi-zone design и disaster recovery
  - Capacity, quotas и дефицит accelerator resources

- **Управление продуктом**
  - Personas и реальные потребности команд
  - Adoption, time-to-first-run и time-to-production
  - Cost per active project и support load
  - Roadmap, compatibility и deprecation
  - Build/buy decisions с учётом размера организации

- **Operational readiness**
  - Service owners и зависимые команды
  - Inventory endpoints, jobs и model versions
  - SLO, dashboards, alerts и runbooks
  - Backup/restore evidence и emergency access
  - Capacity и согласованные support boundaries

- **Изменение платформы**
  - Upgrade registry, orchestrator и metadata schemas
  - Совместимость client SDK и server API
  - Обновление GPU driver/runtime matrix
  - Canary projects и staged rollout
  - Legacy workloads и migration deadlines

- **Массовые операции**
  - Пересборка образов после security advisory
  - Перерегистрация и переподпись artifacts
  - Перенос model storage и credentials
  - Миграция serving runtime и node pools
  - Изменение feature contracts для многих consumers

- **Диагностика сквозного сбоя**
  - Code–data–feature–model–runtime correlation
  - Registry доступен, но модель не загружается
  - Training не стартует при свободных GPU
  - Serving работает, но quality деградирует
  - Незаметный рост затрат без роста нагрузки

- **Управление состоянием**
  - Stuck runs, orphaned jobs и dangling artifacts
  - Reconciliation metadata и фактических deployments
  - Quarantine повреждённых release bundles
  - Retention с учётом юридических и продуктовых требований
  - Очистка ресурсов без разрушения lineage

- **Continuous improvement**
  - Postmortem themes и повторяющиеся причины
  - Toil backlog и self-service automation
  - Capacity forecasting и cost reviews
  - Reliability roadmap и debt retirement
  - Проверка эффекта изменения по пользовательским результатам

</details>

<a id="section-18"></a>

<details>
<summary>

### 18. System design, архитектурные разборы и экономика ML

</summary>

- **Метод проектирования**
  - Функциональные требования и критичные сценарии
  - SLO, quality objectives и ограничения данных
  - Оценка traffic, storage и compute
  - State, contracts и failure domains
  - Tradeoffs, ADR и план эволюции

- **Антифрод в real time**
  - Жёсткий latency budget и online features
  - Доступность feature store и fallback
  - Delayed outcomes и selective labels
  - Canary модели без неконтролируемого риска
  - Audit trail принятого решения

- **Рекомендательный сервис**
  - Batch preparation и online ranking boundaries
  - Candidate retrieval и несколько serving stages
  - Cache freshness и персональные данные
  - Online experiments и feedback loops
  - Capacity при hot users и peak traffic

- **Computer vision workloads**
  - Большие binary inputs и object storage
  - CPU preprocessing и GPU inference
  - Async processing и completion deadlines
  - Multi-model routing и memory capacity
  - Privacy, retention и dataset provenance

- **Корпоративный RAG и agents**
  - Tenant-aware retrieval и права на документы
  - Model gateway и provider fallback
  - Evaluation по domain-specific сценариям
  - Tool permissions и внешние эффекты
  - Token budgets, trace retention и cost allocation

- **Большая training-платформа**
  - Очереди GPU и fair sharing
  - Multi-node placement и network topology
  - Checkpoint/recovery на spot capacity
  - Metadata lineage и reproducible release
  - Региональный отказ и перенос workloads

- **Unit economics**
  - Стоимость тысячи предсказаний
  - Стоимость training run и успешного эксперимента
  - Стоимость миллиона токенов с учётом качества
  - Стоимость pipeline run и соблюдения freshness
  - Cost-to-serve при разных SLO

- **GPU economics**
  - Загрузка GPU, memory и compute как разные показатели
  - Queue time и полезное время эксперимента
  - MIG, time-slicing и совместное использование
  - Резерв capacity для критичных inference workloads
  - Сравнение собственного кластера и managed endpoints

</details>

<a id="section-19"></a>

<details>
<summary>

### 19. Сквозные проекты, портфолио и критерии senior MLOps

</summary>

- **Полный жизненный цикл готовой модели**
  - Принять подготовленную модель и versioned dataset
  - Запустить tracked training/evaluation pipeline
  - Зарегистрировать подписанный release bundle
  - Выполнить canary deployment и rollback
  - Подтвердить service SLO и model quality monitoring

- **Feature platform и retraining**
  - Развернуть offline/online feature access
  - Проверить point-in-time correctness и parity
  - Настроить delayed label collection
  - Запустить retraining по контролируемому trigger
  - Заблокировать candidate, не прошедший quality gates

- **GPU training platform**
  - Организовать очереди и resource quotas
  - Запустить distributed job и собрать lineage
  - Восстановить job из checkpoint после потери worker
  - Измерить throughput и полезные GPU-hours
  - Сравнить dedicated и spot capacity по стоимости

- **LLM/RAG production-контур**
  - Развернуть gateway и выбранный inference backend
  - Версионировать prompt, model и index
  - Добавить evaluation и privacy-aware tracing
  - Проверить token budgets, access boundaries и fallback
  - Измерить quality–latency–cost tradeoff

- **Многопользовательская ML-платформа**
  - Создать self-service project template
  - Разделить identities, network, storage и quotas
  - Предоставить стандартные training и serving interfaces
  - Настроить platform SLO и cost attribution
  - Проверить tenant isolation и отказ control plane

- **Production migration и disaster drill**
  - Перенести registry или serving runtime
  - Сохранить lineage и compatibility releases
  - Провести parallel validation и controlled cutover
  - Восстановить ML-контур после потери окружения
  - Подготовить ADR, runbooks и измеримые результаты

- **Системная компетентность**
  - Объяснить путь запроса от DNS до model runtime
  - Найти bottleneck по evidence разных слоёв
  - Различить проблему кода, данных, инфраструктуры и модели
  - Спроектировать ресурсные ограничения и failure isolation
  - Обосновать архитектурный выбор и альтернативы

- **Доставка и воспроизводимость**
  - Воссоздать окружение из versioned declarations
  - Проследить prediction до model, run и dataset
  - Доставить изменение без повторной сборки артефакта
  - Доказать совместимость и работоспособность rollback
  - Проверить происхождение и целостность release bundle

- **Надёжность и безопасность**
  - Определить SLO и actionable alerting
  - Самостоятельно вести incident до recovery
  - Восстановить state из проверенного backup
  - Обеспечить tenant isolation и минимальные полномочия
  - Устранить повторяющийся риск через системное изменение

- **Эксплуатация ML**
  - Организовать training, registry и serving lifecycle
  - Проверить training-serving consistency
  - Разделить drift, quality degradation и data incident
  - Учитывать delayed labels и feedback bias
  - Контролировать retraining и выпуск кандидата

- **Масштаб, стоимость и продукт**
  - Рассчитать capacity с запасом на отказ
  - Измерить cost per prediction или training run
  - Оптимизировать стоимость при сохранении целей качества
  - Спроектировать self-service с понятными guardrails
  - Согласовать roadmap между инженерными и продуктовыми командами

- **Доказательства уровня**
  - Работающие проекты с воспроизводимым запуском
  - ADR с рассмотренными компромиссами
  - Метрики до/после и честные ограничения измерения
  - Runbooks, postmortems и результаты recovery drills
  - Опыт самостоятельных решений и сопровождения пользователей

</details>

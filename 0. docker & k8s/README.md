# Docker & Kubernetes Zero to Hero

**OCI · Docker · BuildKit · Compose · Kubernetes · Scheduling · Networking · Storage · GitOps**

## Навигация

| Раздел | Название |
| --- | --- |
| 1 | [Контейнеры, Linux isolation, OCI и Docker runtime](#section-01) |
| 2 | [Dockerfile, BuildKit, registry и Docker Compose](#section-02) |
| 3 | [Kubernetes: архитектура, API, reconciliation и workloads](#section-03) |
| 4 | [Kubernetes: ресурсы, scheduling и autoscaling](#section-04) |
| 5 | [Kubernetes: сеть, Gateway API и service mesh](#section-05) |
| 6 | [Kubernetes: хранение и stateful workloads](#section-06) |
| 7 | [Kubernetes: безопасность и многопользовательская среда](#section-07) |
| 8 | [Kubernetes: эксплуатация, обновления и восстановление](#section-08) |
| 9 | [Helm, Kustomize, GitOps и Kubernetes operators](#section-09) |
| 10 | [Практические проекты и критерии готовности](#section-10) |

## Содержание

<a id="section-01"></a>

<details>
<summary>

### 1. Контейнеры, Linux isolation, OCI и Docker runtime

</summary>

- **Модель контейнера**
  - Контейнер как изолированный процесс
  - Image, container и writable layer
  - Namespaces: pid, net, mount, user и uts
  - cgroups и фактические ресурсные ограничения
  - Контейнер, VM и sandbox runtime

- **Экосистема OCI**
  - OCI Image Specification и Runtime Specification
  - Docker Engine, containerd и CRI-O
  - runc и альтернативные runtimes
  - CRI как контракт Kubernetes с runtime
  - Совместимость образа и Linux kernel хоста

- **Жизненный цикл Docker**
  - run, create, start, stop и rm
  - exec, attach, logs и inspect
  - Restart policies и корректная обработка сигналов
  - PID 1, init-процесс и дочерние процессы
  - Exit codes, healthchecks и причины завершения

- **Данные и сеть**
  - Bind mounts, named volumes и tmpfs
  - UID/GID и права на смонтированные каталоги
  - Bridge, host и user-defined networks
  - Port publishing, DNS и межконтейнерный доступ
  - Сохранение состояния при пересоздании контейнера

- **Ресурсы и безопасность**
  - Memory limits, CPU limits и throttling
  - Capabilities, seccomp и read-only filesystem
  - Non-root user и rootless containers
  - Docker socket как привилегированный доступ
  - Devices, GPU access и ограничения изоляции

- **Диагностика runtime**
  - OOM, permission denied и exec format error
  - DNS, ports и недоступный upstream
  - Disk usage, overlay filesystem и cleanup
  - docker stats, events и system df
  - Отличие неисправности процесса от неисправности хоста

</details>

<a id="section-02"></a>

<details>
<summary>

### 2. Dockerfile, BuildKit, registry и Docker Compose

</summary>

- **Устройство образа**
  - Layers, manifests, config и content digest
  - Tags и изменяемые ссылки
  - Multi-platform manifest и architecture
  - Image history и происхождение содержимого
  - Размер compressed image и размер после распаковки

- **Dockerfile**
  - FROM, RUN, COPY, WORKDIR и USER
  - CMD, ENTRYPOINT и exec form
  - ARG, ENV и build-time/runtime конфигурация
  - .dockerignore и минимальный build context
  - HEALTHCHECK, STOPSIGNAL и контракт запуска

- **Качественная сборка**
  - Multi-stage builds и минимальный runtime image
  - Порядок layers и cache reuse
  - BuildKit cache mounts и external cache
  - Secret mounts и SSH forwarding при сборке
  - Cross-compilation, emulation и native builders

- **Зависимости и совместимость**
  - Pinning base image по digest
  - Обновление base images и security rebuilds
  - glibc, musl и native library compatibility
  - CUDA runtime image и драйвер хоста
  - Отдельные образы training, serving и development

- **Registry**
  - Authentication, namespaces и access policies
  - Immutable tags и promotion по digest
  - Replication, pull-through cache и rate limits
  - Retention, lifecycle и garbage collection
  - Приватный registry и offline зеркалирование

- **Проверка цепочки поставки**
  - SBOM и vulnerability scanning
  - Image signing и provenance attestations
  - Проверка подписи перед запуском
  - Запрет secrets и лишних инструментов внутри образа
  - Smoke test image в чистом окружении

- **Описание приложения**
  - Services, networks, volumes и profiles
  - Переменные, interpolation и env files
  - Override files и отдельные окружения
  - Healthchecks и условия старта зависимостей
  - Ограничения depends_on относительно готовности приложения

- **Локальная платформа**
  - API, worker, broker и database
  - MLflow, object storage и metadata backend
  - Prometheus, Grafana и локальный telemetry stack
  - Feature server и online store
  - Заменяемые adapters для локальных и облачных сервисов

- **Управление жизненным циклом**
  - up, down, restart, logs и exec
  - Сохранение и удаление named volumes
  - Пересборка отдельного сервиса
  - Миграции перед запуском приложения
  - Предсказуемая очистка стенда после CI

- **Доступ и безопасность**
  - Внутренняя сеть и минимальное число открытых портов
  - Test credentials и secret files
  - Non-root execution и permissions volumes
  - Resource limits и конкуренция за GPU
  - Разделение учебных и реальных datasets

- **Диагностика и тестирование**
  - Проверка service discovery и readiness
  - Моделирование задержек и отказов зависимостей
  - Восстановление stateful-сервиса из backup
  - Проверка повторного запуска без потери состояния
  - Интеграционные тесты на ephemeral стенде

- **Границы применения**
  - Один хост и область отказа
  - Отсутствие полноценного кластерного scheduler
  - Простой production-сценарий и его ограничения
  - Миграция контрактов в Kubernetes
  - Сохранение простого стенда для разработчиков

</details>

<a id="section-03"></a>

<details>
<summary>

### 3. Kubernetes: архитектура, API, reconciliation и workloads

</summary>

- **Компоненты кластера**
  - API server, etcd, scheduler и controllers
  - kubelet, container runtime и node agents
  - Cluster networking и реализация Service
  - Control plane и worker nodes
  - Managed и self-managed clusters

- **API и объекты**
  - apiVersion, kind, metadata, spec и status
  - Names, UIDs, labels и annotations
  - Namespaces и границы их изоляции
  - Object references и ownerReferences
  - API discovery и документация схемы

- **Декларативное управление**
  - Desired state и reconciliation loop
  - Controllers и eventual convergence
  - Imperative commands и declarative manifests
  - Server-side apply и field ownership
  - Conflicts, patches и concurrent updates

- **Жизненный цикл объекта**
  - ResourceVersion и optimistic concurrency
  - Watch, relist и informer pattern
  - Finalizers и удаление зависимых ресурсов
  - Garbage collection и orphaned objects
  - Conditions, events и наблюдаемое состояние

- **Первое окружение**
  - kind, minikube и k3d
  - kubeconfig, contexts и namespaces
  - kubectl get, describe, explain и logs
  - apply, diff, rollout и wait
  - Проверка маршрута от клиента до Pod

- **Версии и расширяемость**
  - API groups и versioned schemas
  - Feature gates и maturity levels
  - Deprecations, removals и version skew
  - CRD, custom resources и aggregated API
  - Совместимость add-ons с выбранной версией кластера

- **Pods**
  - Pod как единица scheduling
  - Containers внутри Pod и общий сетевой контекст
  - Init containers и sidecar patterns
  - Pod phases, conditions и restart policy
  - Ephemeral containers для диагностики

- **Контроллеры workloads**
  - Deployment и ReplicaSet
  - StatefulSet и стабильная идентичность replicas
  - DaemonSet и node-level services
  - Job и batch execution
  - CronJob, concurrency policy и пропущенные запуски

- **Конфигурация приложения**
  - ConfigMap, Secret и environment variables
  - Mounted configuration и обновление содержимого
  - Immutable configuration и restart при изменении
  - Downward API и projected volumes
  - Secret encoding, encryption at rest и external secrets

- **Готовность и завершение**
  - startupProbe, readinessProbe и livenessProbe
  - Ошибки от агрессивных probes
  - preStop и terminationGracePeriodSeconds
  - Draining соединений и завершение фоновых задач
  - Учет длительной загрузки модели и прогрева

- **Обновление workload**
  - RollingUpdate и параметры maxSurge/maxUnavailable
  - Readiness gates и rollout status
  - Откат Deployment и ограничения отката state
  - PodDisruptionBudget для добровольных disruption
  - Совместимость нескольких версий приложения одновременно

- **Batch и ML-задачи**
  - Retries Job и backoffLimit
  - Deadline, cancellation и TTL очистки
  - Повторяемый запуск и идемпотентные внешние эффекты
  - Checkpoint перед вытеснением
  - Отличие успешного Pod от корректного результата задачи

</details>

<a id="section-04"></a>

<details>
<summary>

### 4. Kubernetes: ресурсы, scheduling и autoscaling

</summary>

- **Ресурсная модель**
  - CPU requests и limits
  - Memory requests, limits и OOM
  - QoS classes и eviction priorities
  - Ephemeral storage и node pressure
  - ResourceQuota, LimitRange и namespace budgets

- **Планирование**
  - Filtering, scoring и binding
  - Node selectors и node affinity
  - Pod affinity и anti-affinity
  - Taints, tolerations и dedicated node pools
  - Topology spread и распределение по зонам

- **Приоритеты и вытеснение**
  - PriorityClass и preemption
  - Voluntary и involuntary disruptions
  - Node-pressure eviction и kubelet thresholds
  - PDB и ограничения его защиты
  - Starvation и справедливость между очередями

- **Autoscaling workloads**
  - HPA и выбор target metric
  - Custom/external metrics и adapter
  - VPA, рекомендации и изменение ресурсов
  - KEDA и event-driven scaling
  - Stabilization windows и предотвращение oscillation

- **Autoscaling узлов**
  - Cluster Autoscaler и provisioning constraints
  - Karpenter и динамический выбор capacity
  - Consolidation, disruption budgets и scale-down
  - Spot nodes, interruptions и запас capacity
  - Недоступность GPU-типа и quota exhaustion

- **Специализированные задачи**
  - Extended resources и device plugins
  - Dynamic Resource Allocation с проверкой поддержки версии
  - NUMA, topology manager и CPU manager
  - Gang scheduling и admission очередей
  - Kueue, Volcano и выбор batch scheduling подхода

</details>

<a id="section-05"></a>

<details>
<summary>

### 5. Kubernetes: сеть, Gateway API и service mesh

</summary>

- **Сетевая модель**
  - Pod IP и межузловая связность
  - CNI и маршрутизация Pod traffic
  - Overlay, routing и eBPF data plane
  - kube-proxy или альтернативная реализация Service
  - MTU и диагностика encapsulation

- **Service discovery**
  - ClusterIP, NodePort и LoadBalancer
  - Headless Services и stateful discovery
  - EndpointSlices и readiness endpoints
  - CoreDNS, search domains и ndots
  - NodeLocal DNS cache и DNS bottlenecks

- **Входящий трафик**
  - Ingress resources и выбранный controller
  - Gateway API: GatewayClass, Gateway и routes
  - TLS termination и certificate automation
  - L7 routing, weights и backend policies
  - Проверка жизненного цикла и поддержки controller

- **Изоляция трафика**
  - NetworkPolicy и поддержка выбранным CNI
  - Ingress/egress policies и default deny
  - Доступ к DNS, metadata и внешним API
  - Namespace boundaries и tenant traffic
  - Проверка политики реальными разрешёнными и запрещёнными запросами

- **Service mesh**
  - Sidecar и альтернативные data plane модели
  - mTLS, identity и authorization policies
  - Traffic splitting, retries и timeout policies
  - Telemetry, overhead и сложность эксплуатации
  - Условия, при которых mesh оправдан

- **Диагностика**
  - Pod-to-Pod, Pod-to-Service и внешние соединения
  - DNS resolution и service endpoints
  - Conntrack exhaustion и SNAT port exhaustion
  - Packet capture и CNI observability
  - Network policy, TLS и application errors по отдельности

</details>

<a id="section-06"></a>

<details>
<summary>

### 6. Kubernetes: хранение и stateful workloads

</summary>

- **Storage abstractions**
  - Volume, PersistentVolume и PersistentVolumeClaim
  - StorageClass и dynamic provisioning
  - CSI drivers и возможности storage backend
  - Access modes и реальные гарантии backend
  - Binding mode и topology-aware provisioning

- **Жизненный цикл данных**
  - Reclaim policy и удаление claims
  - Volume expansion и файловая система
  - Snapshots, clones и application consistency
  - Backup volumes и external state
  - Финализация удаления и зависшие mounts

- **Stateful workloads**
  - StatefulSet, ordinals и persistent identity
  - Headless Service и порядок запуска
  - Rolling updates и partitioned rollout
  - Leader election и корректное failover приложения
  - Почему replicas не заменяют replication приложения

- **Storage для ML**
  - Dataset mounts и object storage clients
  - Shared file storage и parallel read
  - Model cache на локальном NVMe
  - Checkpoints и пропускная способность записи
  - Object FUSE: удобство и ограничения semantics

- **Backup и восстановление**
  - Velero и интеграция с storage snapshots
  - Kubernetes objects и application data
  - Порядок восстановления зависимостей
  - Cross-cluster restore и проверка credentials
  - Проверка dataset/model registry consistency

- **Диагностика**
  - Pending PVC и неподходящий StorageClass
  - Attach/detach failures и multi-attach errors
  - Permission denied, fsGroup и mount options
  - Disk pressure, inode exhaustion и latency
  - Потеря зоны с привязанным zonal volume

</details>

<a id="section-07"></a>

<details>
<summary>

### 7. Kubernetes: безопасность и многопользовательская среда

</summary>

- **Доступ к API**
  - Authentication, authorization и admission
  - RBAC roles, cluster roles и bindings
  - ServiceAccount tokens и projected credentials
  - Impersonation и проверка can-i
  - Audit policies и анализ привилегированных действий

- **Безопасность Pod**
  - SecurityContext и non-root execution
  - Capabilities, seccomp и read-only root filesystem
  - Pod Security Standards и Pod Security Admission
  - Privileged containers, hostPath и host namespaces
  - Sandboxed runtimes и уровень изоляции tenant

- **Admission policies**
  - ValidatingAdmissionPolicy и CEL
  - OPA Gatekeeper и Kyverno
  - Signature verification и image allowlists
  - Mutating webhooks и контролируемые defaults
  - Fail-open/fail-closed и доступность admission infrastructure

- **Secrets и identities**
  - Encryption at rest и KMS integration
  - External Secrets и Secrets Store CSI
  - Workload identity для доступа к облаку
  - Ротация секретов без нарушения работы
  - Запрет общих service accounts между workloads

- **Multi-tenancy**
  - Namespace, cluster и virtual cluster isolation
  - Resource quotas и network boundaries
  - Разделение node pools для разных уровней доверия
  - Metadata leakage и доступ к telemetry
  - Выбор общей и выделенной инфраструктуры

- **Runtime security**
  - Runtime detection и Falco-подобные инструменты
  - Контроль egress и внешних загрузок
  - Реакция на компрометацию Pod или node
  - Изоляция исследования и production inference
  - Проверка baseline и документированные исключения

</details>

<a id="section-08"></a>

<details>
<summary>

### 8. Kubernetes: эксплуатация, обновления и восстановление

</summary>

- **Подготовка production-кластера**
  - HA control plane и topology etcd
  - kubeadm и managed Kubernetes
  - Node images, bootstrap и cluster add-ons
  - Системные resource reservations
  - Проверка готовности сети, storage и identity

- **Обновления**
  - Version skew и поддерживаемый порядок upgrade
  - API deprecation inventory
  - Обновление control plane, nodes и add-ons
  - Cordon, drain и replacement node pools
  - План rollback с учётом необратимых миграций

- **Control plane**
  - API latency, error rate и request saturation
  - API Priority and Fairness
  - etcd latency, storage size и compaction
  - Backup etcd и восстановление кластера
  - Certificates, expiry и ротация

- **Узлы и runtime**
  - Node conditions и причины NotReady
  - kubelet, runtime и image garbage collection
  - Disk pressure, memory pressure и PID pressure
  - OS patches, reboots и автоматическое восстановление
  - Проблемы CNI/CSI после обновления node image

- **Повседневная диагностика**
  - Pending, ImagePullBackOff и CrashLoopBackOff
  - Events, logs, describe и debug containers
  - Зависшие finalizers и deletion
  - Потерянные endpoints и неверная readiness
  - Сопоставление application, node и control plane telemetry

- **Надёжность платформы**
  - Обновление кластеров по canary ring
  - Configuration drift и инвентаризация add-ons
  - Restore drills и замена кластера
  - Cluster SLO и dependency ownership
  - План действий при недоступном Kubernetes API

</details>

<a id="section-09"></a>

<details>
<summary>

### 9. Helm, Kustomize, GitOps и Kubernetes operators

</summary>

- **Helm**
  - Charts, templates и values
  - Dependencies и version pinning
  - Release lifecycle, upgrade и rollback
  - Hooks, CRDs и особенности порядка установки
  - Проверка rendered manifests и chart schema

- **Kustomize**
  - Bases, overlays и patches
  - ConfigMap/Secret generators и name suffixes
  - Image replacements и labels
  - Ограничение числа слоёв наследования
  - Сравнение Kustomize и шаблонизации Helm

- **Argo CD и Flux**
  - Bootstrap, reconciliation и repository access
  - Health assessment и synchronization
  - Argo applications и ApplicationSet
  - Flux sources, Kustomizations и HelmRelease
  - Multi-cluster delivery и ограничение прав controller

- **Progressive delivery**
  - Argo Rollouts и Flagger
  - Traffic management и metric providers
  - Analysis windows и rollback thresholds
  - Pause/resume и ручное решение по ambiguous result
  - Проверка сценария отказа analysis backend

- **Operators и расширения**
  - CRD schema, spec, status и conditions
  - Reconcile, idempotency и retry behavior
  - Finalizers и cleanup внешних ресурсов
  - Conversion webhooks и schema evolution
  - Выбор operator, Helm chart или внешнего automation

- **Сопровождение ecosystem**
  - Operator permissions и blast radius
  - Upgrade CRDs и совместимость custom resources
  - Webhook certificates и доступность API
  - Backup operator-managed state
  - Контроль зависимостей ML operators от инфраструктуры

</details>

<a id="section-10"></a>

<details>
<summary>

### 10. Практические проекты и критерии готовности

</summary>

- **Контейнерная доставка**
  - Собрать минимальный подписанный OCI image
  - Запустить integration environment через Compose
  - Доставить приложение в Kubernetes через GitOps
  - Настроить probes, resource limits и rollback
  - Проверить supply chain gates в CI

- **Production-подобный кластер и проверка отказов**
  - Настроить workload identity, network policies и storage
  - Выделить resources, probes и topology constraints
  - Обновить node pool без нарушения согласованного SLO
  - Проверить потерю node и восстановление stateful workload
  - Подтвердить изоляцию арендаторов разрешёнными и запрещёнными запросами

- **Проверка самостоятельности в Docker/Kubernetes**
  - Проследить digest от CI image до работающего Pod
  - Найти причину Pending, OOM, crash и сетевой недоступности
  - Объяснить controller ownership и последствия удаления ресурсов
  - Проверить upgrade compatibility, backup и восстановление
  - Подготовить manifests, GitOps workflow и эксплуатационные runbooks

</details>

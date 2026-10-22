# DevOps Zero to Hero

**Linux · Сети · Безопасность · Облака · IaC · CI/CD · Platform Engineering**

## Навигация

| Раздел | Название |
| --- | --- |
| 1 | [Фундамент DevOps и инженерный процесс](#section-01) |
| 2 | [Рабочее окружение, терминал, Bash и автоматизация](#section-02) |
| 3 | [Linux: устройство, администрирование, процессы и ресурсы](#section-03) |
| 4 | [Диски, файловые системы и модели хранения](#section-04) |
| 5 | [Сети, DNS, HTTP, TLS и управление трафиком](#section-05) |
| 6 | [Идентификация, доступ, секреты и безопасность](#section-06) |
| 7 | [Git, конфигурация, зависимости и артефакты](#section-07) |
| 8 | [Виртуализация, bare metal и hybrid-инфраструктура](#section-08) |
| 9 | [Облака: архитектура, сервисы и выбор провайдера](#section-09) |
| 10 | [Infrastructure as Code: Terraform и OpenTofu](#section-10) |
| 11 | [Управление конфигурацией и подготовка образов](#section-11) |
| 12 | [Continuous Integration и безопасность сборки](#section-12) |
| 13 | [Continuous Delivery, релизы и GitOps](#section-13) |
| 14 | [Тестирование инфраструктуры и платформ](#section-14) |
| 15 | [Эксплуатация баз данных, брокеров и stateful-сервисов](#section-15) |
| 16 | [Platform Engineering, developer experience и FinOps](#section-16) |
| 17 | [Инженерная зрелость, практические проекты и критерии готовности](#section-17) |

## Содержание

<a id="section-01"></a>

<details>
<summary>

### 1. Фундамент DevOps и инженерный процесс

</summary>

- **Роли и границы ответственности**
  - DevOps как культура совместной разработки и эксплуатации
  - SRE как инженерный подход к надёжности сервисов
  - DataOps как управление доставкой и качеством данных
  - MLOps как управление жизненным циклом ML-систем
  - Platform Engineering, ML Engineer и Data Engineer: зоны взаимодействия

- **Жизненный цикл изменения**
  - Требование, разработка, проверка, доставка и обратная связь
  - Различие deployment, release и фактического использования
  - Код, конфигурация, данные и модель как связанные версии
  - Владение сервисом после запуска и вывод из эксплуатации
  - Ручной процесс, автоматизация и уровни зрелости

- **Базовые инженерные принципы**
  - Воспроизводимость, идемпотентность и декларативное управление
  - Малые изменения, быстрые проверки и ограничение области отказа
  - Простота, явные контракты и управление зависимостями
  - Наблюдаемость, проверяемость и восстановимость по проекту
  - Компромиссы между скоростью, стоимостью, качеством и надёжностью

- **Производственные окружения**
  - Development, test, staging и production
  - Разделение аккаунтов, сетей, данных и полномочий
  - Паритет окружений и допустимые различия
  - Регион, зона доступности и домен отказа
  - Shared responsibility между командой, платформой и провайдером

- **Результаты работы инженера**
  - Работающий сервис и измеримые пользовательские свойства
  - Архитектурное описание, ADR, инструкции и runbooks
  - Автоматизированная доставка и проверенный сценарий восстановления
  - Прозрачные затраты и управляемые риски
  - Передача знаний, сопровождение пользователей и снижение toil

- **Карта подготовки**
  - Системная база перед контейнерами и облаками
  - Доставка и SRE перед эксплуатацией ML-платформы
  - DataOps как эксплуатационный контракт с инженерией данных
  - MLOps для готовых моделей без повторения теории ML/DL
  - Практические доказательства компетенций на каждом этапе

</details>

<a id="section-02"></a>

<details>
<summary>

### 2. Рабочее окружение, терминал, Bash и автоматизация

</summary>

- **Локальная лаборатория**
  - Linux, виртуальная машина, WSL и удалённый сервер
  - Изоляция учебных ресурсов от рабочих окружений
  - Минимальные требования к CPU, RAM, диску и GPU
  - Воспроизводимое создание и удаление стенда
  - Ограничения бюджета и автоматическое выключение ресурсов

- **Терминал и командная строка**
  - Команда, аргументы, параметры и рабочий каталог
  - PATH, переменные окружения и коды завершения
  - Стандартные потоки, конвейеры и перенаправления
  - История команд, completion и безопасная работа с секретами
  - tmux, редактор и устойчивые удалённые сессии

- **Удалённый доступ**
  - SSH-ключи, агент и проверка host keys
  - Bastion, ProxyJump и туннели
  - Передача файлов через scp, sftp и rsync
  - Разделение административного и пользовательского доступа
  - Диагностика авторизации, маршрута и разрыва соединения

- **Чтение документации**
  - man, help и справочники протоколов
  - Документация установленной версии и release notes
  - Experimental, beta, stable и deprecated возможности
  - Матрицы совместимости и политика поддержки
  - Проверка примера в изолированном окружении

- **Инвентаризация и контекст**
  - Проверка аккаунта, региона, namespace и kube-context
  - Профили CLI и отдельные учётные записи
  - Имена ресурсов, labels, tags и владельцы
  - Каталог сервисов и карта зависимостей
  - Сохранение воспроизводимой истории диагностики

- **Лабораторная дисциплина**
  - Фиксация версий инструментов и конфигурации
  - Минимальный сценарий воспроизведения ошибки
  - Сбор baseline перед изменением
  - Проверка результата и очистка ресурсов
  - Отчёт с гипотезой, измерением и выводом

- **Модель исполнения shell**
  - Quoting, expansion и подстановка команд
  - Переменные, параметры и экспорт окружения
  - Условия, циклы и функции
  - Exit status, pipefail и ограничения errexit
  - Subshell, background jobs и управление процессами

- **Текст и структурированные данные**
  - rg, find, sort, uniq, cut и xargs
  - sed и awk для эксплуатационных задач
  - jq для JSON и yq для YAML
  - Нулевые разделители и имена файлов с пробелами
  - Locale, Unicode и стабильность сортировки

- **Надёжные скрипты**
  - Проверка входных параметров и предусловий
  - Идемпотентность и повторяемый запуск
  - Временные каталоги, trap и очистка ресурсов
  - Блокировки, flock и защита от параллельного запуска
  - Явные таймауты, ограниченные retries и backoff

- **Безопасное выполнение**
  - Shell injection и границы доверенного ввода
  - Разделение строки команды и массива аргументов
  - Секреты в аргументах, логах и окружении
  - Dry run, предварительный просмотр и ограничение области изменения
  - Атомарная запись конфигурации и резервная копия

- **Инструменты автоматизации**
  - Make и task runners для повторяемых операций
  - cron и systemd timers: окружение и пересечения запусков
  - curl и HTTP-контракты в скриптах
  - GNU parallel и ограничение конкурентности
  - Переход от shell к полноценному инструменту при росте сложности

- **Проверка и сопровождение**
  - ShellCheck и форматирование shell-кода
  - Тестирование ошибок и очистки ресурсов
  - Логи, диагностика и полезные сообщения об отказе
  - Переносимость Bash и POSIX shell
  - Документация интерфейса и версионирование скриптов

</details>

<a id="section-03"></a>

<details>
<summary>

### 3. Linux: устройство, администрирование, процессы и ресурсы

</summary>

- **Архитектура Linux**
  - Kernel space, user space и системные вызовы
  - Дистрибутив, ядро, userspace и менеджер пакетов
  - Загрузка: firmware, bootloader, initramfs и init
  - Модули ядра и драйверы устройств
  - Различия физических, виртуальных и контейнерных окружений

- **Файловая иерархия**
  - Назначение /etc, /var, /usr, /proc и /sys
  - Абсолютные и относительные пути
  - Обычные файлы, каталоги, сокеты и устройства
  - Символические и жёсткие ссылки
  - Метаданные, inode и права родительских каталогов

- **Пользователи и полномочия**
  - UID, GID, группы и сервисные пользователи
  - Права rwx, umask и ACL
  - setuid, setgid и sticky bit
  - sudo, делегирование и принцип минимальных полномочий
  - PAM, NSS и централизованные каталоги пользователей

- **Пакеты и обновления**
  - Репозитории, подписи и доверие к пакетам
  - apt и dnf: установка, обновление и откат
  - Версии, зависимости и конфликты пакетов
  - Обновление ядра и необходимость перезагрузки
  - Планирование security patches и проверка после обновления

- **Системные службы**
  - Назначение cron, journald, logrotate и системных таймеров
  - Синхронизация времени через NTP и chrony
  - Локаль, кодировки и временные зоны
  - Настройка hostname и системного resolver
  - Управление конфигурацией без ручного дрейфа

- **Базовая диагностика**
  - uname, hostnamectl, lsblk и lscpu
  - journalctl, dmesg и сообщения загрузки
  - Поиск изменений конфигурации и пакетов
  - Rescue mode и восстановление административного доступа
  - Проверка работоспособности после системных изменений

- **Жизненный цикл процесса**
  - PID, PPID, дерево процессов и сессии
  - fork, exec, wait и завершение процесса
  - Состояния running, sleeping, zombie и uninterruptible sleep
  - Сигналы, SIGTERM, SIGKILL и graceful shutdown
  - Дочерние процессы, orphan-процессы и reaping

- **CPU и планирование**
  - Потоки, ядра, SMT и CPU affinity
  - User time, system time, iowait и steal
  - Load average и его интерпретация
  - Приоритеты nice, scheduling classes и throttling
  - CPU saturation и ограничения виртуальной машины

- **Память**
  - Адресное пространство, RSS, PSS и virtual memory
  - Page cache, anonymous memory и memory mapping
  - Swap, page faults и давление на память
  - OOM killer, cgroup OOM и утечки памяти
  - NUMA и последствия удалённого доступа к памяти

- **Управление ресурсами**
  - cgroups v1/v2: accounting, limits и изоляция ресурсов
  - CPU quota, memory limits и ограничения I/O
  - ulimit, файловые дескрипторы и лимиты процессов
  - Pressure Stall Information и признаки конкуренции
  - Резервирование ресурсов системным службам

- **systemd**
  - Units, targets и зависимости служб
  - ExecStart, environment, user и working directory
  - Restart policies, watchdog и start limits
  - Socket activation и timers
  - Hardening unit-файлов и изоляция службы

- **Исследование проблем**
  - ps, top, htop, pidstat и systemd-cgtop
  - free, vmstat, sar и /proc
  - lsof, strace и системные вызовы
  - Core dumps, stack traces и ограничения их сбора
  - Отличие причины сбоя от вторичных симптомов

</details>

<a id="section-04"></a>

<details>
<summary>

### 4. Диски, файловые системы и модели хранения

</summary>

- **Устройства и тома**
  - Block devices, partitions и таблицы разделов
  - HDD, SSD, NVMe и характеристики задержек
  - LVM, software RAID и расширение тома
  - Multipath и отказ отдельных путей
  - TRIM, wear и показатели состояния накопителя

- **Файловые системы**
  - ext4, XFS и критерии выбора
  - Journaling, fsync и гарантии записи
  - Mount options, fstab и зависимость служб от mount
  - Inode exhaustion, quotas и reserved space
  - Online resize и восстановление повреждений

- **Модели хранения**
  - Block, file и object storage
  - NFS, SMB и особенности сетевого монтирования
  - Локальные ephemeral-диски и постоянные тома
  - Распределённое хранение и домены отказа
  - Совместимость модели доступа с рабочей нагрузкой

- **Производительность I/O**
  - IOPS, throughput, latency и queue depth
  - Последовательный и случайный доступ
  - Buffered I/O, direct I/O и page cache
  - iostat, fio и построение репрезентативного теста
  - Конкуренция checkpoint, загрузки данных и системных логов

- **Object storage**
  - Buckets, keys, metadata и multipart upload
  - Префиксы, listing и стоимость операций
  - Versioning, retention, lifecycle и garbage collection
  - ETag, checksum и проверка целостности
  - Консистентность и атомарность операций по контракту провайдера

- **Защита и восстановление**
  - Snapshot, backup, replication и различия гарантий
  - Шифрование диска и объектного хранилища
  - Проверка свободного места и прогноза роста
  - Восстановление удалённого или повреждённого файла
  - Проверка пригодности резервной копии восстановлением

</details>

<a id="section-05"></a>

<details>
<summary>

### 5. Сети, DNS, HTTP, TLS и управление трафиком

</summary>

- **Базовые модели**
  - Уровни TCP/IP и путь сетевого пакета
  - MAC, Ethernet, ARP и neighbour discovery
  - IPv4, IPv6, адреса и подсети
  - CIDR, маски и вычисление адресного пространства
  - MTU, fragmentation и path MTU discovery

- **Маршрутизация**
  - Routing table, default gateway и longest prefix match
  - Статическая маршрутизация, OSPF и BGP
  - NAT, SNAT, DNAT и connection tracking
  - Private networks, VPN и peering
  - Асимметричные маршруты и обратный путь

- **Транспортные протоколы**
  - TCP handshake, sequence numbers и retransmission
  - Congestion control, flow control и receive window
  - UDP и допустимость потери пакетов
  - Keepalive, half-open connections и TIME_WAIT
  - QUIC и отличие transport-level поведения

- **Сетевые ограничения**
  - Bandwidth, latency, jitter и packet loss
  - Connection limits и ephemeral port exhaustion
  - Socket buffers и очереди accept
  - Firewall rules, nftables и security groups
  - Stateful и stateless фильтрация

- **Диагностика соединений**
  - ip, ss, ping и traceroute
  - mtr, tcpdump и Wireshark
  - Проверка маршрута отдельно от проверки приложения
  - Диагностика retransmits, resets и DNS-задержек
  - Тестирование пропускной способности через iperf

- **Сети для ML-нагрузок**
  - Передача dataset, model weights и checkpoints
  - Север–юг и восток–запад трафик
  - Сеть хранения и сеть распределённого обучения
  - Oversubscription и конкуренция арендаторов
  - Планирование сетевого бюджета обучения и inference

- **DNS**
  - Resolver, authoritative server и рекурсивный запрос
  - A, AAAA, CNAME, TXT, MX, NS и SRV
  - TTL, positive cache и negative cache
  - Delegation, split-horizon и private DNS
  - dig и диагностика propagation, SERVFAIL и NXDOMAIN

- **HTTP и API**
  - Методы, коды ответа, headers и тело запроса
  - Идемпотентность, caching и conditional requests
  - HTTP/1.1, HTTP/2 и multiplexing
  - Streaming, Server-Sent Events и WebSocket
  - REST, gRPC, protobuf и совместимость контрактов

- **TLS и сертификаты**
  - Сертификат, цепочка доверия и проверка имени
  - CA, CSR, private key и сертификаты служб
  - TLS handshake, SNI и ALPN
  - mTLS и идентификация клиента
  - Выпуск, автоматическое продление и ротация сертификатов

- **Прокси и балансировка**
  - Forward proxy, reverse proxy и API gateway
  - L4 и L7 балансировка
  - NGINX, HAProxy и Envoy: эксплуатационные роли
  - Health checks, connection pooling и upstream discovery
  - Session affinity и перекос распределения нагрузки

- **Политики трафика**
  - End-to-end deadline и отдельные connect/read timeouts
  - Retries, jitter и ограничение retry budget
  - Rate limiting, quotas и admission control
  - Circuit breaker, bulkhead и load shedding
  - CDN, кеширование и предотвращение cache stampede

- **Диагностика запросов**
  - curl, openssl s_client и grpcurl
  - Различение DNS, TCP, TLS и application latency
  - 429, 499, 502, 503 и 504 в цепочке прокси
  - Request ID, trace context и сквозная корреляция
  - Размер payload, compression и медленные клиенты

</details>

<a id="section-06"></a>

<details>
<summary>

### 6. Идентификация, доступ, секреты и безопасность

</summary>

- **Модель угроз**
  - Активы, доверенные границы и атакующие поверхности
  - Confidentiality, integrity и availability
  - Threat modeling и оценка последствий компрометации
  - Defense in depth и минимизация привилегий
  - Разделение production, research и внешних интеграций

- **Authentication и authorization**
  - Пользовательские и workload identities
  - RBAC, ABAC и resource-based policies
  - OAuth 2.0, OpenID Connect и service accounts
  - SSO, MFA и временные учётные данные
  - Проверка effective permissions и запреты по умолчанию

- **Управление секретами**
  - Secret manager, Vault и зашифрованная конфигурация
  - Статические и динамические секреты
  - Выдача, обновление lease, отзыв и ротация
  - Envelope encryption, KMS и HSM
  - Защита от утечки через git, CI, логи и crash dumps

- **Безопасность узлов**
  - Минимальный образ и отключение лишних служб
  - SELinux, AppArmor и seccomp
  - Патчинг, контроль конфигурации и учёт активов
  - EDR, file integrity monitoring и audit logs
  - Изоляция административной сети и доступ через bastion

- **Workload identity**
  - Federation между CI, кластером и облаком
  - Короткоживущие токены вместо постоянных ключей
  - SPIFFE/SPIRE как подход к идентичности служб
  - Разделение полномочий обучения, registry и serving
  - Защита metadata endpoint и от SSRF

- **Реакция на нарушения**
  - Обнаружение подозрительной активности
  - Отзыв credentials и ограничение распространения
  - Сохранение доказательств и временной шкалы
  - Восстановление доверенного окружения
  - Проверка доступа и аудит после инцидента

</details>

<a id="section-07"></a>

<details>
<summary>

### 7. Git, конфигурация, зависимости и артефакты

</summary>

- **Модель Git**
  - Working tree, index, commits и object database
  - Branch, tag, remote и tracking branch
  - Merge, rebase и fast-forward
  - Cherry-pick, revert и восстановление истории
  - .gitignore, git attributes и окончания строк

- **Совместная разработка**
  - Pull requests, code review и CODEOWNERS
  - Trunk-based development и short-lived branches
  - Branch protection и обязательные проверки
  - Разрешение конфликтов и изменение общего кода
  - Малые изменения и проверяемые описания PR

- **Управление релизами**
  - Semantic versioning и версионирование контрактов
  - Changelog, release notes и подписанные tags
  - Соответствие commit, build, artifact и deployment
  - Hotfix и восстановление после неудачного релиза
  - Политика поддержки версий и deprecation

- **Работа с большим репозиторием**
  - Monorepo и polyrepo: границы ответственности
  - Sparse checkout, submodules и Git LFS
  - Ограничения Git для datasets и model weights
  - Path-based CI и определение затронутых компонентов
  - Общие шаблоны и версии инфраструктурных модулей

- **Защита исходного кода**
  - Secret scanning и dependency review
  - Подпись commits и проверка происхождения
  - Ограничение токенов автоматизации
  - Недоверенные forks и безопасные PR workflows
  - Audit trail административных изменений

- **Диагностика изменений**
  - git bisect и поиск регрессии
  - git blame и контекст решения
  - diff конфигурации и rendered manifests
  - Восстановление через reflog
  - Связывание изменения с инцидентом и метриками

- **Форматы конфигурации**
  - JSON, YAML, TOML и INI
  - YAML types, anchors и опасные неявные преобразования
  - Схемы, валидация и неизвестные поля
  - Значения по умолчанию и порядок переопределения
  - Canonicalization и стабильное сравнение конфигураций

- **Дизайн конфигурации**
  - Разделение конфигурации и секретов
  - Immutable configuration и runtime reload
  - Environment-specific overlays и наследование
  - Версионирование схемы конфигурации
  - Проверка конфигурации до запуска workload

- **Управление зависимостями**
  - Прямые и транзитивные зависимости
  - Lockfiles, checksums и разрешение версий
  - ABI, системные библиотеки и native dependencies
  - Матрицы CPU/GPU, OS, architecture и runtime
  - Обновления зависимостей и контролируемые исключения

- **Типы артефактов**
  - Бинарный пакет, архив и container image
  - Dataset snapshot, model bundle и checkpoint
  - Content addressing и immutable identifiers
  - Метаданные, manifest и dependencies артефакта
  - Совместимость формата с целевой средой выполнения

- **Репозитории артефактов**
  - Registry, package repository и object storage
  - Push, pull, promotion и retention
  - Репликация, зеркала и air-gapped доступ
  - Разделение environments и уровней доверия
  - Garbage collection с учётом активных ссылок

- **Целостность и происхождение**
  - Checksums и проверка при передаче
  - SBOM, provenance и attestations
  - Подпись и доверенная identity сборщика
  - Отзыв уязвимого артефакта
  - Восстановление цепочки source–build–release–deployment

</details>

<a id="section-08"></a>

<details>
<summary>

### 8. Виртуализация, bare metal и hybrid-инфраструктура

</summary>

- **Виртуализация**
  - Hypervisor, VM и аппаратная поддержка виртуализации
  - KVM/QEMU и модель виртуального оборудования
  - vCPU overcommit, ballooning и noisy neighbour
  - Images, snapshots, cloning и cloud-init
  - Live migration и ограничения для GPU workloads

- **Физическая инфраструктура**
  - Rack, power, cooling и домены отказа
  - BMC, IPMI и Redfish
  - Firmware, BIOS и управление совместимостью
  - NUMA, PCIe topology и размещение ускорителей
  - Инвентаризация и замена неисправного оборудования

- **Автоматическая подготовка узлов**
  - PXE/iPXE и сетевой boot
  - Образы ОС и unattended installation
  - Разделение bootstrap и постоянной конфигурации
  - Provisioning, validation и ввод узла в эксплуатацию
  - Sanitization дисков при передаче и списании

- **Частное облако и кластеры**
  - OpenStack и виртуальная инфраструктура
  - vSphere и управление VM-парком
  - Slurm как менеджер вычислительных задач
  - Сопоставление VM, Kubernetes и batch scheduler
  - Границы ответственности инфраструктурной и ML-команды

- **Hybrid и air-gapped среды**
  - Частная связность с облаком
  - Зеркала packages, images и моделей
  - Перенос подписанных артефактов между контурами
  - Offline update, vulnerability feeds и лицензии
  - Доставка метрик без вывода чувствительных данных

- **Эксплуатационные компромиссы**
  - Закупка, lead time и запас ресурсов
  - Capacity buffer и ремонт оборудования
  - Стоимость владения и загрузка ускорителей
  - Согласованные окна обслуживания
  - Обоснование выбора cloud, on-premises или hybrid

</details>

<a id="section-09"></a>

<details>
<summary>

### 9. Облака: архитектура, сервисы и выбор провайдера

</summary>

- **Организация облака**
  - Accounts, subscriptions, projects и organizations
  - Regions, availability zones и failure domains
  - Landing zone и baseline policies
  - Resource hierarchy, naming и tagging
  - Quotas, limits и управление разрешёнными сервисами

- **Облачная сеть**
  - VPC/VNet, subnets и route tables
  - Public/private endpoints и NAT gateways
  - Security groups, network ACL и cloud firewall
  - Peering, transit network и private connectivity
  - Flow logs, DNS и диагностика межсервисного доступа

- **Compute**
  - VM families, machine types и accelerator instances
  - Autoscaling groups и instance templates
  - Spot/preemptible capacity и interruptions
  - Serverless functions и container services
  - Startup time, regional capacity и reserved resources

- **Storage и managed state**
  - Object storage, block volumes и file services
  - Managed databases и caches
  - Queues, event buses и streaming services
  - Encryption, lifecycle и cross-region replication
  - Service quotas, SLAs и провайдерские ограничения

- **IAM и управление**
  - Roles, policies и service principals
  - Federation, workload identity и audit trails
  - Organization policies и service control boundaries
  - Billing accounts, budgets и cost allocation
  - Разделение control plane и data plane доступа

- **Надёжная облачная архитектура**
  - Multi-zone как базовый способ ограничения отказа
  - Multi-region по требованиям RTO и RPO
  - Managed service и реальная область ответственности
  - Regional outage, quota exhaustion и API throttling
  - Проектирование выхода из сервиса и переносимости

- **Метод изучения провайдера**
  - Один основной провайдер до эксплуатационной глубины
  - Сопоставление концепций вместо запоминания каталога
  - Документация API, quotas и service availability
  - Проверка поддерживаемых регионов и типов GPU
  - Фиксация стоимости и требований к данным

- **Практический контур AWS**
  - IAM, Organizations, VPC и CloudTrail
  - EC2, Auto Scaling, EKS и ECS
  - S3, EBS, EFS и RDS
  - ECR, Secrets Manager и CloudWatch
  - SageMaker и границы managed ML-инфраструктуры

- **Практический контур Google Cloud**
  - Organization, projects, IAM и audit logs
  - Compute Engine, GKE и Cloud Run
  - Cloud Storage, Persistent Disk и Cloud SQL
  - Artifact Registry, Secret Manager и Cloud Monitoring
  - Управляемая ML-платформа и её актуальные API

- **Практический контур Azure**
  - Entra ID, subscriptions, resource groups и RBAC
  - Virtual Machines, VM Scale Sets и AKS
  - Blob Storage, Managed Disks и Azure Files
  - Container Registry, Key Vault и Azure Monitor
  - Azure Machine Learning и managed endpoints

- **Сравнение архитектур**
  - Workload identity и привязка ресурсов к окружению
  - Private access к datasets, registry и inference
  - GPU quotas, spot capacity и autoscaling
  - Egress, storage requests и полная стоимость
  - Возможность миграции artifacts, metadata и pipelines

- **Практическая проверка**
  - Поднять приватное окружение через IaC
  - Запустить workload с временными credentials
  - Настроить telemetry и бюджет
  - Проверить отказ зоны и потерю экземпляра
  - Удалить стенд без оставшихся платных ресурсов

</details>

<a id="section-10"></a>

<details>
<summary>

### 10. Infrastructure as Code: Terraform и OpenTofu

</summary>

- **Декларативная модель**
  - Resources, data sources, providers и dependency graph
  - HCL, expressions, types и validation
  - Variables, locals и outputs
  - count, for_each и стабильность resource addresses
  - plan, apply, destroy и жизненный цикл ресурса

- **State**
  - Назначение state и связь с реальной инфраструктурой
  - Remote backend, locking и разграничение доступа
  - Шифрование, versioning и резервное копирование state
  - Import, moved blocks и перенос ресурсов
  - Recovery после partial apply и повреждения state

- **Модули и композиция**
  - Интерфейс модуля и явные входы
  - Версионирование модулей и provider lockfile
  - Root modules и разделение окружений
  - Границы state и ограничение blast radius
  - Сравнение workspaces и отдельных deployment units

- **Управление изменениями**
  - Plan в PR и применение проверенного результата
  - Drift detection и reconciliation
  - Lifecycle rules и опасность ignore_changes
  - Replace, create_before_destroy и зависимые ресурсы
  - Миграция между версиями providers и инструментов

- **Качество и безопасность**
  - fmt, validate и статические проверки
  - Policy as code и запреты опасных конфигураций
  - Tests модулей и интеграционные проверки
  - Секреты в state, plan и CI-логах
  - OIDC federation для CI без постоянных ключей

- **Масштабирование IaC**
  - Каталог модулей и ownership
  - Зависимости нескольких stacks и порядок доставки
  - Terragrunt и альтернативы по сложности проекта
  - Pulumi, Crossplane и границы выбора подхода
  - Аудит, cost estimation и controlled destroy

</details>

<a id="section-11"></a>

<details>
<summary>

### 11. Управление конфигурацией и подготовка образов

</summary>

- **Ansible**
  - Inventory, groups, variables и facts
  - Playbooks, tasks, modules и handlers
  - Roles, collections и dependency management
  - Templates, conditionals и loops
  - become и безопасное повышение привилегий

- **Надёжная конфигурация**
  - Идемпотентность и повторяемое применение
  - Check mode, diff mode и их ограничения
  - Serial rollout, canary hosts и failure thresholds
  - Secrets через Vault или внешний secret manager
  - Проверка состояния после изменения

- **Образы машин**
  - Golden images и immutable infrastructure
  - Packer, image pipeline и source image pinning
  - Bootstrap через cloud-init
  - Сканирование, hardening и подпись образа
  - Версионирование, promotion и deprecation образов

- **Изменение парка узлов**
  - Rolling replacement и maintenance windows
  - Drain задач и graceful shutdown
  - Обновление ОС, драйверов и системных библиотек
  - Проверка совместимости GPU и kernel modules
  - Откат образа и восстановление конфигурации

- **Контроль дрейфа**
  - Desired state и наблюдаемое состояние
  - Периодическая проверка конфигурации
  - Источник истины для hosts и inventories
  - Исключения, срок действия и аудит
  - Выбор repair или полного пересоздания узла

- **Проверка автоматизации**
  - Linting, syntax checks и проверка шаблонов
  - Molecule и тестирование ролей
  - Smoke tests готового образа
  - Проверка доступа, telemetry и resource limits
  - Измерение времени подготовки нового узла

</details>

<a id="section-12"></a>

<details>
<summary>

### 12. Continuous Integration и безопасность сборки

</summary>

- **Проектирование CI**
  - Триггеры, jobs, stages и dependency graph
  - Быстрые обязательные проверки и дорогие проверки по требованию
  - Path filters и проверка изменённых компонентов
  - Fail-fast, cancellation и ограничение конкурентных запусков
  - Версионирование reusable workflows и CI templates

- **Исполнители**
  - Hosted и self-hosted runners
  - Ephemeral workers и очистка после выполнения
  - Изоляция jobs и недоверенного кода
  - CPU/GPU runners, scheduling и capacity
  - Сетевой доступ и минимальные credentials

- **Сборка и кеширование**
  - Воспроизводимая и hermetic сборка
  - Dependency cache и artifact cache
  - Cache keys, invalidation и cache poisoning
  - Сборка один раз и продвижение одного артефакта
  - Проверка CPU architecture и целевой платформы

- **Проверки в pipeline**
  - Lint, validation и unit-level проверки
  - Integration, contract и smoke tests
  - SAST, dependency scanning и license checks
  - Сканирование secrets, images и IaC
  - Публикация отчётов и понятные quality gates

- **Software supply chain**
  - SBOM в SPDX или CycloneDX
  - Build provenance и уровни доверия SLSA
  - Sigstore/cosign и проверка подписи
  - Pinning actions, plugins и base images
  - Исключения уязвимостей с владельцем и сроком

- **Практика CI-систем**
  - GitHub Actions: workflows, contexts и permissions
  - GitLab CI: includes, rules и environments
  - Jenkins: controller, agents и plugin lifecycle
  - OIDC federation и защищённые environments
  - Диагностика нестабильных и медленных pipelines

</details>

<a id="section-13"></a>

<details>
<summary>

### 13. Continuous Delivery, релизы и GitOps

</summary>

- **Модель доставки**
  - Continuous delivery и continuous deployment
  - Promotion между окружениями без повторной сборки
  - Release manifest с версиями всех компонентов
  - Approvals по риску и separation of duties
  - Доставка приложения, конфигурации, инфраструктуры и модели

- **Стратегии deployment**
  - Recreate, rolling update и blue-green
  - Canary по доле трафика или группе пользователей
  - Feature flags и decoupling deployment от release
  - Shadow traffic и ограничения побочных эффектов
  - Progressive delivery и автоматические stop conditions

- **Изменение состояния**
  - Expand–migrate–contract для схем и API
  - Обратная и прямая совместимость
  - Длительные миграции и промежуточные версии
  - Rollback приложения при изменившихся данных
  - Forward fix, rollforward и compensating actions

- **GitOps**
  - Desired state, reconciliation и pull-based delivery
  - Git как источник деклараций и аудит изменений
  - Drift correction и управление ручными hotfix
  - Разделение code repository и deployment repository
  - Секреты, bootstrap и dependency ordering

- **Контроль релиза**
  - Pre-deploy, post-deploy и synthetic checks
  - Сравнение baseline и candidate по SLO
  - Deployment markers в метриках и traces
  - Abort, pause и rollback процедуры
  - Проверка фактической версии у всех replicas

- **Надёжность системы доставки**
  - Отказ CI/CD при работающем production
  - Recovery GitOps controller и credentials
  - Защита от массового ошибочного reconciliation
  - Emergency path с последующим аудитом
  - Метрики времени доставки и доли неудачных изменений

</details>

<a id="section-14"></a>

<details>
<summary>

### 14. Тестирование инфраструктуры и платформ

</summary>

- **Стратегия проверок**
  - Границы unit, integration, system и acceptance tests
  - Контракт инфраструктурного модуля и платформенного API
  - Проверка поведения вместо снимков реализации
  - Стоимость, длительность и доверие к проверке
  - Test ownership и действия при падении

- **Статическая валидация**
  - Схемы конфигурации и manifests
  - Проверка IaC и policy rules
  - Rendered templates и недопустимые комбинации параметров
  - Проверка секретов и небезопасных разрешений
  - Совместимость API с целевым кластером

- **Интеграционные стенды**
  - Ephemeral environments и очистка ресурсов
  - Локальные кластеры и реальные облачные зависимости
  - Test doubles и границы достоверности эмуляторов
  - Тестовые identities, сети и datasets
  - Предотвращение пересечения параллельных прогонов

- **Проверки работоспособности**
  - Smoke tests и synthetic user journeys
  - Сетевые, DNS и TLS проверки
  - Проверка storage semantics и persistence
  - Проверка ограничений доступа и tenant isolation
  - Проверка telemetry, alerts и runbook links

- **Изменения и отказоустойчивость**
  - Upgrade tests и downgrade compatibility
  - Backup–restore test с проверкой целостности
  - Потеря узла, зоны и внешней зависимости
  - Перезапуск во время операции и повторное выполнение
  - Проверка частичного provisioning и cleanup

- **Сопровождение тестов**
  - Flaky tests и воспроизводимость ошибок
  - Диагностические артефакты неудачного запуска
  - Performance regression budgets
  - Разделение обязательных и исследовательских проверок
  - Срок жизни стендов и cost limits

</details>

<a id="section-15"></a>

<details>
<summary>

### 15. Эксплуатация баз данных, брокеров и stateful-сервисов

</summary>

- **Ответственность платформы**
  - Provisioning, patching и конфигурационный baseline
  - Capacity, quotas и управление подключениями
  - Authentication, encryption и сетевой доступ
  - Replication, backups и проверка восстановления
  - Managed service или самостоятельная эксплуатация

- **PostgreSQL как metadata backend**
  - Connections, pools и exhaustion
  - WAL, replication slots и рост хранилища
  - Locks, long transactions и deadlocks
  - Vacuum, bloat и эксплуатационные метрики
  - Point-in-time recovery и переключение replica

- **Redis и online state**
  - Persistence, replication и failover
  - Memory policy, eviction и TTL
  - Hot keys, big keys и blocked clients
  - Cluster sharding и migration
  - Допустимая потеря кеша, features или результатов

- **Kafka и брокеры сообщений**
  - Brokers, controllers, partitions и replication
  - Consumer lag, retention и disk capacity
  - ISR, under-replicated partitions и availability
  - ACL, quotas и безопасное обновление
  - Replay, DLQ и восстановление потребителей

- **Search и vector backends**
  - Индексы, shards, replicas и refresh
  - Память, сегменты, compaction и disk watermarks
  - Snapshots и blue-green reindex
  - Изоляция tenant и фильтры доступа
  - Latency, recall и freshness как эксплуатационные свойства

- **Хранилища платформенных метаданных**
  - Registry database и artifact storage как связанный backup
  - Metadata migrations и совместимость версий
  - Раздельные identities для сервисов
  - Согласованность ссылок на внешние артефакты
  - Runbooks потери state, credentials и capacity

</details>

<a id="section-16"></a>

<details>
<summary>

### 16. Platform Engineering, developer experience и FinOps

</summary>

- **Платформа как продукт**
  - Внутренние пользователи и их задачи
  - User research и карта developer journey
  - Platform API вместо набора ручных заявок
  - Product ownership, roadmap и support model
  - Оценка пользы по времени и надёжности работы

- **Internal Developer Platform**
  - Service catalog и ownership
  - Templates, scaffolding и golden paths
  - Self-service environments и provisioning
  - Документация, портал и API
  - Backstage и альтернативные интерфейсы

- **Контракты платформы**
  - Стандартный runtime и deployment specification
  - Identity, secrets и сетевые политики по умолчанию
  - Telemetry и SLO из шаблона сервиса
  - Quotas и поддерживаемые классы ресурсов
  - Версионирование API и deprecation

- **Организация взаимодействия**
  - Platform team и stream-aligned teams
  - Enabling work и сопровождение внедрения
  - Граница обязательных guardrails и свободы команды
  - Feedback loops и измерение adoption
  - Прозрачные исключения и технический долг

- **Надёжность IDP**
  - Availability provisioning и deployment APIs
  - Частичные отказы внутренних providers
  - Очереди, retries и идемпотентные requests
  - Аудит действий и восстановление workflow
  - Работа приложений при недоступном портале

- **Эволюция платформы**
  - Минимальный полезный контур
  - Build versus buy
  - Избежание избыточной абстракции
  - Миграции пользователей между версиями
  - Стоимость поддержки и вывод функций

- **Учёт затрат**
  - Allocation по команде, продукту и workload
  - Tags, labels и обязательный owner
  - Shared costs и правила распределения
  - Budgets, forecasts и anomaly detection
  - Showback, chargeback и ответственность потребителей

- **Compute optimization**
  - Rightsizing CPU, RAM и GPU
  - Reserved capacity и commitment discounts
  - Spot workloads и цена interruption
  - Autoscaling, scale-to-zero и idle shutdown
  - Bin packing и utilization без нарушения изоляции

- **Storage и сеть**
  - Storage tiers, lifecycle и retention
  - Egress, cross-zone и cross-region traffic
  - Стоимость requests и listing
  - Дублирование datasets, images и model weights
  - Кеширование с учётом полной стоимости

- **Управление оптимизациями**
  - Hypothesis, baseline и измеримый эффект
  - Performance–cost–quality tradeoffs
  - Budget guardrails в self-service и HPO
  - Учет инженерного времени и операционного риска
  - Проверка устойчивости экономии при росте нагрузки

</details>

<a id="section-17"></a>

<details>
<summary>

### 17. Инженерная зрелость, практические проекты и критерии готовности

</summary>

- **Самостоятельное владение системой**
  - Превращение неоднозначной задачи в инженерный план
  - Выявление рисков и неизвестных предположений
  - Выбор минимально достаточного решения
  - Ответственность за production после запуска
  - Измерение результата для пользователей и бизнеса

- **Архитектурные решения**
  - RFC, ADR и design review
  - Build/buy и total cost of ownership
  - Migration plan и обратная совместимость
  - Technical debt и приоритизация исправлений
  - Долгосрочная стоимость операционной сложности

- **Межкомандная работа**
  - Совместные контракты с DS, DE, security и SRE
  - Переговоры о SLO, качестве и бюджете
  - Ownership и escalation без серых зон
  - Передача знаний и mentoring
  - Инженерные стандарты с обоснованными исключениями

- **Измерение доставки**
  - Change lead time и deployment frequency
  - Failed deployment recovery time
  - Change fail rate и deployment rework rate
  - DORA metrics как показатели системы работы
  - Контекст измерений и защита от манипулирования метриками

- **Управление эксплуатацией**
  - План capacity и бюджет на надёжность
  - On-call readiness и снижение toil
  - Incident leadership и проверка postmortem actions
  - Risk register и roadmap mitigations
  - Устойчивость команды и распределение критичных знаний

- **Техническая коммуникация**
  - Объяснение компромисса разным аудиториям
  - Документация решения и ограничений
  - Evidence-based performance и cost reports
  - Понятные PR и release descriptions
  - Признание неопределённости и проверка гипотез

- **Linux-сервис с полноценной эксплуатацией**
  - Развернуть сервис через systemd
  - Ограничить CPU, memory и полномочия
  - Настроить TLS, logs и metrics
  - Диагностировать намеренно внесённый bottleneck
  - Подтвердить восстановление после crash и reboot

- **Инфраструктура через IaC**
  - Создать network, compute и storage
  - Настроить remote state и CI plan
  - Выдать workload identity без постоянных ключей
  - Проверить drift и безопасное изменение
  - Удалить стенд с отчётом по затратам

- **Готовность к самостоятельной работе DevOps**
  - Воссоздать окружение из versioned IaC и configuration management
  - Доставить проверенный артефакт через CI/CD с возможностью возврата
  - Объяснить effective permissions, сетевой маршрут и доверенные границы
  - Проверить восстановление stateful-зависимости вместе с SRE-сценарием
  - Подготовить ADR, эксплуатационную документацию и отчёт о стоимости

</details>

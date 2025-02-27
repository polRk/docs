# Мониторинг состояния кластера и хостов

Вы можете отслеживать состояние кластера {{ dataproc-name }} и отдельных его хостов с помощью инструментов мониторинга в консоли управления. Эти инструменты предоставляют диагностическую информацию в виде графиков.

{% include [monitoring-source](../../_includes/mdb/monitoring-provides.md) %}

{% include [monitoring-frequency](../../_includes/mdb/monitoring-freq.md) %}

{% include [monitoring-units](../../_includes/mdb/note-monitoring-auto-units.md) %}

## Мониторинг состояния кластера {#monitoring-cluster}

Для просмотра детальной информации о состоянии кластера {{ dataproc-name }}:

{% list tabs %}

- Консоль управления

  1. Перейдите на [страницу каталога]({{ link-console-main }}) и выберите сервис **{{ dataproc-name }}**.
  1. Нажмите на имя нужного кластера и выберите вкладку **Мониторинг**.

  На вкладке отображаются следующие графики:

  * **Active nodes** — количество запущенных хостов (кроме управляющих хостов).
  * **Apps failed** — количество приложений с ошибками выполнения.
  * **Available RAM** — объем свободной оперативной памяти, доступной в YARN для хостов в подкластерах с ролями `DATANODE` и `COMPUTENODE` (в байтах).
  * **Available virtual cores** — количество доступных ядер в YARN.
  * **Containers pending** — количество контейнеров, ожидающих запуска сервисом YARN Resource Manager.
  * **Decommissioned nodes** — количество хостов, для которых выполнена [декомиссия](../concepts/decommission.md).

{% endlist %}

## Мониторинг состояния хостов {#monitoring-hosts}

Для просмотра детальной информации о состоянии отдельных хостов {{ dataproc-name }}:

{% list tabs %}

- Консоль управления

  1. Перейдите на [страницу каталога]({{ link-console-main }}) и выберите сервис **{{ dataproc-name }}**.
  1. Нажмите на имя нужного кластера и выберите вкладку **Хосты**.
  1. Откройте ВМ нужного хоста и выберите вкладку **Мониторинг**.

  На вкладке отображаются графики с информацией о потреблении ресурсов на виртуальной машине:

  * **CPU Utilization** — загрузка процессорных ядер.
  * **Connections quota utilization** — процент использования доступных соединений к хосту.
  * **Disk bytes** — скорость чтения и записи данных в хранилище (байт/с).
  * **Disk operations** — интенсивность дисковых операций (операций/с).
  * **Network bytes** — скорость обмена данными по сети (байт/с).
  * **Network packets** — интенсивность обмена данными по сети (пакетов/с).

{% endlist %}

## Состояние и статус кластера {#cluster-health-and-status}

{% include [health-and-status](../../_includes/mdb/monitoring-cluster-health-and-status.md) %}

Для просмотра состояния и статуса кластера:

1. Перейдите на [страницу каталога]({{ link-console-main }}) и выберите сервис **{{ dataproc-name }}**.
1. Наведите курсор на индикатор в столбце **Доступность** в строке нужного кластера.

### Состояния кластера {#cluster-health}

{% include [monitoring-cluster-health](../../_includes/mdb/monitoring-cluster-health.md) %}

### Статусы кластера {#cluster-status}

{% include [monitoring-cluster-status](../../_includes/mdb/monitoring-cluster-status.md) %}

# Сеть и кластеры БД

При создании кластера вы можете:

* задать сеть и подсеть для кластера;
* запросить публичные IP-адреса для доступа к кластеру извне {{ yandex-cloud }}.

Подключение к кластеру {{ mgp-short-name }} производится только через хосты-мастеры.

Для высокоскоростной связи между хостами кластера {{ mgp-short-name }} использует обособленную _внутрикластерную сеть_ (interconnect). Доступ к внутрикластерной сети и прямое подключение к хостам-сегментам не предоставляются.

По умолчанию хосты-мастеры доступны для подключения с ВМ, находящихся в той же облачной сети. [Подробнее о работе сети](../../vpc/).

## Имя хоста и FQDN {#hostname}

{{ mgp-short-name }} при создании кластера назначает имена хостам автоматически. Краткие и полные (FQDN) имена хостов изменить нельзя.

FQDN можно использовать для доступа к хостам-мастерам как внутри, так и извне {{ yandex-cloud }}.

## Публичный доступ к кластеру {#public-access-to-a-host}

Чтобы получить публичные IP-адреса для доступа к хостам-мастерам кластера извне {{ yandex-cloud }}, при создании кластера включите опцию **Публичный доступ**. Для подключения к кластеру используйте FQDN его хостов-мастеров.

После создания кластера запросить публичные адреса или отказаться от них нельзя.

## Группы безопасности {#security-groups}


{% note tip %}

При подключении к кластеру из той же облачной сети, в которой он находится, [настройте группы безопасности](../operations/connect.md#configuring-security-groups) не только для кластера, но и для хоста, с которого выполняется подключение.

{% endnote %}

Особенности работы с группами безопасности:

* Для подключения к кластеру [необходимы правила](../operations/connect.md#configuring-security-groups), разрешающие прохождение трафика между ним и хостом, с которого выполняется подключение, даже если они находятся в одной группе безопасности.

* Настройки групп безопасности влияют на возможность подключения к кластеру, его работоспособность и сетевую связность хостов.


Подробнее см. в [документации Virtual Private Cloud](../../vpc/concepts/security-groups.md).


{% include [greenplum-trademark](../../_includes/mdb/mgp/trademark.md) %}

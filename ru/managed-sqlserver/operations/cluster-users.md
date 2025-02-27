# Управление пользователями

Вы можете добавлять и удалять пользователей, а также управлять их индивидуальными настройками.

{% note warning %}

С помощью команд SQL вы можете назначать пользователям привилегии, но не можете добавлять и изменять пользователей. Подробнее см. в разделе [{#T}](grant.md).

{% endnote %}

## Получить список пользователей {#list-users}

{% list tabs %}

- Консоль управления

  1. Перейдите на [страницу каталога]({{ link-console-main }}) и выберите сервис **{{ mms-name }}**.
  1. Нажмите на имя нужного кластера, затем выберите вкладку **Пользователи**.

- CLI

    {% include [cli-install](../../_includes/cli-install.md) %}

    {% include [default-catalogue](../../_includes/default-catalogue.md) %}

    Чтобы получить список пользователей кластера, выполните команду:

    ```bash
    {{ yc-mdb-ms }} user list \
       --cluster-name=<имя кластера>
    ```

    Имя кластера можно запросить со [списком кластеров в каталоге](cluster-list.md#list-clusters).

- API

  Воспользуйтесь методом API [list](../api-ref/User/list.md): передайте значение идентификатора требуемого кластера в параметре `clusterId` запроса.

  Чтобы узнать идентификатор кластера, [получите список кластеров в каталоге](cluster-list.md#list-clusters).

{% endlist %}

## Добавить пользователя {#adduser}

{% list tabs %}

- Консоль управления

  1. Перейдите на [страницу каталога]({{ link-console-main }}) и выберите сервис **{{ mms-name }}**.
  1. Нажмите на имя нужного кластера и выберите вкладку **Пользователи**.
  1. Нажмите кнопку **Добавить**.
  1. Введите имя пользователя базы данных и пароль.

      {% include [username-and-password-limits](../../_includes/mdb/mms/note-info-user-name-and-pass-limits.md) %}

  1. Выберите одну или несколько баз данных, к которым должен иметь доступ пользователь:
     1. Нажмите кнопку **Добавить базу данных**.
     1. Выберите базу данных из выпадающего списка.
     1. Повторите два предыдущих шага, пока не будут выбраны все требуемые базы данных.
     1. Чтобы удалить базу, добавленную по ошибке, нажмите значок ![image](../../_assets/cross.svg) справа от имени базы данных.
  1. [Задайте роли пользователя](grant.md#grant-role) для каждой из выбранных баз данных.
  1. Нажмите кнопку **Создать**.

- CLI

    {% include [cli-install](../../_includes/cli-install.md) %}

    {% include [default-catalogue](../../_includes/default-catalogue.md) %}

    Чтобы добавить пользователя:

    1. Посмотрите описание команды CLI для создания пользователя:

        ```bash
        {{ yc-mdb-ms }} user create --help
        ```

    1. Укажите параметры пользователя в команде создания (в примере приведены не все доступные параметры):

        ```bash
        {{ yc-mdb-ms }} user create <имя пользователя> \
           --cluster-name=<имя кластера> \
           --password=<пароль пользователя> \
           --databases=<список баз, к которым пользователь должен иметь доступ>
        ```

        Где:

        * `--cluster-name` — имя кластера.
            Имя кластера можно запросить со [списком кластеров в каталоге](cluster-list.md#list-clusters).
        * `--password` — пароль пользователя.
            Длина пароля от 8 до 128 символов.
        * `--databases` — [список имен баз данных](./databases.md#list-db), к которым пользователь должен иметь доступ.

        {% include [user-name-limits](../../_includes/mdb/mms/note-info-user-name-limits.md) %}

- Terraform

    1. Откройте актуальный конфигурационный файл {{ TF }} с планом инфраструктуры.

        О том, как создать такой файл, см. в разделе [{#T}](./cluster-create.md).

    1. Добавьте к описанию кластера {{ mms-name }} блок `user`.

        ```hcl
        resource "yandex_mdb_sqlserver_cluster" "<имя кластера>" {
          ...
          user {
            name     = "<имя пользователя>"
            password = "<пароль>"
          }
        }
        ```

        {% include [user-name-and-passwords-limits](../../_includes/mdb/mms/note-info-user-name-and-pass-limits.md) %}

    1. Проверьте корректность настроек.

        {% include [terraform-validate](../../_includes/mdb/terraform/validate.md) %}

    1. Подтвердите изменение ресурсов.

        {% include [terraform-apply](../../_includes/mdb/terraform/apply.md) %}

    Подробнее см. в [документации провайдера {{ TF }}]({{ tf-provider-mms }}).

    {% include [Terraform timeouts](../../_includes/mdb/mms/terraform/timeouts.md) %}

- API

  Воспользуйтесь методом API [create](../api-ref/User/create.md) и передайте в запросе:
  * Идентификатор кластера, в котором вы хотите создать пользователя в параметре `clusterId`. Чтобы узнать идентификатор, [получите список кластеров в каталоге](cluster-list.md#list-clusters).
  * Имя пользователя в параметре `userSpec.name`.
  * Пароль пользователя в параметре `userSpec.password`.

      {% include [username-and-password-limits](../../_includes/mdb/mms/note-info-user-name-and-pass-limits.md) %}

  * Одну или несколько баз данных, к которым должен иметь доступ пользователь в одном или нескольких параметрах `userSpec.permissions.databaseName`.
  * [Роли пользователя](grant.md#predefined-db-roles) для каждой из выбранных баз данных в одном или нескольких параметрах `userSpec.permissions.roles`.

{% endlist %}

## Изменить пароль {#change-password}

{% list tabs %}

- Консоль управления

  1. Перейдите на [страницу каталога]({{ link-console-main }}) и выберите сервис **{{ mms-name }}**.
  1. Нажмите на имя нужного кластера и выберите вкладку **Пользователи**.
  1. Нажмите значок ![options](../../_assets/horizontal-ellipsis.svg) и выберите пункт **Изменить пароль**.
  1. Задайте новый пароль и нажмите кнопку **Изменить**.

  {% include [password-limits](../../_includes/mdb/mms/note-info-password-limits.md) %}

- CLI

    {% include [cli-install](../../_includes/cli-install.md) %}

    {% include [default-catalogue](../../_includes/default-catalogue.md) %}

    Чтобы изменить пароль пользователя, выполните команду:

    ```bash
    {{ yc-mdb-ms }} user update <имя пользователя> \
       --cluster-name=<имя кластера> \
       --password=<новый пароль>
    ```

    Имя кластера можно запросить со [списком кластеров в каталоге](cluster-list.md#list-clusters).

    {% include [password-limits](../../_includes/mdb/mms/note-info-password-limits.md) %}

- Terraform

    1. Откройте актуальный конфигурационный файл {{ TF }} с планом инфраструктуры.

        О том, как создать такой файл, см. в разделе [{#T}](./cluster-create.md).

    1. Найдите в описании кластера {{ mms-name }} блок `user` для нужного пользователя.

    1. Измените значение поля `password`:

        ```hcl
        resource "yandex_mdb_sqlserver_cluster" "<имя кластера>" {
          ...
          user {
            name     = "<имя пользователя>"
            password = "<пароль>"
          }
        }
        ```

        {% include [passwords-limits](../../_includes/mdb/mms/note-info-password-limits.md) %}

    1. Проверьте корректность настроек.

        {% include [terraform-validate](../../_includes/mdb/terraform/validate.md) %}

    1. Подтвердите изменение ресурсов.

        {% include [terraform-apply](../../_includes/mdb/terraform/apply.md) %}

    Подробнее см. в [документации провайдера {{ TF }}]({{ tf-provider-mms }}).

    {% include [Terraform timeouts](../../_includes/mdb/mms/terraform/timeouts.md) %}

- API

  Воспользуйтесь методом API [update](../api-ref/User/update.md) и передайте в запросе:
  * Идентификатор кластера, в котором находится пользователь в параметре `clusterId`. Чтобы узнать идентификатор, [получите список кластеров в каталоге](cluster-list.md#list-clusters).
  * Имя пользователя в параметре `userName`. Чтобы узнать имя пользователя, [получите список пользователей в кластере](#list-users).
  * Новый пароль пользователя в параметре `password`.

      {% include [password-limits](../../_includes/mdb/mms/note-info-password-limits.md) %}

  - Список полей конфигурации пользователя подлежащих изменению (в данном случае — `password`) в параметре `updateMask`.

  {% note warning %}

  Этот метод API сбросит все настройки пользователя, которые не были явно переданы в запросе, на значения по умолчанию.
  Чтобы избежать этого, обязательно передайте название поля пароля пользователя — `password` — в параметре `updateMask`.

  {% endnote %}

{% endlist %}

## Изменить настройки пользователя {#update-settings}

{% list tabs %}

- Консоль управления

  1. Перейдите на [страницу каталога]({{ link-console-main }}) и выберите сервис **{{ mms-name }}**.
  1. Нажмите на имя нужного кластера и выберите вкладку **Пользователи**.
  1. Нажмите значок ![image](../../_assets/horizontal-ellipsis.svg) и выберите пункт **Настроить**.
  1. Настройте права пользователя на доступ к определенным базам данных:
     1. Чтобы предоставить доступ к требуемым базам данных:
        1. Нажмите кнопку **Добавить базу данных**.
        1. Выберите базу данных из выпадающего списка.
        1. Повторите два предыдущих шага, пока не будут выбраны все требуемые базы данных.
     1. Чтобы отозвать доступ к определенной базе, удалите ее из перечня, нажав значок ![image](../../_assets/cross.svg) справа от имени базы данных.
  1. Задайте нужные роли пользователя для каждой из выбранных баз данных.
  1. Нажмите кнопку **Сохранить**.

- CLI

    {% include [cli-install](../../_includes/cli-install.md) %}

    {% include [default-catalogue](../../_includes/default-catalogue.md) %}

    Чтобы настроить права пользователя на доступ к определенным базам данных, выполните команду, перечислив список имен баз данных в параметре `--databases`:

    ```bash
    {{ yc-mdb-ms }} user update <имя пользователя> \
       --cluster-name=<имя кластера> \
       --databases=<список баз, к которым пользователь должен иметь доступ>
    ```

    Имя кластера можно запросить со [списком кластеров в каталоге](cluster-list.md#list-clusters), имена баз — со [списком баз в кластере](databases.md#list-db).

    Эта команда предоставляет пользователю доступ к базам данных, указанным в списке.

    Чтобы отозвать доступ к базе, передайте в аргументе `--databases` список, из которого эта база исключена.

- Terraform

    Чтобы настроить права пользователя на доступ к определенным базам данных:

    1. Откройте актуальный конфигурационный файл {{ TF }} с планом инфраструктуры.

        О том, как создать такой файл, см. в разделе [{#T}](./cluster-create.md).

    1. Добавьте необходимое количество блоков `permission` к описанию пользователя кластера — по одному на каждую базу:

        ```hcl
        resource "yandex_mdb_sqlserver_cluster" "<имя кластера>" {
          ...
          user {
            name     = "<имя пользователя>"
            password = "<пароль>"

            permission {
              database_name = "<имя базы>"
              roles         = ["<список ролей пользователя>"]
            }
          }
        }
        ```

    1. Проверьте корректность настроек.

        {% include [terraform-validate](../../_includes/mdb/terraform/validate.md) %}

    1. Подтвердите изменение ресурсов.

        {% include [terraform-apply](../../_includes/mdb/terraform/apply.md) %}

    Подробнее см. в [документации провайдера {{ TF }}]({{ tf-provider-mms }}).

    {% include [Terraform timeouts](../../_includes/mdb/mms/terraform/timeouts.md) %}

- API

  Воспользуйтесь методом API [update](../api-ref/User/update.md) и передайте в запросе:
  * Идентификатор кластера, в котором находится пользователь в параметре `clusterId`. Чтобы узнать идентификатор, [получите список кластеров в каталоге](cluster-list.md#list-clusters).
  * Имя пользователя в параметре `userName`. Чтобы узнать имя пользователя, [получите список пользователей в кластере](#list-users).
  * Новые значения настроек пользователя.
  * Список полей конфигурации пользователя подлежащих изменению в параметре `updateMask`.

  {% note warning %}

  Этот метод API сбросит все настройки пользователя, которые не были явно переданы в запросе, на значения по умолчанию.
  Чтобы избежать этого, перечислите настройки, которые вы хотите изменить, в параметре `updateMask` (одной строкой через запятую).

  {% endnote %}

{% endlist %}

Пошаговые инструкции по настройке ролей пользователей представлены в разделе [Назначение привилегий и ролей пользователям](./grant.md#grant-role).

## Удалить пользователя {#removeuser}

{% list tabs %}

- Консоль управления

  1. Перейдите на [страницу каталога]({{ link-console-main }}) и выберите сервис **{{ mms-name }}**.
  1. Нажмите на имя нужного кластера и выберите вкладку **Пользователи**.
  1. Нажмите значок ![image](../../_assets/horizontal-ellipsis.svg) и выберите пункт **Удалить**.
  1. Подтвердите удаление пользователя.

- CLI

    {% include [cli-install](../../_includes/cli-install.md) %}

    {% include [default-catalogue](../../_includes/default-catalogue.md) %}

    Чтобы удалить пользователя, выполните команду:

    ```bash
    {{ yc-mdb-ms }} user delete <имя пользователя> \
       --cluster-name=<имя кластера>
    ```

    Имя кластера можно запросить со [списком кластеров в каталоге](cluster-list.md#list-clusters).

- Terraform

    1. Откройте актуальный конфигурационный файл {{ TF }} с планом инфраструктуры.

        О том, как создать такой файл, см. в разделе [{#T}](cluster-create.md).

    1. Удалите из описания кластера {{ mms-name  }} блок `user` с описанием нужного пользователя.

    1. Проверьте корректность настроек.

        {% include [terraform-validate](../../_includes/mdb/terraform/validate.md) %}

    1. Подтвердите изменение ресурсов.

        {% include [terraform-apply](../../_includes/mdb/terraform/apply.md) %}

    Подробнее см. в [документации провайдера {{ TF }}]({{ tf-provider-mms }}).

    {% include [Terraform timeouts](../../_includes/mdb/mms/terraform/timeouts.md) %}

- API

  Воспользуйтесь методом API [delete](../api-ref/User/delete.md) и передайте в запросе:
  * Идентификатор кластера, в котором находится пользователь в параметре `clusterId`. Чтобы узнать идентификатор, [получите список кластеров в каталоге](cluster-list.md#list-clusters).
  * Имя пользователя в параметре `userName`. Чтобы узнать имя пользователя, [получите список пользователей в кластере](#list-users).

{% endlist %}

{% include [user-ro](../../_includes/mdb/mms-user-examples.md) %}

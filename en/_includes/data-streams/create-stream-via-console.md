{% list tabs %}

- Management console

    1. In the [management console]({{ link-console-main }}), select the folder where you want to create a stream.

    1. Select **{{ yds-full-name }}**.

    1. Click **Create stream**.

    1. Specify a [serverless](../../managed-ydb/concepts/serverless-and-dedicated.md#serverless) {{ ydb-short-name }} database or [create](../../managed-ydb/quickstart.md#create-db) a new one. If you chose to create a new database, click **Update** after creating it to update the list of databases.

    1. Enter the name of the stream. Naming requirements:

        {% include [name-format](../../_includes/name-format.md) %}

    1. Specify the number of [data shards](../../data-streams/concepts/glossary.md#shard).

        {% note warning %}

        You can't reduce the number of shards for the created stream.

        {% endnote %}

    1. Set the maximum [shard throughput](../../data-streams/concepts/glossary.md#shard-thoughput). A stream's throughput is equal to the product of the number of shards by the throughput of each of them.

    1. Specify the maximum [data retention period](../../data-streams/concepts/glossary.md#retention-time) in the stream.

    1. Click **Create**.

    Wait for the stream to start. Once the stream is ready for use, its status changes from `CREATING` to `ACTIVE`.

{% endlist %}


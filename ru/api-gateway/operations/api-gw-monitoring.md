---
title: "Просмотр графиков мониторинга в {{ api-gw-full-name }}"
description: "Вы можете посмотреть графики мониторинга в {{ api-gw-full-name }} для таких показателей, как количество запросов к API-шлюзу, количество ошибок, возникших при обращении к API-шлюзу, и время выполнения запросов к API-шлюзу. Чтобы посмотреть график, откройте раздел {{ api-gw-name }} в каталоге с API-шлюзом, информацию о котором вы хотите получить. В открывшемся окне выберите API-шлюз, графики мониторинга которого вы хотите посмотреть."
---

# Мониторинг

Вы можете отслеживать состояние API-шлюзов с помощью инструментов мониторинга в консоли управления. Эти инструменты предоставляют диагностическую информацию в виде графиков.

Период обновления графиков — 15 секунд.

## Посмотреть графики мониторинга {#charts}

{% list tabs %}

- Консоль управления 

	1. В [консоли управления]({{ link-console-main }}) перейдите в каталог, в котором находится API-шлюз. 
	1. Откройте сервис **{{ api-gw-name }}**.
	1. Выберите API-шлюз, графики мониторинга которого хотите посмотреть.
	1. Перейдите на вкладку **Мониторинг**.
	1. На странице появятся следующие графики:

		* **Requests** — количество обращений к API-шлюзу.

    	   ![image](../../_assets/api-gateway/requests.png)

    	* **Errors** — количество ошибок, возникших при обращении к API-шлюзу.

           ![image](../../_assets/api-gateway/errors.png)

    	* **Latency** — время выполнения запросов к API-шлюзу.
    
    	   ![image](../../_assets/api-gateway/latency.png)

		Вы можете выбрать период, за который необходимо отобразить информацию на графике: час, 3 часа, день, неделя, месяц или произвольный период.

{% endlist %}

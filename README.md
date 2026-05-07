# Big Data Flink

Процесс формирования снежинки был перенесён в Flink.

Все csv файлы парсятся и редактируются внутри Jupyter Notebook'а `kafka.ipynb`. Создаётся Producer в `data-topic`, который
отправляет всю информацию о таблице mock_data.

Затем Flink создаёт Consumer'а для Kafka топика `data-topic` и начинает обработку в снежинку через Table API.

После обработки и создания Statement Set'а, он выполняется с настройками на Parallelism = 5. Все данные синхронизируются
и параллельно вставляются, чтобы не нарушались Foreign Keys.

Инструкция:
1) Запустить Docker: `docker-compose up`
2) Подключиться к Jupyter Notebook'у через `localhost:8888` с токеном: `77b1e2a0561f125aafe62686a954b64f33a00e5c81b99700`
3) Открыть файл `./work/kafka.ipynb` и запустить все ячейки
4) Открыть файл `./work/snowflake-flink-job.ipynb` и запустить все ячейки
5) Запустить DBeaver и подключиться к PostgreSQL (порт `5433`) по логину и паролю: `postgres:admin`.
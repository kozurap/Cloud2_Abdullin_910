# Cloud2_Abdullin_910


1.создать сервисный аккаунт с ролями admin, serverless.functions.invoker

2.сгенерировать ключи доступа и API ключи к аккаунту

3.создать бакет itis-2022-2023-vvot15-photos

4.создать к нему триггер vvot15-photo-trigger, запускающий функцию vvot15-face-detection, когда в бакете появляется новый файл с суффиксом .jpg

5.в функцию скопировать код из vvot15-face-detection.py, в 47 строке вместо * подставить API ключ сервисного аккаунта

6.добавить переменные окружения AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY

7.выбрать сервисный аккаунт созданный нами

8.создать очередь vvot15-tasks

9.создать serverless базу данных, таблицу в ней на три колонки, face(PK), name, orig. Тип String.

Создать API Gateway, скопировать туда содержимое файла gateway
Создать container registry
Сконфигурируйте Docker командой в консоли yc container registry configure-docker
Скачать файлы dockerfile и index.py в одну папку. Сгенерировать файл с ключами сервисного аккаунта командой: yc iam key create --folder-id {folder-id} --service-account-name serv-acc-photo --output /keys.json
Создать образ docker build . -t cr.yandex/crpmnm7hi1vei5ms7qjb/vvot15
Запушить в регистр docker push cr.yandex/crpmnm7hi1vei5ms7qjb/vvot15:latest
Создать контейнер vvot15-face-cut по загруженному образу и с переменными окружения AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, SA_KEY_FILE=/vvot33-admin.json
Создать триггер vvot15-task-trigger, на очередь tasks запускающий контейнер
создать функцию vvot15-boot скопировать туда код из репозитория. Добавить requirements.txt с необходимыми библиотеками, добавить в переменные окружения значения AWS_ACCESS_KEY_ID и AWS_SECRET_ACCESS_KEY взятые из сервисного аккаунта с ролью admin, YDB_DATABASE и YDB_ENDPOINT взятые из параметров базы данных vvot15-db-photo-face, API_GATEWAY служебный домен взятый из itis-2022-2023-vvot15-api
В Telegram создать бота через @BotFather и получить token. Создать Webhook вставив значения в ссылку https://api.telegram.org/bot{токен}/setWebhook?url={вызов функции ссыль"vvot15-boot"}

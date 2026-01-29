📊 Observability & Microservices Stack

Проект содержит микросервисы (mc1, mc2, mc3) с мониторингом и логированием через Prometheus, Grafana, Loki, Kafka и MariaDB. Всё контейнеризовано через Docker.


---

| Компонент                            | Описание                                 |
| ------------------------------------ | ---------------------------------------- |
| `mc1`, `mc2`, `mc3`                  | Микросервисы приложения                  |
| Prometheus                           | Сбор метрик с сервисов и экспортёров     |
| Grafana                              | Визуализация метрик и дашбордов          |
| Loki                                 | Централизованное логирование контейнеров |
| Alloy                                | Сбор логов из Docker и отправка в Loki   |
| Kafka                                | Система обмена сообщениями               |
| MariaDB                              | База данных для приложения               |
| `kafka-exporter`, `mariadb-exporter` | Экспортёры метрик для Prometheus         |


---

🕹️Подготовка окружения

# --- MC1 ---
MC1_DATABASE_URL=jdbc:mariadb://mariadb:3306/events_db
MC1_DATABASE_PASSWORD=password
MC1_DATABASE_USER=user
MC1_DURATION_SECOND=5
MC1_PORT=8000
MC1_WS_URI=ws://mc2:8080/ws

# --- MC2 ---
MC2_KAFKA_ADDRESS=kafka:9092
MC2_KAFKA_TOPIC_NAME=MC2-to-MC3
MC2_ADDRESS=0.0.0.0
MC2_PORT=8080

# --- MC3 ---
MC3_WEBCLIENT_BASE_URL=http://mc1:8000
MC3_WEBCLIENT_TIMEOUT=1000
MC3_KAFKA_ADDRESS=kafka:9092
MC3_KAFKA_CONSUMER_GROUP=test-group
MC3_KAFKA_CONSUMER_TOPICS=MC2-to-MC3
MC3_TRUSTED_PACKAGES=*
MC3_POST_URI=/message/receive
MC3_APPLICATION_PORT=8081


---

🚀Масштабный запуск через Docker Compose
# Из корня проекта
docker compose up -d --build


🔹 Флаг --build гарантирует, что свежесобранные .jar файлы попадут в образы.


---

🟢Масштабный запуск через Docker Compose
docker compose up -d --build


🔹 Флаг --build гарантирует, что свежесобранные .jar файлы попадут в образы.

🔹 В Docker Compose подняты все сервисы: prometheus, grafana, zookeeper, kafka, mariadb, kafka-exporter, mariadb-exporter, mc2, mc1, mc3, loki, alloy. Все работают в одной сети observability-net.


---


🛜Доступ к сервисам
Сервис	URL

Grafana	http://localhost:3000

(user: admin, pass: admin)

Prometheus	http://localhost:9090

Loki	http://localhost:3100

Alloy	http://localhost:9080


---

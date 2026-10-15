# MLflow server

Postgres хранит метаданные (runs, params, metrics), артефакты лежат на диске хоста в `data/artifacts/`

## Запуск

```bash
cd mlflow-server
cp .env.example .env        # и поменять POSTGRES_PASSWORD
docker compose up -d --build
```

UI: http://127.0.0.1:5000

Адрес задаётся в `.env`:
- `MLFLOW_BIND_HOST` - на каком интерфейсе хоста слушать;
- `MLFLOW_PORT` - порт на хосте;
- `MLFLOW_ALLOWED_HOSTS` - какие значения заголовка `Host` сервер принимает. Если открываете UI по другому имени или IP, добавьте его сюда, например `...,192.168.1.10:*`

Остановка: `docker compose down`. Данные сохраняются: метаданные в томе `dl-mlflow_pgdata`,
артефакты в `data/artifacts/`. Команда `docker compose down -v` удалит только метаданные
(runs пропадут из UI, файлы артефактов останутся).

Бэкап метаданных:
```bash
docker compose exec db sh -c 'pg_dump -U "$POSTGRES_USER" "$POSTGRES_DB"' > mlflow-backup.sql
```

## Клиент

`mlflow` для домашки ставится в окружение hwN (`uv add mlflow` в `homeworks/hwN/`). Версия должна совпадать с серверной (см. `uv.lock` здесь)

```python
import mlflow
mlflow.set_tracking_uri("http://127.0.0.1:5000")  # или env MLFLOW_TRACKING_URI
mlflow.set_experiment("hw1-baseline")
```

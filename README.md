## deep-learning

Это репозиторий для выполнения и сдачи домашних заданий на курсе глубокого обучения


### Quick start

Для того, чтобы создать .venv с необходимыми для домашнего задания зависимостями, нужно выполнить следующие этапы:

1) Склонировать репозиторий:
```
git clone https://github.com/mematvey/deep-learning.git
cd deep-learning
git switch hwN
```

2) Установить [uv](https://docs.astral.sh/uv/getting-started/installation/)

3) Выполнить:
```
cd homeworks/hwN
uv sync --locked
```

### MLflow

Сервер для логирования лежит в [mlflow-server/](mlflow-server/). Запуск и настройка — в [mlflow-server/README.md](mlflow-server/README.md)
Образ собирается из `mlflow-server/uv.lock` через простой `docker compose up`

### Pre-commit

```
uv tool install pre-commit
pre-commit install
```

# [airflow](https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html)

```shell
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.9.0/docker-compose.yaml'
```

This file contains several service definitions:

- airflow-scheduler - The scheduler monitors all tasks and DAGs, then triggers the task instances once their dependencies are complete.
- airflow-webserver - The webserver is available at http://localhost:8080.
- airflow-worker - The worker that executes the tasks given by the scheduler.
- airflow-init - The initialization service.
- flower - The flower app for monitoring the environment. It is available at http://localhost:5555.
- postgres - The database.
- redis - The redis - broker that forwards messages from scheduler to worker.


```shell
mkdir -p ./dags ./logs ./plugins ./config
echo -e "AIRFLOW_UID=$(id -u)" > .env
```

## Initialize
```shell
docker-compose up airflow-init
```

The account created has the login airflow and the password airflow

## Running Airflow
```shell
docker-compose up -d
docker-compose up flower


$ docker ps

CONTAINER ID   IMAGE                  COMMAND                  CREATED              STATUS                          PORTS                                       NAMES
0d021eb148b8   apache/airflow:2.9.0   "/usr/bin/dumb-init …"   About a minute ago   Up About a minute (healthy)     0.0.0.0:8080->8080/tcp, :::8080->8080/tcp   airflow-airflow-webserver-1
83c4d204b107   apache/airflow:2.9.0   "/usr/bin/dumb-init …"   About a minute ago   Up About a minute (healthy)     8080/tcp                                    airflow-airflow-worker-1
ccd5f4c8983b   apache/airflow:2.9.0   "/usr/bin/dumb-init …"   About a minute ago   Up About a minute (healthy)     8080/tcp                                    airflow-airflow-scheduler-1
2a224d951dec   apache/airflow:2.9.0   "/usr/bin/dumb-init …"   About a minute ago   Up About a minute (healthy)     8080/tcp                                    airflow-airflow-triggerer-1
33c1969d1d12   apache/airflow:2.9.0   "/bin/bash -c 'if [[…"   3 minutes ago        Exited (0) About a minute ago                                               airflow-airflow-init-1
1ded58c5770f   postgres:13            "docker-entrypoint.s…"   3 minutes ago        Up 3 minutes (healthy)          5432/tcp                                    airflow-postgres-1
7687f414e699   redis:latest           "docker-entrypoint.s…"   3 minutes ago        Up 3 minutes (healthy)          6379/tcp                                    airflow-redis-1
```


## Custom image
https://airflow.apache.org/docs/docker-stack/build.html#build-build-image


## Plug-ins
https://airflow.apache.org/docs/apache-airflow/stable/extra-packages-ref.html
https://airflow.apache.org/docs/apache-airflow-providers-jdbc/stable/operators.html

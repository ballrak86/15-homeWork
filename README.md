## Описание файлов в директории
logFileFull.log - полный лог выполнения  
used_commands.txt - команды которые использовал  

screenshot.jpg - скриншот dashboard

## Краткое описание проделанной работы
Скачал файлы prometheus и node_exporter с официального сайта и сложил все в /bin/  
Поправил настройки prometheus.yml и добавил обработку node_exporter
```
[root@vm-gkuOA1801016 node_exporter-1.2.2.linux-amd64]# cat /etc/prometheus/prometheus.yml
# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
          # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["localhost:9090"]

   - job_name: node
    static_configs:
      - targets: ['localhost:9100']
```
Запустил node_exporter и prometheus (указал файл конфига и папку куда складывать базу данных)
```
node_exporter &
prometheus --config.file=/etc/prometheus/prometheus.yml --storage.tsdb.path /var/lib/prometheus/ &
```
Настроил data sourse и dashboard в grafana. Получил скриншот.


📚Домашнее задание/проектная работа разработано(-на) для курса ["Administrator Linux. Professional"](https://otus.ru/lessons/linux-professional/)
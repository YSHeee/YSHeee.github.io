# Prometheus + Grafana
```yaml title="docker-compose.yml"
version: "3.9"
services:
  api-web:
    build: .
    environment:
     - NUM=4000
    ports:
      - "13583:13583"
    command:
      - "uvicorn"
      - "app.main:app"
      - "--host"
      - "0.0.0.0"
      - "--port"
      - "13583"

  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"

  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    depends_on:
      - prometheus

```




!!!quote
    - Github<div>
      • [Prometheus](https://prometheus.io/)<div>
      • [Grafana](https://grafana.com/docs/grafana-cloud/quickstart/docker-compose-linux/)<div>
      • [prometheus-fastapi-instrumentator](https://github.com/trallnag/prometheus-fastapi-instrumentator)<div>
      • [client_python](https://github.com/prometheus/client_python)
    - Useful<div>
      • [Github-1](https://github.com/docker/awesome-compose/tree/master/prometheus-grafana)<div>
      • [stack-1](https://stackoverflow.com/questions/74029504/spring-prometheus-grafana-err-reading-prometheus-post-http-localhost90)<div>
      • [Blog-1](https://medium.com/@ct.onyemaobi/build-and-monitor-your-fastapi-microservice-with-docker-prometheus-and-grafana-part-2-37472157a2b)<div>
      • [Blog-2](https://umanking.github.io/2021/08/19/prometheus-grafana-example/)<div>
      • [Blog-3](https://docs.netapp.com/ko-kr/storagegrid-116/monitor/commonly-used-prometheus-metrics.html)

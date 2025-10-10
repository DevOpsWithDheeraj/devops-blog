
---

🧠 1. Introduction to Prometheus and Grafana

🔹 Prometheus

What it is: An open-source monitoring and alerting system designed for time-series data.

Developed by: SoundCloud (now part of CNCF, like Kubernetes).

Key Concept: Prometheus pulls metrics from targets via HTTP endpoints (usually /metrics).


🔹 Grafana

What it is: An open-source data visualization and dashboarding tool.

Purpose: To visualize metrics collected by Prometheus, Loki, InfluxDB, etc.

Key Feature: Interactive charts, alerts, panels, and templates.



---

⚙️ 2. Prometheus Architecture

Components:

1. Prometheus Server – Scrapes and stores time-series data.


2. Exporters – Expose metrics (e.g., Node Exporter for Linux servers).


3. Alertmanager – Handles alerts and sends notifications (Slack, Email, PagerDuty).


4. Pushgateway – For short-lived jobs (e.g., batch jobs).


5. Service Discovery – Auto-discovers targets (Kubernetes, EC2, Consul, etc.).



📊 Data Flow Example:

[Node Exporter] ---> [Prometheus Server] ---> [Grafana Dashboard]
                              |
                         [Alertmanager]


---

💻 3. Installing Prometheus and Grafana

🐧 Prometheus Installation on Linux

# Step 1: Download Prometheus
wget https://github.com/prometheus/prometheus/releases/latest/download/prometheus-linux-amd64.tar.gz
tar xvf prometheus-linux-amd64.tar.gz
cd prometheus-*

# Step 2: Run Prometheus
./prometheus --config.file=prometheus.yml

Default UI: http://localhost:9090


⚙️ prometheus.yml (basic config)

global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'node'
    static_configs:
      - targets: ['localhost:9100']


---

📦 4. Exporters

Exporters collect metrics from different systems.

Exporter	Purpose	Default Port

Node Exporter	OS metrics (CPU, RAM, Disk)	9100
cAdvisor	Container metrics	8080
Blackbox Exporter	Probe HTTP, DNS, TCP endpoints	9115
MySQL Exporter	Database metrics	9104
JMX Exporter	Java app metrics	5556


📘 Example: Install Node Exporter

wget https://github.com/prometheus/node_exporter/releases/latest/download/node_exporter-linux-amd64.tar.gz
tar xvf node_exporter-linux-amd64.tar.gz
cd node_exporter-*
./node_exporter &


---

📊 5. Grafana Installation

🧩 Install (on Linux)

sudo apt-get install -y adduser libfontconfig1
wget https://dl.grafana.com/oss/release/grafana_10.0.0_amd64.deb
sudo dpkg -i grafana_10.0.0_amd64.deb
sudo systemctl start grafana-server
sudo systemctl enable grafana-server

Access: http://localhost:3000

Default credentials: admin / admin


➕ Add Prometheus as Data Source

Go to Configuration → Data Sources → Add Data Source → Prometheus

URL: http://localhost:9090

Click Save & Test



---

📈 6. Create Grafana Dashboard

Example Query (PromQL)

PromQL = Prometheus Query Language

rate(node_cpu_seconds_total{mode="idle"}[5m])

👉 Shows average CPU idle time over last 5 minutes.

Common Queries:

Metric	Query

CPU Usage	100 - (avg by(instance)(rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
Memory Usage	(node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) / node_memory_MemTotal_bytes * 100
Disk Usage	(node_filesystem_size_bytes - node_filesystem_free_bytes) / node_filesystem_size_bytes * 100
Uptime	node_time_seconds - node_boot_time_seconds



---

🚨 7. Alerts with Prometheus and Grafana

📁 Alert Rule Example (prometheus.yml)

rule_files:
  - "alert.rules.yml"

🧾 alert.rules.yml

groups:
- name: InstanceDown
  rules:
  - alert: InstanceDown
    expr: up == 0
    for: 1m
    labels:
      severity: critical
    annotations:
      summary: "Instance {{ $labels.instance }} is down"
      description: "Target {{ $labels.instance }} has been down for 1 minute."

📤 Integrate with Alertmanager

Define notification receivers (Slack, Email, etc.)

Example Slack config:


receivers:
- name: 'slack'
  slack_configs:
  - send_resolved: true
    channel: '#alerts'
    api_url: 'https://hooks.slack.com/services/xxxx/yyyy/zzzz'


---

🧠 8. Advanced Prometheus Topics

Feature	Description

Service Discovery	Auto-detect targets in Kubernetes, EC2, Consul.
Recording Rules	Precompute expensive queries for better performance.
Relabeling	Rename or drop metrics dynamically.
Remote Storage	Integrate with long-term storage (Thanos, Cortex, Mimir).
Pushgateway	For short-lived jobs to push metrics.
Federation	Aggregate metrics from multiple Prometheus servers.



---

💡 9. Advanced Grafana Topics

Feature	Description

Variables & Templates	Dynamic dashboards using variables (e.g., $instance).
Annotations	Highlight events on graphs (e.g., deployments).
Provisioning	Automate dashboard and data source setup via YAML.
Alerting	Unified alerting system to send alerts via Email, Slack, Teams.
Plugins	Extend Grafana with extra visualizations or datasources.
Grafana Loki	Log aggregation system (works like Prometheus for logs).



---

🚀 10. Real-World DevOps Use Case

🧩 Monitor Kubernetes Cluster

Deploy Prometheus + Grafana via Helm:

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install monitoring prometheus-community/kube-prometheus-stack

Monitors:

CPU, Memory, Pod status, Node status

Alerts for node down, high usage

Dashboards auto-created in Grafana




---

🧰 11. Integration Examples

Tool	Integration Purpose

Jenkins	Monitor job failures, build times
Docker	Monitor container performance via cAdvisor
AWS CloudWatch	Import AWS metrics into Grafana
Elasticsearch / Loki	Visualize logs alongside metrics
Ansible	Automate installation/config of Prometheus & Grafana



---

🧾 12. Summary

Tool	Purpose

Prometheus	Metric collection & alerting
Grafana	Visualization & dashboards
Node Exporter	System-level metrics
Alertmanager	Alert delivery
Pushgateway	For short-lived jobs
Loki	Log management


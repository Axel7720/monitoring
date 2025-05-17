# 📊 Monitoring Module

## Описание

Этот модуль предназначен для настройки централизованной системы **мониторинга и логирования** инфраструктуры и приложений. Мониторинг развёрнут **на отдельном сервере (srv)**, чтобы в случае сбоя Kubernetes-кластера мы всё равно могли отслеживать его состояние и получать уведомления.

Используемые инструменты:

- **Prometheus** — сбор метрик с node-экспортеров и blackbox-проб
- **Grafana** — визуализация метрик и логов
- **Alertmanager** — отправка уведомлений при сбоях
- **Loki + Promtail** — сбор и хранение логов с серверов и подов
- **Blackbox Exporter** — проверка доступности внешних HTTP/HTTPS сервисов

---

## Структура проекта

monitoring/
├── prometheus/
│ ├── prometheus.yml # Основная конфигурация Prometheus
│ ├── alert_rules.yml # Правила алертов
├── loki/
│ ├── docker-compose.yml # Docker Compose для Loki и Promtail
│ └── config/
│ └── promtail-config.yaml
├── grafana/
│ └── docker-compose.yml # Запуск Grafana
├── alertmanager/
│ └── config.yml # Конфигурация алертов (email, Telegram и пр.)

Метрики и алерты

Мониторинг покрывает:

Состояние подов и нод в Kubernetes
Доступность веб-приложений через Blackbox Exporter
Состояние хоста srv: CPU, RAM, диски (Node Exporter)
Наличие и корректность TLS-сертификатов
Время отклика приложений


В ходе проекта проведена проверка
На http://<srv-IP>:9093 → UI Alertmanager

Создано "падение" инстанса — временно остановлен pod (скриншот proverka_alerta)


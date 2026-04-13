---
title: "Observability i Kubernetes: Prometheus, Grafana og Loki"
description: "Uten god observability flyr du blind i produksjon. Her er vår anbefalte stack for norske Kubernetes-miljøer."
image: "/images/blog-3.jpg"
date: 2026-02-20T08:00:00Z
draft: false
categories:
  - Observability
tags:
  - prometheus
  - grafana
  - loki
  - kubernetes
---

Observability handler om å forstå hva som skjer i systemene dine, basert på metrikker, logger og traces. I Kubernetes er dette ekstra viktig fordi du har mange pods og noder å holde styr på.

## Den klassiske stacken

**Prometheus** scraper metrikker fra pods og noder. Med `kube-prometheus-stack` (Helm-chart fra prometheus-community) får du Prometheus, Alertmanager og Grafana samlet i én pakke.

**Grafana** visualiserer metrikkene og lar deg bygge dashboards for alt fra node-ressursbruk til applikasjonsspesifikke metrikker.

**Loki** aggregerer logger fra alle pods uten å indeksere innholdet, noe som gjør det langt billigere å drifte enn Elasticsearch-baserte løsninger.

## Viktige metrikker å overvåke

- CPU og minnebruk per pod og node
- Request rate, error rate og latency (RED-metrikker)
- PVC-kapasitet
- Certificate expiry (cert-manager metrics)
- etcd-helse og API server latency

## Alerting

Sett opp alerter for det som faktisk betyr noe, ikke for absolutt alt. For mange alerter uten tydelige handlingspunkter fører til alert fatigue. Start med `KubePodCrashLooping`, høy minnebruk og diskkapasitet.

---

Vi hjelper gjerne med å sette opp en komplett observability-stack. post@kiban.no.

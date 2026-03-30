---
title: "Kom i gang med Kubernetes i produksjon de viktigste grepene"
description: "Kubernetes er kraftfullt, men det er mye som kan gå galt i produksjon. Her er våre viktigste anbefalinger for å lykkes."
image: "/images/blog-1.jpg"
date: 2026-01-15T08:00:00Z
draft: false
categories:
  - Kubernetes
tags:
  - kubernetes
  - produksjon
  - platform-engineering
---

Mange virksomheter setter opp Kubernetes i dev og staging uten store problemer, men møter veggen når de skal kjøre i produksjon. Her er de grepene vi mener er mest kritiske.

## 1. Resource requests og limits

Sett alltid `requests` og `limits` på alle containere. Uten requests vet scheduleren ikke hvordan den skal plassere pods, og uten limits kan én buggy applikasjon ta ned hele noden.

```yaml
resources:
  requests:
    cpu: "100m"
    memory: "128Mi"
  limits:
    cpu: "500m"
    memory: "512Mi"
```

## 2. Liveness og readiness probes

En pod som er oppe men ikke svarer bør trekkes ut av load balanceren og eventuelt restartes. Dette håndteres av probes og det er overraskende mange som ikke setter disse opp skikkelig.

## 3. Pod Disruption Budgets

Sørg for at du alltid har minst én instans av kritiske tjenester oppe under node-vedlikehold. `PodDisruptionBudget` er din venn.

## 4. Namespace-oppdeling og RBAC

Del opp workloads i namespaces og gi hvert team minimalt nødvendige rettigheter. Det er mye enklere å stramme inn tidlig enn å låse ned etter at noe har gått galt.

## 5. Overvåking fra dag én

Installer Prometheus og Grafana fra starten. Det er langt enklere å feilsøke en produksjonshendelse når du har historiske metrikker.

---

Lurer du på hvordan dette ser ut i praksis for din virksomhet? [post@kiban.no](mailto:post@kiban.no) for en uforpliktende prat.

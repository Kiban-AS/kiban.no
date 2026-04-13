---
title: "GitOps med ArgoCD: kontinuerlig levering uten manuell håndtering"
description: "GitOps er prinsippet om at Git er sannhetskilden for infrastruktur og applikasjonskonfigurasjon. ArgoCD gjør dette enkelt i Kubernetes."
image: "/images/blog-2.jpg"
date: 2026-02-05T08:00:00Z
draft: false
categories:
  - DevOps
tags:
  - gitops
  - argocd
  - ci-cd
---

GitOps har blitt standarden for mange plattformteam, og med god grunn. Når Git er sannhetskilden for hva som skal kjøre i clusteret ditt, blir deploy-prosessen sporbar, reproduserbar og enkel å rulle tilbake.

## Hva er GitOps?

GitOps betyr at all konfigurasjon, som applikasjonsmanifester, Helm-charts og Kustomize-overlays, bor i Git. En operator (som ArgoCD) synkroniserer clusteret mot det som er i Git. Ønsket tilstand er aldri lenger enn en `git push` unna.

## Hvorfor ArgoCD?

ArgoCD er Kubernetes-native og har et ryddig UI som gjør det enkelt å se hva som er i sync og hva som avviker. Det støtter Helm, Kustomize og plain YAML, og det integrerer sømløst med eksisterende CI-pipelines.

## Vår anbefalte arbeidsflyt

1. Utvikler pusher kode til applikasjonsrepo
2. CI bygger image, tagger med commit-SHA og pusher til registry
3. CI oppdaterer image-tag i konfigurasjonrepo (separat repo)
4. ArgoCD oppdager endringen og synkroniserer mot clusteret

Dette gir et klart skille mellom applikasjonskode og plattformkonfigurasjon.

## Tips for å komme i gang

Start enkelt: ett applikasjonsrepo, ett konfigurasjonrepo, én ArgoCD-instans. Ikke prøv å sette opp multi-cluster og app-of-apps fra dag én. Bygg opp kompleksiteten gradvis.

---

Ønsker du hjelp med å sette opp GitOps i din virksomhet? post@kiban.no.

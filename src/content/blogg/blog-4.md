---
title: "Terraform og Kubernetes: infrastruktur som kode i praksis"
description: "Hvordan vi bruker Terraform til å provisjonere Kubernetes-klynger og tilhørende infrastruktur på en reproduserbar og auditbar måte."
image: "/images/blog-4.jpg"
date: 2026-03-05T08:00:00Z
draft: false
categories:
  - Infrastruktur
tags:
  - terraform
  - infrastruktur-som-kode
  - azure
  - aws
---

Infrastruktur som kode (IaC) er ikke lenger valgfritt for moderne plattformer. Det er forskjellen på å ha kontroll og å fly blind.

## Hvorfor Terraform?

Terraform er provider-agnostisk, har et enormt community og støtter alle store skytjenester. Vi bruker det til å provisjonere AKS (Azure) eller EKS (AWS) klynger, nettverk, IAM-roller og alt annet som hører til.

## Vår mappestruktur

Vi anbefaler å dele Terraform-koden inn i moduler og environments:

```
infrastructure/
├── modules/
│   ├── aks/
│   ├── networking/
│   └── monitoring/
└── environments/
    ├── dev/
    ├── staging/
    └── prod/
```

## State-håndtering

Lagre alltid Terraform state i en remote backend (Azure Blob Storage eller S3) med state locking aktivert. Aldri lagre state lokalt i et prosjekt med flere utviklere.

## Hemmeligheter

Ikke hardkod secrets i Terraform-variabler. Bruk heller Azure Key Vault, AWS Secrets Manager eller HashiCorp Vault, kombinert med dynamiske referanser i Terraform.

## CI/CD for Terraform

Sett opp automatisk `terraform plan` på pull requests slik at teamet kan se hva som vil endres før merge. Kjør `terraform apply` automatisk ved merge til main, gjerne med et manuelt godkjenningssteg i prod.

---

Har du behov for hjelp med IaC? Vi tar gjerne en prat. [post@kiban.no](mailto:post@kiban.no).

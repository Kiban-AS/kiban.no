---
title: "Kubernetes-sikkerhet: de viktigste tiltakene for norske virksomheter"
description: "Sikkerhet i Kubernetes handler om mer enn brannmurer. Her er de viktigste tiltakene vi anbefaler for alle produksjonsmiljøer."
image: "/images/blog-4.jpg"
date: 2026-03-18T08:00:00Z
draft: false
categories:
  - Sikkerhet
tags:
  - kubernetes
  - sikkerhet
  - rbac
  - compliance
---

Kubernetes er bygget for fleksibilitet, men default-konfigurasjonen er ikke spesielt sikker. Her er tiltakene vi alltid anbefaler.

## RBAC og minste privilegiums prinsipp

Gi brukere og tjenester kun de rettighetene de trenger. Unngå `cluster-admin` til alt og alle. Sett opp `RoleBindings` per namespace heller enn `ClusterRoleBindings` der det er mulig.

## Network Policies

Som standard kan alle pods i et cluster kommunisere med hverandre. Det ønsker du sjelden. Implementer `NetworkPolicy`-ressurser for å begrense trafikk til det som faktisk trengs.

## Pod Security

Bruk `SecurityContext` for å hindre at containere kjører som root:

```yaml
securityContext:
  runAsNonRoot: true
  runAsUser: 1000
  readOnlyRootFilesystem: true
```

## Secrets-håndtering

Kubernetes Secrets er base64-kodet, ikke kryptert. For sensitiv data: bruk External Secrets Operator mot Azure Key Vault, AWS Secrets Manager eller HashiCorp Vault.

## Image-skanning

Sett opp Trivy eller Grype i CI-pipelinen for å skanne container-images for kjente sårbarheter. Vurder admission controllers som Kyverno eller OPA Gatekeeper for å håndheve policies i clusteret.

## GDPR og datalagring

For norske virksomheter er det viktig å ha oversikt over hvor data lagres. Sørg for at PVC-er og databaser er i norske eller europeiske datasentre, og at backups er krypterte.

---

Vil du ha en sikkerhetsgjennomgang av din Kubernetes-plattform? post@kiban.no.

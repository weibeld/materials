---
title: "CMP: The Developers Paradise in the Cloud Native World"
desc: ''
updated: 1683907594952
created: 1680028864184
---

## General info

- Date: 23 May 2023
- Event: [[2.records.events.cloud-native-bern-meetup-2023-05-23]]
- Speaker: Reto Hirt, Stadt Zürich

## Summary

Description of the Container Management Platform (CMP) developed by [Organisation und Informatik (OIZ)](https://www.stadt-zuerich.ch/fd/de/index/das_departement/organisation/oiz.html) of [Stadt Zürich](https://www.stadt-zuerich.ch/portal/de/index.html).

CMP is a multi-cloud Kubernetes platform operated with [Google Anthos](https://cloud.google.com/anthos). It's the largest Google Anthos project for the public administration in the EMEA region.

The platform is divided into a Runtime Platform and Delivery Platform:

- Runtime Platform: the Kubernetes clusters running the application workloads
- Delivery Platform: divided into a "Distribute" part, which places workloads in the Runtime Platform and an "Observe" part which collects and displays information from the Runtime Platform

The Runtime Platform consists of Kubernetes and base services including Vault, Falco, Open Policy Agent, PostgreSQL. The Delivery Platform consists of GitLab, Argo CD, Harbor, Keycloak, Prometheus, Grafana, Vault, OpenSearch (logs).

Currently, the Runtime Platform comprises more than 20 Kubernetes clusters (>20) running on-premises in a data centre (on VMware). However, there's the potential to extend the Runtime Platform to public cloud providers such as GCP or Azure. About 140 applications are currently deployed to the Runtime Platform. There's also the potential to use the Delivery Platform for other runtime environments, e.g. an alternative runtime platform.

## References

- https://www.stadt-zuerich.ch/site/klick/de/index/jahresrueckblick-2022.html
- https://www.stadt-zuerich.ch/site/klick/de/index/container-management-plattform.html

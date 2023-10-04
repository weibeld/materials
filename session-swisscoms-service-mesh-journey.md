---
id: 0lmfsf2u3melq401vlgn8mj
title: Swisscom's Service Mesh Journey
desc: ''
updated: 1683911950628
created: 1683909050734
---

## General info

- Date: 11 May 2023
- Event: [[2.records.events.hashicorp-user-group-meetup-2023-05-11]]
- Speaker: Romain Silvestri, Swisscom

## Summary

Description of a project at Swisscom to create a company-wide service mesh service to be used by all applications across the company.

- Motivation for the project: improve networking configuration, security, and monitoring in a uniform way
- Consul (in combination with Envoy) has been selected as the service mesh too because it provides a managed control plane ([HashiCorp Cloud](https://www.hashicorp.com/cloud))
    - Other service mesh candidates were Istio, Linkerd, and Cilium
- Implementation on AWS EKS for applications that are deployed to this platform

## Discussion

## Resources

---
meta:
  created: 2023-06-06T18:38:05+02:00
  edited: 2023-06-06T18:38:05+02:00
data:
  title: How a Fintech bank leverages Elastic Cloud Enterprise (ECE)
  speakers:
    - name: Milad Shkoh
      affiliation: Leonteq
  event: hashicorp-user-group-12-2023-06-06
---

How Leonteq uses Elasticsearch with Elastic Cloud Enterprise (ECE).

ECE allows deploying Elasticsearch and Kibana across different infrastructure.

- Hybrid multi-cloud approach: two on-premises data centres and two different cloud providers
  - Each platform forms a zone across which applications can be deployed
- Use of Terraform for deploying resources
  - ECE provides a Terraform provider
- Use of Ansible for configuring deployed applications
- Use of Vault for managing secrets

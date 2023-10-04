--
meta:
  created: 2023-06-20T18:24:06+02:00
  edited: 2023-06-20T18:24:06+02:00
data:
  title: Automate IaC with LLM Code Generation
  date: 2023-06-20
  speakers:
    - name: Matthias Mertens
      affiliation: Helvetia
  event: '[[event-aws-user-group-basel-meetup-2023-06-20.md]]'
---

- Multi-cloud strategy (AWS and Azure) and switch to Terraform as a unified tool
- Terraform config needs to somehow represent legacy infrastructure
  - Poorly documented, not automated, deployed by hand
- Problem: need to understand the legacy infrastructure
- [Firefly](ps://www.gofirefly.io/)
  - Comercial product: free tier, then starting from $700/month
  - Scans cloud and current Terraform states
  - Generate Terraform config 
    - Also can create code for other IaC tools, such as Pulumi, CloudFormation, Ansible, etc.
  - Allows importing assets (resource IDs, etc.) into Terraform state
  - Allows shaping Terraform config (modules, paramters, etc.)
- Also includes AI agent that allows generating IaC code for resources described in plain text
- Terraform import feature released in v1.5
  - Can be used as an alternative to Firefly
- Based on GPT

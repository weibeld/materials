---
id: zgvyxkyo1owetguiq7af4k8
title: State of the Art Terraform Pipeline for 0 Dollars
desc: ''
updated: 1683907649315
created: 1680031526300
---

## General info

- Date: 28 March 2023
- Event: [[2.records.events.cloud-native-bern-meetup-2023-03-28]]
- Speaker: Stefano Franco, Nuvibit

## Summary

Demonstration of how to build a Terraform pipeline with remote execution of Terraform on [Terraform Cloud](https://developer.hashicorp.com/terraform/cloud-docs).

The main benefits of this architecture are that:

1. The Terraform config is shared and there's only a single source of truth
2. Terraform is run from a central remote location (Terraform Cloud), and never locally, with the shared Terraform config (from GitHub) as input. This ensures that no unreviewed config can be deployed to the infrastructure, and no unwanted actions can be performed (nobody can directly run Terraform against the infrastructure, it can only be run through the pipeline)

Here's how the pipeline is implemented:

- Terraform config is in GitHub repo
- Two GitHub Actions that get triggered on creation and merging of a pull request (PR), respectively
- Create-PR GitHub Action executes checks on Terraform config (formatting, linting, creating docs, security checks) and triggers a `terraform plan` on Terraform Cloud
    - Edits to the Terraform config (e.g. from formatting) are committed back to the PR branch
    - Note that Terraform Cloud also stores the state file
- Human reviewing of the PR includes reviewing the `terraform plan` output from Terraform Cloud
- When the PR is merged, the merge-PR GitHub Action runs `terraform apply`
    - Note that this is the same config that was previously checked with the merge-PR GitHub Action

All of this can be built for free (GitHub Actions is free and Terraform Cloud has a free tier too).

Demo: https://github.com/nuvibit/github-terraform-workflows

### Classical approach

The classical approach to use Terraform in an organisation without Terraform Cloud looks as follows:

- Terraform config in GitHub repo
- Terraform state file in an Amazon S3 bucket
- Terraform is run on the local developer machines
- Amazon DynamoDB is used for state locking, that is, for locking the state file when a Terraform operation is currently ongoing
    - Lock must be acquired before starting a Terraform command (e.g. `terraform plan` or `terraform apply`) and is released after completing the command
    - This is to prevent simultaneous executions of multiple Terraform commands

The problem with this approach is that developers may deploy changes that are not yet committed to the GitHub repository, which may break the deployments of other devs. In general, it also allows undesired or destructive actions (e.g. everybody might run `terraform destroy`).

## Discussion

This approach makes a lot of sense and was a great introduction to Terraform Cloud.

The checks performed in the create-PR may include anything. For example, it would be possible to enforce policies there with Open Policy Agent or [Sentinel](https://www.hashicorp.com/sentinel).

The [terraform-docs](https://terraform-docs.io/) project apparently allows to automatically generate documentation for Terraform configuration.

Open questions:

- What if the infrastructure changes between a `terraform plan` and the subsequent `terraform apply` (e.g. by a `terraform apply` of another PR)? In that case, what will be executed by `terraform apply` is not what was reviewed by `terraform plan`.
    - This can maybe be solved by somehow detecting the deprecation of the `terraform plan` in the merge-PR workflow and then abort the pipeline before executing `terraform apply` (and required running the create-PR workflow again).
- What alternatives to Terraform Cloud are there? Could Terraform be directly run on GitHub Actions instead of Terraform Cloud?
    - In that case, the state file would still have to be manually managed as e.g. in [Classical approach](#classical-approach) above.

### Misc

- [Isoflow](https://isoflow.io/): create isometric and animated infrastructure diagrams (similar to [Cloudcraft](https://www.cloudcraft.co/))
- Age of Empires II was apparently one of the first games to use isometric graphics
    - However, I think that Sim City already used it earlier

## Resources

- https://github.com/nuvibit/github-terraform-workflows
    - Fork: https://github.com/weibeld/github-terraform-workflows
- https://developer.hashicorp.com/terraform/cloud-docs
- https://isoflow.io/

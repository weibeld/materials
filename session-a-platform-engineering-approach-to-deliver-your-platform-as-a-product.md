---
id: jkiorvdm3j6rbxg4h4haz5o
title: A Platform Engineering Approach to Deliver Your Platform as a Product
desc: ''
updated: 1683907594952
created: 1680028864184
---

## General info

- Date: 28 March 2023
- Event: [[2.records.events.cloud-native-bern-meetup-2023-03-28]]
- Speaker: Marcel Härri, Red Hat

## Summary

### Theoretical part

The gist of the presentation is that building a platform (e.g. a container-based application platform) can be seen like building a product.

That means, the platform should have clearly delineated versions, releases, features, capabilities, etc., and should be rolled out and updated like a product.

This is because a platform is never just Kubernetes (or OpensShift), but Kubernetes is only the basis (a building block) and many services are provided on top of it (monitoring, backups, security, etc.).

Developing the platform then means developing releases. A release should have the following features:

- **Identifiable:** every version must be pinned (use hash digests rather than labels), it must be unambiguously clear what's in a release.
- **Consistent:** there must be the same outcome when deploying the release in different environments and at different points in time
- **Reproducible:** anything that's done with a release should be reproducible in a different settign (this is implied by consistency)

### Practical part

Presentation of how this issue is approached (how a platform release is bundled and described) at Red Hat:

- Platform based on OpenShift
- GitOps with Argo CD
- Makes use of ApplicationSets and generators to specify versions of applications
- GitHub repo contains configurations for multiple versions in main branch. These versions can be selectively deployed to different infrastructures.
- Demo: https://github.com/duritong/ocp-gitops

## Discussion

Handling platform configurations like software releases makees a lot of sense. However, it also goes against the paradigm of continuous deployment (i.e. every commit is pushed to production without versions).

However, the benefits of using clearly defined and reproducible versions probably outweighs the loss of the continuous deployment paradigm.

Open questions:

- How to describe features of the required Kubernetes/OpenShift platform itself (CNI plugins, on-premise cluster, managed Kubernetes service, specific Kubernetes distribution, etc.)?

## Resources

- https://github.com/duritong/ocp-gitops
    - Fork: https://github.com/weibeld/ocp-gitops 

---
id: r8tkqmhwkek9kpl3c8kccq1
title: Next Level of Automation through Event-Driven Ansible
desc: ''
updated: 1683907376040
created: 1679526931096
---

## General info

- Date: 22 March 2023
- Event: [[2.records.events.devops-meetup-zurich-2023-03-22]]
- Speaker: Dominik Hahn, Red Hat

## Summary

Presentation of [Event-Driven Ansible](https://github.com/ansible/event-driven-ansible). This is an extension of Ansible allowing the incorporation of event sources and rules (to take action on these events) into Ansible configuration (called rulebooks).

The goal is to automate Ansible tasks that need to be performed after certain events occur (e.g. an error of failure in the system).

Supported event sources include Prometheus, Alertmanager, AppDynamics, Sensu, Dynatrace, Kafka, or webhooks. Support for Azure Service Bus and AWS EventBridge is planned. The action that is taken upon these events  usually consists in running an Ansible playbook.

The Ansible rulebook (that listens for the events) is constantly running and thus must be deployed on a central piece of infrastructure that is accessible by the event sources.

Event-Driven Ansible is developed by Red Hat and currently (at the time of the presentation) in developer preview.

## Discussion

Event-Driven Ansible extends the imperative approach of Ansible. I think, it may make sense in environments that are already heavily based on Ansible.

A more innovative approach would be to wrap the process of automatic incident handling in a declarative system (like Terraform or Kubernetes). That is, the desired state is specified and the system continuously takes corrective actions if it detects a deviation of the actual state from the desired state.

The corrective actions to take in each particular situation could be specified as plugins or functions by the user.

## Resources

- https://github.com/ansible/event-driven-ansible
- https://www.ansible.com/use-cases/event-driven-automation

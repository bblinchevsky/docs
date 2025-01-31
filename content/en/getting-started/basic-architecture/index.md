---
categories: ["overview"]
weight: 1
tags: ["architecture"]
title: "Basic Architecture"
date: 2022-12-28
description: >
  Trustgrid basic architecture overview
---

### Cloud Components

- Portal - The cloud management UI.
- Gatekeeper - Provides configuration updates to edge nodes.
- Zuul - Maintains persistent connection with [nodes]({{<ref "docs/nodes" >}}) for reporting, [events]({{<ref "docs/alarms/events" >}}), and updates.
- API - The management API that exposes 100% of UI elements to automation.
- Repo - The APT repository that stores all firmware, OS, and [node]({{<ref "docs/nodes" >}}) updates.

### Edge Components

- Node - The software that provides core functionality in the edge including [networking]({{<ref "getting-started/networking" >}}), [security]({{<ref "getting-started/security" >}}), compute, and management features. Edge nodes build outbound connections to gateway nodes.

### Use Cases

- Software Defined Networking - Create a mesh [network]({{<ref "getting-started/networking">}}) that connects cloud applications to edge data with load balancing, [clustering]({{<ref "/docs/clusters">}}), and failover managed through a portal or API.
- Edge Compute - Deploy applications to the edge to access datasets not appropriate for replication to the cloud due to [security]({{<ref "getting-started/security">}}) or compliance concerns, latency, or cost.
- Device Management - Manage thousands of [nodes]({{<ref "docs/nodes">}}) with advanced tools to reduce the burden of operations at enterprise scale.
- Edge API - Integrate thousands of edge datasets with a single API interface and ETL functions executing at the edge.
- Security - Leverage Trustgrid's advanced [security]({{<ref "getting-started/security" >}}) to protect against a wide range of threats.

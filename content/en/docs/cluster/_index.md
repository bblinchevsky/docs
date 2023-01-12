---
categories: ["concepts"]
tags: ["cluster", "concepts"]
title: "Cluster"
date: 2022-12-28
weight: 3
---

{{% pageinfo %}}
A cluster is a pair of [nodes]({{< ref "docs/node" >}}) that share configuration.
{{% /pageinfo %}}

A cluster is a pair of [nodes]({{< ref "docs/node" >}}) at a single site that provides automated high-availability (HA) connectivity. An additional IP address is assigned as a Cluster Virtual IP address that can move between the [nodes]({{< ref "docs/node" >}}) if failover occurs.

Additionally, certain settings such as [network]({{< ref "docs/overview/networking">}}) services and [VPN]({{< ref "docs/concepts/VPN" >}}) settings can be configured for the cluster and these settings will override the individual [node's]({{< ref "docs/node" >}}) configuration.
---
categories: ["concepts"]
tags: ["domain", "concepts", "rewrite"]
title: "Routes"
date: 2023-1-9
---

{{% pageinfo %}}
Routes configured under [Domains]({{<ref "docs/domain" >}}) determine to which [node]({{<ref "docs/nodes" >}}) or [cluster]({{<ref "docs/clusters" >}}) the [Trustgrid virtual network]({{<ref "docs/domain/virtual-networks" >}}) should route traffic for a specific subnet.
{{% /pageinfo %}}

## Route Configuration

1. Login to the portal and select [`domains`]({{<ref "docs/domain" >}}).
2. Click the link to the desired domain under the "Name" column.
3. Scroll down to the ["Virtual Networks"]({{<ref "docs/domain/virtual-networks" >}}) section and select the `Routes` tab.

![img](routes-list.png)

A Route has Three Required Fields:

{{<fields>}}
{{<field "Destination" >}}
This will be the name of the [node]({{<ref "docs/nodes" >}}) or [cluster]({{<ref "docs/clusters" >}}) that traffic will be routed to. This list is auto-populated based on the nodes and clusters in the selected [domain]({{<ref "docs/domain" >}}).
{{</field >}}

{{<field "Destination CIDR" >}}
This is the CIDR notation of the [virtual network]({{<ref "docs/domain/virtual-networks" >}}) that should be routed to the above destination [node]({{<ref "docs/nodes" >}}) or [cluster]({{<ref "docs/clusters" >}}).
{{</field >}}

{{<field "Metric" >}}
If there are multiple routes for the same [virtual network]({{<ref "docs/domain/virtual-networks" >}}) the metric will determine which route will be used. The lowest number is the highest priority. See the "Automatic Failover" text below.
{{</field >}}
{{</fields>}}

## Route Failover 

Route failover allows a subnet to be routed to an alternate [node]({{<ref "/docs/nodes" >}}) or [cluster]({{<ref "docs/clusters" >}}) in the event of a failure.  This can be automatic or performed manually.

### Prerequisites 

In either configuration, the [virtual network]({{<ref "docs/domain/virtual-networks" >}}) settings under VPN settings for the primary and backup destination [nodes]({{<ref "docs/nodes" >}})/[clusters]({{<ref "docs/clusters" >}}) must match. Including:

- Network Virtual Route

  ![img](virtual-network-route.png)

- Network Group under Outside NAT Table

  ![img](outside-nat-table.png)

- Virtual CIDR under Inside NAT Table

  ![img](inside-nat-table.png)

### Automatic Failover

To have the route failover without manual intervention you must define two routes for the same subnet (Destination CIDR) with different metrics.  The lowest numerical metric will take precedence unless the destination [node]({{<ref "docs/nodes" >}}) or [cluster]({{<ref "docs/clusters" >}}) is offline.

In the below example configuration we want traffic for the 10.20.0.0/24 network to the `edge` [cluster]({{<ref "docs/clusters" >}}) first, and failover to the `edge-dr` [cluster]({{<ref "docs/clusters" >}}).

![img](automatic-failover.png)

### Preventing Automated Failback or Forcing a Failover

As mentioned above if multiple routes are configured traffic will route to destination with the lowest metric number. So if the primary destination fails but then comes back online traffic will be routed back automatically.

However, there are some circumstances where this is not desirable. For example, if the primary site is unstable you may wish to keep traffic at the backup site until the primary is stabilized. Alternately, you may wish to preemptively reroute traffic to the backup site in advance of planned maintenance at the primary site.

To preemptively reroute traffic to the backup site, update the backup route to have a lower metric than the primary route.

### Manual Failover

In some circumstances, it may be preferable for failover to only occur with manual intervention. In this situation, you will have a single route under the [domain]({{<ref "docs/domain" >}}).  To initiate a failover you'll need to update the destination [cluster]({{<ref "docs/clusters" >}})/[node]({{<ref "docs/nodes" >}}).

1. Login to the Portal and select your domain.
1. Click the link to the desired [domain]({{<ref "docs/domain" >}}) under the "Name" column.
1. Scroll down to the ["Virtual Networks"]({{<ref "docs/domain/virtual-networks" >}}) section and select the "Routes" tab.
1. Find the route you wish to failover.
1. Update the destination device. (e.g. in the below you would switch from edge to edge-dr).
  ![Update Destination](update-destination.png)
1. Click save.

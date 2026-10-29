# 03. Topology and Service Visualization

!!! abstract "Goal"

    Explore the IGP and TE topology, SRv6 policies, and VPN services with Service Health in CNC.

## 3.1 IGP topology

![Topology](images/image01.png)

Click **Topology** in the left menu to show the IGP topology.
In this demo the device locations are set to Australia, so the devices are shown on a map.

The device list on the right shows the alarm and reachability state of each device.

!!! note

    The SR-PCE is set to **Unmanaged** in this demo, so it is shown with a different icon. This is expected.

<!-- SCREENSHOT: images/topology-map.png | IGP topology on the map with the device list -->

Click **Links** to show the link list with link status and utilization.

![Topology](images/image02.png)

<!-- SCREENSHOT: images/link-list.png | Link list with status and utilization -->

## 3.2 Device details

Click a device on the topology (for example PE2) to show its details: links, interfaces, alarms and inventory.

![Topology](images/image03.png)
![Topology](images/image04.png)
![Topology](images/image05.png)
![Topology](images/image06.png)
![Topology](images/image07.png)

- **History** shows CPU and memory utilization, because Device Health monitoring is enabled
![Topology](images/image08.png)
  (see [04. Performance Monitoring and Alarms](../04-performance-alarms/index.md)).

- **Detailed Inventory** shows the inventory as a tree. Use the legend to drill down to power supplies, fans, line cards and ports.
![Topology](images/image09.png)


## 3.3 Link details

Click a link on the topology (for example PE2-P4) to show its utilization and its IGP, delay and TE metrics.
**Admin Groups** shows that an affinity color is set on this link.

![Topology](images/image10.png)

On PE2, the affinity color `RED` is mapped to bit position 3:

```text
RP/0/RP0/CPU0:PE2#show running-config segment-routing traffic-eng interface FourHundredGigE 0/0/0/0
Thu Oct 29 03:32:19.335 UTC
segment-routing
 traffic-eng
  interface FourHundredGigE0/0/0/0
   affinity
    name RED
   !
  !
 !
!
RP/0/RP0/CPU0:PE2#show running-config segment-routing traffic-eng affinity-map 
Thu Oct 29 03:32:28.525 UTC
segment-routing
 traffic-eng
  affinity-map
   name RED bit-position 3
  !
 !
!
```

Click **History** to show the histrical data of the link utilization.
![Topology](images/image11.png)


## 3.4 Traffic Engineering view and Flex-Algo

Switch the view to **Traffic Engineering**. When you change Flex-Algo to **128**, the topology is shown per slice.
Algo 128 is not configured on P4, so P4 is not part of the Algo 128 topology.

![Topology](images/image12.png)
![Topology](images/image13.png)


Change the view back to Algo 0.

## 3.5 SRv6 policies

Select the **SRv6** tab on the right to list the configured SRv6 policies.
Select a policy to highlight its path on the topology. 

![Topology](images/image14.png)

Select **IGP path** to show the routers it goes through.
![Topology](images/image15.png)

Click **View Details** to see the policy details. 
![Topology](images/image16.png)

In this example:
- Head-end is PE1 and end-point is PE2. The SID list goes through PE3.
![Topology](images/image17.png)

- The constraint excludes links with affinity `RED` (bit position 3), with metric type IGP.
- `RED` is set on the P4-PE2 link, so the IGP shortest path is computed to avoid that link.

You can also check the policy configuration from this screen by clicking the "Config ID."
![Topology](images/image18.png)



## 3.6 VPN services

Switch the view to **VPN Services** to list the configured VPNs.
At this point, four services (L3VPN, VPWS and VPLS) are configured. Service Health is enabled, so the health of each service is shown.
![Topology](images/image19.png)

### L3VPN (CustA)

Click **View Details** on CustA to show the PE routers that belong to the L3VPN.
![Topology](images/image20.png)

**Health** shows issues detected by the metrics defined in the selected Heuristic Package.
![Topology](images/image21.png)

In this demo, CustA uses Automated Steering and advertises a color to the remote PEs.
The remote PEs have no SR policy for that color, so Service Health raises an alert.

<!-- SCREENSHOT: images/custa-details.png | CustA details with health alert -->

Click **Assurance Graph** to show how the alerts are related, as a tree.
Expand the tree to see what is monitored and how the items depend on each other.

![Topology](images/image22.png)
![Topology](images/image23.png)
![Topology](images/image24.png)

<!-- SCREENSHOT: images/assurance-graph.png | Assurance Graph for CustA -->

**Administration > Heuristic Package** shows which metrics are collected and the conditions that raise an alert.

![Topology](images/image25.png)

Back on the VPN service, **Transport / SRv6** shows the SR policy that carries the traffic of this L3VPN.
CustA traffic from PE1 to PE2 is forwarded over this SR policy.

![Topology](images/image26.png)

**Configuration** shows the L3VPN configuration for CustA.

![Topology](images/image27.png)

### VPWS (CustD)

For VPWS, the PEs are shown connected one-to-one.

![Topology](images/image28.png)

### VPLS (CustF)

For VPLS, the PEs are shown connected multipoint-to-multipoint.
**Transport / SRv6** shows SR policies in a full mesh. These are instantiated by ODN.

![Topology](images/image29.png)
![Topology](images/image30.png)

## 3.7 Service Health dashboard

The Service Health dashboard shows the health of all VPNs at a glance.

![Topology](images/image31.png)

## Next step

Go to [04. Performance Monitoring and Alarms](../04-performance-alarms/index.md).

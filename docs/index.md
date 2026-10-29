# Crosswork Network Controller Demo

This guide walks through a demo of Cisco Crosswork Network Controller (CNC) 7.2.1-SP on an SRv6 (uSID) network built in CML. It covers network visualization, monitoring, SR policy and VPN service provisioning, and device configuration management.

## Demo flow


| No. | Section                                                             | What you will see                                              |
| --- | ------------------------------------------------------------------- | -------------------------------------------------------------- |
| 01  | [Demo Topology](01-demo-topology/index.md)                          | Routers, SRv6 / IS-IS, SR-PCE, BGP-LS and PCEP                 |
| 02  | [Dashboard and Crosswork Manager](02-dashboard/index.md)            | CNC dashboard, application health, NSO and Function Packs      |
| 03  | [Topology and Service Visualization](03-visualization/index.md)     | IGP / TE topology, SRv6 policies, VPN services, Service Health |
| 04  | [Performance Monitoring and Alarms](04-performance-alarms/index.md) | Performance policies, network and device alarms                |
| 05  | [SR Policy Provisioning](05-sr-policy/index.md)                     | SRv6-TE policy with PCE-computed path (TE metric)              |
| 06  | [L3VPN Provisioning](06-l3vpn/index.md)                             | SRv6 L3VPN with Automated Steering                             |
| 07  | [L2VPN VPWS Provisioning](07-l2vpn-vpws/index.md)                   | SRv6 EVPN VPWS with auto-assigned EVI                          |
| 08  | [L2VPN VPLS Provisioning](08-l2vpn-vpls/index.md)                   | SRv6 EVPN ELAN with ODN and multi-homing                       |
| 09  | [Configuration Templates](09-config-template/index.md)              | Deploying configuration and show commands with templates       |
| 10  | [Configuration Backup and Restore](10-backup-restore/index.md)      | Scheduled backup, compare and restore                          |




## Demo environment


| Component      | Details                                                                                                                  |
| -------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Controller     | Crosswork Network Controller 7.2.1-SP (with NSO and CNC Function Packs 7.2.1)Single VM deployment with build-in CDG/NSO |
| PE / P routers | 5 x Cisco 8711-32FH emulator (IOS XR) on CML (version 25.4.2)                                                            |
| SR-PCE         | XRv 9000, connected to P4 and P5 (version 26.1.1)                                                                        |
| Transport      | SRv6 uSID (F3216) with IS-IS for IPv6, Flex-Algo 128                                                                     |
| CML            | version 2.10.1+build.21                                                                                                  |

A CML lab template used for this demo is in [CML_SRv6_Lab](CML_SRv6_Lab.yaml).



## Addressing


| Router | Role | Router ID | IPv6 Loopback0     | SRv6 Locator MAIN | SRv6 Locator ALGO128 |
| ------ | ---- | --------- | ------------------ | ----------------- | -------------------- |
| PE1    | PE   | 1.1.1.1   | fcbb:bb00:1::1/128 | fcbb:bb00:1::/48  | fcbb:bb01:1::/48     |
| PE2    | PE   | 2.2.2.2   | fcbb:bb00:2::1/128 | fcbb:bb00:2::/48  | fcbb:bb01:2::/48     |
| PE3    | PE   | 3.3.3.3   | fcbb:bb00:3::1/128 | fcbb:bb00:3::/48  | fcbb:bb01:3::/48     |
| P4     | P    | 4.4.4.4   | fcbb:bb00:4::1/128 | fcbb:bb00:4::/48  | -                    |
| P5     | P    | 5.5.5.5   | fcbb:bb00:5::1/128 | fcbb:bb00:5::/48  | fcbb:bb01:5::/48     |
| SR-PCE | PCE  | -         | fcbb:bb00:6::1/128 | -                 | -                    |


- Core links use IPv6 link-local addresses only (`ipv6 enable`).
- All PEs are in BGP AS 65000 and peer with each other for VPNv4 and L2VPN EVPN.



## Services used in the demo


| Customer | Service   | State at demo start | Section                         |
| -------- | --------- | ------------------- | ------------------------------- |
| CustA    | L3VPN     | Pre-configured      | [03](03-visualization/index.md) |
| CustB    | L3VPN     | Pre-configured      | [03](03-visualization/index.md) |
| CustD    | EVPN VPWS | Pre-configured      | [03](03-visualization/index.md) |
| CustF    | EVPN VPLS | Pre-configured      | [03](03-visualization/index.md) |
| CustC    | L3VPN     | Created in the demo | [06](06-l3vpn/index.md)         |
| CustE    | EVPN VPWS | Created in the demo | [07](07-l2vpn-vpws/index.md)    |
| CustG    | EVPN VPLS | Created in the demo | [08](08-l2vpn-vpls/index.md)    |


All payloads are listed in [Appendix - Demo Payloads](payloads.md).

## Before the demo

!!! warning "Reset the environment"
    Do these steps before each demo so that the provisioning sections start from a clean state.

    - Take a configuration backup of P5 (used in [10. Configuration Backup and Restore](10-backup-restore/index.md)).
    - Delete the VPN services created in the previous demo (CustC, CustE, CustG) and the SR policy `PE1-PE3_COLOR20`.
    - Remove `Loopback101` from P5 if it is left from the configuration template demo.




## Next step

Go to [01. Demo Topology](01-demo-topology/index.md).
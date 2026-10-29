# Appendix - Demo Payloads

These are the JSON payloads loaded into CNC during the demo. Use **Import** on each provisioning screen to load them.

## Created in the demo

| Section | Object                       | Payload |
| ------- | ---------------------------- | ------- |
| [05](05-sr-policy/index.md) | SR policy `PE1-PE3_COLOR20` | [pcc-init_policy_color20.json](payloads/pcc-init_policy_color20.json) |
| [06](06-l3vpn/index.md)     | L3VPN `CustC`               | [l3vpn-service_CustC.json](payloads/l3vpn-service_CustC.json) |
| [07](07-l2vpn-vpws/index.md) | EVPN VPWS `CustE_vpws`     | [l2vpn-vpws-CustE.json](payloads/l2vpn-vpws-CustE.json) |
| [08](08-l2vpn-vpls/index.md) | EVPN VPLS `CustG_vpls`     | [l2vpn-vpls-odn_CustG.json](payloads/l2vpn-vpls-odn_CustG.json) |

## Pre-configuration

Load these before the demo, in this order: route policy tags, routing policies, SR policies / ODN templates, then services.

| Type                  | Payload |
| --------------------- | ------- |
| L3VPN route policy tag | [Color10](payloads/preconfiguration/l3vpn-route-policy-tag_Color10.json), [Color20](payloads/preconfiguration/l3vpn-route-policy-tag_Color20.json) |
| L3VPN routing policy   | [Policy1](payloads/preconfiguration/l3vpn-route-policy_Policy1.json), [Policy2](payloads/preconfiguration/l3vpn-route-policy_Policy2.json) |
| L2VPN route policy tag | [Color30](payloads/preconfiguration/l2vpn-route-policy-tag_Color30.json), [Color40](payloads/preconfiguration/l2vpn-route-policy-tag_Color40.json) |
| L2VPN routing policy   | [Policy3](payloads/preconfiguration/l2vpn-route-policy_Policy3.json), [Policy4](payloads/preconfiguration/l2vpn-route-policy_Policy4.json) |
| SR policy              | [pcc-init_policy_color10.json](payloads/preconfiguration/pcc-init_policy_color10.json) |
| ODN template           | [Color30](payloads/preconfiguration/odn_policy_color30.json), [Color40](payloads/preconfiguration/odn_policy_color40.json) |
| L3VPN service          | [CustA](payloads/preconfiguration/l3vpn-service_CustA.json), [CustB](payloads/preconfiguration/l3vpn-service_CustB.json) |
| L2VPN service          | [CustD (VPWS)](payloads/preconfiguration/l2vpn-vpws-CustD.json), [CustF (VPLS)](payloads/preconfiguration/l2vpn-vpls-odn_CustF.json) |

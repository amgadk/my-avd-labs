# FABRIC

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| FABRIC | l3leaf | dc1-borderleaf1 | 172.16.1.105/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | dc1-borderleaf2 | 172.16.1.106/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | dc1-leaf1 | 172.16.1.101/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | dc1-leaf2 | 172.16.1.102/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | dc1-leaf3 | 172.16.1.103/24 | vEOS-lab | Provisioned | - |
| FABRIC | l3leaf | dc1-leaf4 | 172.16.1.104/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | dc1-spine1 | 172.16.1.11/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | dc1-spine2 | 172.16.1.12/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | dc1-spine3 | 172.16.1.13/24 | vEOS-lab | Provisioned | - |
| FABRIC | spine | dc1-spine4 | 172.16.1.14/24 | vEOS-lab | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | dc1-borderleaf1 | Ethernet1 | mlag_peer | dc1-borderleaf2 | Ethernet1 |
| l3leaf | dc1-borderleaf1 | Ethernet2 | mlag_peer | dc1-borderleaf2 | Ethernet2 |
| l3leaf | dc1-borderleaf1 | Ethernet3 | spine | dc1-spine1 | Ethernet7 |
| l3leaf | dc1-borderleaf1 | Ethernet4 | spine | dc1-spine2 | Ethernet7 |
| l3leaf | dc1-borderleaf1 | Ethernet5 | spine | dc1-spine3 | Ethernet7 |
| l3leaf | dc1-borderleaf1 | Ethernet6 | spine | dc1-spine4 | Ethernet7 |
| l3leaf | dc1-borderleaf2 | Ethernet3 | spine | dc1-spine1 | Ethernet8 |
| l3leaf | dc1-borderleaf2 | Ethernet4 | spine | dc1-spine2 | Ethernet8 |
| l3leaf | dc1-borderleaf2 | Ethernet5 | spine | dc1-spine3 | Ethernet8 |
| l3leaf | dc1-borderleaf2 | Ethernet6 | spine | dc1-spine4 | Ethernet8 |
| l3leaf | dc1-leaf1 | Ethernet1 | mlag_peer | dc1-leaf2 | Ethernet1 |
| l3leaf | dc1-leaf1 | Ethernet2 | mlag_peer | dc1-leaf2 | Ethernet2 |
| l3leaf | dc1-leaf1 | Ethernet3 | spine | dc1-spine1 | Ethernet3 |
| l3leaf | dc1-leaf1 | Ethernet4 | spine | dc1-spine2 | Ethernet3 |
| l3leaf | dc1-leaf1 | Ethernet5 | spine | dc1-spine3 | Ethernet3 |
| l3leaf | dc1-leaf1 | Ethernet6 | spine | dc1-spine4 | Ethernet3 |
| l3leaf | dc1-leaf2 | Ethernet3 | spine | dc1-spine1 | Ethernet4 |
| l3leaf | dc1-leaf2 | Ethernet4 | spine | dc1-spine2 | Ethernet4 |
| l3leaf | dc1-leaf2 | Ethernet5 | spine | dc1-spine3 | Ethernet4 |
| l3leaf | dc1-leaf2 | Ethernet6 | spine | dc1-spine4 | Ethernet4 |
| l3leaf | dc1-leaf3 | Ethernet1 | mlag_peer | dc1-leaf4 | Ethernet1 |
| l3leaf | dc1-leaf3 | Ethernet2 | mlag_peer | dc1-leaf4 | Ethernet2 |
| l3leaf | dc1-leaf3 | Ethernet3 | spine | dc1-spine1 | Ethernet5 |
| l3leaf | dc1-leaf3 | Ethernet4 | spine | dc1-spine2 | Ethernet5 |
| l3leaf | dc1-leaf3 | Ethernet5 | spine | dc1-spine3 | Ethernet5 |
| l3leaf | dc1-leaf3 | Ethernet6 | spine | dc1-spine4 | Ethernet5 |
| l3leaf | dc1-leaf4 | Ethernet3 | spine | dc1-spine1 | Ethernet6 |
| l3leaf | dc1-leaf4 | Ethernet4 | spine | dc1-spine2 | Ethernet6 |
| l3leaf | dc1-leaf4 | Ethernet5 | spine | dc1-spine3 | Ethernet6 |
| l3leaf | dc1-leaf4 | Ethernet6 | spine | dc1-spine4 | Ethernet6 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 10.255.255.0/24 | 256 | 48 | 18.75 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| dc1-borderleaf1 | Ethernet3 | 10.255.255.65/31 | dc1-spine1 | Ethernet7 | 10.255.255.64/31 |
| dc1-borderleaf1 | Ethernet4 | 10.255.255.67/31 | dc1-spine2 | Ethernet7 | 10.255.255.66/31 |
| dc1-borderleaf1 | Ethernet5 | 10.255.255.69/31 | dc1-spine3 | Ethernet7 | 10.255.255.68/31 |
| dc1-borderleaf1 | Ethernet6 | 10.255.255.71/31 | dc1-spine4 | Ethernet7 | 10.255.255.70/31 |
| dc1-borderleaf2 | Ethernet3 | 10.255.255.73/31 | dc1-spine1 | Ethernet8 | 10.255.255.72/31 |
| dc1-borderleaf2 | Ethernet4 | 10.255.255.75/31 | dc1-spine2 | Ethernet8 | 10.255.255.74/31 |
| dc1-borderleaf2 | Ethernet5 | 10.255.255.77/31 | dc1-spine3 | Ethernet8 | 10.255.255.76/31 |
| dc1-borderleaf2 | Ethernet6 | 10.255.255.79/31 | dc1-spine4 | Ethernet8 | 10.255.255.78/31 |
| dc1-leaf1 | Ethernet3 | 10.255.255.33/31 | dc1-spine1 | Ethernet3 | 10.255.255.32/31 |
| dc1-leaf1 | Ethernet4 | 10.255.255.35/31 | dc1-spine2 | Ethernet3 | 10.255.255.34/31 |
| dc1-leaf1 | Ethernet5 | 10.255.255.37/31 | dc1-spine3 | Ethernet3 | 10.255.255.36/31 |
| dc1-leaf1 | Ethernet6 | 10.255.255.39/31 | dc1-spine4 | Ethernet3 | 10.255.255.38/31 |
| dc1-leaf2 | Ethernet3 | 10.255.255.41/31 | dc1-spine1 | Ethernet4 | 10.255.255.40/31 |
| dc1-leaf2 | Ethernet4 | 10.255.255.43/31 | dc1-spine2 | Ethernet4 | 10.255.255.42/31 |
| dc1-leaf2 | Ethernet5 | 10.255.255.45/31 | dc1-spine3 | Ethernet4 | 10.255.255.44/31 |
| dc1-leaf2 | Ethernet6 | 10.255.255.47/31 | dc1-spine4 | Ethernet4 | 10.255.255.46/31 |
| dc1-leaf3 | Ethernet3 | 10.255.255.49/31 | dc1-spine1 | Ethernet5 | 10.255.255.48/31 |
| dc1-leaf3 | Ethernet4 | 10.255.255.51/31 | dc1-spine2 | Ethernet5 | 10.255.255.50/31 |
| dc1-leaf3 | Ethernet5 | 10.255.255.53/31 | dc1-spine3 | Ethernet5 | 10.255.255.52/31 |
| dc1-leaf3 | Ethernet6 | 10.255.255.55/31 | dc1-spine4 | Ethernet5 | 10.255.255.54/31 |
| dc1-leaf4 | Ethernet3 | 10.255.255.57/31 | dc1-spine1 | Ethernet6 | 10.255.255.56/31 |
| dc1-leaf4 | Ethernet4 | 10.255.255.59/31 | dc1-spine2 | Ethernet6 | 10.255.255.58/31 |
| dc1-leaf4 | Ethernet5 | 10.255.255.61/31 | dc1-spine3 | Ethernet6 | 10.255.255.60/31 |
| dc1-leaf4 | Ethernet6 | 10.255.255.63/31 | dc1-spine4 | Ethernet6 | 10.255.255.62/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 10.255.0.0/26 | 64 | 10 | 15.63 % |
| 10.255.0.0/27 | 32 | 10 | 31.25 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| FABRIC | dc1-borderleaf1 | 10.255.0.13/32 |
| FABRIC | dc1-borderleaf2 | 10.255.0.14/32 |
| FABRIC | dc1-leaf1 | 10.255.0.9/32 |
| FABRIC | dc1-leaf2 | 10.255.0.10/32 |
| FABRIC | dc1-leaf3 | 10.255.0.11/32 |
| FABRIC | dc1-leaf4 | 10.255.0.12/32 |
| FABRIC | dc1-spine1 | 10.255.0.1/32 |
| FABRIC | dc1-spine2 | 10.255.0.2/32 |
| FABRIC | dc1-spine3 | 10.255.0.3/32 |
| FABRIC | dc1-spine4 | 10.255.0.4/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------ | ------------------- | ------------------ | ------------------ |
| 10.255.1.0/26 | 64 | 6 | 9.38 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| FABRIC | dc1-borderleaf1 | 10.255.1.13/32 |
| FABRIC | dc1-borderleaf2 | 10.255.1.13/32 |
| FABRIC | dc1-leaf1 | 10.255.1.9/32 |
| FABRIC | dc1-leaf2 | 10.255.1.9/32 |
| FABRIC | dc1-leaf3 | 10.255.1.11/32 |
| FABRIC | dc1-leaf4 | 10.255.1.11/32 |

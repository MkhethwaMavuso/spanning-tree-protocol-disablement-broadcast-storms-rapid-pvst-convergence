# spanning-tree-protocol-disablement-broadcast-storms-rapid-pvst-convergence
Layer 2 Triangular Switched Topology featuring three Cisco 2960 Catalyst switches (Switch0, Switch1, and Switch2) interconnected in a redundant loop configuration, with end-user workstations PC0 (192.168.1.1) and PC1 (192.168.1.2) connected to the access edge.

🌐 Quick Overview & Network Specs🟢 Architecture & Topology: Layer 2 Triangular Switched Topology featuring three Cisco 2960 Catalyst switches (Switch0, Switch1, and Switch2) interconnected in a redundant loop configuration, with end-user workstations PC0 (192.168.1.1) and PC1 (192.168.1.2) connected to the access edge.   🔵 Switch MAC Addresses & STP Priorities:Switch0: MAC 00:E0:F7:C7:14:97, STP Priority 8193.   Switch1: MAC 00:E0:A3:8B:94:93, STP Priority 12289.   Switch2: MAC 00:E0:B0:09:C9:80, STP Priority 4096 (Elects Switch2 as the Root Bridge due to having the lowest configurable bridge priority).   🟣 Lab Experiment Objectives:STP Disablement & Broadcast Storm Analysis: Disabling Spanning Tree Protocol across all switches, saving configurations, restarting the lab, and observing the impact on ICMP traffic (ping from PC0 to PC1).   Rapid STP Convergence: Enabling Rapid PVST+ (802.1w) to identify the Root Bridge, port roles (Root, Designated, Alternate/Blocking), and sub-second convergence behavior.   💡 Key Technical Insights & What This Lab Demonstrates🔍 Broadcast Storms & MAC Table Instability: Demonstrates how removing Layer 2 loop-prevention mechanisms (STP) causes broadcast frames, ARP requests, and unicast floods to circulate infinitely around the redundant triangle topology, consuming 100% CPU utilization and causing network collapse.   ⚡ Rapid PVST+ (802.1w) Superiority: Highlights how enabling Rapid STP transitions ports rapidly through proposal-agreement handshakes, replacing legacy 50-second 802.1D forwarding delays.   🛠️ Root Bridge Determination: Proves how switches elect the Root Bridge by comparing configurable bridge priorities (4096 on Switch2 vs. 8193 and 12289) combined with base MAC addresses.   🛡️ Port Role Identifications: Audits active port states to confirm designated forwarding paths and alternative blocking ports that prevent physical loops while retaining high-availability failover paths.   🛠️ Essential Cisco CLI Configuration & Troubleshooting SnippetsDisabling Spanning Tree Across All VLANsCisco CLIno spanning-tree vlan 1
write memory
reload
Enabling Rapid PVST+ and Verifying Root Bridge PriorityCisco CLIspanning-tree mode rapid-pvst
spanning-tree vlan 1 priority 4096
🧪 Verification & Audit CommandsBash# Verify STP operational status, root bridge details, and local bridge parameters
show spanning-tree
show spanning-tree summary

# Inspect interface-level port roles (Root/Desg/Altn) and forwarding states
show spanning-tree interface fastEthernet 0/1

# Test basic end-to-end connectivity between user endpoints
ping 192.168.1.2

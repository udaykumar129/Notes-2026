- There is an architecture diagram only
- sb-mgt subscritption - related to logging- it is not there in diagram 
- sb-ssh - network related ( FW )
- This needs to be moved to UK-South
- azure firewall needs to be replicated ( Active/Active)  to UK south from UAE North
- talk to Dinesh...about what all needs to be done
- earlier when Teams spoke....he was expecting the documentation/procedure
- Santosh & Vijay working on DR part
- sd-id ( domain server )
- These three fall under hub subscription
- There is no documentation...whatsoever

---

# Hub and Spoke Model in Azure

The **hub and spoke** is a network topology pattern in Azure where a central network (the **hub**) connects to multiple peripheral networks (the **spokes**).

---

## Core Concept

Think of it like a bicycle wheel — the hub sits at the center, and spokes radiate outward. All traffic between spokes flows *through* the hub, giving you centralized control.

---

## Components

### Hub Virtual Network (VNet)
The central VNet that hosts shared services used by all spokes, typically containing:
- Azure Firewall or Network Virtual Appliance (NVA)
- VPN Gateway / ExpressRoute Gateway
- Azure Bastion (for secure VM access)
- DNS servers
- Monitoring and logging resources

### Spoke Virtual Networks
Individual VNets for different workloads, teams, or environments (e.g., Dev, Prod, Analytics). Each spoke is connected to the hub via **VNet Peering**.

---

## How Traffic Flows

```
On-premises / Internet
         |
       [Hub VNet]
      /    |     \
[Spoke1] [Spoke2] [Spoke3]
 (Dev)    (Prod)  (Analytics)
```

All inter-spoke traffic routes through the hub, where firewalls and policies are enforced centrally.

---

## Key Benefits

- **Centralized security** — one place to manage firewalls, routing, and inspection
- **Cost efficiency** — shared services (gateways, firewalls) aren't duplicated in every spoke
- **Isolation** — spokes are isolated from each other by default
- **Scalability** — easy to add new spokes without redesigning the network
- **Simplified management** — consistent policy enforcement from the hub

---

## Common Azure Services Used

| Role | Azure Service |
|---|---|
| Connectivity hub | Azure Virtual WAN or custom hub VNet |
| Firewall | Azure Firewall |
| Hybrid connectivity | VPN Gateway / ExpressRoute |
| Secure remote access | Azure Bastion |
| Routing control | User Defined Routes (UDRs) |
| DNS | Azure Private DNS Zones |

---

## Hub and Spoke vs. Azure Virtual WAN

| | Traditional Hub-Spoke | Azure Virtual WAN |
|---|---|---|
| Management | Manual (you build the hub) | Managed by Microsoft |
| Scale | Moderate | Very large / global |
| Complexity | More control, more effort | Simpler but less flexible |
| Best for | Single-region, custom setups | Multi-region enterprise networks |

---

## When to Use It

- You have **multiple workloads** needing shared network services
- You need **centralized security inspection** (East-West and North-South traffic)
- You're connecting **on-premises** to Azure via a single gateway
- You want **environment isolation** (Dev/Test/Prod) with shared infrastructure

> It's one of the most recommended network architectures in the **Azure Well-Architected Framework** and **Cloud Adoption Framework (CAF)**.

# Regions

---
# Availability zones
- Isolated locations with in a region
- Each zone has independent power and network connectivity.
- Zones in a region are connected through low latency links ( high speed )
- Advantage - increased availability and fault tolerance with in same region, survive the failure of complete datacenter

---

# Sole-tenant nodes 

- These are a Google Cloud feature where an entire physical server is dedicated to a single customer.
- Normally in cloud computing:
- Multiple customers share the same physical server (multi-tenant).
- You only see virtual machines (VMs), not the hardware.
- With sole-tenant nodes:
- The entire physical machine is reserved just for your workloads.
- No other company’s VMs run on that hardware.
- You still use VMs, but they run only on your dedicated host.

---

# Managed Instance Groups

- Managed Instance group - identical vms created using an instance template
- Important Features:
      - Maintain certain number of instances. If an instance crashes, MIG launches another instance
- Detect application features using health checks ( self healing )
- Increase and decrease instances based on load ( auto scaling )
- Add load balancer to distribute load
- create instances in multiple zones ( regional MIGs ) - Regional MIGs provide higher availability compared to zonal MIGs
- release new applicaiton versions without downtime

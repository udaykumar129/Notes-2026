# Regions

# Availability zones
- Isolated locations with in a region
- Each zone has independent power and network connectivity.
- Zones in a region are connected through low latency links ( high speed )
- Advantage - increased availability and fault tolerance with in same region, survive the failure of complete datacenter

# Sole-tenant nodes 

- These are a Google Cloud feature where an entire physical server is dedicated to a single customer.
- Normally in cloud computing:
- Multiple customers share the same physical server (multi-tenant).
- You only see virtual machines (VMs), not the hardware.
- With sole-tenant nodes:
- The entire physical machine is reserved just for your workloads.
- No other company’s VMs run on that hardware.
- You still use VMs, but they run only on your dedicated host.

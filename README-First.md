\# Redis Solution Architect Assignment — Overview



\---



\## 📌 Setup Description



This setup demonstrates a Redis replication architecture deployed on Microsoft Azure using two Linux virtual machines within the same virtual network.



\---



\## 🏗️ Infrastructure Details



\* \*\*Resource Group\*\*: VPN-RG

\* \*\*Virtual Network\*\*: VPNVM-VNET

\* \*\*Address Space\*\*: 10.0.0.0/16

\* \*\*Subnet\*\*: Shared subnet (same for both servers)



\---



\## 🖥️ Servers



\### 🔹 Server A — Primary



\* \*\*Name\*\*: VPNVM

\* \*\*IP Address\*\*: 10.0.0.4

\* \*\*OS\*\*: Linux (Ubuntu 24.04)

\* \*\*Role\*\*: Redis OSS (Primary)



\---



\### 🔹 Server B — Replica



\* \*\*Name\*\*: RedisEnt2

\* \*\*IP Address\*\*: 10.0.0.6

\* \*\*OS\*\*: Linux (Ubuntu 22.04)

\* \*\*Role\*\*: Redis Enterprise (Replica)



\---



\## 🔁 Replication Flow



\* Data is written to \*\*Redis OSS (Server A)\*\*

\* Replication is configured to \*\*Redis Enterprise (Server B)\*\*

\* Both servers are in the same subnet enabling low-latency internal communication



\---



\## 🌐 Network Diagram



!\[Network Diagram](images/network-diagram.png)



\---



\## ✅ Summary



\* Single VNet architecture

\* Two VMs in same subnet

\* OSS → Enterprise replication

\* Private IP communication (secure, internal traffic only)



\---




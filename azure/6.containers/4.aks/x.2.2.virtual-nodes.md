# 🚀 What Are Virtual Nodes?

**Virtual Nodes** allow AKS to burst into **Azure Container Instances (ACI)** — a serverless container runtime — when your cluster needs extra capacity.  
Instead of provisioning new VM-backed nodes, AKS can instantly schedule pods to ACI, giving you **elastic, pay-per-use scaling**.

---

## 🔧 How It Works

- You enable **Virtual Nodes** on an AKS cluster with **Azure CNI**.
- AKS creates a **virtual kubelet** that acts like a node in the cluster.
- When your regular nodes are full, AKS can schedule pods to the virtual node.
- These pods run in **ACI**, not on your VM-backed nodes.

---

## 🧠 Key Benefits

| Feature            | Value                                                                          |
| ------------------ | ------------------------------------------------------------------------------ |
| **Burst capacity** | Instantly scale without waiting for VM provisioning                            |
| **Serverless**     | No need to manage infrastructure for overflow pods                             |
| **Cost-efficient** | Pay only for the ACI runtime used                                              |
| **Integrated**     | Pods scheduled to virtual nodes behave like regular pods (logs, metrics, etc.) |

---

## ⚠️ VIP Notes for DevOps

- **Only supports Linux pods** (no Windows containers).
- **No support for DaemonSets or privileged pods** on virtual nodes.
- **Best for stateless workloads** like jobs, batch, or overflow web traffic.
- **Requires Azure CNI** (not Kubenet).
- **Pods in ACI get public IPs** unless configured otherwise — watch your egress.
- **Billing is per-second for ACI usage**, separate from AKS node pool costs.

---

## 🛠️ How to Enable

You can enable virtual nodes during AKS creation or later via CLI:

```bash
az aks enable-addons \
  --resource-group myRG \
  --name myAKS \
  --addons virtual-node \
  --subnet-name aciSubnet
```

> Make sure `aciSubnet` is in the same VNet and has enough IPs.

---

## 🧪 Use Case Examples

- **Traffic spikes**: Overflow web pods during peak hours.
- **Batch jobs**: Offload compute-heavy jobs without scaling node pools.
- **CI/CD pipelines**: Run ephemeral build/test pods in ACI.

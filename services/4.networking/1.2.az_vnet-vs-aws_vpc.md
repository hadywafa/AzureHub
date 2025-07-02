# 👩‍⚖️ AWS vs Azure

## 📌 **AWS vs Azure – Subnet and Zone Comparison**

> Think of Azure subnets as region-wide slices of IP space. You overlay AZs on top of that _when needed_, without fragmenting your network design.

| Concept                    | AWS                                        | Azure                                               |
| -------------------------- | ------------------------------------------ | --------------------------------------------------- |
| **Subnet**                 | Tied to a specific **Availability Zone**   | Spans the **entire region**, not AZ-specific        |
| **Availability Zone**      | You choose AZ when creating the **subnet** | You choose AZ when creating the **resource**        |
| **VMs/Instances**          | Deployed into subnets, which are AZ-scoped | Deployed into AZs directly, even within same subnet |
| **Cross-AZ Communication** | Requires routing or load balancing setup   | Handled automatically if using a shared subnet      |

---

### ⚙️ **Concrete Example:**

Let’s say you have a VNet (like a VPC in AWS), and you create a subnet with the range `10.0.0.0/24` in Azure:

- In AWS, if that subnet is in `us-east-1a`, you **can’t** place EC2 instances into it from `us-east-1b`.
- In Azure, however, that **same subnet can host VMs across different AZs**, like Zone 1, 2, and 3 of the same region.

You only specify the AZ at **VM deployment**, not when creating the subnet.

---

Absolutely! Since you're coming from an AWS background, let’s stack up **Azure Network Security Groups (NSGs)** side by side with **AWS Security Groups (SGs)** and **Network ACLs (NACLs)**—because Azure NSGs are kind of a hybrid between the two.

---

## 📌 **Azure NSGs vs AWS Security Tools**

| Feature                | **Azure NSG**                                                    | **AWS Security Group**                      | **AWS Network ACL (NACL)**                              |
| ---------------------- | ---------------------------------------------------------------- | ------------------------------------------- | ------------------------------------------------------- |
| **Applies To**         | Subnets or NICs (network interfaces)                             | EC2 instances (via ENIs)                    | Subnets                                                 |
| **Direction of Rules** | Inbound & outbound                                               | Stateful (implies both directions)          | Inbound & outbound                                      |
| **Statefulness**       | **Stateful** (return traffic automatically allowed)              | **Stateful**                                | **Stateless** (must specify both directions explicitly) |
| **Default Rules**      | Built-in rules for deny/allow (lowest priority)                  | Implicit deny all unless explicitly allowed | Implicit deny all unless explicitly allowed             |
| **Rule Evaluation**    | Evaluated by **priority number** (lowest wins)                   | Evaluated as **allow rules only**           | Evaluated in number order (lowest to highest)           |
| **Rule Action**        | **Allow** or **Deny**                                            | **Allow only**                              | **Allow** or **Deny**                                   |
| **Logging Support**    | NSG Flow Logs with Network Watcher                               | VPC Flow Logs                               | VPC Flow Logs                                           |
| **Granularity**        | Supports tags (e.g. `Internet`, `VirtualNetwork`) + service tags | Supports security group referencing         | Limited to IPs, ports, protocols                        |

---

### 🧠 **Mental Model**

- **NSG ≈ SG + NACL Hybrid**  
  Azure NSGs are **stateful like SGs**, but you can apply them at both the subnet and NIC level (more like NACL + SG). They also support **deny rules**, which SGs don’t.

---

### ⚙️ Example Use Case

If you want to:

- Restrict external SSH to a VM
- Allow internal communication among app tiers
- Deny all traffic from a known IP range

**In Azure**, that’s one NSG with inbound/outbound rules—applied to the subnet **and** optionally to the NIC for fine-grained control.

---

Absolutely, Hady. Let's reshape that comparison to tell a clearer story — from a public and private VM perspective — and make it easier to visualize the differences between **Azure and AWS** when it comes to **internet access**.

---

## 📌 **Internet Access Flow: Azure vs AWS**

| Scenario                        | AWS                                                                                                   | Azure                                                                                                                          |
| ------------------------------- | ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **Inbound to VM from Internet** | Requires: <br>• Public IP (dynamic or Elastic IP) <br>• Security Group allow rule <br> <Route to IGW> | Requires: <br>• Public IP (dynamic or Standard static) <br>• NSG inbound allow rule <br> <Azure auto-routes public IP traffic> |
| **Outbound from Private VM**    | Requires: <br>• NAT Gateway <br>• Route table with 0.0.0.0/0 → NAT GW                                 | Requires: <br>• Azure NAT Gateway **or** outbound rules on Load Balancer                                                       |
| **Elastic IP Equivalent**       | Elastic IP (static, reusable)                                                                         | Standard Public IP (static, zone-resilient optional)                                                                           |
| **Internet Gateway?**           | Must attach IGW to VPC                                                                                | **No IGW needed.** Internet access auto-managed if public IP assigned                                                          |
| **Route Table Config**          | Manual setup: <br>• 0.0.0.0/0 → IGW (public) <br>• 0.0.0.0/0 → NAT GW (private)                       | Usually **no manual route** needed for public VMs <br>Only set up routes for NAT Gateway manually                              |
| **Security Layer**              | Security Groups (stateful) + NACLs (stateless)                                                        | NSGs (stateful) + optional Azure Firewall                                                                                      |

---

### 🧠 **Quick Visual Model**

**AWS (Public VM):**

- EC2 instance ← Public IP
- Route → IGW
- SG allows SSH  
  ✅ Internet inbound + outbound

**Azure (Public VM):**

- VM ← Public IP (assigned to NIC)
- NSG allows SSH  
  ✅ Internet inbound + outbound (routing is built-in)

---

### 🧩 **Where People Often Get Tripped Up**

- **No IGW in Azure**: Azure abstracts the internet gateway concept—you don’t need to provision or attach one.
- **Routing simplicity**: Azure handles internet routing **automatically** when a public IP is attached and NSG allows traffic.
- **Outbound needs planning**: Just like AWS, for **private-only VMs**, you’ll still need a NAT Gateway in Azure.

---

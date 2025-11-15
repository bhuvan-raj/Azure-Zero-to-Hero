# Hierrarchy in Azure
<img src="https://github.com/bhuvan-raj/Azure-Zero-to-Hero/blob/main/assets/hierrarchy.png" alt="Banner" />

## Overview
Azure uses a hierarchical organizational structure to manage resources, governance, billing, and access control. Understanding this hierarchy is crucial for proper Azure administration and architecture.

---

# **🔥 Full Explanation**

### **1. Tenant (Entra ID Tenant)**

* The top-most identity boundary for your organization.

### **2. Management Groups**

* Used to structure multiple subscriptions.
* Policies & RBAC applied here flow downward.

### **3. Subscriptions**

* Billing boundary.
* All resources must be inside a subscription.

### **4. Resource Groups**

* Logical containers grouping related resources.

### **5. Resources**

* The actual Azure services:

  * VM
  * Storage Account
  * VNet
  * App Service
  * AKS
  * Key Vault
  * etc.

---

# **📘 Official Diagram (ASCII Hierarchy)**

```
                      +---------------------------+
                      |      Azure Tenant         |
                      |     (Entra ID Tenant)     |
                      +-------------+-------------+
                                    |
                         +----------+----------+
                         |     Management       |
                         |       Group          |
                         +----------+----------+
                                    |
        -------------------------------------------------
        |                                               |
+-------+--------+                             +--------+-------+
|   Subscription |                             |   Subscription |
+-------+--------+                             +--------+-------+
        |                                               |
   -------------                                   ---------------
   |           |                                   |             |
+--+--+    +---+---+                          +----+---+     +---+---+
| RG1 |    |  RG2  |                          |   RG1   |    |  RG2  |
+--+--+    +---+---+                          +----+---+     +---+---+
   |           |                                   |              |
   |           |                                   |              |
   |       -------------                       ----------      ----------
   |       |     |     |                       |    |   |      |    |   |
+------+ +------+ +-------+                +--------+---+   +-------+---+
| VM   | | VNet | | Storage|                | AKS Cluster | | Key Vault |
+------+ +------+ +--------+                +------------+  +-----------+
```

---

If you want a **DevOps-oriented version** or a **real enterprise hierarchy example**, just tell me Bubu 😌🔥

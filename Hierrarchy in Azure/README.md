# Hierrarchy in Azure


```
Azure Active Directory (AAD) Tenant
            |
    Management Groups
            |
      Subscriptions
            |
      Resource Groups
            |
        Resources
```

## Overview
Azure uses a hierarchical organizational structure to manage resources, governance, billing, and access control. Understanding this hierarchy is crucial for proper Azure administration and architecture.

---

# ** Full Explanation**

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

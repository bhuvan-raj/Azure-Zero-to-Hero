# Azure Hierarchy Structure - Complete Guide


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

## **1. Azure Active Directory (AAD) Tenant / Microsoft Entra ID**

### **What is it?**
The **AAD Tenant** (now called Microsoft Entra ID) is the root of your Azure hierarchy. It's a dedicated instance of Azure Active Directory that represents your organization.

### **Key Characteristics:**

**Identity and Access Management:**
- Central identity provider for all Azure resources
- Manages users, groups, and service principals
- Handles authentication and authorization
- Single sign-on (SSO) across applications

**Tenant Properties:**
- **Unique identifier:** Every tenant has a unique Tenant ID (GUID)
- **Primary domain:** yourcompany.onmicrosoft.com
- **Custom domains:** Can add verified custom domains (yourcompany.com)
- **Global uniqueness:** Tenant names must be globally unique

**What Lives in AAD Tenant:**
- User accounts (employees, partners)
- Groups (security groups, Microsoft 365 groups)
- Service principals (application identities)
- Managed identities
- App registrations
- External identities (B2B guest users)
- Devices registered/joined to AAD

### **Important Concepts:**

**Single Tenant vs Multi-Tenant:**
- **Single tenant:** One organization = one AAD tenant (most common)
- **Multi-tenant:** Some organizations have multiple tenants (separate business units, acquisitions)
- Typically, one organization should use one tenant

**Tenant-Level Features:**
- Conditional Access policies
- Multi-factor authentication (MFA)
- Password policies
- Security defaults
- Identity protection
- Privileged Identity Management (PIM)

### **Common Scenarios:**

**Example 1: Small Business**
```
Contoso Ltd.
└── AAD Tenant: contoso.onmicrosoft.com
    ├── 50 user accounts
    ├── 10 security groups
    └── 1 subscription
```

**Example 2: Enterprise**
```
Fabrikam Corporation
└── AAD Tenant: fabrikam.onmicrosoft.com
    ├── 10,000 user accounts
    ├── 500+ groups
    ├── Synced with on-premises Active Directory
    └── Multiple subscriptions
```

### **Key Differences: AAD vs On-Premises Active Directory**

| Feature | On-Premises AD | Azure AD (Entra ID) |
|---------|----------------|---------------------|
| **Purpose** | Network resources | Cloud applications |
| **Protocol** | Kerberos, LDAP | HTTP/HTTPS, OAuth, SAML |
| **Structure** | Domains, OUs, forests | Flat structure, tenants |
| **Authentication** | Windows auth | Modern auth (OAuth2, OpenID) |
| **Objects** | Computers, GPOs | Apps, devices, licenses |

### **Tenant-Level Roles:**

**Global Administrator:**
- Highest level of access
- Full control over AAD tenant
- Can manage all Azure subscriptions
- Should be limited to 2-5 people

**Other Important Roles:**
- User Administrator
- Security Administrator
- Billing Administrator
- Application Administrator
- Cloud Application Administrator

### **Best Practices:**
- ✓ Use one AAD tenant per organization
- ✓ Limit Global Administrators (max 5 people)
- ✓ Enable MFA for all administrative accounts
- ✓ Use Privileged Identity Management (PIM)
- ✓ Implement Conditional Access policies
- ✓ Sync with on-premises AD if applicable
- ✓ Regular access reviews

---

## **2. Management Groups**

### **What Are Management Groups?**

Management Groups are **containers that help you manage access, policies, and compliance across multiple Azure subscriptions**. They provide enterprise-grade management at scale.

### **Key Characteristics:**

**Hierarchy Features:**
- Can nest up to **6 levels deep** (excluding root and subscription level)
- Each management group can have many children
- Each child (subscription or management group) has only one parent
- Inheritance flows down from parent to children

**What They Enable:**
- Apply policies across multiple subscriptions
- Organize subscriptions by department, environment, or geography
- Implement governance at scale
- Role-Based Access Control (RBAC) inheritance
- Budget management across subscriptions

### **Management Group Structure:**

```
Root Management Group (Tenant Root Group)
    |
    ├── Management Group: Production
    |   ├── Subscription: Prod-App1
    |   ├── Subscription: Prod-App2
    |   └── Subscription: Prod-Database
    |
    ├── Management Group: Non-Production
    |   ├── Management Group: Development
    |   |   ├── Subscription: Dev-Team1
    |   |   └── Subscription: Dev-Team2
    |   |
    |   └── Management Group: Testing
    |       ├── Subscription: Test-App1
    |       └── Subscription: Test-QA
    |
    └── Management Group: Shared Services
        ├── Subscription: Networking
        └── Subscription: Security
```

### **Root Management Group:**

**Characteristics:**
- Automatically created for each AAD tenant
- Cannot be moved or deleted
- Includes ALL subscriptions in the tenant
- Name: "Tenant Root Group" (can be customized)
- ID: Same as AAD Tenant ID

**Root-Level Capabilities:**
- Apply policies to all subscriptions
- Global RBAC assignments
- Compliance requirements across organization

### **Detailed Example: Enterprise Structure**

```
Fabrikam Corporation (Root)
    |
    ├── Corporate (Management Group)
    |   ├── Finance (Management Group)
    |   |   ├── Finance-Prod (Subscription)
    |   |   └── Finance-Dev (Subscription)
    |   |
    |   ├── HR (Management Group)
    |   |   ├── HR-Prod (Subscription)
    |   |   └── HR-Dev (Subscription)
    |   |
    |   └── IT (Management Group)
    |       ├── IT-Infrastructure (Subscription)
    |       └── IT-Security (Subscription)
    |
    ├── Business Units (Management Group)
    |   ├── Manufacturing (Management Group)
    |   |   ├── Manufacturing-Prod (Subscription)
    |   |   └── Manufacturing-Dev (Subscription)
    |   |
    |   └── Sales (Management Group)
    |       ├── Sales-Prod (Subscription)
    |       └── Sales-Dev (Subscription)
    |
    └── Sandbox (Management Group)
        ├── Sandbox-Team1 (Subscription)
        ├── Sandbox-Team2 (Subscription)
        └── Sandbox-Team3 (Subscription)
```

### **Use Cases for Management Groups:**

**1. Policy Enforcement:**
```
Production Management Group
├── Policy: Require encryption for all storage accounts
├── Policy: Only allow specific VM sizes
├── Policy: Require tags (CostCenter, Owner)
└── Inherited by all child subscriptions
```

**2. Cost Management:**
```
Department Management Group
├── Budget: $100,000/month
├── Alert at 80% usage
└── Applies to all subscriptions within
```

**3. RBAC at Scale:**
```
Development Management Group
├── RBAC: Developer Group = Contributor
├── RBAC: Architects = Owner
└── All developers get Contributor on all dev subscriptions
```

**4. Geographic Organization:**
```
Root
├── North America
|   ├── US-East
|   └── US-West
├── Europe
|   ├── EU-West
|   └── EU-North
└── Asia Pacific
    ├── APAC-East
    └── APAC-Southeast
```

**5. Environment Separation:**
```
Root
├── Production (strict policies)
├── Staging (moderate policies)
├── Development (relaxed policies)
└── Sandbox (minimal policies)
```

### **Policy Inheritance Example:**

```
Root Management Group
├── Policy: All resources must have 'Owner' tag ✓
|
└── Production Management Group
    ├── Inherits: 'Owner' tag requirement ✓
    ├── Policy: Deny public IP addresses ✓
    |
    └── Production-App1 Subscription
        ├── Inherits: 'Owner' tag requirement ✓
        ├── Inherits: Deny public IPs ✓
        └── All resources must comply with both policies
```

### **Management Group Limitations:**

- **6 levels of depth** (not including root and subscription)
- **10,000 management groups** per AAD tenant
- Each management group tree can support up to **10,000 children** (subscriptions + management groups)
- **30 seconds** to reflect management group hierarchy changes

### **RBAC in Management Groups:**

**Scope Inheritance:**
```
Management Group (Contributor assigned here)
    ↓ (inheritance)
Child Subscription 1 (automatically has Contributor)
Child Subscription 2 (automatically has Contributor)
Child Subscription 3 (automatically has Contributor)
```

**Common RBAC Assignments:**
- **Management Group Contributor:** Manage the management group itself
- **Owner:** Full access to subscriptions within
- **Contributor:** Deploy and manage resources
- **Reader:** View-only access
- Custom roles for specific needs

### **Best Practices:**

**Organization:**
- ✓ Design hierarchy before implementing
- ✓ Keep hierarchy simple (3-4 levels typically sufficient)
- ✓ Align with organizational structure
- ✓ Use consistent naming conventions

**Governance:**
- ✓ Apply policies at highest appropriate level
- ✓ Use management groups for environment separation
- ✓ Implement least privilege access
- ✓ Document hierarchy and policies

**Security:**
- ✓ Limit who can create/modify management groups
- ✓ Use Privileged Identity Management (PIM)
- ✓ Regular access reviews
- ✓ Enable Azure Policy for compliance

### **When NOT to Use Management Groups:**

- Small organizations with 1-2 subscriptions
- No need for cross-subscription governance
- Simple organizational structure
- Just starting with Azure (can add later)

---

## **3. Subscriptions**

### **What is an Azure Subscription?**

A **subscription** is a logical container for your Azure resources. It's also the **billing boundary** and **access control boundary** for Azure services.

### **Key Characteristics:**

**Primary Functions:**
1. **Billing boundary:** Each subscription has its own bill
2. **Resource container:** Holds resource groups and resources
3. **Access boundary:** RBAC scope for managing resources
4. **Service limits boundary:** Each subscription has its own quotas

**Subscription Properties:**
- **Subscription ID:** Unique GUID identifier
- **Subscription name:** Human-readable name
- **Subscription type:** Free, Pay-As-You-Go, Enterprise, CSP, etc.
- **Associated AAD tenant:** Trusts one AAD tenant
- **Owner/administrator:** Users with access

### **Subscription Types:**

**1. Free Trial:**
- $200 credit for 30 days
- 12 months of popular free services
- Always-free services
- Converts to Pay-As-You-Go after trial

**2. Pay-As-You-Go:**
- Standard retail pricing
- No upfront commitment
- Pay for what you use
- Most flexible option
- For individuals and small businesses

**3. Enterprise Agreement (EA):**
- For organizations with 500+ users/devices
- Discounted pricing
- 3-year commitment
- Prepaid annual commitment
- Organizational accounts
- Volume licensing benefits

**4. Cloud Solution Provider (CSP):**
- Through Microsoft partners
- Partner manages billing
- Bundled with partner services
- Monthly billing
- Partner provides support

**5. Microsoft Partner Network (MPN):**
- For Microsoft partners
- Monthly Azure credits
- Based on partnership level
- Not for production workloads

**6. Visual Studio Subscriptions:**
- Monthly credits ($50-$150/month)
- For development and testing
- Cannot be used for production
- Based on Visual Studio subscription tier

**7. Microsoft for Startups:**
- For eligible startups
- Up to $150,000 in credits
- Technical support included
- Application required

### **Subscription as Billing Boundary:**

**How Billing Works:**
```
Subscription: Production-Apps
├── Month: January 2024
├── Resource Group: Web-Apps
|   ├── App Service: $100
|   └── SQL Database: $200
├── Resource Group: Storage
|   └── Storage Account: $50
└── Total Bill: $350
```

**Multiple Subscriptions for Cost Separation:**
```
AAD Tenant: Contoso
├── Subscription: Production ($10,000/month)
├── Subscription: Development ($2,000/month)
├── Subscription: Testing ($1,500/month)
└── Each receives separate monthly invoice
```

### **Subscription Limits and Quotas:**

**Common Limits (per subscription):**
- **Resource Groups:** 980 per subscription
- **VMs:** 25,000 per region
- **Storage Accounts:** 250 per region
- **Virtual Networks:** 1,000 per region
- **Public IP Addresses:** Varies by region
- **Network Security Groups:** 5,000 per region
- **Load Balancers:** 1,000 (standard)

**Why Limits Matter:**
- Prevent accidental resource sprawl
- Ensure fair resource distribution
- Can request limit increases via support ticket
- Some limits are hard (cannot be increased)

### **When to Use Multiple Subscriptions:**

**1. Billing Separation:**
```
Finance Department
├── Finance-Prod Subscription → Finance dept pays
├── IT-Prod Subscription → IT dept pays
└── HR-Prod Subscription → HR dept pays
```

**2. Environment Isolation:**
```
Company Structure
├── Production Subscription (strict policies)
├── Staging Subscription (moderate policies)
├── Development Subscription (relaxed policies)
└── Sandbox Subscription (minimal policies)
```

**3. Regional Separation:**
```
Global Company
├── North-America Subscription
├── Europe Subscription
├── Asia-Pacific Subscription
└── Each handles local compliance requirements
```

**4. Organizational Boundaries:**
```
Large Enterprise
├── Business-Unit-A Subscription
├── Business-Unit-B Subscription
├── Shared-Services Subscription
└── Security-Services Subscription
```

**5. Quota/Limit Requirements:**
```
High-Scale Application
├── Subscription-1 (25,000 VMs)
├── Subscription-2 (25,000 VMs)
└── Total: 50,000 VMs across subscriptions
```

**6. Security Boundaries:**
```
Security Separation
├── High-Security Subscription (financial data)
├── Medium-Security Subscription (business data)
└── Low-Security Subscription (public content)
```

### **Subscription Design Patterns:**

**Pattern 1: Single Subscription (Small Organizations)**
```
Small Business
└── Primary Subscription
    ├── Production Resource Group
    ├── Development Resource Group
    └── Testing Resource Group
```
- **Pros:** Simple to manage, single bill
- **Cons:** No billing separation, shared limits

**Pattern 2: Environment-Based**
```
Company
├── Prod Subscription ($100K/month)
├── Stage Subscription ($20K/month)
├── Dev Subscription ($10K/month)
└── Sandbox Subscription ($5K/month)
```
- **Pros:** Clear environment separation, different policies
- **Cons:** Multiple subscriptions to manage

**Pattern 3: Department-Based**
```
Enterprise
├── Finance Subscription
├── HR Subscription
├── IT Subscription
├── Sales Subscription
└── Shared Services Subscription
```
- **Pros:** Chargeback to departments, clear ownership
- **Cons:** Complexity, potential resource duplication

**Pattern 4: Application-Based**
```
Software Company
├── App-Product1 Subscription
├── App-Product2 Subscription
├── App-Product3 Subscription
└── Platform-Services Subscription
```
- **Pros:** Cost per product, clear boundaries
- **Cons:** Many subscriptions, cross-app services complex

**Pattern 5: Hybrid (Most Common)**
```
Large Organization
├── Shared Services
|   ├── Networking Subscription
|   └── Security Subscription
├── Production
|   ├── Prod-App1 Subscription
|   └── Prod-App2 Subscription
└── Non-Production
    ├── Development Subscription
    └── Testing Subscription
```
- **Pros:** Balanced approach, clear separation
- **Cons:** Moderate complexity

### **Subscription Lifecycle:**

**1. Creation:**
- Created via Azure Portal, CLI, or PowerShell
- Associated with AAD tenant
- Assigned subscription type
- Initial owner designated

**2. Active State:**
- Resources can be deployed
- Billing is active
- Policies enforced
- RBAC in effect

**3. Disabled State:**
- Triggered by payment issues
- Resources stop but aren't deleted
- Cannot deploy new resources
- Read-only access

**4. Deleted/Cancelled:**
- All resources deleted after 90 days
- Cannot be recovered after deletion
- Billing stops immediately

### **Subscription Transfer:**

**Scenarios:**
- Change from CSP to EA
- Company acquisition/merger
- Change billing ownership
- Move between AAD tenants

**Considerations:**
- Some transfers require support ticket
- Can affect resource access temporarily
- RBAC assignments may need reconfiguration
- Test in non-production first

### **Subscription RBAC:**

**Key Roles:**

**Owner:**
- Full access to all resources
- Can grant access to others
- Manage all aspects of subscription
- Highest privilege level

**Contributor:**
- Create and manage all resources
- Cannot grant access to others
- Cannot change subscription settings
- Developer/admin role

**Reader:**
- View all resources
- Cannot make any changes
- Read-only access
- Audit and monitoring use

**Custom Roles:**
- Tailored permissions
- Specific to organizational needs
- Based on Actions/NotActions
- Can be scoped to subscription

### **Subscription Best Practices:**

**Naming Convention:**
```
<Company>-<Environment>-<Department>-<Region>-<Purpose>

Examples:
Contoso-Prod-Finance-EastUS-Apps
Contoso-Dev-IT-WestEU-Shared
Fabrikam-Stage-Sales-AsiaPac-Web
```

**Organization:**
- ✓ Use meaningful, consistent names
- ✓ Document subscription purpose
- ✓ Tag subscriptions for cost tracking
- ✓ Implement naming standards

**Security:**
- ✓ Limit subscription owners (2-5 people)
- ✓ Use Privileged Identity Management (PIM)
- ✓ Enable Azure Policy
- ✓ Configure Microsoft Defender for Cloud
- ✓ Regular access reviews

**Cost Management:**
- ✓ Set budgets and alerts
- ✓ Use Cost Management + Billing
- ✓ Tag resources for cost allocation
- ✓ Review spending regularly
- ✓ Right-size resources

**Governance:**
- ✓ Apply Azure Policies
- ✓ Use Blueprints for standardization
- ✓ Implement naming conventions
- ✓ Regular compliance audits

### **Common Mistakes to Avoid:**

- ❌ Too many subscriptions (over-segmentation)
- ❌ Unclear ownership and responsibility
- ❌ Inconsistent naming conventions
- ❌ No cost monitoring or budgets
- ❌ Overly permissive RBAC assignments
- ❌ No disaster recovery plan
- ❌ Mixing production and development
- ❌ Not using management groups when needed

---

## **4. Resource Groups**

### **What is a Resource Group?**

A **resource group** is a **logical container** that holds related Azure resources. It's the fundamental organizational unit within a subscription.

### **Key Characteristics:**

**Core Concepts:**
- **Lifecycle management:** Deploy, update, or delete resources together
- **Logical grouping:** Group resources that share the same lifecycle
- **Access control boundary:** Apply RBAC at resource group level
- **Deployment unit:** ARM templates deploy to resource groups
- **No nesting:** Cannot create resource groups within resource groups

**Resource Group Properties:**
- **Name:** Must be unique within subscription
- **Location (Region):** Where metadata is stored (not resources)
- **Subscription:** Belongs to exactly one subscription
- **Tags:** Key-value pairs for organization
- **Locks:** Prevent accidental deletion/modification

### **What Goes in a Resource Group?**

**Resources with Shared:**
- **Lifecycle:** Created, updated, deleted together
- **Ownership:** Same team/department manages
- **Purpose:** Serve the same application/workload
- **Environment:** Same stage (prod, dev, test)

### **Resource Group Organization Patterns:**

**Pattern 1: Application-Based (Most Common)**
```
Subscription: Production
├── RG: webapp-frontend-prod
|   ├── App Service Plan
|   ├── App Service
|   ├── Application Insights
|   └── CDN Profile
|
├── RG: webapp-backend-prod
|   ├── App Service Plan
|   ├── App Service (API)
|   ├── API Management
|   └── Application Insights
|
├── RG: webapp-data-prod
|   ├── SQL Server
|   ├── SQL Database
|   ├── Storage Account
|   └── Key Vault
|
└── RG: webapp-network-prod
    ├── Virtual Network
    ├── Network Security Groups
    ├── Public IP Addresses
    └── Application Gateway
```

**Pattern 2: Tier-Based**
```
Subscription: Company-Production
├── RG: web-tier-prod
|   ├── Load Balancer
|   ├── VM Scale Set (Web Servers)
|   └── Public IP
|
├── RG: app-tier-prod
|   ├── Internal Load Balancer
|   ├── VM Scale Set (App Servers)
|   └── Application Insights
|
├── RG: data-tier-prod
|   ├── SQL Database
|   ├── Cosmos DB
|   ├── Storage Accounts
|   └── Redis Cache
|
└── RG: shared-services-prod
    ├── Virtual Network
    ├── VPN Gateway
    ├── Key Vault
    └── Log Analytics Workspace
```

**Pattern 3: Lifecycle-Based**
```
Subscription: Development
├── RG: app1-resources-v1
|   ├── Old version resources
|   ├── Can be deleted as a unit
|   └── Retained for rollback
|
├── RG: app1-resources-v2
|   ├── Current version resources
|   ├── Active in production
|   └── Delete v1 after stable
|
└── RG: app1-resources-v3
    ├── Next version resources
    ├── Being tested
    └── Will replace v2
```

**Pattern 4: Environment + Application**
```
Subscription: Multi-Environment
├── RG: prod-ecommerce-web
├── RG: prod-ecommerce-api
├── RG: prod-ecommerce-data
├── RG: dev-ecommerce-web
├── RG: dev-ecommerce-api
├── RG: dev-ecommerce-data
├── RG: test-ecommerce-web
├── RG: test-ecommerce-api
└── RG: test-ecommerce-data
```

**Pattern 5: Team/Department-Based**
```
Subscription: Corporate-IT
├── RG: finance-team-resources
├── RG: hr-team-resources
├── RG: sales-team-resources
├── RG: marketing-team-resources
└── RG: it-team-resources
```

### **Resource Group Naming Conventions:**

**Best Practice Format:**
```
<app/workload>-<component>-<environment>-<region>-rg

Examples:
ecommerce-web-prod-eastus-rg
ecommerce-api-prod-eastus-rg
ecommerce-data-prod-eastus-rg
crm-app-dev-westeu-rg
analytics-processing-stage-centralus-rg
```

**Components Explained:**
- **app/workload:** Application or workload name
- **component:** Tier or function (web, api, data, network)
- **environment:** prod, dev, test, stage, sandbox
- **region:** Azure region abbreviation
- **rg:** Resource Group suffix

### **Resource Group Location (Metadata)**

**Important Distinction:**
```
Resource Group Location: East US (where metadata stored)
    ├── Storage Account: West US
    ├── SQL Database: North Europe
    ├── VM: East Asia
    └── Resources can be in ANY region
```

**Why It Matters:**
- Metadata stored in resource group location
- Affects data residency compliance
- Doesn't limit where resources can be deployed
- Choose location for compliance or proximity

**Best Practice:**
- Place resource group in same region as most resources
- Consider data sovereignty requirements
- If compliance critical, place in required region

### **Resource Group Access Control (RBAC):**

**RBAC Inheritance:**
```
Subscription (Reader)
    ↓ (inherits Reader)
Resource Group (Contributor assigned here)
    ↓ (inherits Reader + gets Contributor)
Resource
    ← Has both Reader and Contributor
```

**Common RBAC Patterns:**

**Pattern 1: Team-Based Access**
```
RG: prod-web-app-rg
├── App Team: Contributor (deploy and manage)
├── DBA Team: Reader (view only on web resources)
├── Security Team: Security Admin
└── Auditors: Reader
```

**Pattern 2: Environment-Based**
```
RG: production-app-rg
├── Production Team: Contributor
└── Developers: Reader (view-only in production)

RG: development-app-rg
├── Developers: Contributor (full access in dev)
└── Production Team: Reader
```

**Pattern 3: Separation of Duties**
```
RG: database-resources-rg
├── DBA Team: Contributor (manage databases)
├── App Team: Reader (view only)
└── Backup Admin: Backup Contributor (backup only)
```

### **Resource Group Locks:**

**Lock Types:**

**1. CanNotDelete Lock:**
- Can read and modify resources
- **Cannot delete** resources
- Protection against accidental deletion
- Most commonly used

**2. ReadOnly Lock:**
- Can only **read** resources
- Cannot modify or delete
- Strictest protection
- Can impact operations

**Lock Inheritance:**
```
Resource Group (CanNotDelete lock applied)
    ↓
All resources inherit lock
    ├── Virtual Machine (protected)
    ├── Disk (protected)
    ├── Network Interface (protected)
    └── Cannot delete any of these
```

**Use Cases:**
```
Critical Production RG
├── CanNotDelete lock
├── Prevents accidental deletion
├── Must remove lock to delete
└── Good for production databases, networking

Compliance Environment
├── ReadOnly lock during audit
├── Prevents any changes
├── Remove lock after audit
└── Ensures integrity during review
```

**Best Practices:**
- ✓ Lock critical production resource groups
- ✓ Use CanNotDelete for most scenarios
- ✓ Document why locks are applied
- ✓ Process for removing locks when needed
- ✓ Use ReadOnly sparingly (can break operations)

### **Resource Group Tags:**

**What Are Tags?**
Key-value pairs for organizing and tracking resources:
```
Key: Value
Environment: Production
CostCenter: IT-001
Owner: john.doe@company.com
Project: CustomerPortal
Expiration: 2024-12-31
```

**Common Tagging Strategies:**

**1. Cost Allocation:**
```
Resource Group: prod-app-rg
├── CostCenter: IT-001
├── Department: Finance
├── Project: OnlineBanking
└── Budget: FY2024-Q1
```

**2. Operational:**
```
Resource Group: web-app-rg
├── Environment: Production
├── SLA: 99.9%
├── MaintenanceWindow: Sunday-02:00-04:00
└── Owner: webapp-team@company.com
```

**3. Security/Compliance:**
```
Resource Group: sensitive-data-rg
├── DataClassification: Confidential
├── Compliance: PCI-DSS
├── BackupRequired: Yes
└── DRRequired: Yes
```

**4. Lifecycle Management:**
```
Resource Group: test-env-rg
├── Environment: Testing
├── CreatedDate: 2024-01-15
├── ExpirationDate: 2024-03-15
└── AutoShutdown: Enabled
```

**Tag Inheritance:**
- Tags do NOT automatically inherit from resource group to resources
- Must apply tags explicitly to resources if needed
- Can use Azure Policy to enforce tagging
- Automation scripts can copy tags

**Azure Policy for Tags:**
```
Policy: Require tags on resource groups
├── Required tags: Environment, Owner, CostCenter
├── Deny creation if tags missing
└── Applied at subscription level
```

### **Resource Group Deployment:**

**ARM Templates (Infrastructure as Code):**
```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "resources": [
    {
      "type": "Microsoft.Web/serverfarms",
      "apiVersion": "2021-02-01",
      "name": "myAppServicePlan",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "S1",
        "tier": "Standard"
      }
    }
  ]
}
```

**Deployment Scope:**
- ARM templates deploy to resource groups
- All resources created in specified resource group
- Can reference other resource groups if needed
- Atomic operation: all or nothing

**Linked Templates:**
```
Main Template (deploys to RG: networking)
├── Deploys Virtual Network
└── References template for Subnets

Linked Template (same RG)
├── Deploys Subnets
└── Depends on VNet from main template
```

### **Moving Resources Between Resource Groups:**

**When You Can Move:**
- Same subscription (usually possible)
- Different subscription (depends on resource type)
- Some resources cannot be moved
- Check Azure documentation for specific resource

**What Happens During Move:**
- Source and destination RGs locked
- Resource IDs change
- Tags are preserved
- RBAC may need reconfiguration
- No downtime for most resources

**Move Example:**
```
Before:
RG: old-rg
└── VM: myVM

After Move:
RG: new-rg
└── VM: myVM (new resource ID)
```

**Resources That Cannot Move:**
- Some Azure services are region-specific
- Resources with dependencies may require moving dependencies
- Check Microsoft documentation before moving

### **Resource Group Limits:**

- **980 resource groups** per subscription
- **800 deployments** per resource group (deployment history)
- **No limit** on number of resources per resource group (within subscription limits)
- Template size: **4 MB** maximum
- Parameter file size: **64 KB** maximum

### **Resource Group Best Practices:**

**Organization:**
- ✓ Group resources by lifecycle
- ✓ Use consistent naming conventions
- ✓ Document resource group purpose
- ✓ Keep related resources together
- ✓ Separate by environment when needed

**Security:**
- ✓ Apply principle of least privilege
- ✓ Use RBAC at resource group level
- ✓ Lock critical resource groups
- ✓ Regular access reviews
- ✓ Use managed identities where possible

**Management:**
- ✓ Tag all resource groups
- ✓ Use Azure Policy for governance
- ✓ Deploy via ARM templates/Bicep
- ✓ Clean up unused resource groups
- ✓ Monitor costs per resource group

**Cost Optimization:**
- ✓ Track costs by resource group
- ✓ Set budgets and alerts
- ✓ Identify and remove unused resources
- ✓ Right-size resources regularly
- ✓ Use tags

---

# In-Depth Study Guide: Azure Storage

## **1. Introduction to Azure Storage**

### **What is Azure Storage?**

Azure Storage is Microsoft's **cloud storage solution** for modern data storage scenarios. It provides massively scalable, durable, and highly available storage for data objects, file shares, message queues, NoSQL data, and virtual machine disks.

### **Why Azure Storage?**

**Key Benefits:**

**1. Durability and High Availability**
- 11 nines (99.999999999%) durability
- Multiple redundancy options
- Automatic replication
- Geographic distribution
- Built-in disaster recovery

**2. Scalability**
- Virtually unlimited storage capacity
- Exabytes of data storage
- Millions of requests per second
- Auto-scaling capabilities
- No capacity planning required

**3. Security**
- Encryption at rest (256-bit AES)
- Encryption in transit (HTTPS/TLS)
- Multiple authentication methods
- Network isolation options
- Compliance certifications (GDPR, HIPAA, ISO, SOC, etc.)

**4. Accessibility**
- Access from anywhere over HTTPS
- REST APIs for programmatic access
- Client libraries (.NET, Java, Python, Node.js, etc.)
- Azure Portal, CLI, PowerShell
- Mobile and desktop applications

**5. Cost-Effectiveness**
- Pay only for what you use
- Multiple access tiers for cost optimization
- No upfront costs
- Storage capacity pricing
- Transaction pricing

**6. Manageability**
- Fully managed service
- No hardware maintenance
- Automatic updates
- Built-in monitoring
- Integration with Azure services

### **Azure Storage Services Overview**

Azure Storage offers **five main services**:

```
Azure Storage Account
    |
    ├── Blob Storage (Object Storage)
    |   └── Unstructured data, files, media, backups
    |
    ├── Azure Files (File Shares)
    |   └── SMB/NFS file shares, lift-and-shift
    |
    ├── Queue Storage (Message Queue)
    |   └── Messaging between applications
    |
    ├── Table Storage (NoSQL)
    |   └── Structured NoSQL data
    |
    └── Disk Storage (Managed Disks)
        └── Block storage for VMs
```

**Quick Comparison:**

| Service | Purpose | Protocol | Use Case |
|---------|---------|----------|----------|
| **Blob** | Object storage | HTTP/HTTPS REST | Files, media, backups, data lakes |
| **Files** | File shares | SMB 3.0, NFS 4.1 | Shared files, lift-and-shift |
| **Queue** | Messaging | HTTP/HTTPS REST | Async messaging, decoupling |
| **Table** | NoSQL data | HTTP/HTTPS REST | Structured data, key-value store |
| **Disk** | VM disks | iSCSI | OS and data disks for VMs |

### **Storage Account Hierarchy**

```
Azure Subscription
    |
    └── Resource Group
        |
        └── Storage Account (mystorageaccount)
            |
            ├── Blob Service
            |   ├── Container: images
            |   |   ├── Blob: photo1.jpg
            |   |   └── Blob: photo2.jpg
            |   └── Container: videos
            |       └── Blob: video1.mp4
            |
            ├── File Service
            |   ├── File Share: share1
            |   |   ├── Directory: documents
            |   |   └── File: report.docx
            |   └── File Share: share2
            |
            ├── Queue Service
            |   ├── Queue: orders
            |   └── Queue: notifications
            |
            └── Table Service
                ├── Table: customers
                └── Table: products
```

---

## **2. Azure Storage Account Fundamentals**

### **What is a Storage Account?**

A **Storage Account** is a unique namespace in Azure that provides access to Azure Storage services. It's the **fundamental container** for all your Azure Storage data objects.

### **Storage Account Naming Rules**

**Requirements:**
- **Length:** 3 to 24 characters
- **Characters:** Lowercase letters and numbers only
- **Uniqueness:** Globally unique across all of Azure
- **No special characters:** No hyphens, underscores, or spaces
- **Cannot change:** Name is immutable after creation

**Valid Examples:**
```
mystorageaccount123
contosostg2024
prodappdata001
```

**Invalid Examples:**
```
MyStorageAccount     ❌ (uppercase)
storage-account      ❌ (hyphen)
storage_account      ❌ (underscore)
st                   ❌ (too short)
my-storage-account-very-long-name  ❌ (too long)
```

**Naming Convention Best Practice:**
```
<company><environment><region><purpose><number>

Examples:
contosoprodeusweb001
fabrikamdevwestdata002
adatumtestcusapp001
```

### **Storage Account Components**

**Every Storage Account Has:**

**1. Account Name**
- Globally unique identifier
- Part of the endpoint URL
- Example: `mystorageaccount`

**2. Account Endpoints**
Each storage service gets a unique endpoint:

```
Blob Service:
https://mystorageaccount.blob.core.windows.net

File Service:
https://mystorageaccount.file.core.windows.net

Queue Service:
https://mystorageaccount.queue.core.windows.net

Table Service:
https://mystorageaccount.table.core.windows.net
```

**3. Account Keys (Access Keys)**
- Two 512-bit keys for authentication
- Provide full access to storage account
- Can be regenerated independently
- Should be kept secure (like passwords)

```
Primary Access Key: 
[512-bit key]

Secondary Access Key: 
[512-bit key]
```

**Why Two Keys?**
- Key rotation without downtime
- Update applications to use Key 2
- Regenerate Key 1
- Update applications back to Key 1
- Regenerate Key 2

**4. Connection String**
Pre-formatted string containing endpoint and key:
```
DefaultEndpointsProtocol=https;
AccountName=mystorageaccount;
AccountKey=youraccountkey==;
EndpointSuffix=core.windows.net
```

### **Storage Account Properties**

**Location (Region):**
- Where data is physically stored
- Affects latency, cost, compliance
- Cannot be changed after creation
- Choose closest region to users/applications

**Performance Tier:**
- **Standard:** HDD-backed, cost-effective
- **Premium:** SSD-backed, low latency

**Replication:**
- LRS, ZRS, GRS, GZRS, RA-GRS, RA-GZRS
- Determines data redundancy
- Can be changed for some types

**Access Tier (Blob only):**
- Hot, Cool, Cold, Archive
- Affects cost and access times

**Secure Transfer Required:**
- Enforce HTTPS for all connections
- Reject HTTP requests
- Recommended: Always enabled

**Public Network Access:**
- Allow from all networks
- Allow from selected networks
- Disable public access

### **Storage Account Limits**

**Per Subscription:**
- **250 storage accounts** per region per subscription
- Can request increase via support

**Per Storage Account:**
- **Capacity:** 5 PB (petabytes) for standard accounts
- **Capacity:** Varies for premium (depends on type)
- **Max ingress:** 60 Gbps (GRS), 120 Gbps (LRS/ZRS)
- **Max egress:** 120 Gbps (GRS), 200 Gbps (LRS/ZRS)
- **Max request rate:** 20,000 requests/second

**Blob-Specific Limits:**
- **Max blob size:** 190.7 TiB (block blob)
- **Max block size:** 4000 MiB
- **Max blocks per blob:** 50,000 blocks
- **Containers:** Unlimited per account
- **Blobs:** Unlimited per container

---

## **3. Azure Blob Storage (Object Storage)**

### **What is Blob Storage?**

**Blob Storage** is Azure's object storage solution for the cloud. It's optimized for storing massive amounts of **unstructured data** (data that doesn't conform to a specific data model or definition, such as text or binary data).

### **Key Characteristics:**

- **Unstructured data:** Any type of file
- **Massive scale:** Exabytes of data
- **HTTP/HTTPS access:** REST API
- **Globally accessible:** Via URLs
- **Cost-effective:** Multiple access tiers

### **Blob Storage Hierarchy**

```
Storage Account: mystorageaccount
    |
    └── Container: images (like a folder)
        |
        ├── Blob: vacation/beach/photo1.jpg
        ├── Blob: vacation/beach/photo2.jpg
        ├── Blob: vacation/mountain/photo3.jpg
        └── Blob: profile/avatar.png
```

**Three Levels:**
1. **Storage Account:** Root container
2. **Container:** Organizational unit (like folders)
3. **Blob:** The actual file/object

### **Containers**

**What is a Container?**
A container organizes a set of blobs, similar to a directory in a file system. A storage account can contain an unlimited number of containers, and a container can store an unlimited number of blobs.

**Container Naming Rules:**
- **Length:** 3 to 63 characters
- **Characters:** Lowercase letters, numbers, and hyphens
- **Start/End:** Must start and end with letter or number
- **No consecutive hyphens:** Cannot have --
- **Unique:** Within storage account

**Valid Examples:**
```
images
user-documents
backup-2024-01
web-content
$root (special system container)
```

**Invalid Examples:**
```
Images              ❌ (uppercase)
user_documents      ❌ (underscore)
-backup             ❌ (starts with hyphen)
my--container       ❌ (consecutive hyphens)
```

**Container Access Levels:**

**1. Private (No anonymous access)** - Default
```
Container: private-data
├── Access: Requires authentication
├── Visibility: Not publicly accessible
└── Use Case: Sensitive data, internal files
```

**2. Blob (Anonymous read access for blobs only)**
```
Container: public-images
├── Access: Blobs accessible via URL
├── Visibility: Anyone can read blobs
├── Container listing: Requires auth
└── Use Case: Public images, downloads
```

**3. Container (Anonymous read access for containers and blobs)**
```
Container: public-content
├── Access: Full public read access
├── Visibility: List and read all blobs
├── Container listing: Public
└── Use Case: Public static content, CDN
```

**Public Access Example:**
```
Private Access:
❌ https://mystorageaccount.blob.core.windows.net/private/file.pdf
(Returns 404 or requires authentication)

Public Blob Access:
✓ https://mystorageaccount.blob.core.windows.net/public/file.pdf
(Anyone can access directly)
```

### **Types of Blobs**

Azure Blob Storage supports **three types of blobs**:

---

#### **1. Block Blobs**

**Description:**
Store text and binary data. Made up of blocks of data that can be managed individually. Ideal for storing files that don't change often.

**Characteristics:**
- **Max size:** 190.7 TiB (approximately 195,000 GB)
- **Max block size:** 4000 MiB
- **Max blocks:** 50,000 blocks per blob
- **Upload:** Can upload blocks in parallel
- **Modification:** Can update individual blocks

**Block Structure:**
```
Block Blob: video.mp4 (1 GB)
    |
    ├── Block 1: [0-100 MB]    (Block ID: AAA)
    ├── Block 2: [100-200 MB]  (Block ID: BBB)
    ├── Block 3: [200-300 MB]  (Block ID: CCC)
    ├── ...
    └── Block 10: [900-1000 MB] (Block ID: JJJ)

If Block 5 gets corrupted, only upload Block 5 again.
```

**Use Cases:**
- **Documents:** PDFs, Word docs, spreadsheets
- **Images:** Photos, graphics, thumbnails
- **Videos:** Media files, recordings
- **Backups:** Database backups, VM backups
- **Logs:** Application logs, audit trails
- **Code:** Application binaries, packages
- **Data lakes:** Big data analytics

**Upload Methods:**

**Small Files (< 256 MB):**
```
PUT Blob (single operation)
├── Upload entire file in one request
└── Fast and simple
```

**Large Files (> 256 MB):**
```
Staged Upload
├── 1. Put Block (upload blocks in parallel)
├── 2. Put Block (continue uploading)
├── 3. Put Block List (commit all blocks)
└── More efficient, resumable
```

**Best Practices:**
- Use block blobs for most scenarios
- Upload large files in blocks (parallel)
- Optimize block size (4-100 MB typically)
- Use appropriate access tier

---

#### **2. Append Blobs**

**Description:**
Optimized for **append operations**. Similar to block blobs but optimized for scenarios where you only add data to the end of the blob.

**Characteristics:**
- **Max size:** 195 GB
- **Max block size:** 4 MB per append
- **Append only:** Cannot modify existing data
- **Efficient appending:** Optimized for sequential writes
- **Not for random access:** Cannot update middle sections

**Structure:**
```
Append Blob: application.log
    |
    ├── Append 1: [Log entry 1] (9:00 AM)
    ├── Append 2: [Log entry 2] (9:01 AM)
    ├── Append 3: [Log entry 3] (9:02 AM)
    └── Append 4: [Log entry 4] (9:03 AM)
         ↓
    Cannot modify Append 1, 2, or 3
    Can only add Append 5, 6, etc.
```

**Use Cases:**
- **Logging:** Application logs, audit logs
- **Monitoring:** System metrics, telemetry data
- **Data streaming:** Continuous data ingestion
- **Event data:** Time-series events
- **IoT data:** Sensor data collection

**Example Scenario:**
```
Application Logging:
├── App starts → Create append blob: app-2024-01-15.log
├── 9:00:00 → Append: "Application started"
├── 9:00:05 → Append: "Database connected"
├── 9:00:10 → Append: "User logged in"
├── 9:00:15 → Append: "Order processed"
└── Day ends → 195 GB of logs (max size reached)
    → Next day → Create new blob: app-2024-01-16.log
```

**Operations:**
- **Create Append Blob:** Initialize
- **Append Block:** Add data to end
- **Read:** Read entire blob or range
- **Cannot:** Delete or modify existing blocks

**Best Practices:**
- Perfect for write-once, read-many scenarios
- Rotate logs when approaching size limit
- Use for sequential data
- Consider block blobs if random access needed

---

#### **3. Page Blobs**

**Description:**
Optimized for **random read/write operations**. Collection of 512-byte pages optimized for representing IaaS disks and supporting random writes.

**Characteristics:**
- **Max size:** 8 TiB
- **Page size:** 512 bytes
- **Random access:** Read/write any page
- **Sparse files:** Only pay for used pages
- **High performance:** Designed for VMs

**Structure:**
```
Page Blob: datadisk.vhd (1 TB capacity)
    |
    ├── Pages 0-1000: [OS data]      (Used)
    ├── Pages 1001-5000: [Empty]     (Not charged)
    ├── Pages 5001-7000: [App data]  (Used)
    ├── Pages 7001-10000: [Empty]    (Not charged)
    └── Pages 10001-12000: [DB data] (Used)

Only charged for used pages (approximately 300 GB)
Not charged for empty pages (approximately 700 GB)
```

**Use Cases:**
- **VM Disks:** OS and data disks for Azure VMs
- **Databases:** Database files requiring random I/O
- **Virtual Hard Disks (VHDs):** Disk images
- **High I/O applications:** Applications needing random access

**Page Blob Operations:**
- **Put Page:** Write a range of pages
- **Get Page Ranges:** Identify which pages contain data
- **Clear Pages:** Mark pages as empty
- **Copy:** Incremental copy of changes

**Performance Tiers:**
- **Standard (HDD):** Cost-effective, lower performance
- **Premium (SSD):** High performance, low latency

**Example: VM Disk**
```
Azure VM: Production-Web-Server
    |
    ├── OS Disk: [Page Blob - 127 GB]
    |   ├── Windows Server OS
    |   └── System files
    |
    └── Data Disk: [Page Blob - 1 TB]
        ├── Application files
        ├── Database files
        └── User data
```

**Snapshots:**
```
Original Page Blob: disk.vhd
    |
    ├── Snapshot 1: disk-snapshot-2024-01-15
    |   └── Point-in-time copy
    |
    └── Snapshot 2: disk-snapshot-2024-01-16
        └── Incremental (only changes)
```

**Best Practices:**
- Use Premium for production VMs
- Take regular snapshots for backups
- Monitor IOPS and throughput
- Use managed disks (abstraction over page blobs)

---

### **Blob Types Comparison**

| Feature | Block Blob | Append Blob | Page Blob |
|---------|------------|-------------|-----------|
| **Max Size** | 190.7 TiB | 195 GB | 8 TiB |
| **Upload Type** | Blocks | Append only | Pages |
| **Access Pattern** | Sequential | Append-only | Random |
| **Modification** | Replace blocks | Append only | Modify any page |
| **Use Case** | Files, media | Logs | VM disks |
| **Cost Model** | Per GB | Per GB | Per GB used |
| **Optimization** | Large files | Sequential writes | Random I/O |

---

### **Blob Naming and Paths**

**Blob Names:**
- **Length:** 1 to 1,024 characters
- **Characters:** Any UTF-8 character
- **Case sensitive:** `File.txt` ≠ `file.txt`
- **Path delimiters:** Use `/` for virtual directories

**Hierarchical Namespace:**
```
Container: documents
    |
    ├── reports/2024/january/sales.pdf
    ├── reports/2024/january/expenses.pdf
    ├── reports/2024/february/sales.pdf
    ├── invoices/customer1/invoice001.pdf
    └── invoices/customer2/invoice002.pdf
```

**Note:** Blob storage is **flat** (no true directories), but uses `/` in names to simulate folder structure.

**Virtual Directories:**
```
Blob Name: reports/2024/january/sales.pdf
    |
    ├── Virtual Folder: reports
    ├── Virtual Folder: reports/2024
    ├── Virtual Folder: reports/2024/january
    └── Blob: sales.pdf
```

**Accessing Blobs:**
```
Full URL:
https://mystorageaccount.blob.core.windows.net/documents/reports/2024/january/sales.pdf

Components:
├── Account: mystorageaccount
├── Service: blob.core.windows.net
├── Container: documents
└── Blob path: reports/2024/january/sales.pdf
```

---

### **Blob Access Tiers**

Azure Blob Storage offers **four access tiers** to optimize costs based on how frequently you access data.

---

#### **1. Hot Tier**

**Description:**
Optimized for data that is **accessed frequently**.

**Characteristics:**
- **Storage cost:** Highest (most expensive per GB)
- **Access cost:** Lowest (cheapest per transaction)
- **Performance:** Best performance
- **Latency:** Milliseconds
- **Default tier:** Default for new blobs

**Pricing Model:**
```
Storage: $$$$ (highest per GB)
Transactions: $ (lowest per operation)
Total Cost = (Storage Cost × GB) + (Transaction Cost × Operations)

Example:
100 GB × $0.018/GB = $1.80/month (storage)
10,000 reads × $0.0004/10K = $0.004 (transactions)
Total: $1.804/month
```

**Use Cases:**
- **Active data:** Frequently accessed files
- **Websites:** Website images, CSS, JavaScript
- **Applications:** Application data in use
- **Working datasets:** Data being actively processed
- **Logs:** Recent application logs
- **Databases:** Active database backups

**Best Practices:**
- Use for data accessed daily/weekly
- Default choice for new data
- Monitor access patterns
- Move to cooler tiers when access decreases

---

#### **2. Cool Tier**

**Description:**
Optimized for data that is **infrequently accessed** and stored for at least 30 days.

**Characteristics:**
- **Storage cost:** Lower than Hot
- **Access cost:** Higher than Hot
- **Performance:** Good performance
- **Latency:** Milliseconds
- **Minimum storage:** 30 days (early deletion fee if < 30 days)

**Pricing Model:**
```
Storage: $$ (lower per GB than Hot)
Transactions: $$ (higher per operation than Hot)

Example:
100 GB × $0.010/GB = $1.00/month (storage)
10,000 reads × $0.001/10K = $0.01 (transactions)
Total: $1.01/month

Savings: ~44% compared to Hot tier
```

**Cost Comparison:**
```
Hot Tier:  Storage $$$$ + Transactions $  = Best for frequent access
Cool Tier: Storage $$   + Transactions $$ = Best for monthly access
```

**Use Cases:**
- **Short-term backups:** 30-90 day retention
- **Older data:** Data accessed monthly
- **Disaster recovery:** DR data sets
- **Media archives:** Video/images accessed occasionally
- **Compliance data:** Data kept for regulations
- **Historical data:** Older reports and documents

**Early Deletion Penalty:**
```
Cool Tier (30-day minimum):
├── Upload blob on Day 1
├── Delete blob on Day 10
├── Charged for 30 days storage (not just 10)
└── Penalty = 20 days × storage cost
```

**Best Practices:**
- Use for data accessed monthly
- Keep data for at least 30 days
- Consider lifecycle policies
- Monitor access patterns

---

#### **3. Cold Tier**

**Description:**
Optimized for data that is **rarely accessed** and stored for at least 90 days.

**Characteristics:**
- **Storage cost:** Lower than Cool
- **Access cost:** Higher than Cool
- **Performance:** Good performance
- **Latency:** Milliseconds
- **Minimum storage:** 90 days (early deletion fee if < 90 days)

**Pricing Model:**
```
Storage: $ (even lower per GB)
Transactions: $$$ (higher per operation)

Example:
100 GB × $0.0045/GB = $0.45/month (storage)
10,000 reads × $0.005/10K = $0.05 (transactions)
Total: $0.50/month

Savings: ~50% compared to Cool, ~72% compared to Hot
```

**Use Cases:**
- **Long-term backups:** 90-365 day retention
- **Archives:** Rarely accessed archives
- **Compliance data:** Long-term regulatory storage
- **Historical records:** Seldom accessed historical data
- **Old media:** Archived media files
- **Forensic data:** Data kept for investigation

**Early Deletion Penalty:**
```
Cold Tier (90-day minimum):
├── Upload blob on Day 1
├── Delete blob on Day 30
├── Charged for 90 days storage
└── Penalty = 60 days × storage cost
```

**Best Practices:**
- Use for data accessed quarterly or less
- Keep data for at least 90 days
- Perfect for compliance archives
- Use lifecycle policies for automation

---

#### **4. Archive Tier**

**Description:**
Optimized for data that is **rarely accessed** and stored for at least 180 days with **flexible latency requirements** (hours).

**Characteristics:**
- **Storage cost:** Lowest (cheapest per GB)
- **Access cost:** Highest (most expensive)
- **Performance:** Offline (must rehydrate)
- **Latency:** Hours (1-15 hours for Standard priority)
- **Minimum storage:** 180 days (early deletion fee)

**Pricing Model:**
```
Storage: ¢ (lowest per GB)
Rehydration: $$$$ (expensive to retrieve)

Example:
100 GB × $0.00099/GB = $0.099/month (storage)
Rehydrate 100 GB × $0.02/GB = $2.00 (one-time)
10,000 reads × $0.005/10K = $0.05 (transactions)
Total: $0.099/month + $2.05 per access

Savings: ~95% storage cost compared to Hot
```

**Special Considerations:**

**Offline Storage:**
```
Archive Blob: backup-2023.tar.gz
├── Status: Archived (offline)
├── Cannot read directly ❌
├── Must rehydrate first ✓
└── Then accessible
```

**Rehydration Process:**
```
Step 1: Request rehydration
   ├── Priority: Standard (1-15 hours)
   └── Priority: High (< 1 hour)

Step 2: Wait for rehydration
   └── Blob becomes online

Step 3: Access data
   └── Read/download blob

Step 4: Optional - return to Archive
   └── Or keep in Hot/Cool/Cold
```

**Rehydration Options:**

**Option 1: Copy to Online Tier**
```
Source: archive-blob (Archive)
    ↓ (copy and rehydrate)
Destination: archive-blob-copy (Hot/Cool/Cold)
    └── Original stays in Archive
```

**Option 2: Change Tier (In-place)**
```
Blob: backup.tar.gz
├── Current tier: Archive
├── Change tier to: Hot
├── Rehydration begins
└── After rehydration: blob accessible in Hot tier
```

**Use Cases:**
- **Long-term archives:** Years of retention
- **Compliance archives:** 7-10 year retention
- **Backup archives:** Old backups rarely needed
- **Legal/regulatory:** Data for legal requirements
- **Historical records:** Company historical data
- **Cold backups:** Disaster recovery last resort

**Early Deletion Penalty:**
```
Archive Tier (180-day minimum):
├── Upload blob on Day 1
├── Delete blob on Day 90
├── Charged for 180 days storage
└── Penalty = 90 days × storage cost
```

**Best Practices:**
- Use for long-term archival only
- Plan for rehydration time
- Use standard priority unless urgent
- Consider cost of rehydration
- Perfect for compliance with rare access

---

### **Access Tier Comparison Table**

| Feature | Hot | Cool | Cold | Archive |
|---------|-----|------|------|---------|
| **Storage Cost** | Highest | Medium | Lower | Lowest |
| **Access Cost** | Lowest | Medium | Higher | Highest |
| **Latency** | ms | ms | ms | Hours |
| **Minimum Duration** | None | 30 days | 90 days | 180 days |
| **Availability** | Online | Online | Online | Offline |
| **Use Case** | Frequent access | Monthly access | Quarterly | Yearly/Never |
| **Cost per GB/month** | ~$0.018 | ~$0.010 | ~$0.0045 | ~$0.00099 |
| **Ideal Frequency** | Daily/Weekly | Monthly | Quarterly | Yearly+ |

---

### **Access Tier Selection Guide**

**Decision Tree:**
```
How often is data accessed?
    |
    ├── Daily/Weekly → HOT TIER
    |
    ├── Monthly → COOL TIER
    |
    ├── Quarterly → COLD TIER
    |
    └── Yearly or less → ARCHIVE TIER

Can you wait hours for access?
    |
    ├── No → HOT/COOL/COLD
    └── Yes → ARCHIVE
```

**Cost Optimization Strategy:**
```
Data Lifecycle:
├── Day 0-30: Hot Tier (active use)
├── Day 31-120: Cool Tier (occasional access)
├── Day 121-365: Cold Tier (rare access)
└── Day 366+: Archive Tier (long-term storage)
```

---

### **Changing Blob Access Tiers**

**Methods:**

**1. Manual Tier Change:**
```
Azure Portal:
├── Navigate to blob
├── Click "Change tier"
├── Select new tier
└── Confirm
```

**2. Programmatic (Azure CLI):**
```bash
az storage blob set-tier \
  --account-name mystorageaccount \
  --container-name mycontainer \
  --name myblob.txt \
  --tier Cool
```

**3. Lifecycle Management Policies** (Automated):
```json
{
  "rules": [
    {
      "name": "MoveToArchive",
      "type": "Lifecycle",
      "definition": {
        "filters": {
          "blobTypes": ["blockBlob"],
          "prefixMatch": ["backups/"]
        },
        "actions": {
          "baseBlob": {
            "tierToCool": {
              "daysAfterModificationGreaterThan": 30
            },
            "tierToArchive": {
              "daysAfterModificationGreaterThan": 90
            }
          }
        }
      }
    }
  ]
}
```

**Tier Transition Costs:**
```
Transitions:
├── Hot → Cool: Write operation cost
├── Hot → Archive: Write operation cost
├── Cool → Hot: Read operation cost
├── Cool → Archive: Write operation cost
├── Archive → Hot: Rehydration cost + Read
└── Archive → Cool: Rehydration cost + Read
```

---

### **Blob Metadata and Properties**

**System Properties (Read-only):**
- Created date/time
- Last modified
- Content type
- Content length (size)
- E Tag (for concurrency)
- Lease state
- Access tier

**Custom Metadata:**
Key-value pairs for your own use:
```
Blob: photo.jpg
├── Metadata: Department = "Marketing"
├── Metadata: Project = "Campaign2024"
├── Metadata: Owner = "john.doe@company.com"
└── Metadata: Approved = "true"
```

**Metadata Rules:**
- Up to 8 KB of metadata per blob
- Key names: ASCII characters only
- Case-insensitive
- Value: Any string
- Total: Up to 8 KB

---

### **Blob Snapshots**

**What is a Snapshot?**
A read-only version of a blob at a specific point in time.

**Characteristics:**
- Read-only (cannot modify)
- Same name as base blob + DateTime
- Share blocks with base blob (efficient)
-

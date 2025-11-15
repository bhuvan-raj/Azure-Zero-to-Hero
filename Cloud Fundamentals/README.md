# Phase 1: Cloud Computing Basics - In-Depth Study Guide

<img src="https://github.com/bhuvan-raj/Azure-Zero-to-Hero/blob/main/assets/cloud.png" alt="Banner" />

## **1. What is Cloud Computing and Why It Matters**

### **Definition**
Cloud computing is the on-demand delivery of computing services—including servers, storage, databases, networking, software, analytics, and intelligence—over the Internet ("the cloud") to offer faster innovation, flexible resources, and economies of scale.

### **Traditional IT vs Cloud Computing**

**Traditional On-Premises IT:**
- You purchase physical servers and hardware
- You maintain data centers with cooling, power, and physical security
- You hire staff to manage infrastructure
- You plan capacity years in advance
- High upfront capital expenditure (CapEx)
- Resources often sit idle or become insufficient during peak times
- Upgrades require purchasing new hardware
- Recovery from disasters is complex and expensive

**Cloud Computing:**
- You rent resources from cloud providers (pay-as-you-go)
- No physical infrastructure to maintain
- Global reach with data centers worldwide
- Scale resources up or down based on demand
- Operational expenditure (OpEx) model
- Access to enterprise-grade infrastructure
- Automatic updates and maintenance
- Built-in disaster recovery options

### **Why Cloud Computing Matters**

**1. Cost Efficiency**
- No upfront hardware costs
- Pay only for what you use
- Reduce total cost of ownership (TCO)
- Convert CapEx to OpEx for better cash flow
- Eliminate costs of maintaining data centers

**2. Scalability**
- **Vertical Scaling (Scale Up/Down):** Increase CPU, RAM, or storage on existing resources
- **Horizontal Scaling (Scale Out/In):** Add or remove instances of resources
- Handle traffic spikes without overprovisioning
- Auto-scaling based on demand

**3. Global Reach**
- Deploy applications closer to users worldwide
- Reduce latency with distributed data centers
- Comply with data residency requirements
- Serve global customers efficiently

**4. Speed and Agility**
- Deploy infrastructure in minutes, not months
- Experiment quickly without long-term commitments
- Fast time-to-market for applications
- Enable innovation through rapid prototyping

**5. Reliability and Availability**
- Multiple redundant data centers
- Built-in backup and disaster recovery
- Service Level Agreements (SLAs) guarantee uptime
- Geographic distribution prevents single points of failure

**6. Security**
- Enterprise-grade security from day one
- Compliance with international standards (ISO, SOC, GDPR, etc.)
- Regular security updates and patches
- Advanced threat detection and prevention

**7. Focus on Business Value**
- IT teams focus on innovation, not infrastructure management
- Developers spend time on applications, not servers
- Reduce operational overhead
- Enable digital transformation

### **Key Cloud Computing Characteristics (NIST Definition)**

1. **On-demand self-service:** Users can provision resources automatically without human interaction
2. **Broad network access:** Services available over the network via standard mechanisms
3. **Resource pooling:** Provider's resources serve multiple customers with dynamic assignment
4. **Rapid elasticity:** Resources can be quickly scaled up or down
5. **Measured service:** Usage is monitored, controlled, and reported (pay-per-use)

---

## **2. Service Models: IaaS, PaaS, SaaS**

<img src="https://github.com/bhuvan-raj/Azure-Zero-to-Hero/blob/main/assets/service.jpg" alt="Banner" />


Cloud services are typically categorized into three main models, often visualized as a stack.

### **Understanding the Shared Responsibility Model**

Before diving into service models, understand that cloud security and management follow a **shared responsibility model**:

- **Cloud Provider Responsibilities:** Physical security, infrastructure, hypervisor
- **Customer Responsibilities:** Data, access control, applications
- **Shared Responsibilities:** Vary by service model

The more managed the service, the more responsibility the provider takes.

---

### **A. Infrastructure as a Service (IaaS)**

**Definition:** The most basic category of cloud computing services. You rent IT infrastructure (servers, VMs, storage, networks) from a cloud provider on a pay-as-you-go basis.

### What Provider Manages

- Virtualisation
- Servers
- Storage
- Networking


**Use Cases:**
- Migrating existing applications to the cloud ("lift and shift")
- Development and test environments
- Website hosting
- Big data analysis
- Backup and disaster recovery
- High-performance computing

**Azure IaaS Examples:**
- **Virtual Machines (VMs):** Windows or Linux servers in the cloud
- **Virtual Networks:** Isolated network environments
- **Storage Accounts:** Block storage, file storage
- **Load Balancers:** Distribute traffic across VMs

**Benefits:**
- Complete control over infrastructure
- No need to purchase physical hardware
- Pay only for what you use
- Quick deployment and scaling
- Geographic distribution

**Drawbacks:**
- You must manage OS, patches, and updates
- Requires IT expertise
- More management overhead than PaaS/SaaS

**Analogy:** IaaS is like **renting a house**. You get the structure (walls, roof, plumbing), but you furnish it, maintain it, and manage everything inside.

---

### **B. Platform as a Service (PaaS)**

**Definition:** Provides a complete development and deployment environment in the cloud. You manage applications and data; the provider handles everything else.

### What Provider Manages

- Runtime
- Middleware
- OS
- Virtualisation
- Servers
- Storage
- Networking

**Use Cases:**
- Application development and hosting
- API development and management
- Business analytics and intelligence
- Database hosting
- IoT application platforms

**Azure PaaS Examples:**
- **Azure App Service:** Host web apps, REST APIs, mobile backends
- **Azure SQL Database:** Managed relational database
- **Azure Functions:** Serverless compute (run code without managing servers)
- **Azure Kubernetes Service (AKS):** Managed container orchestration
- **Azure Cosmos DB:** Globally distributed database

**Benefits:**
- Focus on application development, not infrastructure
- Built-in scalability and high availability
- Faster development cycles
- Reduced management overhead
- Automatic patching and updates
- Development frameworks and tools included

**Drawbacks:**
- Less control over underlying infrastructure
- Potential vendor lock-in
- Migration can be complex if switching providers
- Limited customization in some cases

**Analogy:** PaaS is like **renting a furnished apartment**. The furniture (platforms, tools, databases) is already there; you just bring your belongings (applications and data) and live there.

---

### **C. Software as a Service (SaaS)**

**Definition:** Complete software applications delivered over the internet. You simply use the software; the provider manages everything.

### What Provider Manages

- Applications
- Data
- Runtime
- Middleware
- OS
- Virtualisation
- Servers
- Storage
- Networking

**Use Cases:**
- Email and collaboration tools
- Customer relationship management (CRM)
- Enterprise resource planning (ERP)
- Document management
- Project management
- Communication platforms

**Azure SaaS Examples:**
- **Microsoft 365:** Office applications, email, SharePoint
- **Dynamics 365:** CRM and ERP solutions
- **Microsoft Teams:** Communication and collaboration

**Other Popular SaaS:**
- Salesforce (CRM)
- Google Workspace (productivity)
- Dropbox (file storage)
- Slack (communication)
- Zoom (video conferencing)

**Benefits:**
- No installation or management required
- Access from anywhere with internet
- Automatic updates
- Subscription-based pricing
- Scales effortlessly
- Lower upfront costs

**Drawbacks:**
- Least control over infrastructure
- Limited customization
- Data stored with third party
- Dependent on internet connectivity
- Compliance concerns in some industries

**Analogy:** SaaS is like **staying at a hotel**. Everything is managed for you—cleaning, maintenance, amenities. You just check in and use the services.

---

### **Service Model Comparison Table**

| Aspect | IaaS | PaaS | SaaS |
|--------|------|------|------|
| **Control** | High | Medium | Low |
| **Management** | You manage more | Provider manages more | Provider manages everything |
| **Flexibility** | Very flexible | Moderate flexibility | Limited flexibility |
| **Use Case** | Infrastructure needs | Development platform | Ready-to-use software |
| **Target User** | IT administrators | Developers | End users |
| **Examples** | VMs, Storage | App Services, Databases | Office 365, Salesforce |

---

### **Additional Service Models**

**Function as a Service (FaaS) / Serverless:**
- A subset of PaaS
- Run code without managing servers
- Pay only for execution time
- Event-driven architecture
- Example: Azure Functions, AWS Lambda

**Container as a Service (CaaS):**
- Between IaaS and PaaS
- Manage and deploy containers
- Less infrastructure management than IaaS
- Example: Azure Container Instances, Azure Kubernetes Service

**Database as a Service (DBaaS):**
- Specialized PaaS for databases
- Managed database services
- Example: Azure SQL Database, Azure Cosmos DB

---

## **3. Deployment Models: Public, Private, Hybrid, Multi-cloud**

Deployment models describe where and how cloud resources are deployed.

---

### **A. Public Cloud**

**Definition:** Computing services offered by third-party providers over the public internet, available to anyone who wants to purchase them.

**Characteristics:**
- Owned and operated by cloud service providers (Microsoft, Amazon, Google)
- Resources shared among multiple organizations (multi-tenant)
- Accessed via the public internet
- No upfront capital expenditure
- Pay-as-you-go pricing

**Benefits:**
- **No maintenance:** Provider manages all hardware and infrastructure
- **Near-unlimited scalability:** Vast resources available on-demand
- **Cost-effective:** No hardware to purchase; pay only for usage
- **Reliability:** Multiple data centers ensure high availability
- **Easy setup:** Quick provisioning without hardware procurement

**Use Cases:**
- Web applications and websites
- Development and test environments
- Applications with variable workloads
- Collaboration tools
- Storage and backup

**Concerns:**
- **Security perception:** Data stored off-premises (though often more secure than on-premises)
- **Compliance:** May not meet certain regulatory requirements
- **Limited control:** Less customization of infrastructure
- **Internet dependency:** Requires reliable internet connectivity

**Examples:**
- Microsoft Azure
- Amazon Web Services (AWS)
- Google Cloud Platform (GCP)

---

### **B. Private Cloud**

**Definition:** Cloud computing resources used exclusively by one organization. Can be physically located at the organization's on-site data center or hosted by a third-party provider.

**Characteristics:**
- Single-tenant environment
- Dedicated resources for one organization
- Greater control over security and compliance
- Can be on-premises or hosted

**Types:**
1. **On-Premises Private Cloud:** Organization owns and manages infrastructure in their data center
2. **Hosted Private Cloud:** Third party hosts dedicated infrastructure for the organization

**Benefits:**
- **Enhanced security:** Complete control over data and resources
- **Compliance:** Meet strict regulatory requirements
- **Customization:** Tailor infrastructure to specific needs
- **Predictable performance:** No "noisy neighbor" issues
- **Legacy integration:** Better integration with existing systems

**Drawbacks:**
- **High costs:** Significant capital expenditure for hardware
- **Limited scalability:** Constrained by physical resources
- **Maintenance responsibility:** Organization manages all aspects
- **Requires expertise:** Need skilled IT staff

**Use Cases:**
- Financial services (banks, insurance)
- Healthcare organizations (HIPAA compliance)
- Government agencies
- Large enterprises with strict security requirements
- Industries with data sovereignty regulations

**Technologies:**
- **Azure Stack:** Azure services on-premises
- VMware Private Cloud
- OpenStack
- Microsoft System Center

---

### **C. Hybrid Cloud**

**Definition:** A computing environment that combines public and private clouds, allowing data and applications to be shared between them.

**Characteristics:**
- Resources in both public and private environments
- Connected through secure networks (VPN or dedicated connections)
- Orchestration between platforms
- Workloads can move between environments

**Architecture Components:**
- Public cloud resources
- Private cloud or on-premises data center
- Network connectivity (VPN, ExpressRoute, Direct Connect)
- Management tools for both environments
- Identity and access management spanning environments

**Benefits:**
- **Flexibility:** Choose where to run each workload
- **Cost optimization:** Use public cloud for variable workloads, private for steady state
- **Scalability:** Burst to public cloud during peak demand ("cloud bursting")
- **Compliance:** Keep sensitive data on-premises, use public cloud for others
- **Modernization:** Gradually migrate to cloud at your pace
- **Disaster recovery:** Use public cloud as backup site

**Use Cases:**
- **Data processing:** Process sensitive data on-premises, analytics in public cloud
- **Cloud bursting:** Handle traffic spikes with public cloud resources
- **Gradual migration:** Move workloads to cloud incrementally
- **Backup and DR:** Use public cloud for backup and disaster recovery
- **Development/Test:** Dev/test in public cloud, production on-premises

**Challenges:**
- **Complexity:** Managing two environments requires expertise
- **Integration:** Ensuring seamless communication between clouds
- **Security:** Securing connections and data transfer
- **Cost management:** Tracking costs across platforms
- **Latency:** Network delays between environments

**Azure Hybrid Solutions:**
- **Azure Arc:** Manage resources across environments from Azure
- **Azure Stack Hub/Edge:** Run Azure services on-premises
- **Azure ExpressRoute:** Private connectivity to Azure
- **Azure Hybrid Benefit:** Use existing licenses in Azure
- **Azure Site Recovery:** Disaster recovery orchestration

---

### **D. Multi-Cloud**

**Definition:** Using cloud services from multiple public cloud providers (AWS, Azure, GCP, etc.) within a single architecture.

**Characteristics:**
- Resources from two or more public cloud providers
- Different services used based on strengths
- No single cloud dependency
- Requires multi-cloud management tools

**Reasons for Multi-Cloud:**
1. **Avoid vendor lock-in:** Don't depend on a single provider
2. **Best-of-breed services:** Use each provider's strongest offerings
3. **Geographic coverage:** Leverage different data center locations
4. **Regulatory compliance:** Meet data residency requirements
5. **Cost optimization:** Use competitive pricing across providers
6. **Risk mitigation:** Distribute risk across multiple providers
7. **Mergers and acquisitions:** Inherit different cloud infrastructures

**Benefits:**
- **Flexibility:** Choose best services from each provider
- **Resilience:** Reduced risk of provider outages
- **Negotiating power:** Leverage competition for better pricing
- **Innovation:** Access to latest features across providers

**Challenges:**
- **Increased complexity:** Managing multiple platforms
- **Skills required:** Expertise in multiple clouds
- **Integration issues:** Connecting services across providers
- **Cost management:** Tracking spending across platforms
- **Security:** Consistent security policies across clouds
- **Data transfer costs:** Moving data between clouds can be expensive

**Multi-Cloud vs Hybrid Cloud:**
- **Hybrid:** Public + Private cloud, often from same vendor family
- **Multi-cloud:** Multiple public clouds, often from different vendors
- **Note:** You can have hybrid multi-cloud (private cloud + multiple public clouds)

**Tools for Multi-Cloud Management:**
- Terraform (infrastructure as code across clouds)
- Kubernetes (container orchestration)
- Cloud management platforms (CloudBolt, Scalr)
- Monitoring tools (Datadog, New Relic)

---

### **Deployment Model Comparison**

| Model | Ownership | Location | Security | Cost | Scalability | Use Case |
|-------|-----------|----------|----------|------|-------------|----------|
| **Public** | Provider | Provider data centers | Shared | Low CapEx, OpEx | Unlimited | General applications |
| **Private** | Organization | On-premises or hosted | High | High CapEx | Limited | Compliance-driven |
| **Hybrid** | Mixed | Both | Flexible | Medium | Moderate | Gradual migration |
| **Multi-cloud** | Multiple providers | Multiple locations | Complex | Variable | High | Avoid lock-in |

---

## **4. Basic Networking Concepts**

Understanding networking is crucial for cloud computing. Here's what you need to know.

---

### **A. IP Addresses**

**What is an IP Address?**
An Internet Protocol (IP) address is a unique numerical label assigned to each device connected to a network. It serves two main purposes:
1. **Identification:** Identifies the device on the network
2. **Location addressing:** Enables routing of data to the device

**Types of IP Addresses:**

**1. IPv4 (Internet Protocol version 4)**
- Format: Four decimal numbers (0-255) separated by dots
- Example: `192.168.1.100`
- Total addresses: ~4.3 billion (2^32)
- Status: Running out of addresses
- Most commonly used currently

**2. IPv6 (Internet Protocol version 6)**
- Format: Eight groups of four hexadecimal digits separated by colons
- Example: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- Total addresses: 340 undecillion (2^128)
- Status: Gradual adoption to solve IPv4 shortage

**IP Address Classes (IPv4):**

- **Class A:** 1.0.0.0 to 126.255.255.255 (Large networks, 16 million hosts)
- **Class B:** 128.0.0.0 to 191.255.255.255 (Medium networks, 65,000 hosts)
- **Class C:** 192.0.0.0 to 223.255.255.255 (Small networks, 254 hosts)
- **Class D:** 224.0.0.0 to 239.255.255.255 (Multicast)
- **Class E:** 240.0.0.0 to 255.255.255.255 (Reserved/Experimental)

**Public vs Private IP Addresses:**

**Public IP:**
- Globally unique and routable on the internet
- Assigned by Internet Service Providers (ISPs)
- Required for internet communication
- Can be accessed from anywhere
- Example: `40.76.123.45`

**Private IP:**
- Used within private networks (home, office, VPCs)
- Not routable on the public internet
- Multiple networks can use the same private IPs
- Reserved ranges (RFC 1918):
  - `10.0.0.0` to `10.255.255.255` (Class A)
  - `172.16.0.0` to `172.31.255.255` (Class B)
  - `192.168.0.0` to `192.168.255.255` (Class C)

**Static vs Dynamic IP:**

**Static IP:**
- Manually assigned and doesn't change
- Used for servers, printers, critical devices
- More expensive
- Better for hosting services

**Dynamic IP:**
- Automatically assigned by DHCP (Dynamic Host Configuration Protocol)
- Changes periodically
- Common for end-user devices
- More cost-effective

**Azure IP Addressing:**
- **Public IP:** Assigned to resources that need internet access (VMs, Load Balancers)
- **Private IP:** Used within Virtual Networks (VNets)
- **Dynamic allocation:** IP assigned from available pool (default)
- **Static allocation:** IP address reserved and doesn't change
- **IP Address SKUs:** Basic (free, dynamic) or Standard (always static, zone-redundant)

---

### **B. Subnets and CIDR Notation**

**What is a Subnet?**
A subnet (subnetwork) is a logical subdivision of an IP network. Subnetting divides a network into smaller networks for better organization, security, and performance.

**Why Use Subnets?**
- **Security:** Isolate resources (web servers, databases, etc.)
- **Performance:** Reduce network congestion
- **Organization:** Logical grouping of resources
- **IP management:** Efficient use of IP address space

**CIDR Notation (Classless Inter-Domain Routing):**

Format: `IP_ADDRESS/PREFIX_LENGTH`

Example: `192.168.1.0/24`
- `192.168.1.0` = Network address
- `/24` = Subnet mask (first 24 bits for network, remaining 8 for hosts)

**Common CIDR Blocks:**

| CIDR | Subnet Mask | Available IPs | Usable Hosts | Use Case |
|------|-------------|---------------|--------------|----------|
| /32 | 255.255.255.255 | 1 | 1 | Single host |
| /30 | 255.255.255.252 | 4 | 2 | Point-to-point links |
| /28 | 255.255.255.240 | 16 | 14 | Small subnet |
| /24 | 255.255.255.0 | 256 | 254 | Standard subnet |
| /20 | 255.255.240.0 | 4,096 | 4,094 | Medium network |
| /16 | 255.255.0.0 | 65,536 | 65,534 | Large network |
| /8 | 255.0.0.0 | 16,777,216 | 16,777,214 | Huge network |

**Subnet Calculation Example:**

Network: `10.0.0.0/16`
- Can be divided into multiple `/24` subnets:
  - `10.0.1.0/24` (Web tier)
  - `10.0.2.0/24` (Application tier)
  - `10.0.3.0/24` (Database tier)
  - ... up to `10.0.255.0/24`

**Azure Subnet Considerations:**
- Azure reserves 5 IPs in each subnet (first 4 and last 1)
- Example: `10.0.1.0/24` has 256 IPs, but only 251 are usable
- Plan subnet sizes based on expected growth

---

### **C. DNS (Domain Name System)**

**What is DNS?**
DNS is the "phonebook of the internet." It translates human-readable domain names (like `www.microsoft.com`) into IP addresses (like `13.107.213.40`) that computers use to communicate.

**Why DNS Matters:**
- Humans remember names better than numbers
- IP addresses can change, but domain names remain constant
- Enables load balancing and failover
- Critical for internet functionality

**How DNS Works:**

1. **User types:** `www.example.com` in browser
2. **Browser cache check:** Looks for cached IP address
3. **OS cache check:** Operating system checks its DNS cache
4. **Recursive resolver:** Query sent to ISP's DNS server
5. **Root nameserver:** Points to Top-Level Domain (TLD) server
6. **TLD nameserver:** Points to authoritative nameserver for `.com`
7. **Authoritative nameserver:** Returns IP address for `www.example.com`
8. **Response:** IP address returned to browser
9. **Connection:** Browser connects to web server using IP address

**DNS Record Types:**

| Record Type | Purpose | Example |
|-------------|---------|---------|
| **A** | Maps domain to IPv4 address | `example.com` → `192.0.2.1` |
| **AAAA** | Maps domain to IPv6 address | `example.com` → `2001:0db8::1` |
| **CNAME** | Alias one domain to another | `www.example.com` → `example.com` |
| **MX** | Mail exchange servers | Points to mail server |
| **TXT** | Text information (verification, SPF) | Domain verification strings |
| **NS** | Nameserver records | Specifies authoritative nameservers |
| **SOA** | Start of Authority | Administrative info about zone |
| **PTR** | Reverse DNS lookup | IP → domain name |

**DNS Hierarchy:**
```
                       Root (.)
                          |
         -----------------+----------------
         |                |               |
       .com             .org            .net
         |                |               |
    example.com      wikipedia.org   microsoft.net
         |
    www.example.com
```

**Time to Live (TTL):**
- How long DNS records are cached
- Lower TTL = More frequent lookups, faster propagation of changes
- Higher TTL = Less DNS traffic, slower change propagation
- Typical values: 300 seconds (5 min) to 86400 seconds (24 hours)

**Azure DNS:**
- Host DNS domains in Azure
- Manage DNS records using Azure tools
- High availability with SLA
- Integration with other Azure services
- Private DNS zones for internal name resolution
- Alias records for dynamic Azure resources

---

### **D. Ports and Protocols**

**What is a Port?**
A port is a logical endpoint for network communication. It allows multiple services to run on a single IP address. Think of an IP address as a building and ports as apartment numbers.

**Port Number Range:**
- Total ports: 0 to 65,535
- **Well-known ports:** 0-1,023 (system/standard services)
- **Registered ports:** 1,024-49,151 (user/application services)
- **Dynamic/Private ports:** 49,152-65,535 (temporary/client-side)

**Common Ports You Should Know:**

| Port | Protocol | Service | Description |
|------|----------|---------|-------------|
| **20, 21** | FTP | File Transfer | Data (20), Control (21) |
| **22** | SSH | Secure Shell | Encrypted remote access |
| **23** | Telnet | Telnet | Unencrypted remote access (avoid) |
| **25** | SMTP | Email | Send email |
| **53** | DNS | Domain Name System | Name resolution |
| **80** | HTTP | Web | Unencrypted web traffic |
| **110** | POP3 | Email | Receive email |
| **143** | IMAP | Email | Receive email (keeps on server) |
| **443** | HTTPS | Secure Web | Encrypted web traffic (SSL/TLS) |
| **445** | SMB | File Sharing | Windows file and printer sharing |
| **3306** | MySQL | Database | MySQL database |
| **3389** | RDP | Remote Desktop | Windows remote access |
| **5432** | PostgreSQL | Database | PostgreSQL database |
| **8080** | HTTP | Web (Alt) | Alternative web server port |

**Protocols:**

**TCP (Transmission Control Protocol):**
- **Connection-oriented:** Establishes connection before sending data
- **Reliable:** Guarantees delivery and order of packets
- **Error checking:** Detects and retransmits lost packets
- **Use cases:** Web browsing (HTTP/HTTPS), email, file transfer
- **Three-way handshake:** SYN → SYN-ACK → ACK
- Slower but reliable

**UDP (User Datagram Protocol):**
- **Connectionless:** No connection establishment
- **Unreliable:** No guarantee of delivery or order
- **No error checking:** Lost packets not retransmitted
- **Use cases:** Video streaming, VoIP, DNS, gaming
- Faster but less reliable

**HTTP vs HTTPS:**
- **HTTP (Port 80):** Hypertext Transfer Protocol
  - Unencrypted communication
  - Data sent in plain text
  - Vulnerable to eavesdropping
  
- **HTTPS (Port 443):** HTTP Secure
  - Encrypted with SSL/TLS
  - Protects data in transit
  - Authentication of server
  - Mandatory for modern websites

**SSH (Secure Shell - Port 22):**
- Encrypted remote access to servers
- Secure alternative to Telnet
- Used for command-line access and file transfers (SFTP)
- Public-key authentication supported

**RDP (Remote Desktop Protocol - Port 3389):**
- Microsoft's protocol for remote desktop access
- Graphical interface to Windows servers
- Should be secured (VPN, NSG rules, etc.)

**Firewalls and Port Security:**
- Control which ports are open/closed
- Block unwanted traffic
- Allow only necessary services
- Azure Network Security Groups (NSGs) control port access

**Port Scanning:**
- Technique to discover open ports
- Used by both security professionals and attackers
- Azure automatically blocks port scanning from external sources

---

### **E. Networking Components in Cloud**

**Virtual Networks (VNets) - Azure Terminology:**
- Isolated network environment in Azure
- Similar to traditional on-premises networks
- Contains subnets, IP addresses, route tables
- Can connect to other VNets or on-premises networks

**Network Interface Card (NIC):**
- Virtual network adapter for VMs
- Connects VM to VNet
- Has private IP address
- Can have public IP attached

**Load Balancers:**
- Distribute traffic across multiple servers
- Improve availability and performance
- Types: Layer 4 (transport) and Layer 7 (application)
- Azure Load Balancer vs Application Gateway

**Network Security Groups (NSG):**
- Virtual firewall for Azure resources
- Control inbound and outbound traffic
- Rules based on source/destination IP, port, protocol
- Applied at subnet or NIC level

**Route Tables:**
- Control network traffic routing
- Define next hop for traffic
- Custom routes for specific scenarios
- Override default Azure routing

**VPN (Virtual Private Network):**
- Encrypted connection over public internet
- Connects on-premises to cloud securely
- **Site-to-Site:** Office to Azure
- **Point-to-Site:** Individual device to Azure

**ExpressRoute:**
- Private, dedicated connection to Azure
- Doesn't go over public internet
- Higher reliability, speeds, and security
- Higher cost than VPN

**Latency:**
- Time delay in network communication
- Measured in milliseconds (ms)
- Lower is better
- Affected by distance, network quality, routing

**Bandwidth:**
- Amount of data transferred per unit time
- Measured in bits per second (bps, Mbps, Gbps)
- Higher is better
- Think of it as pipe width, latency as pipe length

**Throughput:**
- Actual amount of data successfully transferred
- Often less than bandwidth due to various factors
- Real-world performance measure

---

## **5. Understanding Virtualization**

Virtualization is the foundation of cloud computing. Understanding it is crucial.

---

### **What is Virtualization?**

**Definition:** Virtualization is the creation of a virtual (rather than physical) version of something, such as an operating system, server, storage device, or network resources.

**Core Concept:**
Instead of running one operating system on one physical server, virtualization allows multiple virtual machines (VMs) to run on a single physical machine, each with its own operating system and applications.

---

### **Why Virtualization Matters**

**Before Virtualization:**
- One application per physical server (security, licensing, stability)
- Most servers ran at 10-15% utilization
- Expensive: hardware, space, power, cooling
- Slow provisioning: order, ship, install, configure
- Difficult to scale

**With Virtualization:**
- Multiple VMs on one physical server
- 70-80% or higher utilization
- Reduced hardware costs
- Quick VM provisioning (minutes, not weeks)
- Easy to scale and move VMs
- Foundation for cloud computing

---

### **Key Virtualization Components**

**1. Host Machine (Physical Server):**
- The actual physical hardware
- Has CPU, RAM, storage, network cards
- Runs the hypervisor
- Shared among multiple VMs

**2. Hypervisor (Virtual Machine Monitor):**
- Software layer that creates and manages VMs
- Sits between hardware and VMs
- Allocates physical resources to VMs
- Ensures isolation between VMs

**3. Guest Machine (Virtual Machine):**
- The virtualized server
- Has virtual CPU, RAM, storage, network
- Runs its own operating system (Guest OS)
- Thinks it's running on dedicated hardware
- Completely isolated from other VMs

**4. Virtual Hardware:**
- **vCPU:** Virtual processor cores
- **vRAM:** Virtual memory
- **vDisk:** Virtual hard drives
- **vNIC:** Virtual network adapters

---

### **Types of Hypervisors**

**Type 1 Hypervisor (Bare Metal):**
- Runs directly on hardware
- No underlying operating system
- Better performance and security
- Used in enterprise and cloud environments

**Examples:**
- **VMware ESXi:** Industry leader, enterprise-grade
- **Microsoft Hyper-V:** Windows Server-based
- **Xen:** Open-source, used by AWS
- **KVM (Kernel-based Virtual Machine):** Linux-based

**Characteristics:**
- Minimal overhead
- Direct hardware access
- Better resource management
- Production workloads

**Type 2 Hypervisor (Hosted):**
- Runs on top of an existing operating system
- More overhead due to host OS
- Easier to set up
- Used for development, testing, desktop virtualization

**Examples:**
- **VMware Workstation/Fusion:** Professional desktop virtualization
- **Oracle VirtualBox:** Free, open-source
- **Parallels Desktop:** Mac virtualization

**Characteristics:**
- Easier to install and use
- Good for learning and development
- Lower performance than Type 1
- Not ideal for production

---

### **How Virtualization Works**

**Resource Allocation:**

**CPU:**
- Physical CPU cores divided among VMs
- Hypervisor schedules VM CPU time
- Can oversubscribe (more vCPUs than physical cores)
- CPU stealing: when VM

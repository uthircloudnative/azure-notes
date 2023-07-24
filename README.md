# azure-notes

Azure Fundamental Learning notes.

# Reference

https://learn.microsoft.com/en-us/training/paths/microsoft-azure-fundamentals-describe-cloud-concepts/

# Azure Core Architecture

## Azure Accounts

  - Every user or org needs to have an Azure Accounts under which miultiple subscriptions will created and each subscription will have ResourceGroups and under each ResourceGroups we can have multiple Resources.
    
  - Azure provides multiple ways to interact with Azure Cloud.

        1. PowerShell CLI - Based on Microsoft Power Shell CLI using which we can able to interact with Azure Cloud.
        2. BASH CLI - Based on BASH Command Line Interface to interact with Azure Cloud.
        3. Azure CLI (IDE like) - Azure CLI is created dedicatedly for Azure to interact with Azure cloud. One advantage over other
                                  approaches is it have auto-completion capability of command and we don't need to give az at front of
                                  every command.
        4. Azure Portal - Its an Azure provided Web and monbile based interface to interact and manga Azure resources.

   ### Power CLI 
```
       az version // This command will give current version of Power Shell. All the Azure specific command will start with AZ

       Get-Date  //This command will give current Date.

```

  ### BASH CLI

```
     date // This command will give current date in BASH CLI

     az upgrade // This will update upgrade CLI

```

  ### Azure CLI (Interactive mode)

```
   az interactive // This will enable the CLI interactive mode. This will provide ability to get auto completion for commands.
                  // Also we don't need to give az prefix while using interactive CLI mode.

    upgrade // This will update upgrade CLI
```

# Azure Physical Infra

### Regions

   - Region is a geographical area on the planet it contains one ore more data centers.
   - Whenever we deploy a resource we need to choose a region.
   - There are few Azure services for which we don't need to select a particular region.
        - Azure Active Directory
        - Azure Traffic Manager
        - Azure DNS

### Availability Zones

    - Availability zones are physically sperated datacenters within a specific Region.
    - A Region consist of one or more Availabilty Zones.
    - To ensure resiliency a minimum of three seperate availability zones are present in all availability zone-enabled regions.
      But not all Azure Regions currently support availability zones.
    - If we want to have high availabilty of our apps its better to create a reduantant stack in another availabilty zone.
      Mostly AZ's are for VM's, managed disks, load balancers and SQL DBs.

    - Azure services that support AZ's will fall in following 3 categorries.

      - Zonal Services - These services are tagged to a specific zone (VM's Managed Disks, IP address)

      - Zone-Redundant Services - The platform replicates automatically across zones (zone-redundant storage, SQL Database)

      - Non-Regional Services - Services are always available from Azure geographies and resilient to zone-wide outages as well as region-wide outages.

### Region Pairs (West US & East US)

    - Two Azure Regions are paired with one another on the same geography.
    - These paired regions are mostly 300 miles apart eachother.
    - Eventhough Regions pairs will have maximum protection in the event of any disaster not all
      the services are have the ability to fall back.
    - Most of these region pairs have bidirectional pairs. Each regions pairs will have backup of there region and vice versa.
      Ex West US & East US both have their own back up.
    - There are few regions are only unidirectional. Ex West India has Backup in South India but South India has back up in Central India.

### Sovereign Regions

     - These kind of regions are instances of Azure that are isolated from main Azure infra due government regulatory
       and compliance rules.

        Ex, US DoD Centeral, US Gov Virginia etc.

# Azure Management Infra

### Azure Resource Groups

    - Azure Resources - Any resource we use in Azure is Resource.
    - These Azure Resources are grouped together under a Resource Group.
    - A Resource can only belong to only one Resource Group.
    - If a Resource is moved from one Resource Group to another it won't have any access or privilage from previous group.
    - All the Resources from a Resource group will inherit rules from its Resource group.
    - Any change applied to Resource group will impact all the resourrces under that resource group.
    - When we delete a Resource group all the resource under that group will be deleted.

### Azure Subscriptions

    - Azure Subcriptions are logical grouping of Resource Groups to manage billing and scalability of resources.
    - A Subscription provide an Authenticated and authorized access to Azure product and services.
    - Azure Subscriptions are links to azure account.
    - Azure subscribtions are grouped under two boundaries.

       - Billing boundary - Determinses how an Azure account is billed for using Azure.
       - Access Control boundary - Access control can be applied to Subscription level. These access level
                                   will be applied to all the Resource groups under that Subscription.
### Azure Management Group

    - A Management Group is root level heirarchy. Under a Management Group multiple Subscriptions will be grouped.
    - We can create Azure Role based Access control (Azure RBAC) which can be applied to entire Management group.

# Azure architecture and services

### Azure Virtual Machines

   - VM's are physical servers which is hosted or provisioned on the cloud.
   - Its fundamental building block of an infrastructure where applications will be run.
   - In cloud terms VM's fall under IaaS category where user of VM have more control and responsibility over it.
   - User's of VM needs to take care of update and patching of OS and other tools installed in the VM's.
   - These VM's can be provisioned quickly using image templates where each templates will have predefined configs.
     Similarly we can create custom configuration image templates as per our requirements.
   - It provides an option of virtualized physical infrstructure which is hosted on the cloud.
   - User only need to pay as long as VM is running or in use.

### Azure VM Scale Sets (Grouping of identical VM's to achieve Scale on demand - IaaS offering)

  - In Azure Scale sets are grouping of identical VMs together with load balancer.
  - This type of grouping makes it easy to scale in or scale out number of VM's required based on the need and load
    among the VM's will be managed effectively and efficently.
  - By grouping like this its easy to monitor the utilization of each set of VM's based on different factors.

### Azure VM Availability Sets (Deals with Availability of physical infra)

  - Availability Sets make sure availability of physical infrastructure by grouping VMs.
  - It's ensures VMs stagger update and have high availability of VMs during any power and network connectivity issues.
  - AZ have two type of Availability Sets.

       - Update domain
       - Fault domain

  #### Update domain

    - This groups VM's in a way it can be rebooted at the same time. This helps when one group update is inprogress
      other group will be online to make sure no disruption.
    - An update domain group of VMs given 30 mins to complete the update then next group update will be started.

#### Fault domain

    - In this type VMs are grouped and make sure each group will have different power and network conncectivity.
    - Each fault domain VM's will be hosted on different network and has it's own power.
    - By default in this grouping VMs will be grouped under 3 different fault domains.

#### VM Resources

   - VM's are provisioned based on following 3 resource allocation.

     - Size (purpose, number of processor cores, and amount of RAM)
     - Storage disks (hard disk drives,solid state drives etc)
     - Networking (virtual network, public IP address and port configuration)
    
### Azure Virtual Desktop (A local desktop on the cloud)

  - It's cloud hosted Windows it can be accessed any location through browser.
  - With this we can move our local Windows provisioning for application development of any purpose to the cloud.
  - Provisoning of Windows systems will be done in minitues.
  - It will enhance security as these cloud hosted machines are already integrated with other AZ services
    like AZ Active Directory (AZ AD) and AZ Role based Access (RBAC).
  - With this kind of integration we can easily control who can access what type of resources.
  - Also in same single VM we can enable multiple users to access different Desktops.
  - This will reduce need to have Desktop Virtualization support team in house.
  - Also provisioned Desktops are billed on the usage basis only.

  ### Azure Containers (To run different type of OS on single host - PaaS offering)

   - Azure containers will provide ability to run different type of OS in single host.
   - Unlike in VM we can only run or host one type of OS where as in Containers we can inclue different type of OS
     whcih can run on single host.
   - Compare to VM's AZ Containers are light weight in nature where it can be provisoned and scaled quickly.
   - Conatiners are great choice when we want to run different types of OS specific apps in sinlge host.
   - AZ containers are example of PaaS offering.

### Azure Functions (Run code on demand Event driven - Serverless)

  - Azure Functions are serverless option to run our code on demand.
  - Where developer no need to worry about underlying infrastructure and its availability. Only
    give the code which neeeds to be executed based on event AZ will take care of infra needed to run it.
  - With Azure Function we can achieve Scalability, Performance and Pay as you use model.
  - Azure Functions are great choice when we want to run a specific code on need basis and it needs to be completed in
    short span of time.

### Azure App Service (An offering to build and run different type of Apps without worry about infra - PaaS)

  - Azure App service enables us to develop and host web apps, API apps, backgroundJobs, mobile apps without
    worry about the infrastructure in which it runs.
  - As Azure Apps will provide set of tools to enable hosting these apps it makes easy to up and running an app or API.
  - As a developer we don't need to provision infra and need to take care load balance configuration of the apps
    or deployment and scalability of the apps. All these concerns are handled through Azure App service.
  - All these feature will let developers only focus on building business apps and remaing cocerns will be taken care
    by Azure.
  - It can suppirt multiple languages like Java, Python, .NET, Ruby etc.

 Type of Azure App Services

    - Web Apps -> It supports hosting of Web apps using languages like Java, Python, .NET, Ruby etc. in Windows or
      Linux OS.

    - API Apps -> It support development and hosting or REST APIs using language of our choice. We can get full Swagger support.
                  These API's can be pacakged and publised in Azure market place and can be accessed in any HTTP supported clients.

    - WbJobs -> WebJobs can be used to run a backend jobs in any popular language of choice. Using this we can schedule or
                trigger these Jobs.

    - Mobile Apps -> This is used to build and deploy iOS or Android Apps.

 ### Advantage of Azuer Apps

   - Deployment and management are integrated into the platform.
   - Endpoints can be secured.
   - Sites can be scaled quickly to handle high traffic.
   - Build-in load balancing and traffic manager provide high availability.

# Azure Virtual Networking

### AZ Virtual Networks and Subnets

  - AZ Virtual Networks and Subnets enables AZ resoutces (VMs, Azure Web app, DBs etc) communicate with each other
    withint the  AZ network, on-perm and over the internet.It provides following key capabilities.

      - Isolation and Segmentation
      - Internet Communication
      - Communicate between AZ resources
      - Communicate with on-perm resources
      - Rote network traffic
      - Filter netwok traffic
      - Connect virtual networks
      - AZ networ supports Public and private endpoints to communicate between internal and external resources.
          - Public endpoints have a public IP address and can be accessed from anywhere in the world.
          - Private endpoints exist within a virtaul network and have a private IP addresss from within address space/range of that
            virtaul network.

### Isolation and Segmentation

  - Virtual networks will allows us to create multiple isolated virtual networks.
  - When we create a virtual network we can define a private IP address space by using either public or private IP address ranges.
  - This IP range exist only within that virtual netwrok and isn't internet routable.
  - We can divide that virtual network IP space into multiple subnets and allocate part of the defined address space to each named subnet.
  - For these subnet's IP name resolution we can use Azure name resolution service.

### Internet Communication (Through public IP address or public/Internet facing load balancer)

  - To comminicate between AZ resources we can do in 2 ways.

      - By default virtual networks connect multiple AZ resources like VMs, App Service Environment for Power Apps,
        AZ kubernetes Service, AZ virtual machine Scale sets.
      - Service Endpoints can connect to other AZ resource types like AZ SQL DBs and storage Accounts.

### On-prem Communication AZ resources

  - Point-to-Site virtual private network connections are from a computer outside of organization into corporate network.
    This communication client computer initiates an encrypted VPN connection to connect AZ virtual network.

  - Site-to-Site virtual private networks links on-perm VPN device or gateway to AZ VPN gateway in a virtual network.
    In this mode device in AZ can appear being local to on-perm network. This connection is encrypted and works over internet.

  - AZ Express Route provides a dedicated private connectivity to Azure that doesn't travel over the internet.
    It provide greater bandwidth and higher levels of security.

### Network traffic Routing

  - By default AZ routes traffic between connected networks, on-prem networks and internet. These setup can be overriden.
  - Using Routetables we can define rules about how traffic should be directed. We can create more route table and define
    how traffice to be routed between subnets.
  - Border Gateway Protocal (BGP) works with AZ VPN gateways, AZ Route Server or AZ ExpressRoute to propagate on-per BGP route to
    AZ virtual networks.

### Filter network traffic

  - Network security group resources are used to define multiple inbound and outbound security rules. Based on these
    rules we can control traffic flow into networ based in IP, Port and protocol.

  - Network virtual appliances are special VMs which carries a network funtion such as running a firewall or performing
    area network optimization.

### Connect Virtual networks (Peering)

  - Peering is way of connecting two virual networks together and make their comminication private.
  - Throuh peering two virtual networks comminicate via dedicated Microsoft network. This traffic never enter public internet.
  - These virtual network can be in two different regions.

# Azure Virtual Private Network (AZ VPN)

  - AZ VPN's enables a secured connection between two private networks over the internet. Traffic between these networks encrypted.

### VPN Gateways

  - AZ VPN gateway is deployedd in a dedicated subnet of the virtual network abd ebable following connectivity.

     - Connect on-prem datacenters to vitual networks through a Site-to-Site connection.
     - Connect individual devices to virtual networks through a Point-to-Site connection.
     - Connect virtaul networks to other virtual networks through a network-to-network connection.
     - A virtual network can have only one VPN gateway deployed. But it can connect to multiple locations like other virtual networks,
       on-prem datacenters, other virtual networks.
     - There are 2 types of VPN gateways 1. Policy based, 2. Route based.The main difference in the two type of VPN gateway is
       how traffic is encrypted.
     - Policy-based VPN gateway specify statically the IP address of packets that should be encyrpted through each tunnel.
     - Route-based gateways IPSec tunnels are modeled as a network interface or virtual tunner interface. IP routing will
       (static route or dynamic routing protocols)decided which one of these tunnes interface to use when sending each packet.
       Route-based VPN's are preferred connection method for on-prem devices as they are more resilient to topology changes.

### High-availability Scenarios

  - Active/Standby - By default VPN gateways are deployed as two instances in active/standby configuration.
    In case of any event for active VPN standby will assume the role of Active in few seconds for planned maintenance and
    within 90 seconds for unplanned disruptions.

  - Active/active - In this mode we can deploy two VPN gateways by assign unique public IP address to each instance and create
    a seperate tunnels froom the on-prem device to each IP address.

  - Express Route failover - Express Routes have built in resiliency configuration. But it can't gurantee during cable outages.
    In this scenario we can deploy VPN gateways as secure failover path for Express Route connections during the failover
    traffic is routed to internet through this VPN gateways.

### Zone-redundant gateways

  - In regions that support availability zones VPN gateways and Express Route gateways can be deployed zone-redundant configuration.
    This will bring higher availability to virtual network gateways.

# Azure Storage Accounts

  - A storage account provides a unique namespace for Azure storage data that's accessible from anywhere in the world over
    HTTP or HTTPS.
  - This storage accounts is secure, highly available, durable and massively scalable.
  - Creation of Storage Account will determine by picking correct account type and this account type determines storage services
    redundancy options baed on use cases.Following are list of available redundancy options.

      - Locally redundant storage (LRS)
      - Geo-redundant storage (GRS)
      - Read-access geo-redundant storage (RA-GRS)
      - Zone-redundant storage (ZRS)
      - Geo-zone-redundant storage (GZRS)
      - Read-access geo-zone-redundant storage (RA-GZRS)

## Account Types and Usage patterns/possible use case scenrios

### Standard general-purpose v2

  - Standard storgae account type for blobs,file shares,queues and tables.
  - Recommended for most scenarios using Azure Storage.
  - If we need network file system (NFS) then we can use the premium file shares account type.

### Premium block blobs

  - This is premium storage account type for block blobs and append blobs.
  - Recommended for scenarios with high transactions rates or that smaller objects or requires
    consistently low storage latency.

### Premium file shares

  - It only for file shares.
  - Recommended for enterprise or high-performance scale applications.
  - This recommended when we need support for Server Message Block (SMB) and NFS files shares.

### Premium page blobs

  - Premium storage account type for page blobs only.

### Storage Account Endpoints (Storage Account + Storage Service)

  - Each storage account will have global uniqueue account name. Combination of Storage Account Name with
    respective storage account service will form a Storage Account Service Endpoint.
  - Storage Account names must be between 2 and 24 characters in length and may contain numbers and lowercase
       letters only.
     - Storage account name must be uniqueu with Azure.

       Ex -> https://<storage-account-name>.blob.core.windows.net

# Azure Storage Redundancy

  - Azure Storage will always stores multiple copies of data based on type of storage account and its redundancy preference.
  - It helps to recover data in the event of any type of outages.
  - Following factors detemine which type of redundancy option we need to choose.

      - How data is replicated in the primary region.
      - Wheather data is replicated in regional level or not. This is to ensure any regional level disaster
        will keep our data safe.
      - Whether application requires read access to the replicated data in the secondary region if the primary region
        becomes unavailable.

### Primary Region Redundancy (LRS & ZRS)

  - In Azure Storage account data is always replicated 3 times in the Primary Reegion.
  - There are 2 types of Primary region Redundancy is possible.

      - LRS -> Locally Redundant Storage
      - ZRS -> Zone Redundant Storage

### LRS -> Locally Redundant Storage (Data stored in Single Data Center)

  - Thress copies of Data is stored in Single Data center of the primary region.
  - This is least cost efficient storage option and provides 11 nines of durability.
  - This type of storage can help us to protect server rack and dive failures. But if any issue to that
    data center(major fire in the building and any natural disaster etc) entire data will be lost.
  - To avoid this kind of issues we can use ZRS (Zone Redundant Storage) or GZRS (Geo Zone Redundant Storage)

### Zone Redundant Storage (Data is stored in 3 different Zones in Same Region)

  - In ZRS same data is replicated in 3 different data centers of 3 different AZ of the same region.
  - It offers 12 nines of durability over year.
  - In this type of storage data can be access for both read and write even if a zone is unavailable.
  - No remounting of Azure file shares from connected clients is required.
  - If zone becomes unavailable Azure undertakes networking updates such as DNS repointing. This migh impact
    the application until those updates are completed successfully.
  - This type of storage is recommended where we need high availability and where we have some restriction
    based on geo graphy due to govenment regulations on data movement.

### Secondary Region Redundancy (Replication of data in Secondary Region)

  - In this type of Storage data can be stored in another region other than Primary Region through Azure Region pairs.
  - This secondrary region will get data asynchronously from primary region.
  - So if any issue during primary region we have to make a failove to secondary region. Once failover is completed
    Secondary region will become a primary region.Due to this Secondary region data won't be available for Read or Write.
  - During any failure in primary region and switch to the Secondary region will have time delay and there is a possiblity
    of data loss during this duration.
  - The intervel between most recent writes to primary region and last write to secondary region is called recover point object RPO.
  - Azure storage has an RPO of 15 mins, but currently no guranteed SLA of the same.
  - Azure supports two type of Secondary region data coping.

     - GRS -> Geo Redundant Storage 
         - Data is copied to three times in single physical location synchronously. And same date is copied to another region single data center in Secondary region. It offeres 16 nines of durability.
           
     - GZRS -> Geo Zone Redundant Storage
         - Data is copied to multi zone data centers in Primary region synchronously and three copies of the same data is stored in secondary region single data center asynchronously.
       
# Azure Storage Services

  - Blob Storage
  - Azure Files
  - Azure Queues
  - Azure Disks

### Blob Storage

  - Blob Storage stores text and binary form of data at massive scale.
  - It supporst unstructured data so it can be applicable for different type of use cases.
  - With this we can store large volume of Audio and Video files, log events, IoT specific data at massive scale.
  - Developer don't need to worry about storage space.
  - This data can be easily accessable over the internet throuh HTTP & HTTPS.

### Blob Data access tiers (Based on frequency of access and planned retention)

  - Hot Access tier -> Optimized for storing data that is accessed frequently (images for websites)
      - Can be set Account level
      - Can be set Blob level during or after upload
  - Cool Access tier -> Optimized for infrequently accessed data and stored for at least 30 days (Customer invoice)
      - Can be set Account level
      - Can be set Blob level during or after upload
      - Lower availability and higher access cost.
  - Archive Access tier -> Data which is rarely accessed and stored at least 180 days with flexible latency requirements.
      - Data is stored offline and offers lowest storage cost.
      - But high cost to regudrate and access data.

### Azure Files

  - Offers fully managed file shares in the cloud that are accessible via industry standard Server Message Block (SMB) or
    Network File System (NFS) protocols.
  - These files shares can be mounted concurrently by cloud or on-perm deployments.
  - Server Message Block Azure files are accessible from Windows, Linux and macOS clients. Alos it can be cahced on Windoes Servers.
  - NFS Azure files shares are accessible from Linux and macOS.

### Azure Queue Storage

  - Azure Queue storage we can store large number of messages as long as Azure Account storage has space to allow storage.
  - Each message can be up to 64 KB in Size.
  - Store messages can be accessed via internet through HTTP or HTTPS calls with authentication enabled.

### Disk Storage

  - Azure managed disk for VM's. These are used for block-level storage volumes managed by Azure.
  - These are virtualized physical disk and managed by Azure for us.

### Azure Data migration options

  - Azure Migrate -> Helps to migrate on-perm to cloud (Azure)
  - It provides set of tools to migrate on-perm data to Cloud most efficiently.

      - Azure Migrate: Discover and Assessment -> Acess and plan
      - Azure Migrate: Server Migration -> Migrate physical servers to Cloud
      - Data Migration Assistant -> To acess SQL servers.
      - Database Migration Service -> To migrate on-perm DB's mostly SQL based DB's
      - Web app migration assitant -> To migrate on-perm .NET and PHP baed apps to Azure app service
      - Azure Data Box -> To move large data through physical box.

### File movement options

  - Azure has three tools AzCopy, Azure Storage Explorer and Azure Fily Sync to copy files or blobs.

### AzCope (To Copy files or blobs) 

  - It's a command-line utility tool to support copy files or blobs
  - With this we can upload, download or copy files between storage accounts and even synchronize files.
  - This can be integrated with other providers and move files between different cloud vendors.
  - AzCopy will support synchronization of files in one direction only.

### Azure Storage Explorer

  - A standalone GUI to manage file and blobs in Azure storage account.
  - It works in Windows, macOS and Linux.
  - It uses AzCopy under the hood.

### Azure File Sync

  - It will act as intermediate component between local windows server and Azure Files in cloud.
  - It provide bi-directional sync between you local server and Azure file.
  - With this we can use any protocl that's available on windows Server to access data locally including SMB,NFS and FTPS.
  - Have as many caches we need across the world.
  - Replace failed local server by installing Azure File Sync on a new server in the same data center.
  - Configure cloud tiering so the most frequently accessed files are replicated locally, while infrequently accessed files are kept in the cloud until its requested.

# Azure Identity, Access and Security

### Azure Directory Service (Azure AD (Active Directory))

  - Active Directory running on windows server will provides an identity and access management service. This might be manged by an
    organization and run on local on-perm.
  - Azure Active Directory which is managed by Azure will provide support to manage access to both Microsoft cloud applications
    and application which we develop and deploy on cloud.
  - With Azure AD we can use it globally to control access management of cloud applications.
  - With on-perm Active directory Microsoft doesn'y monitor singn-in attempts. But with Azure AD Microsft help to identify
    suspicious sign-in attempts at no extra cost.
  - It can be used by
      - IT administrartors -> To control access to apps and resources based on business requirements
      - App Developers -> To enable SSO functionality
      - Users -> Password Re-set
      - Online service subscribers -> Subscribers of Microsoft 365, Mocriosoft Office 365, Azure etc will already using it.
  - It can do and support following things.
      - Authentication
      - SSO
      - Application Management -> By providong Application proxy, SaaS apps, My Apps portal and SSO.
      - Device Management -> To manage device based access. Using Azure AD we can control access based on specific registered device.
  - Using Azure AD Connect we can connect both on-perm AD and Azure AD. But both the systems will maintian two different identities.
    Azure AD connect synchronizes user identities between on-perm AD with Azure AD.

### Azure Active Directory Domain Services

  - It provides services like domain join, group policy, light weight directory access protocol (LDAP) and Kerberos/NTLM
    authentication.
  - It's a cloud managed service so users don't have to manage or maintin it.
  - It mainly used to manage/run legacy application in the cloud that can't use modern authentication methods.
  - Azure AD DS integrates with existing Azure tenant. This integration allows user singn into services and applications
    connected to managed domain using their existing credentials.
  - Azure AD DS is configured to perform one-way synchroniztion from Azure AD to Azure AD DS.

### Azure Authentication methods

  - SSO (Single Sign On)
  - MFA (Multi Factor Authentication)
  - Passwordless Authentication
    - Windows Hellow for Business -> Tied to user Device like laptop and a biometric or PIN is attached/setup an extra authentication
                                     mechanism.
    - Microsoft Authenticator App -> An app which is downloaded in to users devive and registered which provide a authentication PIN.
    - FIDO2 Security Keys -> Fast Identity Online supports and promote open authentication standards and reduce the use of passwords.
                             with this user can register and select a FIDO2 security key at the sign-in interface as main means of 
                             authentication. These keys are are USB devices or Bluetooth. Then these hardware devices are used to
                             authenticate instead of password.
      
### Azure external identities

  - An external identities are one might be external users, apps, devices etc.
  - Azure will support to mange these external users authentication usinh Azure AD External Identites.
  - These users can bring their own identity through which we can give our Azure app access. Azure will support this
    kind of authentication using Azure AD External Identities.

      - Business to business (B2B) collaboration -> Collaborate with external users by letting them use their preferred identity to
                                                    sign-in our micorsoft applications. B2B collaboration user are mostly guest users.
      - B2B Direct Connect -> Establish mutual two way trust with Azure AD org for seamless collaboration through Team shared channels.
                              B2B direct connect users are not in our directory but they are managed by teams admin.
      - Azure AD Business to Consumer (B2C) -> Consumers of published apps.
   
### Azure conditional Access

  - It's a Tool which allows Azure Active directory uses to allow or deny access to a resources based on identity signals.
  - A signal is user, location of user, device of user etc.
  - Based on this signal Conditional Access tool will decide to allow or deny the user to access that resource.

### Azure RBAC (Role Based Access Control)

  - To control access to a resource based on defined allowed rules.
  - There are 2 type of components. 1. Scope , 2. Role
      - Scope A management group, Single Subscription, Resource Group, Single Resource.
      - People belong to these Scope will be given different type of access like Reader, Resource specific, Custom, Owner or
        Contributor kind of access.
  - In RBAC when access is granted to parent Scope then that access will be inherited to all the users under the group.
  - RBAC access contorl is enfored by Resource Manger service in Azure.

### Zero Trust Model (Design system for worst case scenario)

  - Always have security layer designed for worst case scenario in mind. It's based on following principle.
      - Verify explicitly -> Always authenticate and authorize based on all available data points.
      - Use least privilege access -> Limit user access with Just-in-Time and Just-Enough-Access (JIT/JEA) risk based
        adaptive policies and data protection.
      - Assume breach -> Minimize blast radius and segment access and verify E2E encryption. Use effective analytics to get visibility,
                         drive threat detection and improve defence.

### Defence-in-Depth

  - It provides a framework or methodalogy proetction of data which is secured by 7 layers of security consideration.

  - Physical Security -> Limited and only authorized access to physical data center.
  - Identity and Access -> Access is granted to what's needed and Sign-in events are properly logged.
  - Perimeter -> It protects data from Network based attacks against resource. User DDoS protection to filter large-scale attacks
                 before it can affect system availability. Use perimeter firewalls to indentify and alert on malicious attacks.
  - Network -> Limiting network connectivity to resources. Use deny by default rules.
  - Compute -> Secure access to VM's and implement endpoint protection and make sure system is patched properly.
  - Application -> Integrating Scurity Vulnarability checks as part of Application Development life cycle.
  - Data -> Those who store and access data should be responsible for security of it.

### Microsoft Defender for Cloud (To Secure Azure, on-perm, Multi Cloud resources) 

  - It provides various tools to secure Azure, on-perm and other cloud provider resources.
  - It gather all the security specific data and logs and analysis send specific aletrs based on analysis.
  - For  Hybrid and multicloud environments Microsoft Defender plans extent to non Azure machines with help of Azure Arc.
  - Cloud Security Posture Management (CSPM) features are extended to multicloud machines.
  - It works based on 3 principles Assess, Secure and Defend.

# Factors which affect Azure Cost

  - With cloud we will not worry about initial cost of setting up infrastructure and investment on those skillset(CapEx-Capital Expenditure).
    We only need to pay what we will be using by pay-you-use model. This is called OpEx - Operational Expenditure.

    Following factors will impact cost of the Azure.

      - Resource Type -> Type of Resource we choose will be one of the major factore will have cost component. Like what type
                          of storage account and its access pattern and region in which we create this resource etc.

      - Consumption -> With Pay-as-you go or use model we will be paying what is the resources we are using actively.
                       With this when we choose a particular resource if we choose it with long term useage model we will
                       get huge discounts etc.

      - Maintenance -> With Resource groups based on need we can scale up or down our resources based on demand.

      - Geography -> Based on region in which we create a resource it will have a cost factor associated with it.

      - Network Traffic -> Data movement between resources and in and out of the cloud will be one of the important factor
                           deciding cost. Mostly data which coming in to Azure will be free but data going out will be costly.

      - Subscription Type -> Type of subscription will decide the overall cost of Cloud in Azure. Free subscription will be no cost to us.

      - Azure Marketplace -> Apart from Azure Services there are multiple third party vendor.

### Pricing Calculator

  - Used to calculate cost of Azure resource. It will give an estimate cost of Individual Azure resource.

  - With this calculator we can't provision any resource as such.

### Total Cost of Ownership (TCO)

  - TCO calculator is used to derive an estimate to move on-perm configuration to Azure Cloud.
  - With this we can provide our current on-perm server details, storage, Network bandwidth info and it
    will provide an anticipated cost for when we create/move this infra to Azure.



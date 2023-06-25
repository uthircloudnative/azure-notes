# azure-notes
Azure Fundamental Learning notes


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

### Region Pais (West US & East US)

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

### Azure VM Scale Sets (Grouping of identical VM's to achieve Scale on demand)

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

  ### Azure Containers (To run different type of OS on single host)

   - Azure containers will provide ability to run different type of OS in single host.
   - Unlike in VM we can only run or host one type of OS where as in Containers we can inclue different type of OS
     whcih can run on single host.
   - Compare to VM's AZ Containers are light weight in nature where it can be provisoned and scaled quickly.
   - Conatiners are great choice when we want to run different types of OS specific apps in sinlge host.
   - AZ containers are example of PaaS offering.



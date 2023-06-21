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

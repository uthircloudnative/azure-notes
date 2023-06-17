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

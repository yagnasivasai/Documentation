#  Team Foundation Server 2013 (TFS 2013), but intend to migrate to Azure DevOps

1. Get Started
This phase is all about preparing for the migration. You choose a location for your Azure DevOps Services organization data. You find out which licenses you need. And you establish the name of your Azure DevOps environment. You can then download the TFS Migrator Tool.

2. Prerequisites
The second phase focuses on the requirements for migrating your data to the cloud. Your team must have an active Azure Active Directory tenant which is used for authentication of your team members. By synchronizing your local Active Directory with your Azure Active Directory, team members can use the current login details.

3. Upgrade TFS
You cannot just migrate from every version of TFS to Azure DevOps Services. You need to start by upgrading TFS to a version that is supported by the TFS Migrator Tool. We recommend upgrading to the latest version of Azure DevOps Server.

4. Validation
Once you have upgraded to a supported version of Azure DevOps Server, the database needs to be validated for the migration. The TFS Migrator Tool is used to carry out verifications and to identify any errors. Any errors that are found must be repaired at this stage. 

5. Get Ready
Nearly there! In this phase, you need to make preparations for the dry run and the final imports. You can use the TFS Migrator Tool to generate the import settings and related files. This involves creating an Azure Storage Container in the same data center as your ultimate Azure DevOps Services organization. 

We recommend that you use this phase to prepare thoroughly for the new environment and to ensure that all subscriptions are properly organized.

6. Import
Time for the final phase: the import. You must start by completing a dry run. You should monitor how long each step takes so that you can schedule the final import properly. But what are the steps?

You must first disconnect the Team Project Collection in the Administration Console. You should then make a backup of the Team Project Collection SQL Database and then upload the SQL Database and Identity Map to your Azure Storage Container. 

You then need to generate a shared access signature (SAS) key for your Azure Storage Container and populate the final fields of your import specifications (such as your SAS key and the name that you chose in phase one).

In the end, you configure the invoicing settings based on the subscriptions that you identified in phase five. Finally, you need to create the new connection – from your on-premise servers to the Azure DevOps Services environment that you have just imported.

https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/migrate/azure-best-practices/contoso-migration-tfs-vsts

# Build on-premises Bitbucket repositories

https://learn.microsoft.com/en-us/azure/devops/pipelines/repos/on-premises-bitbucket?view=azure-devops
1. If Bit server is reachable you can create Microsoft hosted agent and Other Git service connection. CI triggers work through polling and not through webhooks. In other words, Azure Pipelines periodically checks the Bitbucket server if there are any updates to code. If there are, then Azure Pipelines will start a new run.
2. Not reachable from Microsoft-hosted agents 
   - If the simple test pipeline mentioned in the above section fails with the error TF401019: The Git repository with name or identifier <your repo name> does not exist or you do not have permissions for the operation you are attempting, then the Bitbucket server is not reachable from Microsoft-hosted agents. This is again probably caused by a firewall blocking traffic from these servers. You have two options in this case:
   - Work with your IT department to open a network path between Microsoft-hosted agents and Bitbucket server. See the section on networking in Microsoft-hosted agents.
   - Switch to using self-hosted agents or scale-set agents. These agents can be set up within your network and hence will have access to the Bitbucket server. These agents only require outbound connections to Azure Pipelines. There is no need to open a firewall for inbound connections. Make sure that the name of the server you specified when creating the service connection is resolvable from the self-hosted agents.

# Threat Code analysis
https://learn.microsoft.com/en-us/previous-versions/azure/security/develop/security-code-analysis-overview

+ Microsoft Security Code Analysis tool set
    - The Anti-Malware Scanner build task is now included in the Microsoft Security Code Analysis extension.
    - BinSkim is a Portable Executable (PE) lightweight scanner that validates compiler settings, linker settings, and other security-relevant characteristics of binary files. This build task provides a command-line wrapper around the binskim.exe console application. BinSkim is an open-source tool.
    - Passwords and other secrets stored in source code are a significant problem. Credential Scanner is a proprietary static-analysis tool that helps solve this problem. The tool detects credentials, secrets, certificates, and other sensitive content in your source code and your build output
    - Roslyn Analyzers is Microsoft's compiler-integrated tool for statically analyzing managed C# and Visual Basic code.
    - TSLint is an extensible static-analysis tool that checks TypeScript code for readability, maintainability, and errors in functionality. It's widely supported by modern editors and build systems. You can customize it with your own lint rules, configurations, and formatters. TSLint is an open-source tool

+ Prerequisites to getting started with Microsoft Security Code Analysis:
    -   An eligible Microsoft Unified Support offering, as detailed in the following section.
    -   An Azure DevOps organization.
    -   Permission to install extensions to the Azure DevOps organization.
    -   Source code that can be synced to a cloud-hosted Azure DevOps pipeline


# DSC Configurations
+ DSC configurations are PowerShell scripts that define a special type of function. To define a configuration, you use the PowerShell keyword Configuration.
+ Before you can enact a configuration, you have to compile it into a MOF document. You do this by calling the configuration like you would call a PowerShell function
+ The Register-AzAutomationDscNode cmdlet registers an Azure virtual machine as an APS Desired State Configuration (DSC) node in an Azure Automation account. This cmdlet will only register VMs running Windows OS as an Automation DSC Node for an account.
If you need to register a node to an automation account in a different subscription, you will need to use an ARM template rather than cmdlets. See the Azure Automation documentation for more details


# VMSS
+ https://ochzhen.com/blog/azure-custom-script-extension-windows
+ https://cloudblogs.microsoft.com/opensource/2018/06/18/tutorial-canary-deployment-for-azure-virtual-machine-scale-sets/


# Teams
+ https://azuredevopslabs.com/labs/vstsextend/teams/
+ 
  

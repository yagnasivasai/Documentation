Networking

https://docs.microsoft.com/en-us/azure/virtual-network/network-security-group-how-it-works

https://docs.microsoft.com/en-us/azure/security/fundamentals/network-best-practices

https://docs.microsoft.com/en-us/azure/virtual-network/security-overview#application-security-groups

https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal

https://learn.microsoft.com/en-us/azure/load-balancer/skus

https://learn.microsoft.com/en-us/azure/load-balancer/load-balancer-custom-probe-overview

https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-network-interface

https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances

https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-faq#name-resolution-dns

https://docs.microsoft.com/en-us/azure/load-balancer/backend-pool-management

https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-certificates-point-to-site

https://docs.microsoft.com/en-us/azure/azure-policy/policy-definition

https://azure.microsoft.com/en-us/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/

https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-manage-peering#requirements-and-constraints

https://fastreroute.com/azure-network-security-groups-explained/

https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview

https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview

The connection monitor capability monitors communication at a regular interval and informs you of reachability, latency, and network topology changes between the VM and the endpoint
The IP flow verify capability enables you to specify a source and destination IPv4 address, port, protocol (TCP or UDP), and traffic direction (inbound or outbound). IP flow verify then tests the communication and informs you if the connection succeeds or fails. If the connection fails, IP flow verify tells you which security rule allowed or denied the communication, so that you can resolve the problem.
The connection troubleshoot capability enables you to test a connection between a VM and another VM, an FQDN, a URI, or an IPv4 address. The test returns similar information returned when using the connection monitor capability, but tests the connection at a point in time, rather than monitoring it over time, as connection monitor does.
The NSG flow log capability allows you to log the source and destination IP address, port, protocol, and whether traffic was allowed or denied by an NSG.

https://docs.microsoft.com/en-us/azure/vpn-gateway/create-routebased-vpn-gateway-portal

https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps

- A VPN gateway is used when creating a VPN connection to your on-premises network.

Route-based VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic to different IPsec tunnels. It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).

- Policy-based VPN devices use the combinations of prefixes from both networks to define how traffic is encrypted/decrypted through IPsec tunnels. It is typically built on firewall devices that perform packet filtering. IPsec tunnel encryption and decryption are added to the packet filtering and processing engine

https://docs.microsoft.com/en-us/azure/dns/private-dns-overview

https://docs.microsoft.com/en-us/azure/dns/private-dns-virtual-network-links

https://docs.microsoft.com/en-us/azure/dns/private-dns-autoregistration
 
https://azure.microsoft.com/en-us/updates/general-availability-azure-network-watcher-connection-monitor-in-all-public-regions/

Loadbalancer
Limitations
IP based backends can only be used for Standard Load Balancers
The backend resources must be in the same virtual network as the load balancer for IP based LBs
A load balancer with IP based Backend Pool can’t function as a Private Link service
Private endpoint resources can't be placed in a IP based backend pool
ACI containers aren't currently supported by IP based LBs
Load balancers or services such as Application Gateway can’t be placed in the backend pool of the load balancer
Inbound NAT Rules can’t be specified by IP address
You can configure IP based and NIC based backend pools for the same load balancer. You can’t create a single backend pool that mixes backed addresses targeted by NIC and IP addresses within the same pool.
A virtual machine in the same virtual network as an internal load balancer cannot access the frontend of the ILB and its backend VMs simultaneously


Floating IP
Some application scenarios prefer or require the same port to be used by multiple application instances on a single VM in the backend pool. Common examples of port reuse include:

clustering for high availability
network virtual appliances
exposing multiple TLS endpoints without re-encryption.
If you want to reuse the backend port across multiple rules, you must enable Floating IP in the rule definition.

When Floating IP is enabled, Azure changes the IP address mapping to the Frontend IP address of the Load Balancer frontend instead of backend instance's IP. Without Floating IP, Azure exposes the VM instances' IP. Enabling Floating IP changes the IP address mapping to the Frontend IP of the load Balancer to allow for more flexibility. Learn more here.

What types of Azure Load Balancer exist?
Internal load balancers, which load balance traffic within a virtual network.

External load balancers, which load balance external traffic to an internet connected endpoint. For more information, see Azure Load Balancer Types.

For both of the types, Azure offers a basic SKU and standard SKU that have different functional, performance, security and health tracking capabilities. For more information about the different load balancer SKUs, see SKU Comparison.

How can I upgrade from a basic to a standard load balancer?
For more information about an automated script and guidance on upgrading a load balancer SKU, see upgrade from Basic to Standard.

What are the different load-balancing options in Azure?
For the available load-balancing services and recommended uses for each, see the load balancer technology guide.

Where can I find the load balancer ARM templates?
See the list of Azure Load Balancer quickstart templates for ARM templates of common deployments.

How are inbound NAT rules different from load-balancing rules?
Inbound NAT rules are used to specify a backend resource to route traffic to. For example, configuring a specific load balancer port to send RDP traffic to a specific VM. Load-balancing rules are used to specify a pool of backend resources to route traffic to, balancing the load across each instance. For example, a load balancer rule can route TCP packets on port 80 of the load balancer across a pool of web servers.

What is IP 168.63.129.16?
The virtual IP address for the host tagged as the Azure infrastructure load balancer where the Azure health probes originate. Traffic must be allowed from this IP address to successfully respond to health probes when backend instances are configured. This rule doesn't interact with access to your load balancer frontend. If you're not using the Azure Load Balancer, you can override this rule. You can learn more about service tags here.

Can I use global virtual network peering with a basic load balancer?
No. Basic load balancer doesn't support global virtual network peering. You can use a standard load balancer instead. See the upgrade from Basic to Standard article for information about the upgrade.

How can I discover the public IP that an Azure VM uses?
There are many ways to determine the public source IP address of an outbound connection. OpenDNS provides a service that can show you the public IP address of your VM. By using the nslookup command, you can send a DNS query for the name myip.opendns.com to the OpenDNS resolver. The service returns the source IP address that was used to send the query. When you run the following query from your VM, the response is the public IP used for that VM:

nslookup myip.opendns.com resolver1.opendns.com

Can I add a VM from the same availability set to different backend pools of a load balancer?
Adding a VM from the same availability set to different backend pools isn't possible.

What is the maximum data throughput that can be achieved via an Azure Load Balancer?
Azure Load Balancer is a pass-through network load balancer. Throughput limitations are determined by the type of virtual machine in the backend pool. To learn about other network throughput related information, see Virtual Machine network throughput.

How do connections to Azure Storage in the same region work?
Having outbound connectivity via the scenarios above isn't necessary to connect to storage in the same region as the VM. Use network security groups (NSGs) as explained above to prevent this behavior. For connectivity to storage in other regions, outbound connectivity is required. The source IP address in the storage diagnostic logs will be an internal provider address, and not the public IP address of your VM when connecting to storage from a VM in the same region. To restrict access to your storage account to VMs in one or more virtual network subnets in the same region, use Virtual Network service endpoints. Don't use your public IP address when configuring your storage account firewall. When service endpoints are configured, you'll see your virtual network private IP address in your storage diagnostic logs and not the internal provider address.

Does Azure Load Balancer support TLS/SSL termination?
No, Azure Load Balancer doesn't currently support termination as it's a pass through network load balancer. Application Gateway could be a potential solution if your application requires termination.

How do I configure my load balancer with an Azure Firewall?
Follow these instructions to configure your load balancer with an Azure Firewall.

Can I use my custom IP address prefix (BYOIP) with Azure Load Balancer?
Yes, this scenario is supported. You will need to create a public IP prefix and public IP address from your custom IP address prefix before using it with your load balancer. To learn more, visit Manage a custom IP address prefix.

How do I configure my load balancer with an Azure SQL Server Always On availability group?
Follow these Portal or PowerShell instructions to configure your load balancer with an Azure SQL Server Always On availability group.

Can I access the frontend of my internal load balancer from the participating backend pool VM?
No, Azure Load Balancer doesn't support this scenario. To learn more, visit our troubleshoot page.

What are best practices with respect to outbound connectivity?
Standard load balancer and standard public IP introduce abilities and different behaviors to outbound connectivity. They aren't the same as basic SKUs. If you want outbound connectivity with standard SKUs, you must explicitly define it either with standard public IP addresses or a standard public load balancer. Standard internal load balancer must have outbound connectivity defined. It's recommended you always use outbound rules on a standard public load balancer. When an internal standard load balancer is used, you must take steps to create outbound connectivity for the VMs in the backend pool if outbound connectivity is desired. In the context of outbound connectivity, a single standalone VM, all the VMs in an Availability Set, all the instances in a virtual machine scale set behave as a group. If a single VM in an Availability Set is associated with a standard SKU, all VM instances within this Availability Set now behave by the same rules as if they're associated with standard SKU even if an individual instance isn't directly associated with it. This behavior is also observed in a standalone VM with multiple network interface cards attached to a load balancer. If one NIC is added as a standalone, it will have the same behavior. Review this entire document to understand the overall concepts, review Standard Load Balancer for differences between SKUs, and review outbound rules. Using outbound rules allows you fine grained control over all aspects of outbound connectivity.

How can I view the traffic from my configured health probe(s)?
To view the traffic sent to each backend instance from the health probe you can use IP stack statistics with a tool such as netstat. The health probe traffic will originate from 168.63.129.16.

If I enable DDoS Protection for my load balancer frontend, what does that mean for the resources in the backend pool?
When enabled on the frontend IP for a load balancer, DDoS Protection will apply protection for all backend pool resources that are accessible through that public IP. For more information, see Azure DDoS Protection Reference.

Why are certain ports restricted for HTTP health probes?
The following ports are restricted for HTTP health probes: 19, 21, 25, 70, 110, 119, 143, 220, 993. These ports are blocked for security reasons by WinHTTP, meaning that Load Balancer health probes are unable to use these ports. For more information, see What's New in WinHTTP 5.1

Point to Site

Point-to-site connections use certificates to authenticate.

The PowerShell cmdlets that you use to generate certificates are part of the operating system and don't work on other versions of Windows. The host operating system is only used to generate the certificates. Once the certificates are generated, you can upload them or install them on any supported client operating system.

If you don't have a computer that meets the operating system requirement, you can use MakeCert to generate certificates. The certificates that you generate using either method can be installed on any supported client operating system


Service tags
A service tag represents a group of IP address prefixes from a given Azure service. It helps to minimize the complexity of frequent updates on network security rules.

For more information, see Azure service tags. For an example on how to use the Storage service tag to restrict network access, see Restrict network access to PaaS resources.

Application security groups
Application security groups enable you to configure network security as a natural extension of an application's structure, allowing you to group virtual machines and define network security policies based on those groups. You can reuse your security policy at scale without manual maintenance of explicit IP addresses. To learn more, see Application security groups.

Azure Network Watcher provides tools to monitor, diagnose, view metrics, and enable or disable logs for resources in an Azure virtual network. Network Watcher is designed to monitor and repair the network health of IaaS (Infrastructure-as-a-Service) products including Virtual Machines (VM), Virtual Networks, Application Gateways, Load balancers, etc.

Diagnose network traffic filtering problems to or from a VM
When you deploy a VM, Azure applies several default security rules to the VM that allow or deny traffic to or from the VM. You might override Azure's default rules, or create additional rules. At some point, a VM may become unable to communicate with other resources, because of a security rule. The IP flow verify capability enables you to specify a source and destination IPv4 address, port, protocol (TCP or UDP), and traffic direction (inbound or outbound). IP flow verify then tests the communication and informs you if the connection succeeds or fails. If the connection fails, IP flow verify tells you which security rule allowed or denied the communication, so that you can resolve the problem. Learn more about IP flow verify by completing the Diagnose a virtual machine network traffic filter problem tutorial.

Diagnose network routing problems from a VM
When you create a virtual network, Azure creates several default outbound routes for network traffic. The outbound traffic from all resources, such as VMs, deployed in a virtual network, are routed based on Azure's default routes. You might override Azure's default routes, or create additional routes. You may find that a VM can no longer communicate with other resources because of a specific route. The next hop capability enables you to specify a source and destination IPv4 address. Next hop then tests the communication and informs you what type of next hop is used to route the traffic. You can then remove, change, or add a route, to resolve a routing problem. Learn more about the next hop capability.

Diagnose outbound connections from a VM
The connection troubleshoot capability enables you to test a connection between a VM and another VM, an FQDN, a URI, or an IPv4 address. The test returns similar information returned when using the connection monitor capability, but tests the connection at a point in time, rather than monitoring it over time, as connection monitor does. Learn more about how to troubleshoot connections using connection-troubleshoot.

Capture packets to and from a VM
Advanced filtering options and fine-tuned controls, such as the ability to set time and size limitations, provide versatility. The capture can be stored in Azure Storage, on the VM's disk, or both. You can then analyze the capture file using several standard network capture analysis tools. Learn more about packet capture.

Diagnose problems with an Azure Virtual network gateway and connections
Virtual network gateways provide connectivity between on-premises resources and Azure virtual networks. Monitoring gateways and their connections are critical to ensuring communication are not broken. The VPN diagnostics capability provides the ability to diagnose gateways and connections. VPN diagnostics diagnoses the health of the gateway, or gateway connection, and informs you whether a gateway and gateway connections are available. If the gateway or connection is not available, VPN diagnostics tells you why, so you can resolve the problem. Learn more about VPN diagnostics by completing the Diagnose a communication problem between networks tutorial

Azure DNS Private Resolver is a new service that enables you to query Azure DNS private zones from an on-premises environment and vice versa without deploying VM based DNS servers.

- NSG flow log data is written to an Azure Storage account. You need to create an Azure Storage account,

With an Azure Storage account NSG flow logs can be enabled.

- Enable network watcher in the East US region.

- NSG flow logging requires the Microsoft.Insights provider.

https://learn.microsoft.com/en-us/azure/dns/dns-web-sites-custom-domain
https://learn.microsoft.com/en-us/azure/dns/delegate-subdomain
https://learn.microsoft.com/en-us/azure/storage/common/storage-network-security?tabs=azure-portal
https://learn.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-portal

With Sticky Sessions when a client starts a session on one of your web servers, session stays on that specific server. To configure An Azure Load-Balancer For

Sticky Sessions set Session persistence to Client IP.
https://cloudopszone.com/configure-azure-load-balancer-for-sticky-sessions/


https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-udr-overview
https://www.quora.com/What-is-IP-forwarding
https://learn.microsoft.com/en-us/azure/load-balancer/load-balancer-multivip-overview
https://learn.microsoft.com/en-us/azure/load-balancer/load-balancer-overview

The virtual networks can be in the same or different regions, and from the same or different subscriptions. When connecting VNets from different subscriptions, the subscriptions do not need to be associated with the same Active Directory tenant.

Configuring a VNet-to-VNet connection is a good way to easily connect VNets. Connecting a virtual network to another virtual network using the VNet-to-VNet connection type (VNet2VNet) is similar to creating a Site-to-Site IPsec connection to an on-premises location. Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE, and both function the same way when communicating.

The local network gateway for each VNet treats the other VNet as a local site. This lets you specify additional address space for the local network gateway in order to route traffic.

https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances
https://learn.microsoft.com/en-us/azure/dns/private-dns-autoregistration
https://learn.microsoft.com/en-us/azure/virtual-network/move-across-regions-publicip-powershell
https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/move-support-resources
https://learn.microsoft.com/en-us/azure/dns/private-dns-migration-guide
https://learn.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal


https://learn.microsoft.com/en-us/azure/import-export/storage-import-export-requirements
https://learn.microsoft.com/en-us/azure/storage/file-sync/file-sync-deployment-guide?tabs=azure-portal%2Cproactive-portal
https://learn.microsoft.com/en-us/azure/storage/file-sync/file-sync-planning
https://learn.microsoft.com/en-us/azure/storage/common/storage-redundancy
https://learn.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-certificates-point-to-site


Azure Import/Export service supports the following of storage accounts:
✑ Standard General Purpose v2 storage accounts (recommended for most scenarios)
✑ Blob Storage accounts
✑ General Purpose v1 storage accounts (both Classic or Azure Resource Manager deployments),
Azure Import/Export service supports the following storage types:
✑ Import supports Azure Blob storage and Azure File storage
✑ Export supports Azure Blob storage

Step 1: Install the Azure File Sync agent on Server1
The Azure File Sync agent is a downloadable package that enables Windows Server to be synced with an Azure file share
Step 2: Register Server1.
Register Windows Server with Storage Sync Service
Registering your Windows Server with a Storage Sync Service establishes a trust relationship between your server (or cluster) and the Storage Sync Service.
Step 3: Create a sync group and a cloud endpoint.
A sync group defines the sync topology for a set of files. Endpoints within a sync group are kept in sync with each other. A sync group must contain one cloud endpoint, which represents an Azure file share and one or more server endpoints. A server endpoint represents a path on registered server.
Reference:

Group1 already has a cloud endpoint named Share1.
A sync group must contain one cloud endpoint, which represents an Azure file share and one or more server endpoints.

Correct Answers:
Yes, one or more server endpoints can be added to the sync group.
Yes, one or more server endpoints can be added to the sync group.

If you add an Azure file share that has an existing set of files as a cloud endpoint to a sync group, the existing files are merged with any other files that are already on other endpoints in the sync group.

ZRS currently supports standard general-purpose v2, FileStorage and BlockBlobStorage storage account types.
Incorrect Answers:
storage1 and storage3: Live migration is supported only for storage accounts that use LRS replication. If your account uses GRS or RA-GRS, then you need to first change your account's replication type to LRS before proceeding. This intermediary step removes the secondary endpoint provided by GRS/RA-GRS.
Also, only standard storage account types support live migration. Premium storage accounts must be migrated manually.
storage4: ZRS currently supports standard general-purpose v2, FileStorage and BlockBlobStorage storage account types.

a PowerShell PS1 file: Modify the dataset.csv file in the root folder where the tool resides. Depending on whether you want to import a file or folder or both, add entries in the dataset.csv file
a driveset CSV file: Modify the driveset.csv file in the root folder where the tool resides

Azure Import/Export service is used to securely import large amounts of data to Azure Blob storage and Azure Files by shipping disk drives to an Azure datacenter.
The maximum size of an Azure Files Resource of a file share is 5 TB.
Note:
There are several versions of this question in the exam. The question has two correct answers:
1. Azure File Storage
2. Azure Blob Storage
The question can have other incorrect answer options, including the following:
✑ Azure Data Lake Store
✑ Azure SQL Database
✑ Azure Data Factory


AzCopy is a command-line utility that you can use to copy blobs or files to or from a storage account.
Incorrect Answers:
blob, file, table, and queue, file and table only and blob, table, and queue only: AzCopy does not support table and queue storage services.
file only: AzCopy supports file storage services, as well as blob storage services.


Contoso is moving the existing product blueprint files to Azure Blob storage.
Use unmanaged standard storage for the hard disks of the virtual machines. We use Page Blobs for these.

https://learn.microsoft.com/en-us/azure/import-export/storage-import-export-data-to-files?tabs=azure-portal-preview
https://learn.microsoft.com/en-us/azure/import-export/storage-import-export-service
https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10
https://learn.microsoft.com/en-us/azure/storage/file-sync/file-sync-deployment-guide?tabs=azure-portal%2Cproactive-portal#create-a-sync-group-and-a-%20cloud-endpoint
https://learn.microsoft.com/en-us/azure/storage/blobs/lifecycle-management-overview?tabs=azure-portal


Correct Answers:
- A Basic Load Balancer supports virtual machines in a single availability set or virtual machine scale set.



- When using load-balancing rules with Azure Load Balancer, you need to specify health probes to allow Load Balancer to detect the backend endpoint status. The configuration of the health probe and probe responses determine which backend pool instances will receive new flows. You can use health probes to detect the failure of an application on a backend endpoint. You can also generate a custom response to a health probe and use the health probe for flow control to manage load or planned downtime. When a health probe fails, Load Balancer will stop sending new flows to the respective unhealthy instance. Outbound connectivity is not impacted, only inbound connectivity is impacted.

If you use Azure Provided DNS then appropriate DNS suffix will be automatically applied to your virtual machines. For all other options you must either use Fully

Qualified Domain Names (FQDN) or manually apply appropriate DNS suffix to your virtual machines.


Recovery Services vault
Is there any limit on the number of vaults that can be created in each Azure subscription?
Yes. You can create up to 500 Recovery Services vaults, per supported region of Azure Backup, per subscription. If you need additional vaults, create an additional subscription.

Are there limits on the number of servers/machines that can be registered against each vault?
You can register up to 1000 Azure Virtual machines per vault. If you're using the Microsoft Azure Backup Agent, you can register up to 50 MARS agents per vault. And you can register 50 MABS servers/DPM servers to a vault.

How many datasources/items can be protected in a vault?
You can protect up to 2000 datasources/items across all workloads (such as IaaS VM, SQL, AFS) in a vault. For example, if you've already protected 500 VMs and 400 Azure Files shares in the vault, you can only protect up to 1100 SQL databases in it.

How many policies can I create per vault?
You can only have up to 200 policies per vault. However, adding new backup policies or editing current policies through Azure Resource Manager (ARM) templates or Azure automation clients such as PowerShell, CLI is limited to 50 over a span of 24 hours.

If my organization has one vault, how can I isolate data from different servers in the vault when restoring data?
Server data that you want to recover together should use the same passphrase when you set up backup. If you want to isolate recovery to a specific server or servers, use a passphrase for that server or servers only. For example, human resources servers could use one encryption passphrase, accounting servers another, and storage servers a third.

Can I move my vault between subscriptions?
Yes. To move a Recovery Services vault, refer this article

Can I move backup data to another vault?
No. Backup data stored in a vault can't be moved to a different vault.

Can I change the storage redundancy setting after a backup?
The storage replication type by default is set to geo-redundant storage (GRS). Once you configure the backup, the option to modify is disabled and can't be changed.

Storage replication type

If you've already configured the backup and must move from GRS to LRS, then see How to change from GRS to LRS after configuring backup.

Can I do an Item Level Restore (ILR) for VMs backed up to a Recovery Services vault?
ILR is supported for Azure VMs backed up by Azure VM backup. For more information, see article
ILR isn't supported for online recovery points of on-premises VMs backed up by Azure Backup Server (MABS) or System Center DPM.
How can I move data from the Recovery Services vault to on-premises?
To move backup data out of Recovery Services Vault, you need to restore the necessary data. If your vault contains backup of on-premises data, use the corresponding agent (MARS, MABS, or DPM) to restore to on-premises.

We do not support exporting data directly from the Recovery Services vault to on-premises storage for backup of cloud workload (Azure VMs, SQL, and SAP HANA in Azure VMs). However, you can restore these to the corresponding cloud resources in Azure Storage Accounts, and then move the data to on-premises. You can also export this data to on-premises via Data Box or Import/Export.

What is the difference between a geo-redundant storage (GRS) vault with and without the Cross-Region Restore (CRR) capability enabled?
In the case of a GRS vault without CRR capability enabled, the data in the secondary region can't be accessed until Azure declares a disaster in the primary region. In such a scenario, the restore happens from the secondary region. When CRR is enabled, even if the primary region is up and running, you can trigger a restore in the secondary region.

Can I move a subscription that contains a vault to a different Azure Active Directory?
Yes. To move a subscription (that contains a vault) to a different Azure Active Directory (AD), see Transfer subscription to a different directory.

 Important

Ensure that you perform the following actions after moving the subscription:

Role-based access control permissions and custom roles are not transferrable. You must recreate the permissions and roles in the new Azure AD.
You must recreate the Managed Identity (MI) of the vault by disabling and enabling it again. Also, you must evaluate and recreate the MI permissions.
If the vault uses features which leverage MI, such as Private Endpoints and Customer Managed Keys, you must reconfigure the features.
Can I move a subscription that contains a Recovery Services Vault to a different tenant?
Yes. Ensure that you do the following:

 Important

Ensure that you perform the following actions after moving the subscription:

If the vault uses CMK (customer managed keys), you must update the vault. This enables the vault to recreate and reconfigure the vault managed identity and CMK (which will reside in the new tenant), otherwise the backups/restore operation will fail.
You must reconfigure the RBAC permissions in the subscription as the existing permissions can’t be moved.
Azure Backup agent
Where can I find common questions about the Azure Backup agent for Azure VM backup?
For the agent running on Azure VMs, read this FAQ.
For the agent used to back up Azure file folders, read this FAQ.
General backup
Are there limits on backup scheduling?
Yes.

You can back up Windows Server or Windows machines up to three times a day. You can set the scheduling policy to daily or weekly schedules.
You can back up DPM up to twice a day. You can set the scheduling policy to daily, weekly, monthly, and yearly.
You back up Azure VMs once a day.
What operating systems are supported for backup?
Azure Backup supports these operating systems for backing up files and folders, and apps protected by Azure Backup Server and DPM.

OS	SKU	Details
Workstation		
Windows 10 64 bit	Enterprise, Pro, Home	Machines should be running the latest services packs and updates.
Windows 8.1 64 bit	Enterprise, Pro	Machines should be running the latest services packs and updates.
Windows 8 64 bit	Enterprise, Pro	Machines should be running the latest services packs and updates.
Windows 7 64 bit	Ultimate, Enterprise, Professional, Home Premium, Home Basic, Starter	Machines should be running the latest services packs and updates.
Server		
Windows Server 2022 64 bit	Standard, Datacenter, Essentials, IoT	With the latest service packs/updates.
Windows Server 2019 64 bit	Standard, Datacenter, Essentials, IoT	With the latest service packs/updates.
Windows Server 2016 64 bit	Standard, Datacenter, Essentials	With the latest service packs/updates.
Windows Server 2012 R2 64 bit	Standard, Datacenter, Foundation	With the latest service packs/updates.
Windows Server 2012 64 bit	Datacenter, Foundation, Standard	With the latest service packs/updates.
Windows Storage Server 2016 64 bit	Standard, Workgroup	With the latest service packs/updates.
Windows Storage Server 2012 R2 64 bit	Standard, Workgroup, Essential	With the latest service packs/updates.
Windows Storage Server 2012 64 bit	Standard, Workgroup	With the latest service packs/updates.
Windows Server 2008 R2 SP1 64 bit	Standard, Enterprise, Datacenter, Foundation	With the latest updates.
Windows Server 2008 64 bit	Standard, Enterprise, Datacenter	With latest updates.
Azure Backup doesn't support 32-bit operating systems.

For Azure VM Linux backups, Azure Backup supports the list of distributions endorsed by Azure, except Core OS Linux and 32-bit operating system. Other bring-your-own Linux distributions might work as long as the VM agent is available on the VM, and support for Python exists.

Are there size limits for data backup?
Sizes limits are as follows:

OS/machine	Size limit of data source
Windows 8 or later	54,400 GB
Windows 7	1700 GB
Windows Server 2012 or later	54,400 GB
Windows Server 2008, Windows Server 2008 R2	1700 GB
Azure VM	See the support matrix for Azure VM backup
How is the data source size determined?
The following table explains how each data source size is determined.

Data source	Details
Volume	The amount of data being backed up from single volume VM being backed up.
SQL Server database	Size of single database size being backed up.
SharePoint	Sum of the content and configuration databases within a SharePoint farm being backed up.
Exchange	Sum of all Exchange databases in an Exchange server being backed up.
BMR/System state	Each individual copy of BMR or system state of the machine being backed up.
Is there a limit on the amount of data backed up using a Recovery Services vault?
There's no limit on the total amount of data you can back up using a Recovery Services vault. The individual data sources (other than Azure VMs), can be a maximum of 54,400 GB in size. For more information about limits, see the vault limits section in the support matrix.

Why is the size of the data transferred to the Recovery Services vault smaller than the data selected for backup?
Data backed up from Azure Backup Agent, DPM, and Azure Backup Server is compressed and encrypted before being transferred. With compression and encryption is applied, the data in the vault is 30-40% smaller.

Can I view the expiration time for the recovery points?
No, you can't view the expiration time for the scheduled backups. However, you can view the expiration time for the on-demand backups through backup jobs.

Can I delete individual files from a recovery point in the vault?
No, Azure Backup doesn't support deleting or purging individual items from stored backups.

If I cancel a backup job after it starts, is the transferred backup data deleted?
No. All data that was transferred into the vault before the backup job was canceled remains in the vault.

Azure Backup uses a checkpoint mechanism to occasionally add checkpoints to the backup data during the backup.
Because there are checkpoints in the backup data, the next backup process can validate the integrity of the files.
The next backup job will be incremental to the data previously backed up. Incremental backups only transfer new or changed data, which equates to better utilization of bandwidth.
If you cancel a backup job for an Azure VM, any transferred data is ignored. The next backup job transfers incremental data from the last successful backup job.

Can backup items in a vault be deleted if its Resource Group has a delete lock?
No, backup items in a vault cannot be deleted if the corresponding Resource Group has a delete lock.

Retention and recovery
Are the retention policies for DPM and Windows machines without DPM the same?
Yes, they both have daily, weekly, monthly, and yearly retention policies.

Can I customize retention policies?
Yes, you have customize policies. For example, you can configure weekly and daily retention requirements, but not yearly and monthly.

Can I use different times for backup scheduling and retention policies?
No. Retention policies can only be applied on backup points. For example, this image shows a retention policy for backups taken at 12am and 6pm.

Schedule Backup and Retention

If a backup is kept for a long time, does it take more time to recover an older data point?
No. The time to recover the oldest or the newest point is the same. Each recovery point behaves like a full point.

If each recovery point is like a full point, does it impact the total billable backup storage?
Typical long-term retention point products store backup data as full points.

The full points are storage inefficient but are easier and faster to restore.
Incremental copies are storage efficient but require you to restore a chain of data, which impacts your recovery time
Azure Backup storage architecture gives you the best of both worlds by optimally storing data for fast restores and incurring low storage costs. This ensures that your ingress and egress bandwidth is used efficiently. The amount of data storage, and the time needed to recover the data, is kept to a minimum. Learn more about incremental backups.

Is there a limit on the number of recovery points that can be created?
You can create up to 9999 recovery points per protected instance. A protected instance is a computer, server (physical or virtual), or workload that backs up to Azure.

Learn more about backup and retention.
How many times can I recover data that's backed up to Azure?
There's no limit on the number of recoveries from Azure Backup.

When restoring data, do I pay for the egress traffic from Azure?
No. Recovery is free and you aren't charged for the egress traffic.

What happens when I change my backup policy?
When a new policy is applied, schedule and retention of the new policy is followed.

If retention is extended, existing recovery points are marked to keep them according to new policy.
If retention is reduced, they are marked for pruning in the next cleanup job and subsequently deleted.
How long is data retained when stopping backups, but selecting the option to retain backup data?
When backups are stopped and the data is retained, existing policy rules for data pruning will cease and data will be retained indefinitely until initiated by the administrator for deletion.

Encryption
Is the data sent to Azure encrypted?
Yes. Data is encrypted on the on-premises machine using AES256. The data is sent over a secure HTTPS link. The data transmitted in cloud is protected by HTTPS link only between storage and recovery service. iSCSI protocol secures the data transmitted between recovery service and user machine. Secure tunneling is used to protect the iSCSI channel.

Is the backup data on Azure encrypted as well?
Yes. The data in Azure is encrypted-at-rest.

For on-premises backup, encryption-at-rest is provided using the passphrase you provide when backing up to Azure.
For Azure VMs, data is encrypted-at-rest using Storage Service Encryption (SSE).
Microsoft doesn't decrypt the backup data at any point.

What is the minimum length of the encryption key used to encrypt backup data?
The encryption key used by the Microsoft Azure Recovery Services (MARS) Agent is derived from a passphrase that should be at least 16 characters long. For Azure VMs, there's no limit to the length of keys used by Azure KeyVault.

What happens if I misplace the encryption key? Can I recover the data? Can Microsoft recover the data?
The key used to encrypt the backup data is present only on your site. Microsoft doesn't maintain a copy in Azure and doesn't have any access to the key. If you misplace the key, Microsoft can't recover the backup data.




 

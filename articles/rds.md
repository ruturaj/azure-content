Introduction
============

Remote Desktop Services (RDS) provides virtualized desktop and
application deployments to any device, improving productivity and
employee morale while helping to keep critical data secure and
compliant. RDS enables virtual desktops and applications using client
VM’s (VDI) as well as server based sessions.

Azure Site Recovery Service (ASR) is a service from Azure that helps you
protect important applications by coordinating their configuration,
replication and recovery using a remote site. Environments can be
protected by automating the replication of the virtual machines based on
policies that you set and control. Site Recovery then coordinates and
manages the ongoing replication of data by integrating with existing
technologies such as Hyper-V Replica, System Center, and SQL Server
AlwaysOn.

Azure Site Recovery also integrates with SAN replication options from
storage vendors such as NetApp, HP, and EMC to help further simplify and
improve your disaster recovery protection.

RDS run the desktops and apps that employees require for their job.
Protecting RDS is important to keep the business up and running after a
disaster. Azure Site Recovery can be used to protect Remote Desktop
Services with its On-Click Orchestration to recover workloads into a
remote Hyper-V Site or Azure virtual machines.

Overview of Remote Desktop Services and Azure Site Recovery Manager
===================================================================

This section defines the components of an RDS deployment that needs to
be protected. The section also provides an overview of the ASR features
that can be used to automate the recovery of RDS workloads.

Remote Desktop Topology and components
--------------------------------------

![](media/image1.png)

Remote Desktop services has six roles and are explained in detail in the
following table:

  **Role service name**    **Role service description**
  ------------------------ ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  RD Virtualization Host   Remote Desktop Virtualization Host (RD Virtualization Host) integrates with Hyper-V to host client virtual machine based RemoteApp programs or full client desktops.
  RD Session Host          Remote Desktop Session Host (RD Session Host) enables a server to host session based RemoteApp programs or session-based desktops to provide a Windows virtual machine for each user within your organization.
  RD Connection Broker     Remote Desktop Connection Broker (RD Connection Broker) performs the initial authentication and starts the required session or VM based resource. It performs load balancing between hosts and ensures that a connection goes to the current running instance if a reconnect.
  RD Web Access            Remote Desktop Web Access (RD Web Access) provides a website and web feed that allows users to access RemoteApp and desktop connection through the **Start** menu, and other mechanisms on a computer that is running Windows 8, Windows 7.RD Web Access can provide a customized view of RemoteApp programs, session-based desktops, and virtual desktops available to each user.
  RD Licensing             Remote Desktop Licensing (RD Licensing) manages the licenses required to connect using RDS. You can use RD Licensing to install, issue, and track the availability of licenses.
  RD Gateway               Remote Desktop Gateway (RD Gateway) enables authorized users to connect to virtual desktops, RemoteApp programs, and session-based desktops on an internal corporate network from any Internet-connected device.

### Remote Desktop Services Collections Types

Remote Desktop services can provide either a virtual desktop based
service or a session based service depending on the type of collection.
Collection is a logical grouping of Remote Desktop Servers that provides
either session-based or virtual machine-based (VDI) deployments.

-   **Virtual Desktop Infrastructure (VDI)**. An individual virtual
    machine running a desktop operating system (OS). Although there can
    be multiple virtual machines per a given underlying physical server,
    there is only one user at a time logged on to a given virtual
    machine. Each user can be assigned their own virtual machine or
    given a free virtual machine from a pool of virtual machines.

-   **Session-Based Desktop**. An user session running on a server OS
    with the RD Session Host role service installed. The RD Session Host
    server can run on either a virtual machine or a physical server.
    There can be multiple user sessions per virtual/physical machine,
    and each virtual/physical machine is shared by multiple users.

Under VDI, the virtual machines can be provisioned in either of the
below configurations

-   **Pooled Desktops**. In this deployment, the virtual machines are
    created from a template and provisioned on-demand when the user
    connects. The state of the virtual machine is rolled back after the
    user disconnects. The users data can be persisted by using User
    Profile Disks that are placed remotely on a share. The desktop is
    assigned to the user from the pooled collection at random when the
    user connects. These are often referred to as non-persistent
    desktops

-   **Personal Desktops**. In this VDI deployment model, each user is
    assigned a personal virtual machine. Each time the user logs in he
    is connected to the same machine and the state of the machine is
    persisted. These are often referred to as persistent desktops.

The pooled and personal desktops, in turn can be either managed or
unmanaged. The lifecycle of a managed desktop is controlled by the
Remote Desktop Management service. It can be configured to conteol
provisioning and rollbacks. In unmanaged deployments, the desktops can
be created using either System Center VMM or other virtual machine
management software.

Below is a schematic to explain the different deployments.

![](media/image2.png)

### Highly available deployments

The different components of RDS can be deployed as single instances or
as farms to allow higher availability and scalability. Below is the
different ways each component can be deployed as HA.

  **Component**              **Simple Single Role Deployment**             **Scaled Deployment **
  -------------------------- --------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Web Access**             Web Access instances                          Web access farm using load balancer
  **Gateway Server**         Single Gateway instance                       Load balanced using a load balancer that supports client affinity
  **License Server**         RD License instance                           Use Windows host clustering or licenses split across multiple license servers
  **Connection Broker**      Data stored in local Windows database store   Multiple brokers configured to store data in SQL server. SQL implemented in Always-on Availability group. SQL servers configured with write permission to all RD connection broker
  **Session Host**           RD session host server instance               A farm of session host servers in the same collection (either physical machines or virtual machines). Individual VMs can be HA using Hyper-V host clusters.
  **SQL Server**             Standard SQL server deployments               SQL is highly available Always-on Availability groups.
  **Virtualization Hosts**   Standalone RDVH server                        RDVH servers in Hyper-V host clusters

Azure Site Recovery Features used to protect RDS Deployments
------------------------------------------------------------

Azure Site Recovery services has a collection of features that help
address many important issues in orchestrating the recovery of an RDS
deployment. It leverages System Center Virtual Machine Manager (SCVMM)
to configure and manage protection at scale for large RDS deployments.
The features that makes ASR the ideal choice to protect RDS deployments
are:

-   **Simple automated protection –** With cloud configuration at scale,
    you can protect workloads application agnostically. That allows you
    to protect applications running on SAN, remote storage and also
    running on complicated networking topologies.

-   **Replication to remote hyper-v site and Recovery to Cloud –**
    Asynchronous replication to a remote site or to Azure at a
    replication frequency of 30sec, 5mins or 15mins gives your
    application the control to replicate at its churn requirements.
    Crash consistent and App consistent recovery points help your
    recover to the right point in time.

-   **Continuous health monitoring –** ASR monitors the health of your
    workloads’ replication and can alert you if the workloads are not
    protected.

-   **Orchestrated Recovery plan –** Recovery plans give ability to
    recover your workload in an ordered manner. You can specify the boot
    order and also specify different scripts to automate

Some of the salient features that we will use in recovering RDS are

-   Protection and configuration at scale for large Session Host farms
    and personal desktops by using Cloud Protection at scale.

-   Continuous monitoring of replication via Azure Site Recovery portal.

-   Recovery plans to orchestrate the recovery in a specific order so
    that the dependency of the various roles are captured.

-   Scripting support to allow one click recovery of RDS deployment in a
    remote site.

RDS Protection and Recovery Solution Brief
------------------------------------------

In case of a disaster that impacts an RDS Deployment, there needs to be
a way to quickly recover the components to a secondary site so that the
enterprise workforce can continue to work. Each component of RDS can
also be deployed as HA or as a farm to allow load balancing.

There is also a tight dependency between the different roles and the
broker and also Active Directory. The broker contains information about
the different mapping from an end user to the collection instance. A
gold VM template also needs to be protected and replicated to ensure
that the latest Gold VM is available on the secondary site. Handling the
scale out after new servers are added and new remote applications are
published is also challenging.

ASR can recover the RDS deployments using the recovery plans and extends
them with scripts to enable one-click recovery. It can recover the
session hosts and the personal desktops and ensure that the user
mappings are handled. For pooled desktops, it saves cost of protection
by ensuring that the gold VM template is replicated and the pooled
desktops are created in an automated fashion.

ASR Supported topologies of RDS Deployments
-------------------------------------------

Following is the ASR support for the different RDS deployments that we
discuss in the document.

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **RD Service deployment type**                                             **On-premises to On-premises**   **On-premises to Azure**   **Data replication**
  -------------------------------------------------------------------------- -------------------------------- -------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Personal Virtual Desktop**                                               Yes                              No                         Replicate VMs using Hyper-V replica/SAN
                                                                                                                                         
  **(unmanaged)**                                                                                                                        

  **Pooled Virtual Desktop**                                                 Yes                              No                         Replicate Broker VMs and template using Hyper-V replica and recreate pooled VMs on the fly on recovery. Not supported for Remote Applications published via Pooled VMs
                                                                                                                                         
  **(managed and without User Profile Disk)**                                                                                            

  **Remote applications and Desktop Sessions (without User Profile Disk)**   Yes                              Yes                        Replicate SH VMs using Hyper-V replica/SAN and shared data on file system using DFSR
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Azure Site Recovery planning for RDS
====================================

We will look at the different considerations you need to review when you
use ASR for RDS. The top considerations are:

1.  [Setup recovery site](#_Setup_recovery_site)

2.  [Replication frequency on each role](#_Replication_frequency_on)

3.  Understand RDS role dependency

4.  [Plan for recovery plan scripts](#_Plan_for_Recovery)

We will look at each point one by one to ensure you have the necessary
pre-requisites completed

<span id="_Setup_recovery_site" class="anchor"><span id="_Toc411622378" class="anchor"></span></span>Setup recovery site
------------------------------------------------------------------------------------------------------------------------

1.  Ensure that the recovery site is setup to protect the RDS virtual
    machines. The secondary site can be managed by the same VMM or a
    secondary VMM server.

2.  Ensure that the required capacity exists on the secondary site so
    that the RDS workload can be recovered.

3.  Ensure that the Virtualization host candidates on the secondary site
    has the RD-VH role installed.

<span id="_Replication_frequency_on" class="anchor"><span id="_Toc411622379" class="anchor"></span></span>Replication frequency on each role
--------------------------------------------------------------------------------------------------------------------------------------------

For the following roles you can use the following replication frequency.

The Gateway and the Webaccess roles are least updated and can be
replicated at a lower frequency.

The Session host servers need to be replicated as fast as the data might
written to the disk. In case the Session hosts are using User Profile
Disks then the session host can be replicated at 15mins.

The Connection Broker needs to be replicated as fast as possible to
ensure that the connection assignments are not dropped off.

The license server can be replicated at a lower frequency since the
licenses can be released and reattached on the secondary site.

<span id="_Understand_RDS_role" class="anchor"><span id="_Toc411622380" class="anchor"></span></span>Understand RDS role dependency
-----------------------------------------------------------------------------------------------------------------------------------

Dependency between the different roles needs to be identified so that
the VMs can be placed in the right groups in a recovery plan. The
dependency model ensures that all the required roles come up running so
that all the roles that are dependent on them can start consuming them
when they are running.

Different Deployments have different dependency models and are listed
below. In the below listing - \#1 should happen before \#2.

  ----------------------------------------------------------------------------------------------------------------------------
  **RD Service deployment type**                               **Dependency model**
  ------------------------------------------------------------ ---------------------------------------------------------------
  **Personal Virtual Desktop**                                 All Virtualization hosts are ready with RD-VH role installed.
                                                               
  **(unmanaged)**                                              Connection Broker
                                                               
                                                               Personal Desktops
                                                               
                                                               Gold Template VM
                                                               
                                                               Webaccess, License Server and Gateway server

  **Pooled Virtual Desktop**                                   All Virtualization hosts are ready with RD-VH role installed.
                                                               
  **(managed and without UPD)**                                Connection Broker
                                                               
                                                               Gold Template VM
                                                               
                                                               Webaccess, License Server and Gateway server

  **Remote applications and Desktop Sessions (without UPD)**   Session Hosts
                                                               
                                                               Connection Broker
                                                               
                                                               Webaccess, License Server and Gateway server
  ----------------------------------------------------------------------------------------------------------------------------

<span id="_Plan_for_Recovery" class="anchor"><span id="_Toc411622381" class="anchor"></span></span>Plan for Recovery plan scripts
---------------------------------------------------------------------------------------------------------------------------------

To automate the recovery we can run recovery plan scripts so that the
plan is automated as much as possible. In some cases scripts might not
be available and there are manual actions that user will need to do to
ensure that the recovery is successful. An ASR recovery plan gives the
capability to run powershell scripts on the VMM server. Below are a few
things to take care of before using the scripts.

### Specify VMM Library share

By default the local share of an SCVMM server is used to place the
scripts. The location of the default share is
[\\\\SCVMMSERVERFQDN\\MSCVMMLibrary\\](file:///\\SCVMMSERVERFQDN\MSCVMMLibrary\)

You can create an additional folder inside this share to store the
scripts. For example the DR scripts for RDS can be stored at

[\\\\SCVMMSERVERFQDN\\MSCVMMLibrary\\DRScripts\\RDS\\](file:///\\SCVMMSERVERFQDN\MSCVMMLibrary\DRScripts\RDS\)

In this case the script path as specified on the portal will be
\\DRScripts\\RDS\\Script.ps1 for a powershell script Script.ps1.

In case the VMM Library share is not on the SCVMM Server (example in the
case of a HA VMM) then you can specify the path to the share in the
registry key of the DRA. Follow the below steps to set
[\\\\libserver2.contoso.com\\share](file:///\\libserver2.contoso.com\share)
as the VMM Library share for the ASR Scripts.

1.  Open the Registry Editor.

2.  Navigate to **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Microsoft
    System Center Virtual Machine Manager
    Server\\DRAdapter\\Registration**

3.  Edit the value **ScriptLibraryPath**

4.  Place the value as **\\\\libserver2.contoso.com\\share\\**. Specify
    the full fully qualified domain name (FQDN)

5.  Provide permissions to the share location.

The script path as specified on the ASR Portal remains the relative path
\\DRScripts\\RDS\\Scripts.ps1

Ensure that the script is found in the VMM Library shares.

In case the scripts are not signed, you can set the execution policy to
bypass for the VMM server.

### Enable CredSSP on servers

To login to the Connection broker – today you need to ensure that
CredSSP is enabled on the servers.

On the Connection Broker run the following command to set it as a server

PS C:\\\> enable-wsmancredssp -role server

On the VMM server run the following command to set it as a client

PS C:\\\> enable-wsmancredssp -role client -delegatecomputer
broker.contoso.com

### Logon user to broker

To allow the script to logon to the broker as an administrator you need
to follow one of the two steps

1.  Ensure that VMM Server Service account is an Administrator on the
    Connection Broker machine

Or

1.  Ensure that you use the following script to logon to the remote by
    using a PS Session and run scripts in it.

> We will be writing all scripts with the assumption that the VMM
> Service account is not the administrator on the Broker.
>
> Note that this might cause the Password to be in plain string.

  ----------------------------------------------------------------------------------------------------------------
  \$pw = convertto-securestring -AsPlainText -Force -String Password

  \$cred = new-object -typename System.Management.Automation.PSCredential -argumentlist "fareast\\username",\$pw

  \$session = new-pssession -computername broker.contoso.com -credential \$cred -Authentication CredSSP

  invoke-command -session \$session -ScriptBlock {Command to Run}
  ----------------------------------------------------------------------------------------------------------------
  ----------------------------------------------------------------------------------------------------------------

Protection steps for the Session Based Deployment
=================================================

To recover a typical session host deployment you need to protect all the
roles and replicate them to the secondary site. When the recovery plan
executes and all the VMs are recovered on the secondary site, the
application will reestablish all the connections and continue to work.

Note that in this case the broker is also replicated as is. The state of
the broker does not change except its IP address (which can also be the
same if using NVGRE or if mapped to the same IP address pool). The
Session assignments are available with the broker and the end user
connections to the broker will continue to be established after
failover.

Let us look at a typical deployment with Session Based deployment and
see how to recover it. The following deployment is the one we have tried
out and confirmed that it worked well.

  RDS Role                   Protection to Remote Site   Protection to Azure
  -------------------------- --------------------------- ---------------------
  Connection Broker          Replica/SAN                 Replica
  Session Host server        Replica/SAN                 Replica
  Web Access                 Replica/SAN                 Replica
  License Server + Gateway   Replica/SAN                 Replica

After referencing the dependency model as seen in Section Understand RDS
role dependency you can create a recovery plan as given below.

![](media/image3.png)

Exactly same technique and recovery plan can be used to recover the RDS
into Azure.

Considerations for recovering RDSH to Azure
-------------------------------------------

\<TODO\>

Protection steps for Pooled Desktops
====================================

The strategy to recover the pooled desktops is as follows

1.  Protect Broker, Web Access, Gateway, License servers using
    replica/SAN

2.  Protect the VM that will be used as a template for the Pooled VMs

3.  During recovery, get all the roles protected to the recovery site

    a.  Add new Virtualization hosts to the Broker

    b.  Delete all existing pooled VMs from the collection

    c.  Assign the new template image to the collection

    d.  Re-create the pooled VMs

Below is the recovery plan we used in the experimental deployment.

![](media/image4.png)

The scripts in each section are as below

  ----------------------------------------------------------------------------------------------------------------------------
  Group 1 Manual Action – Update DNS
  ----------------------------------------------------------------------------------------------------------------------------
  Run powershell on elevated mode on the Broker

  run the command

  \> ipconfig /registerdns

  Wait for a couple of minutes to ensure the DNS has been updated with new value.

  Note - this step is not required if you have retained IP address using NVGRE or mapping to the same IP address Pool

  This action may not be necessary in case the IP address of the broker does not change.

  You will need to wait for a few minutes before the DNS propagates hence this is a manual action. It can also be automated.
  ----------------------------------------------------------------------------------------------------------------------------

  ----------------------------------------------------------------------------------------------------
  Group 1 Script – Add Virtualization Hosts
  ----------------------------------------------------------------------------------------------------
  Modify the script to run it for each Virtualization host in the Cloud.

  Here broker is the broker.contoso.com

  Virtualization host is VH1.contoso.com

  ipmo RemoteDesktop;

  add-rdserver –ConnectionBroker broker.contoso.com –Role RDS-VIRTUALIZATION –Server VH1.contoso.com

  Typically after adding a virtualization host to a broker, the host needs a reboot.

  Ensure that the Hosts does not have a reboot pending else this step will fail.
  ----------------------------------------------------------------------------------------------------

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Group 2 Script – Turn Off Template VM
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  The Template VM when recovered to the secondary site will boot up. However it is a syspreped VM and cannot boot up. Also RDS will require it in a shutdown state to create a Pooled VM configuration from it. So we need to turn it off.

  ipmo virtualmachinemanager;

  Foreach(\$vm in \$VMsAsTemplate)

  {

  Get-SCVirtualMachine -ID \$vm | Stop-SCVirtualMachine –Force

  }

  In case of single VMM server, the template VM name will be the same as on Primary or secondary. Hence use the VM ID as specified by the Context variable in the script.

  If there are multiple templates then you can turn them all off.
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Group 2 Script – remove Existing Pooled VMs
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  The pooled VMs on the primary site need to be removed from the Broker so that new VMs can be created on the secondary site. Note that in this case, you need to specify the exact host on which the Pooled VM will be created. You can write mote advanced script to equally distribute the VMs on the host or

  ipmo RemoteDesktop

  \$desktops = Get-RDVirtualDesktop -CollectionName Win8Desktops;

  Foreach(\$vm in \$desktops){

  Remove-RDVirtualDesktopFromCollection -CollectionName Win8Desktops -VirtualDesktopName \$vm.VirtualDesktopName –Force

  }

  Note that this will delete the VMs from the collection only.
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Group 2 Manual Action – Assign new template
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  You need to assign the new template to the Broker for that collection so that you can create new Pooled VMs on the recovery site.

  Go to the RDS Broker and Identify the collection

  Select to edit the properties and specify a new VM Image as its template

  This can also be automated by the below script by understanding the template VM name and Host name and assigning it to the Broker as below.

  \$VMsAsTemplate = \$context.vmIDList -split ","

  \$vm = \$VMsAsTemplate[0]

  ipmo virtualmachinemanager; \$Template = Get-SCVirtualMachine -ID \$vm;

  Next connect to the Broker and assign the image (here Win8Desktops in the collection name.

  ipmo RemoteDesktop;

  Update-RDVirtualDesktopCollection -CollectionName "Win8Desktops" -VirtualDesktopTemplateHostServer \$Template.HostName -VirtualDesktopTemplateName \$Template.name -confirm;
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Group 2 Script – Re-create all pooled VMs
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  The pooled VMs on the recovery site need to be recreated via the Broker. Note that in this case, you need to specify the exact host on which the Pooled VM will be created. You can write mote advanced script to equally distribute the VMs on the host.

  ipmo RemoteDesktop;

  Add-RDVirtualDesktopToCollection -CollectionName Win8Desktops

  -VirtualDesktopAllocation @{"RDVH1.contoso.com" = 1}

  Note that the Pooled VM name will need to be unique by using the Prefix and Suffix. In case the VM name already exists, this will fail. Also if the primary side VMs were numbered from 1-5, the recovery site numbering will continue from 6 and above.
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Next the Web Access and the Gateway server will come up to allow users
to access the collection once again.

Protection steps for Personal Desktops
======================================

We support Personal Desktops that are unmanaged.

The strategy to recover the pooled desktops is as follows

1.  Protect Broker, Web Access, Gateway, License servers using
    replica/SAN

2.  Protect the VM that will be used as a template for the Personal
    VMs[^1]

3.  During recovery, get all the roles protected to the recovery site

    a.  Add new Virtualization hosts to the Broker

    b.  Un-manage/remove all Personal VMs from the collection

    c.  Assign the new template image to the collection

    d.  Add the Personal VMs back to the collection

Below is the recovery plan we used in the experimental deployment.

![](media/image5.png)

The scripts in each section are as below

  ----------------------------------------------------------------------------------------------------------------------------
  Group 1 Manual Action – Update DNS
  ----------------------------------------------------------------------------------------------------------------------------
  Run powershell on elevated mode on the Broker

  run the command

  \> ipconfig /registerdns

  Wait for a couple of minutes to ensure the DNS has been updated with new value.

  Note - this step is not required if you have retained IP address using NVGRE or mapping to the same IP address Pool

  This action may not be necessary in case the IP address of the broker does not change.

  You will need to wait for a few minutes before the DNS propagates hence this is a manual action. It can also be automated.
  ----------------------------------------------------------------------------------------------------------------------------

  ----------------------------------------------------------------------------------------------------
  Group 1 Script – Add Virtualization Hosts
  ----------------------------------------------------------------------------------------------------
  Modify the script to run it for each Virtualization host in the Cloud.

  Here broker is the broker.contoso.com

  Virtualization host is VH1.contoso.com

  ipmo RemoteDesktop;

  add-rdserver –ConnectionBroker broker.contoso.com –Role RDS-VIRTUALIZATION –Server VH1.contoso.com

  Typically after adding a virtualization host to a broker, the host needs a reboot.

  Ensure that the Hosts does not have a reboot pending else this step will fail.
  ----------------------------------------------------------------------------------------------------

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Group 2 Script – Turn Off Template VM
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  The Template VM when recovered to the secondary site will boot up. However it is a syspreped VM and cannot boot up. Also RDS will require it in a shutdown state to create a Pooled VM configuration from it. So we need to turn it off.

  ipmo virtualmachinemanager;

  Foreach(\$vm in \$VMsAsTemplate)

  {

  Get-SCVirtualMachine -ID \$vm | Stop-SCVirtualMachine –Force

  }

  In case of single VMM server, the template VM name will be the same as on Primary or secondary. Hence use the VM ID as specified by the Context variable in the script.

  If there are multiple templates then you can turn them all off.
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Group 3 Script – Remove Existing Personal VMs from the collection and Re-Add them
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  The personal VMs on the primary site need to be removed from the Broker so that new VMs can be created on the secondary site. Note that in this case, you need to extract the VMs assignments. Next you re-add the virtual machines to the broker with the hash of assignments

  ipmo RemoteDesktop

  \$desktops = Get-RDVirtualDesktop -CollectionName CEODesktops;

  Export-RDPersonalVirtualDesktopAssignment -CollectionName CEODesktops -Path ./Desktopallocations.txt -ConnectionBroker broker.contoso.com

  Foreach(\$vm in \$desktops){

  Remove-RDVirtualDesktopFromCollection -CollectionName CEODesktops -VirtualDesktopName \$vm.VirtualDesktopName –Force

  }

  Import-RDPersonalVirtualDesktopAssignment -CollectionName CEODesktops -Path ./Desktopallocations.txt -ConnectionBroker broker.contoso.com

  Note that this will only remove the Personal VMs from the collection and re-add them. New VMs will not be created. The personal desktop allocation will be exported and imported back into the collection.
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Next the Web Access and the Gateway server will come up to allow users
to access the collection once again.

Summary
=======

We saw how to protect the different deployment topologies of RDS using
Azure Site Recovery services. ASR provides at scale protection,
continuous monitoring and one-click recovery of your RDS Environments.

Some of the specific cases such as User Profile Disks and HA Broker has
not been tested in our deployments but are easy to extend will be
addressed in the next iteration of validation

[^1]: This is to ensure that the VM template is also available on the
    secondary site.

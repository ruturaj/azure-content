Setup

-   The selected certificate cannot be validated. Please select a
    different certificate.

-   [The VMM server cannot be registered due to an internal error.
    Please refer to the jobs view in the Site Recovery Portal for more
    details on the error. Run Setup again to register the
    server.](http://social.technet.microsoft.com/wiki/contents/articles/25570.the-vmm-server-cannot-be-registered-due-to-an-internal-error-please-refer-to-the-jobs-view-in-the-site-recovery-portal-for-more-details-on-the-error-run-setup-again-to-register-the-server.aspx)

-   [A connection can’t be established to the Hyper-V Recovery Manager
    vault. Verify the proxy settings or try again
    later.](http://social.technet.microsoft.com/wiki/contents/articles/25571.a-connection-cant-be-established-to-the-hyper-v-recovery-manager-vault-verify-the-proxy-settings-or-try-again-later.aspx)

<span id="Configuration" class="anchor"></span>Configuration

-   Hyper-V host cluster contains at least one static network adapter,
    or no connected adapters are configured to use DHCP

-   [The Hyper-V profile isn't enabled in the Capability Profiles for
    cloud](http://social.technet.microsoft.com/wiki/contents/articles/25499.the-hyper-v-profile-isn-t-enabled-in-the-capability-profiles-for-cloud.aspx)

-   [Protection configuration for '%CloudName;' couldn't be applied. A
    newly added Hyper-V host or cluster couldn't be configured because
    cloud protection isn't
    configured.](http://social.technet.microsoft.com/wiki/contents/articles/25500.protection-configuration-for-cloudname-couldn-t-be-applied-a-newly-added-hyper-v-host-or-cluster-couldn-t-be-configured-because-cloud-protection-isn-t-configured.aspx)

<span id="Protection" class="anchor"></span>Protection

-   A suitable host for the replica virtual machine can't be found - Due
    to low compute resources

-   [A suitable host for the replica virtual machine can't be found -
    Due to no logical network
    attached](http://social.technet.microsoft.com/wiki/contents/articles/25502.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-no-logical-network-attached.aspx)

<span id="Recovery" class="anchor"></span>Recovery

-   **VMM cannot complete the host operation** -

    -   [Fail over to the selected recovery point for virtual machine:
        General access denied
        error.](http://social.technet.microsoft.com/wiki/contents/articles/25504.fail-over-to-the-selected-recovery-point-for-virtual-machine-general-access-denied-error.aspx)

    -   [Hyper-V failed to fail over to the selected recovery point for
        virtual machine: Operation aborted Try a more recent recovery
        point.
        (0x80004004)](http://social.technet.microsoft.com/wiki/contents/articles/25503.hyper-v-failed-to-fail-over-to-the-selected-recovery-point-for-virtual-machine-operation-aborted-try-a-more-recent-recovery-point-0x80004004.aspx)

    -   **A connection with the server could not be established
        (0x00002EFD)**

        -   [Hyper-V failed to enable reverse replication for virtual
            machine](http://social.technet.microsoft.com/wiki/contents/articles/25505.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-reverse-replication-for-virtual-machine.aspx)

        -   [Hyper-V failed to enable replication for virtual machine
            virtual
            machine](http://social.technet.microsoft.com/wiki/contents/articles/25506.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-replication-for-virtual-machine-virtual-machine.aspx)

    -   [Could not commit failover for virtual
        machine](http://social.technet.microsoft.com/wiki/contents/articles/25508.could-not-commit-failover-for-virtual-machine.aspx)

-   [The recovery plan contains virtual machines which are not ready for
    planned
    failover](http://social.technet.microsoft.com/wiki/contents/articles/25509.the-recovery-plan-contains-virtual-machines-which-are-not-ready-for-planned-failover.aspx)

-   [The virtual machine isn't ready for planned
    failover](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)

-   [Virtual machine is not running and is not powered
    off](http://social.technet.microsoft.com/wiki/contents/articles/25510.virtual-machine-is-not-running-and-is-not-powered-off.aspx)

<span id="Miscellaneous" class="anchor"></span>Miscellaneous 

Error message: The selected certificate cannot be validated. Please select a different certificate.       
----------------------------------------------------------------------------------------------------------

Error code :

Resolution

ACS50008 SAML token is invalid. (There may be more details in the
message).To fix this error ensure that the system time of the operating
system on which the registration is being performed is in synch with the
time zone.

For more information, see How to Fix Error ACS50008 .

ACS50017 The certificate with subject '\<Certificate subject name\>' and
issuer '\<Issuer name\>' failed validation. Ensure that the certificate
is either self-signed or that it chains to a trusted root certification
authority. The certificate must also not be revoked and must be within
its validity period. For more information, see How to Fix Error ACS50017
.

Error message: The VMM server cannot be registered due to an internal error. Please refer to the jobs view in the Site Recovery Portal for more details on the error. Run Setup again to register the server.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Error code :

Resolution

There was no endpoint listening at
https://pod01-id1.ea.backup.windowsazure.com/IdmgmtService.svc that
could accept the message. This is often caused by an incorrect address
or SOAP action. See InnerException, if present, for more details.

Retry registration by re-running setup to fix this error.

Error message: A connection can’t be established to the Hyper-V Recovery Manager vault. Verify the proxy settings or try again later.
-------------------------------------------------------------------------------------------------------------------------------------

Error code :

Resolution

This error can occur if there is no internet connectivity. Check the
proxy settings.
If internet connectivity exists, the failure may be caused by an
internal server error. Retry registration by re-running setup in this
case.

### Error Message: The virtual machine must have exactly one disk specified as the operating system disk. 

Error code:  70003 

Resolution:
Service couldn't find the virtual machine OS from VMM server. Ensure
that the 'Operating System' setting is configured in the 'General' tab
for the virtual machine properties in the VMM console.

###Error Message: The operating system of the virtual machine OS isn't supported. The operation system must be Windows (Windows Server 2008 R2 and later versions) or Linux. 

Error code:  70002
Resolution:
Service couldn't find the virtual machine hard-disk which contains the
OS from VMM server. Configure only one disk as 'Contains the operating
system for the virtual machine' which contains the operating system for
the virtual machine in 'Hardware Configuration' tab for the virtual
machine properties in the VMM console, and retry the operation.

### Error Message: A suitable host for the replica virtual machine can't be found.
Zero ratings: Not enough memory available. Total memory on the host is 0
MB. Remaining memory for use by existing and new virtual machines is 0
MB. At the time of valuation, the remaining memory was 0 MB and the
amount requested by this virtual machine was 576 MB. ()

Deployment errors: Configuration issues related to the virtual machine
[57422422-74c5-49ea-9a5d-d1fab11369e9] prevent deployment and must be
resolved before deployment can continue. (Get ratings for the virtual
machine to determine an appropriate host and try the operation again.)
Add at least one host with Hyper-V replication enabled to the recovery
cloud. Then try to enable protection for the virtual machine again. 

Error code:  Service error: 40004      Provider error: 31225 

Resolution:
This error indicates that the VMM server is unable to find a Hyper-V
host with the required rating, most likely because the recovery cloud
doesn’t have a Hyper-V host with free memory. Make sure that the
recovery cloud has Hyper-V hosts with enough resources available for
replication and that protection is enabled for the virtual machine.

Error Message: A suitable host for the replica virtual machine can't be found. 
-------------------------------------------------------------------------------

Error:  host1.contoso.com Zero ratings: The virtual machine or tier load
balancer configuration requires an IP pool and there are no appropriate
IP pools accessible from the host. (Select a host with access to an
appropriate IP pool and try the operation again.) No available
connection to selected VM Network can be found. (Ensure host NICs have
connection to the fabric network on which VM Network is created.)  
Deployment errors: Configuration issues related to the NIC with ID
[XXXXXXX-1fdf-XXXX-ba84-XXXXXXXXXX] of VM
[XXXXXXX-DCEE-XXXX-XXXX-1DC00586XXXX] prevent deployment. (Get ratings
for the virtual machine to determine an appropriate host and try the
operation again.) Add at least one host with Hyper-V replication enabled
to the recovery cloud. Then try to enable protection for the virtual
machine again.

Error code: Service error: 40004     Provider error: 31225 

Resolution: Ensure the following:
The VM network that is mapped to the VM network of the primary virtual machine is available to at least one of the hosts of the recovery cloud and the corresponding logical network is available to the recovery cloud. 

You can do so by

1. Adding Network to Host
2. Go to VMM Console
3. Right click on host, click on properties
4. Go to Hardware tab
5. Go to Network Adapters
6. Ensure that the appropriate logical network is associated with network adapter 
7. Adding network to Cloud
8. Go to VMM Console
9. Right click on cloud, click on properties
10. Go to Logical Network tab
11. Ensure that the appropriate logical network is selected

###Error Message : VMM cannot complete the host operation on the host.contoso.com server 
------------------------------------------------------------------------------------------
error: Hyper-V failed to fail over to the
selected recovery point for 'sharepoint-vm1': General access denied
error. Try a more recent recovery point. (0x80070005). (Virtual machine
ID XXXXXXX-DCEE-XXXX-XXXX-1DC00586XXXX) Replication operation for
virtual machine ' sharepoint-vm1' failed: General access denied error
(0x80070005). (Virtual machine ID 590D394F-DCEE-45BD-8187-1DC00586DA00)
(Primary server: 'host.contoso.com', Replica server:
'host5.contoso.com') Resolve the host issue and then try the operation
again.

Error code: Service error: 20013     Provider error: 12700\

Resolution:
Failover on the replica virtual machine couldn't be initiated due to access issues.

Error message: VMM cannot complete the host operation on the host1.contoso.com server
------------------------------------------------------------------------------------------

Hyper-V failed to enable reverse replication for 'SHAREPOINT-VM1': A
connection with the server could not be established (0x00002EFD).
(Virtual machine ID XXXXXXX-DCEE-XXXX-XXXX-1DC00586XXXX) Hyper-V cannot
connect to the specified Replica server 'Host5.contoso.com'. Error: A
connection with the server could not be established (0x00002EFD). Verify
that the specified server is enabled as a Replica server, allows inbound
connection on port '8084', and supports the same authentication scheme.
Resolve the host issue and then try the operation again.

Error code: Service error: 20011      Provider error: 12700
Resolution: The virtual machine couldn't begin reverse replication.
Reverse replication can fail if the protecting location isn't ready to
receive the replication data from the protected location.

Error Message: VMM cannot complete the host operation on the Host5.contoso.com server
----------------------------------------------------------------------------------------

Hyper-V failed to enable replication for virtual machine
'SHAREPOINT-VM1': A connection with the server could not be established
(0x00002EFD). (Virtual Machine ID XXXXXXX-DCEE-XXXX-XXXX-1DC00586XXXX)
Hyper-V cannot connect to the specified Replica server
'Host1.contoso.com'. Error: A connection with the server could not be
established (0x00002EFD). Verify that the specified server is enabled as
a Replica server, allows inbound connection on port '8084', and supports
the same authentication scheme. Resolve the host issue and then try the
operation again.
Error code: Service error code: 40000     Provider error code:12700

Resolution: Enable Protection failed because the primary Hyper-V
host is not able to connect to the recovery Hyper-V host. Ensure that
the network firewall is configured so that Hyper-V host machines can
communicate with each other over port 8084.

Error Message: VMM cannot complete the host operation on the host1.contoso.com 
-------------------------------------------------------------------------------

Could not commit failover for virtual machine 'SHAREPOINT-VM1'. (Virtual
machine ID XXXXXXX-DCEE-XXXX-XXXX-1DC00586XXXX) Replication task 'Commit
Failover' cannot be performed when replication is in 'Replicating' state
for virtual machine 'SHAREPOINT-VM1'. (Virtual machine ID
XXXXXXX-DCEE-XXXX-XXXX-1DC00586XXXX) Resolve the host issue and then try
the operation again.

Error code: Service error code: 20008     Provider error code:12700

Resolution: The commit failover couldn't be completed because the
virtual machine is in replicating state. An operation has happened out
of the band and HRM service is not in sync with the on premise
replication state.

Error Message: VMM cannot complete the host operation on the host1.contoso.com server
-------------------------------------------------------------------------------------

Hyper-V failed to fail over to the selected recovery point for
'SHAREPOINT-VM1': Operation aborted Try a more recent recovery point.
(0x80004004). (Virtual machine ID XXXXXXX-DCEE-XXXX-XXXX-1DC00586XXXX)
Hyper-V did not allow the operation for virtual machine 'SHAREPOINT-VM1'
because test failover is enabled. Stop test failover and try again.
(Virtual machine ID XXXXXXX-DCEE-XXXX-XXXX-1DC00586XXXX) Replication
operation for virtual machine 'SHAREPOINT-VM1' failed. (Virtual machine
ID XXXXXXX-DCEE-XXXX-XXXX-1DC00586XXXX) (Primary server:
'Host5.contoso.com', Replica server: 'Host1.contoso.com') Resolve the
host issue and then try the operation again.

Error code: Service error code: 20013     Provider error code:12700

Resolution: Failover of the virtual machine failed because the test
failover of the virtual machine is in progress. Complete the test
failover and then retry the operation.

Error Message: The recovery plan contains virtual machines which are not ready for planned failover.
------------------------------------------------------------------------------------------------------------
Error code: Service error code: 25014 
Resolution: Ensure that the virtual machines that are part of the
recovery plan have completed Enable Protection. Go the virtual machine
view in the portal and ensure that the virtual machines are in a
Replication Status - "Protected – OK" and "Failover Status" - "Ready".
Once confirmed, try the operation again.

Error Message: The virtual machine isn't ready for planned failover.
-------------------------------------------------------------------------------
Error code: Service error code: 25007 

Resolution: Go the virtual machine view in the portal and ensure
that the virtual machines are in a Replication Status - "Protected – OK"
and "Failover Status" - "Ready". Once confirmed, try the operation
again.

Error Message: Virtual machine sharepoint-vm1 is not running and is not powered off.
-------------------------------------------------------------------------------------

Error code: Service error code: 25016

Resolution: Site Recovery is not able to shut down the virtual
machine because the virtual machine is in a state from which shutdown
can’t be triggered. Ensure that the virtual machine in an appropriate
state for shutdown, then retry the operation.

Error Message: The Hyper-V profile isn't enabled in the Capability Profiles for cloud CHICAGOCLOUD.
----------------------------------------------------------------------------------------------------
Error code: Service error code: 10003
Resolution: Enable the Hyper-V profile in the Capability Profiles
for the cloud, or select another cloud with this capability enabled.

Error Message: Hyper-V host cluster HRMBROKER01.contoso.com contains at least one static network adapter, or no connected adapters are configured to use DHCP.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------
Error code: Service error code: 10003     Provider error code:
12700 
Resolution: Create a Hyper-V Replica broker resource manually
and retry the operation. Please check the steps required to create a
Hyper-V Replica broker [here ![](media/image1.png)](http://blogs.technet.com/b/virtualization/archive/2012/08/15/configuring-hyper-v-replica-broker-using-powershell.aspx)

Error Message: Hyper-V host cluster %DRAClusterName; contains at least one static network adapter, or no connected adapters are configured to use DHCP.
--------------------------------------------------------------------------------------------------------------------------------------------------------------
Error code: Service error code: 67508     Provider error code:31207

Resolution: Create a replica broker manually and retry the
operation. Please check the steps required to create a Hyper-V Replica
broker [here ![](media/image1.png)](http://blogs.technet.com/b/virtualization/archive/2012/08/15/configuring-hyper-v-replica-broker-using-powershell.aspx)

Error Message: VMM does not have appropriate permissions to access the resource 
--------------------------------------------------------------------------------

Error occured which is getting recorded. | Params: {ErrorCode = 10003}
{WorkflowName = } {WorkflowId = 03e73e93-ea82-4765-956f-1a11d300ec0f}
{ErrorInfo = Microsoft.Carmine.WSManWrappers.WSManProviderException: VMM
does not have appropriate permissions to access the resource
C:\\Windows\\system32\\qmgr.dll on the r2mac.contoso.com server.

Ensure that Virtual Machine Manager has the appropriate rights to
perform this action.

Also, verify that CredSSP authentication is currently enabled on the
service configuration of the target computer XYZ,corp.com. To enable the
CredSSP on the service configuration of the target computer, run the
following command from an elevated command line: winrm set
winrm/config/service/auth @{CredSSP="true"} ---\>
System.UnauthorizedAccessException: Access is denied.

Error code: Provider error code: 10003

Resolution: This happens when the Run-As Account used to access the
host has an updated password. Change the Run-As Account password to the
latest password and retry the operation.


###Error Message: Protection couldn't be enabled for the virtual machine.
-------------------------------------------------------------------------------

The virtual machine isn't a generation-1 virtual machine.
Recommendation Configure the virtual machine as generation-1 and then retry the operation.

Error code: 70009

Resolution:
Generation 2 (Gen 2) VMs are not currently for ASR. You
will need to configure the VM as a Gen 1 VM to enable protection.



Error Message:  The requested action couldn't be performed by the 'Hyper-V Replica To Azure' Replication Provider
-----------------------------------------------------------------------------------------------------------------

(Error code: 539)
Possible causes The Provider action failed. Check other errors for more
information.
Recommendation Resolve the issue and retry the operation.
Error (1):
The failover operation failed. ( Error code :  70044)
Possible Causes:  Failover couldn't be started for virtual machine
'Server WithSpace'.
Recommended Actions:  Manually update the name of the target Azure
virtual machine in the Microsoft Azure Site Recovery vault, and retry
the operation.

Error code: Service Error code: 539, ** **70044

Resolution: Azure does not allow for computer names with spaces in
them.  Configure the resource name in source and target properties under
Recovery Services\\\<Vault Name\>\\Protected Items\\\<Cloud Name\>\\\<VM
Name - e.g. "Server WithSpace"\>

### Error Message: Enabling protection couldn't be completed for the virtual machine.
----------------------------------------------------------------------------------------

Provider error: The Microsoft Azure Recovery Services Agent isn't
installed on the Hyper-V host server hv07.contoso.com.\
Install the agent on the server. (Provider error code: 31313)\
Possible causes: Check the Provider errors for more details.\
Recommendation: Manually clear protection settings. For details see
http://go.microsoft.com/fwlink/?LinkId=398534.

<span id="Error_code_Service_Error_code_70095_Prov"
class="anchor"></span>\
**Error code:**  Service Error code:  70095     Provider error code:
31313\
\
**Resolution:**  Install the ASR Agent on the specified host. 
See [http://msdn.microsoft.com/en-us/library/dn788913.aspx ![](media/image1.png) ](http://msdn.microsoft.com/en-us/library/dn788913.aspx)for
more details

## Setup
* The selected certificate cannot be validated. Please select a different certificate.
* The VMM server cannot be registered due to an internal error. Please refer to the jobs view in the Site Recovery Portal for more details on the error. Run Setup again to register the server.
* A connection can’t be established to the Hyper-V Recovery Manager vault. Verify the proxy settings or try again later.

## Configuration
* Hyper-V host cluster contains at least one static network adapter, or no connected adapters are configured to use DHCP
* The Hyper-V profile isn't enabled in the Capability Profiles for cloud
* Protection configuration for '%CloudName;' couldn't be applied. A newly added Hyper-V host or cluster couldn't be configured because cloud protection isn't configured.

## Protection
* A suitable host for the replica virtual machine can't be found - Due to low compute resources
* A suitable host for the replica virtual machine can't be found - Due to no logical network attached

## Recovery

### VMM cannot complete the host operation -
* Fail over to the selected recovery point for virtual machine: General access denied error.
* Hyper-V failed to fail over to the selected recovery point for virtual machine: Operation aborted Try a more recent recovery point. (0x80004004)

#### A connection with the server could not be established (0x00002EFD)
* Hyper-V failed to enable reverse replication for virtual machine
* Hyper-V failed to enable replication for virtual machine virtual machine
* Could not commit failover for virtual machine
* The recovery plan contains virtual machines which are not ready for planned failover
* The virtual machine isn't ready for planned failover
* Virtual machine is not running and is not powered off
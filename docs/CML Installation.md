In order to get CML working on VMWare Workstation on a Ryzen CPU, you can try the following steps and references:

Do make sure to enable the virtualization option for your CPU in the BIOS. How to do this depends on the motherboard and CPU model if it is capable but the configurations are similar. Intel uses VT-x/EPT and AMD uses AMD-V/RVI/SMV.

**References**

Fix for AMD Virtualization (AMD-V/SMV) - `https://community.broadcom.com/vmware-cloud-foundation/discussion/disabling-hyper-v-hypervisor-on-windows-11-pro-host-to-get-vmware-17s-cpl0-vs-ulm-monitor-mode`

Installation Guide - `https://developer.cisco.com/docs/modeling-labs/cml-installation-guide/`
*Note: Select the appropriate CML version guide*

Fix for "No PCIe Slot available for Ethernet0" error - `https://learningnetwork.cisco.com/s/question/0D56e0000E3MmJWCQ0/error-i-get-when-starting-up-the-vm-no-pcie-slot-available-for-ethernet0-remove-ethernet0-and-try-again-i-have-checked-bios-and-the-setting-are-as-requested-i-am-using-vmware-workstation-17-pls-can-someone-help`


Virtualization Issue
![[AMD Virtualization Issue (CML).png]]
This error occurs when first running the CML as a VM. When the memory, storage, cpu, OS, and reference ISOs are set, Virtualization with AMD CPUs can cause problems. See workarounds below:

Do the following one by one and test if CML can run:
**Option 1**
1. Turn off **Memory Integrity protection** in **Windows Security** > **Core Isolation**. Don't restart yet.
2.  Open the Run dialog box by pressing **Win key** + **R** and type **optionalfeatures**. Turn off the following by unchecking: 
	- Hyper-V and all its subfeatures
	- Windows Hypervisor platform
	- Virtual Machine Platform
	- Windows Sandbox.
3. Restart your device.

**Option 2**
1. Open **Command Prompt** as an administrator and execute the command `bcdedit /set hypervisorlaunchtype off`.
2. Open the local Group policy editor and go to **Computer Configuration** > **Administrative Templates** > **System** > **Device Guard**. Open **Turn on Virtualization Based Security** and toggle it to disabled. Restart your device.

The fix from the [broadcom link](https://community.broadcom.com/vmware-cloud-foundation/discussion/disabling-hyper-v-hypervisor-on-windows-11-pro-host-to-get-vmware-17s-cpl0-vs-ulm-monitor-mode|broadcom link) includes a third option that utilizes a tool from Microsoft itself. You can check it if methods above did not work.
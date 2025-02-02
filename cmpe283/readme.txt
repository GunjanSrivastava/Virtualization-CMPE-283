# Assignment1: Discovering VMX Features

# Group Members: 
Anupama Kurudi (anupama.kurudi@sjsu.edu )
Gunjan Srivastava (gunjan.srivastava@sjsu.edu)

# Course: CMPE-283 Sec 48 Virtualization Technologies

# Problem:
Your assignment is to create a Linux kernel module that will query various MSRs to determine
virtualization features available in your CPU. This module will report (via the system message log) the
features it discovers.

# Questions 1:
For each member in your team, provide 1 paragraph detailing what parts of the lab that member
implemented / researched. (You may skip this question if you are doing the lab by yourself).

# Answer:
Both the team members set up the environment and configured VM fusion to host nested VMs on their
individual machines (Mac). The instructions were equally divided. 

We worked on  IA32_VMX_PINBASED_CTLS together to understand how it works.

## Gunjan Srivastav implemented 2 instructions: 
IA32_VMX_PROCBASED_CTLS - 0x482  - Use this MSR for proc based controls if no true
controls capability

IA32_VMX_ENTRY_CTLS - 0x484 - Use this MSR for entry controls if no true
controls capability


## Anupama Kurudi implemented 2 instructions: 
IA32_VMX_PROCBASED_CTLS2 - 0x48B - Use this MSR for secondary procbased
controls, if available

IA32_VMX_EXIT_CTLS - 0x483 - Use this MSR for exit controls if no true
controls capability

All of the code has been committed from their respective machines to the common Git repository.

# Question 2: 
Describe in detail the steps you used to complete the assignment. Consider your reader to be someone
skilled in software development but otherwise unfamiliar with the assignment. Good answers to this
question will be recipes that someone can follow to reproduce your development steps.

# Answer: 
1. Download and install VM Fusion with a compatible version to your local environment.
2. Install Ubuntu on VM Fusion
3. In the Settings tab, under Memory & Processor - enable nested vms and increase the disk space to the required limit
4. Install KVM
5. Install CentOS on KVM as a nested VM and exit CentOS
6. In the Ubuntu VM, fork and clone the master Git repository
7. Create the cmpe283 folder and add MakeFile
8. Write the code to know about the VMX CPU capabilities in cmpe283-Main.c by referring to the Intel SDM for each of the corresponding controls and make appropriate changes.
9. Update the Make file to point to  cmpe283-Main.o and run command - make
10. The cmp283-Main.ko file gets generated
11. Run command - sudo insmod ./cmpe283-Main.ko
12. Run command - dmesg , to view the details (Refer: Output 1)
13. If the previous module has to be removed, run command - sudo rmmod ./cmpe283-Main.ko


# Output 1: 

[21708.856572] CMPE 283 Assignment 1 Module Start
[21708.856575] Primary ProcBased Controls MSR: 0xfff9fffe0401e172
[21708.856576]   Interrupt Window Exiting: Can set=Yes, Can clear=Yes
[21708.856576]   Use TSC Offsetting: Can set=Yes, Can clear=Yes
[21708.856577]   HLT Exiting: Can set=Yes, Can clear=Yes
[21708.856577]   INVLPG Exiting: Can set=Yes, Can clear=Yes
[21708.856578]   MWAIT Exiting: Can set=Yes, Can clear=Yes
[21708.856578]   RDPMC Exiting: Can set=Yes, Can clear=Yes
[21708.856579]   RDTSC Exiting: Can set=Yes, Can clear=Yes
[21708.856579]   CR3 Load Exiting: Can set=Yes, Can clear=No
[21708.856580]   CR3 Store Exiting: Can set=Yes, Can clear=No
[21708.856580]   CR8 Load Exiting: Can set=Yes, Can clear=Yes
[21708.856581]   CR8 Store Exiting: Can set=Yes, Can clear=Yes
[21708.856581]   Use TPR Shadow: Can set=Yes, Can clear=Yes
[21708.856582]   NMI Window Exiting: Can set=Yes, Can clear=Yes
[21708.856582]   MOV DR Exiting: Can set=Yes, Can clear=Yes
[21708.856583]   Unconditional I/O Exiting: Can set=Yes, Can clear=Yes
[21708.856583]   Use I/O Bitmaps: Can set=Yes, Can clear=Yes
[21708.856584]   Monitor Trap Flag: Can set=Yes, Can clear=Yes
[21708.856584]   Use MSR Bitmaps: Can set=Yes, Can clear=Yes
[21708.856585]   MONITOR Exiting: Can set=Yes, Can clear=Yes
[21708.856585]   PAUSE Exiting: Can set=Yes, Can clear=Yes
[21708.856585]   Activate Secondary Controls: Can set=Yes, Can clear=Yes
[21708.856587] Secondary Procbased Controls MSR: 0x553cfe00000000
[21708.856587]   Virtualize APIC accesses: Can set=No, Can clear=Yes
[21708.856588]   Enable EPT: Can set=Yes, Can clear=Yes
[21708.856588]   Descriptor Table Exiting: Can set=Yes, Can clear=Yes
[21708.856588]   Enable RDTSCP: Can set=Yes, Can clear=Yes
[21708.856589]   Virtualize x2APIC Mode: Can set=Yes, Can clear=Yes
[21708.856590]   Enable VPID: Can set=Yes, Can clear=Yes
[21708.856590]   WBINVD Exiting: Can set=Yes, Can clear=Yes
[21708.856590]   Unrestricted Guest: Can set=Yes, Can clear=Yes
[21708.856591]   APIC Register Virtualization: Can set=No, Can clear=Yes
[21708.856591]   Virtual Interrupt Delivery: Can set=No, Can clear=Yes
[21708.856592]   PAUSE Loop Exiting: Can set=Yes, Can clear=Yes
[21708.856592]   RDRAND Exiting: Can set=Yes, Can clear=Yes
[21708.856593]   Enable INVPCID: Can set=Yes, Can clear=Yes
[21708.856593]   Enable VM Functions: Can set=Yes, Can clear=Yes
[21708.856594]   VMCS Shadowing: Can set=No, Can clear=Yes
[21708.856594]   Enable ENCLS Exiting: Can set=No, Can clear=Yes
[21708.856595]   RDSEED Exiting: Can set=Yes, Can clear=Yes
[21708.856595]   Enable PML: Can set=No, Can clear=Yes
[21708.856596]   EPT-violation #VE: Can set=Yes, Can clear=Yes
[21708.856596]   Conceal VMX from PT: Can set=No, Can clear=Yes
[21708.856597]   Enable XSAVES/XRSTORS: Can set=Yes, Can clear=Yes
[21708.856597]   Mode-based Execute Control for EPT: Can set=Yes, Can clear=Yes
[21708.856598]   Sub Page Write Permissions for EPT: Can set=No, Can clear=Yes
[21708.856598]   Intel PT Uses Guest Physical Addresses: Can set=No, Can clear=Yes
[21708.856599]   Use TSC Scaling: Can set=No, Can clear=Yes
[21708.856599]   Enable User Wait and Pause: Can set=No, Can clear=Yes
[21708.856600]   Enable ENCLV Exiting: Can set=No, Can clear=Yes
[21708.856601] VM Entry Controls MSR: 0xf3ff000011ff
[21708.856601]   Load Debug Controls: Can set=Yes, Can clear=No
[21708.856602]   IA-32e Mode Guest: Can set=Yes, Can clear=Yes
[21708.856602]   Entry to SMM: Can set=No, Can clear=Yes
[21708.856603]   Deactivate Dual Monitor Treatment: Can set=No, Can clear=Yes
[21708.856603]   Load IA32 PERF GLOBA L_CTRL: Can set=Yes, Can clear=Yes
[21708.856604]   Load IA32_PAT: Can set=Yes, Can clear=Yes
[21708.856604]   Load IA32_EFER: Can set=Yes, Can clear=Yes
[21708.856605]   Load IA32_BNDCFGS: Can set=No, Can clear=Yes
[21708.856605]   Conceal VMX From PT: Can set=No, Can clear=Yes
[21708.856606]   Load IA32_RTIT_CTL: Can set=No, Can clear=Yes
[21708.856606]   Load CET state: Can set=No, Can clear=Yes
[21708.856607]   Load PKRS: Can set=No, Can clear=Yes
[21708.856608] VM-Exit Controls MSR: 0x3fffff00036dff
[21708.856608]   Save Debug Controls: Can set=Yes, Can clear=No
[21708.856609]   Host Address Space Size: Can set=Yes, Can clear=Yes
[21708.856609]   Load IA32_PERF_GLOBAL_CTRL: Can set=Yes, Can clear=Yes
[21708.856609]   Acknowledge Interrupt on Exit: Can set=Yes, Can clear=Yes
[21708.856610]   Save IA32_PAT: Can set=Yes, Can clear=Yes
[21708.856610]   Load IA32_PAT: Can set=Yes, Can clear=Yes
[21708.856611]   Save IA32_EFER: Can set=Yes, Can clear=Yes
[21708.856611]   Load IA32_EFER: Can set=Yes, Can clear=Yes
[21708.856612]   Save VMX- Preemption Timer Value: Can set=No, Can clear=Yes
[21708.856612]   Clear IA32_BNDCFGS: Can set=No, Can clear=Yes
[21708.856613]   Conceal VMX from PT: Can set=No, Can clear=Yes
[21708.856613]   Clear IA32_RTIT_CTL: Can set=No, Can clear=Yes
[21708.856614]   Load CET state: Can set=No, Can clear=Yes
[21708.856614]   Load PKRS: Can set=No, Can clear=Yes


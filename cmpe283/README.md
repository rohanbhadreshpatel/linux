# CMPE-283 Assignment #1
## Questions
1. For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched. (You may skip this question if you are doing the lab by yourself).
- Implemented and worked on the assignment individually by myself.

2. Describe in detail the steps you used to complete the assignment. Consider your reader to be someone skilled in software development but otherwise unfamiliar  with the assignment. Good answers to this question will be recipes that someone can follow to reproduce your development steps.
Note: I may decide to follow these instructions for random assignments, so you should make sure they are accurate.
- Steps followed to complete the assignment are listed below: 

# Steps to follow
1. Install VMware Fusion (Mac OS) and Ubuntu.
2. Create a VM using VMWare Fusion that will run on Ubuntu.
    - Configure the VM with custom settings for processors and memory per your computer's specifications. 
    - I assigned 2 processor cores and 4096MB for Memory and 200 GB of SSD storage. 
2. Upon successfully installation, power off the VM to enable virtualization in guest VM.
3. Navigate to Settings -> Processors & Memory -> Advanced Options
    - Tick the box for -> "Enable hypervisor applications in this Virtual Machine"
4. Power on the VM and execute the following command to verify that nested virtualization is enabled in VM:
    ```
    cat /proc/cpuinfo | more
    ```
5. Required packages to be installed to run this assignment using the following commands on terminal:
    ```
    sudo apt update
    Install Github: sudo apt-get install git
    Install gcc: sudo apt-get install gcc
    Install Make: sudo apt-get install make
    Install linux source: sudo apt-get install linux-source
    ```
6. Fork linux code from https://github.com/torvalds/linux and clone to your github repository.
7. Configure Github CLI to your github account, clone the repository:
    ```
    git clone git@github.com:rohanbhadreshpatel/linux.git  
    ```
# Steps for Kernel Code Compilation:
8. ```
   sudo apt-get install build-essential kernel-package fakeroot libncurses5-dev libssl-dev ccache bison flex libelf-dev
   ```
9. Run the following commands upon cloning the code from github repository:
    ```
    cd linux/
    cp -v /boot/config-$(uname -r) .config
    make oldconfig  
    make prepare
    make -j 2 modules
    make -j 2
    sudo make INSTALL_MOD_STRIP=1 modules_install #reduces the kernel build size that ignores the debug info
    sudo make install
    
    sudo reboot
    ```
10. Download cmpe283-1.c and Makefile from Canvas provided for the assignment, and navigate to the directory containing those files:
    ```
    cd linux/cmpe283/
    ```    
11. Perform the code changes in cmpe283-1.c as per the assignment file:
    Build code from the file by executing the following command:
    ```
    make
    ```
    After building the file verify if the kernel object file is created, run the command:
    ```
    ls *.ko
    ```
12. Execute:
    ```
    sudo insmod cmpe283-1.ko
    dmesg
    sudo rmmod cmpe283_1
    dmesg
    ```
13. To rebuild the file run commands – 
    ```
    sudo rmmod cmpe283-1
    sudo insmod ./cmpe283-1.ko
    dmesg
    ```
## Output
```
[  504.838725] CMPE 283 Assignment 1 Module Start

[  504.838741] Pinbased Controls MSR: 0x3f0000003f
[  504.838743]   External Interrupt Exiting: Can set=Yes, Can clear=No
[  504.838744]   NMI Exiting: Can set=Yes, Can clear=No
[  504.838745]   Virtual NMIs: Can set=Yes, Can clear=No
[  504.838746]   Activate VMX Preemption Timer: Can set=No, Can clear=Yes
[  504.838746]   Process Posted Interrupts: Can set=No, Can clear=Yes

[  504.838755] Procbased Controls MSR: 0xf5f9fffe9501e97a
[  504.838757]   Interrupt-window exiting: Can set=Yes, Can clear=Yes
[  504.838757]   Use TSC offsetting: Can set=Yes, Can clear=No
[  504.838758]   HLT exiting: Can set=Yes, Can clear=Yes
[  504.838759]   INVLPG exiting: Can set=Yes, Can clear=Yes
[  504.838759]   MWAIT exiting: Can set=Yes, Can clear=Yes
[  504.838760]   RDPMC exiting: Can set=Yes, Can clear=No
[  504.838761]   RDTSC exiting: Can set=Yes, Can clear=Yes
[  504.838761]   CR3-load exiting: Can set=Yes, Can clear=No
[  504.838762]   CR3-store exiting: Can set=Yes, Can clear=No
[  504.838763]   CR8-load exiting: Can set=Yes, Can clear=Yes
[  504.838763]   CR8-store exiting: Can set=Yes, Can clear=Yes
[  504.838764]   Use TPR shadow: Can set=Yes, Can clear=Yes
[  504.838777]   NMI-window exiting: Can set=Yes, Can clear=Yes
[  504.838778]   MOV-DR exiting: Can set=Yes, Can clear=Yes
[  504.838778]   Unconditional I/O: Can set=Yes, Can clear=No
[  504.838780]   Use I/O bitmaps: Can set=No, Can clear=Yes
[  504.838781]   Monitor trap flag: Can set=No, Can clear=Yes
[  504.838782]   Use MSR Bitmaps: Can set=Yes, Can clear=No
[  504.838783]   MONITOR exiting: Can set=Yes, Can clear=Yes
[  504.838783]   PAUSE exiting: Can set=Yes, Can clear=Yes
[  504.838784]   Activate secondary controls: Can set=Yes, Can clear=No

[  504.838795] Secondary Procbased Controls MSR: 0x111cfe00000000
[  504.838797]   Virtualize APIC accesses: Can set=No, Can clear=Yes
[  504.838798]   Enable EPT: Can set=Yes, Can clear=Yes
[  504.838799]   Descriptor-table exiting: Can set=Yes, Can clear=Yes
[  504.838800]   Enable RDTSCP: Can set=Yes, Can clear=Yes
[  504.838801]   Virtualize x2APIC mode: Can set=Yes, Can clear=Yes
[  504.838802]   Enable VPID: Can set=Yes, Can clear=Yes
[  504.838803]   WBINVD exiting: Can set=Yes, Can clear=Yes
[  504.838803]   Unrestricted guest: Can set=Yes, Can clear=Yes
[  504.838804]   APIC-register virtualization: Can set=No, Can clear=Yes
[  504.838805]   Virtual-interrupt delivery: Can set=No, Can clear=Yes
[  504.838806]   PAUSE-loop exiting: Can set=Yes, Can clear=Yes
[  504.838807]   RDRAND exiting: Can set=Yes, Can clear=Yes
[  504.838808]   Enable INVPCID: Can set=Yes, Can clear=Yes
[  504.838808]   Enable VM functions: Can set=No, Can clear=Yes
[  504.838809]   VMCS shadowing: Can set=No, Can clear=Yes
[  504.838810]   Enable ENCLS exiting: Can set=No, Can clear=Yes
[  504.838811]   RDSEED exiting: Can set=Yes, Can clear=Yes
[  504.838812]   Enable PML: Can set=No, Can clear=Yes
[  504.838813]   EPT-violation: Can set=No, Can clear=Yes
[  504.838814]   Conceal VMX nonroot operation from Intel PT: Can set=No, Can clear=Yes
[  504.838815]   Enable XSAVES/XRSTORS: Can set=Yes, Can clear=Yes
[  504.838816]   Mode-based execute control for EPT: Can set=No, Can clear=Yes
[  504.838817]   Sub-page Write Permissions for EPT: Can set=No, Can clear=Yes
[  504.838818]   Intel PT Uses Guest Physical Addresses: Can set=No, Can clear=Yes
[  504.838819]   Use TSC scaling: Can set=No, Can clear=Yes
[  504.838823]   Enable user wait and pause: Can set=No, Can clear=Yes
[  504.838824]   Enable ENCLV exiting: Can set=No, Can clear=Yes

[  504.838835] Exit Controls MSR: 0x3fefff00036dff
[  504.838837]   Save debug controls: Can set=Yes, Can clear=No
[  504.838838]   Host addressspace size: Can set=Yes, Can clear=Yes
[  504.838839]   Load IA32_PERF_GLOB AL_CTRL: Can set=No, Can clear=Yes
[  504.838840]   Acknowledge interrupt on exit: Can set=Yes, Can clear=Yes
[  504.838853]   Save IA32_PAT: Can set=Yes, Can clear=Yes
[  504.838853]   Load IA32_PAT: Can set=Yes, Can clear=Yes
[  504.838854]   Save IA32_EFER: Can set=Yes, Can clear=Yes
[  504.838855]   Load IA32_EFER: Can set=Yes, Can clear=Yes
[  504.838866]   Save VMXpreemption timer value: Can set=No, Can clear=Yes
[  504.838867]   Clear IA32_BNDCFGS: Can set=No, Can clear=Yes
[  504.838868]   Conceal VM exits from Intel PT: Can set=No, Can clear=Yes
[  504.838869]   Clear IA32_RTIT_CTL: Can set=No, Can clear=Yes
[  504.838870]   Load CET state: Can set=No, Can clear=Yes
[  504.838871]   Load PKRS: Can set=No, Can clear=Yes

[  504.838908] Entry Controls MSR: 0xd3ff000011ff
[  504.838913]   Load debug controls: Can set=Yes, Can clear=No
[  504.838914]   IA-32e mode guest: Can set=Yes, Can clear=Yes
[  504.838916]   Entry to SMM: Can set=No, Can clear=Yes
[  504.838917]   Deactivate dual-monitor treatment: Can set=No, Can clear=Yes
[  504.838918]   Load IA32_PERF_GLOBAL_CTRL: Can set=No, Can clear=Yes
[  504.838919]   Load IA32_PAT: Can set=Yes, Can clear=Yes
[  504.838920]   Load IA32_EFER: Can set=Yes, Can clear=Yes
[  504.838921]   Load IA32_BNDCFGS: Can set=No, Can clear=Yes
[  504.838949]   Conceal VM entries from Intel PT: Can set=No, Can clear=Yes
[  504.838959]   Load IA32_RTIT_CTL: Can set=No, Can clear=Yes
[  504.838960]   Load CET state: Can set=No, Can clear=Yes
[  504.838961]   Load PKRS: Can set=No, Can clear=Yes

[  523.868882] CMPE 283 Assignment 1 Module Exits
```


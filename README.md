## Are You Ready to ROCK?
The ROCm Platform brings a rich foundation to advanced computing by seamlessly
 integrating the CPU and GPU with the goal of solving real-world problems.

On April 25th, 2016, we delivered ROCm 1.0 built around three pillars:

1) Open Heterogeneous Computing Platform (Linux Driver and Runtime Stack), 
   optimized for HPC & Ultra-scale class computing;
   
2) Heterogeneous C and C++ Single Source Compiler, to approach computation 
   holistically, on a system level, rather than as a discrete GPU artifact;
   
3) HIP, acknowledging the need for freedom of choice when it comes to platforms
   and APIs for GPU computing.

Using our knowledge of the HSA Standards and, more importantly, the HSA
Runtime, we have been able to successfully extended support to the dGPU with
critical features for accelerating NUMA computation. As a result, the ROCK
driver is composed of several components based on our efforts to develop the
Heterogeneous System Architecture for APUs, including the new AMDGPU driver,
the Kernel Fusion Driver (KFD), the HSA+ Runtime and an LLVM based compilation
stack which provides support for key languages. This support starts with AMD’s
Fiji family of dGPUs, and has expanded to include the Hawaii dGPU family in ROCm
1.2. ROCm 1.3 further extends support to include the Polaris family of ASICs.

#### Supported CPUs
The ROCm Platform leverages PCIe Atomics (Fetch ADD, Compare and SWAP, 
Unconditional SWAP, AtomicsOpCompletion).
[PCIe atomics](https://github.com/RadeonOpenCompute/RadeonOpenCompute.github.io/blob/master/ROCmPCIeFeatures.md)
are only supported on PCIe Gen3 Enabled CPUs and PCIe Gen3 Switches like
Broadcom PLX. When you install your GPUs make sure you install them in a fully
PCIe Gen3 x16 or x8 slot attached either directly to the CPU's Root I/O 
controller or via a PCIe switch directly attached to the CPU's Root I/O 
controller. In our experience many issues stem from trying to use consumer 
motherboards which provide Physical x16 Connectors that are electrically 
connected as e.g. PCIe Gen2 x4. This typically occurs when connecting via the 
Southbridge PCIe I/O controller. If you motherboard is part of this category,
please do not use this connector for your GPUs, if you intend to exploit ROCm.


Our GFX8 GPU's (Fiji & Polaris Family) and GFX9 (Vega)  use PCIe Gen 3 and PCIe Atomics. 

Current CPUs which support PCIe Gen3 + PCIe Atomics are: 
  * Intel Xeon E5 v3 or newer CPUs; 
  * Intel Xeon E3 v3 or newer CPUs; 
  * Intel Core i7 v4, Core i5 v4, Core i3 v4 or newer CPUs (i.e. Haswell family or newer).
  * AMD Ryzen CPUs;
  
Upcoming CPUs which will support PCIe Gen3 + PCIe Atomics are:
  * AMD Naples Server CPUs; 
  * Cavium Thunder X Server Processor. 

Experimental support for our GFX7 GPUs Radeon R9 290, R9 390, AMD FirePro S9150, S9170 note they do not support or
take advantage of PCIe Atomics. However, we still recommend that you use a CPU
from the list provided above. 

#### Not supported or very limited support under ROCm 
* We do not support ROCm with PCIe Gen 2 enabled CPUs such as the AMD Opteron,
Phenom, Phenom II, Athlon, Athlon X2, Athlon II and Older Intel Xeon and Intel
Core Architecture and Pentium CPUs.  
* We also do not support AMD Carrizo and Kaveri APU as host for compliant dGPU
 attachments.
* Thunderbolt 1 and 2 enabled GPU's are not supported by ROCm. Thunderbolt 1 & 2
are PCIe Gen2 based.
* AMD Carrizo based APUs have limited support due to OEM & ODM's choices when it
comes to some key configuration parameters. On point, we have observed that
Carrizo Laptops, AIOs and Desktop systems showed inconsistencies in exposing and
enabling the System BIOS parameters required by the ROCm stack. Before
purchasing a Carrizo system for ROCm, please verify that the BIOS provides an
option for enabling IOMMUv2. If this is the case, the final requirement is
associated with correct CRAT table support - please inquire with the OEM about 
the latter.
* AMD Merlin/Falcon Embedded System is also not currently supported by the public Repo. 

#### Support for future APUs
We are well aware of the excitement and anticipation built around using ROCm
with an APU system which fully exposes Shared Virtual Memory alongside and cache
coherency between the CPU and GPU. To this end, in mid 2017 we plan on testing 
commercial AM4 motherboards for the Bristol Ridge and Raven Ridge families of 
APUs. Just like you, we still waiting for access to them! Once we have the first
boards in the lab we will detail our experiences via our blog, as well as build
a list of motherboard that are qualified for use with ROCm.

### New Features to ROCm 1.7

#### DKMS driver installation

 * New driver installation uses Dynamic Kernel Module Support (DKMS)
 * Only amdkfd and amdgpu kernel modules are installed to support AMD hardware
 * Currently only Debian packages are provided for DKMS (no Fedora suport available)
 * See the [ROCT-Thunk-Interface](https://github.com/RadeonOpenCompute/ROCT-Thunk-Interface/tree/roc-1.7.x) and [ROCK-Kernel-Driver](https://github.com/RadeonOpenCompute/ROCK-Kernel-Driver/tree/roc-1.7.x) for additional documentation on driver setup

#### Developer preview of the new OpenCL 1.2 compatible language runtime and compiler

 * OpenCL 2.0 compatible kernel language support with OpenCL 1.2 compatible
   runtime 
 * Supports offline ahead of time compilation today;
   during the Beta phase we will add in-process/in-memory compilation. 
 * Binary Package support for Ubuntu 16.04
 * Binary Package support for Fedora 24 is not currently available
 * Dropping binary package support for Ubuntu 14.04, Fedora 23
 
#### IPC support 

### The latest ROCm platform - ROCm 1.7
The latest tested version of the drivers, tools, libraries and source code for
the ROCm platform have been released and are available under the roc-1.7.x or rocm-1.7.x tag
of the following GitHub repositories:

* [ROCK-Kernel-Driver](https://github.com/RadeonOpenCompute/ROCK-Kernel-Driver/tree/roc-1.7.x)
* [ROCR-Runtime](https://github.com/RadeonOpenCompute/ROCR-Runtime/tree/roc-1.7.x)
* [ROCT-Thunk-Interface](https://github.com/RadeonOpenCompute/ROCT-Thunk-Interface/tree/roc-1.7.x)
* [ROC-smi](https://github.com/RadeonOpenCompute/ROC-smi/tree/roc-1.7.x)
* [HCC compiler](https://github.com/RadeonOpenCompute/hcc/tree/roc-1.7.x)
* [compiler-runtime](https://github.com/RadeonOpenCompute/compiler-rt/tree/roc-1.7.x)
* [HIP](https://github.com/GPUOpen-ProfessionalCompute-Tools/HIP/tree/roc-1.7.x)
* [HIP-Examples](https://github.com/GPUOpen-ProfessionalCompute-Tools/HIP-Examples/tree/roc-1.7.x)
* [atmi](https://github.com/RadeonOpenCompute/atmi/tree/0.3.7)

Additionally, the following mirror repositories that support the HCC compiler
are also available on GitHub, and frozen for the rocm-1.7.0 release:

* [llvm](https://github.com/RadeonOpenCompute/llvm/tree/roc-1.7.x)
* [lld](https://github.com/RadeonOpenCompute/lld/tree/rocm-1.7.x)
* [hcc-clang-upgrade](https://github.com/RadeonOpenCompute/hcc-clang-upgrade/tree/roc-1.7.x)
* [ROCm-Device-Libs](https://github.com/RadeonOpenCompute/ROCm-Device-Libs/tree/roc-1.7.x)

#### Supported Operating Systems

The ROCm 1.7 platform has been tested on the following operating systems:
 * Ubuntu 16.04

### Installing from AMD ROCm repositories
AMD is hosting only debian repositories for the ROCm 1.7 packages at this time. It is expected
that an rpm repository will be available in the next point release.

The packages in the Debian repository have been signed to ensure package integrity.
Directions for each repository are given below:

##### First make sure your system is up to date 

```shell
sudo apt update
sudo apt dist-upgrade
sudo apt-get install libnuma-dev
sudo reboot
```

#### Packaging server update
The packaging server has been changed from the old http://packages.amd.com
to the new repository site http://repo.radeon.com. 

#### Debian repository - apt-get

##### Add the ROCm apt repository
For Debian based systems, like Ubuntu, configure the Debian ROCm repository as
follows:

```shell
wget -qO - http://repo.radeon.com/rocm/apt/debian/rocm.gpg.key | sudo apt-key add -
sudo sh -c 'echo deb [arch=amd64] http://repo.radeon.com/rocm/apt/debian/ xenial main > /etc/apt/sources.list.d/rocm.list'
```
The gpg key might change, so it may need to be updated when installing a new 
release. The current rocm.gpg.key is not avialable in a standard key ring distribution,
but has the following sha1sum hash:

f0d739836a9094004b0a39058d046349aacc1178  rocm.gpg.key

##### Install or Update
Next, update the apt-get repository list and install/update the rocm package:

>**Warning**: Before proceeding, make sure to completely
>[uninstall any previous ROCm package](https://github.com/RadeonOpenCompute/ROCm#removing-pre-release-packages):

```shell
sudo apt-get update
sudo apt-get install rocm-dkms
```

###### Next set your permsions 
With move to upstreaming the KFD driver and the support of DKMS,  for all Console aka headless user, you will need to add all  your users to the  'video" group by setting the Unix permissions

Configure 
Ensure that your user account is a member of the "video" group prior to using the ROCm driver. You can find which groups you are a member of with the following command:

```shell
groups
```

To add yourself to the video group you will need the sudo password and can use the following command:

```shell
sudo usermod -a -G video $LOGNAME 
``` 

Once complete, reboot your system.

We recommend you [verify your installation](https://github.com/RadeonOpenCompute/ROCm#verify-installation) to make sure everything completed successfully.

#### To install ROCm with Developer Preview of OpenCL 

##### Start by following the instruction of installing ROCm with Debian repository:

 at the step "sudo apt-get install rocm-dkms" replace it with:
 
 ```shell
 sudo apt-get install rocm-dkms rocm-opencl
 ```
 
 To install the development kit for OpenCL, which includes the OpenCL header files, execute this installation command:
 
 ```shell
 sudo apt-get install rocm-opencl-dev
  ```
  
 Then follow the direction for Debian Repository 
 
###### Upon restart, To test your OpenCL instance 

 Build and run Hello World OCL app..

HelloWorld sample:
```
 wget https://raw.githubusercontent.com/bgaster/opencl-book-samples/master/src/Chapter_2/HelloWorld/HelloWorld.cpp
 wget https://raw.githubusercontent.com/bgaster/opencl-book-samples/master/src/Chapter_2/HelloWorld/HelloWorld.cl
```

 Build it using the default ROCm OpenCL include and library locations:
```
g++ -I /opt/rocm/opencl/include/ ./HelloWorld.cpp -o HelloWorld -L/opt/rocm/opencl/lib/x86_64 -lOpenCL
```

 Run it:
 ```
 ./HelloWorld
```

##### Un-install
To un-install the entire rocm development package execute:

```shell
sudo apt-get autoremove rocm-dkms
```

##### Installing development packages for cross compilation
It is often useful to develop and test on different systems. In this scenario,
you may prefer to avoid installing the ROCm Kernel to your development system.

In this case, install the development subset of packages:

```shell
sudo apt-get update
sudo apt-get install rocm-dev
```

>**Note:** To execute ROCm enabled apps you will require a system with the full
>ROCm driver stack installed

##### Removing pre-release packages
If you installed any of the ROCm pre-release packages from github, they will
need to be manually un-installed:

```shell
sudo apt-get purge libhsakmt
sudo apt-get purge radeon-firmware
sudo apt-get purge $(dpkg -l | grep 'kfd\|rocm' | grep linux | grep -v libc | awk '{print $2}')
```

If possible, we would recommend starting with a fresh OS install.

#### RPM repository - dnf (yum)

A repository containing rpm packages is currently no available for the ROCm 1.7 release.

#### Closed source components
The ROCm platform relies on a few closed source components to provide legacy
functionality like HSAIL finalization and debugging/profiling support. These
components are only available through the ROCm repositories, and will either be
deprecated or become open source components in the future. These components are
made available in the following packages:

*  hsa-ext-rocr-dev

### Getting ROCm source code
Modifications can be made to the ROCm 1.7 components by modifying the open
source code base and rebuilding the components. Source code can be cloned from
each of the GitHub repositories using git, or users can use the repo command
and the ROCm 1.7 manifest file to download the entire ROCm 1.7 source code.

#### Installing repo
Google's repo tool allows you to manage multiple git repositories
simultaneously. You can install it by executing the following commands:

```shell
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```
Note: make sure ~/bin exists and it is part of your PATH

#### Cloning the code
```shell
mkdir ROCm && cd ROCm
repo init -u https://github.com/RadeonOpenCompute/ROCm.git -b roc-1.7.0
repo sync
```
These series of commands will pull all of the open source code associated with
the ROCm 1.7 release. Please ensure that ssh-keys are configured for the
target machine on GitHub for your GitHub ID.

* OpenCL Runtime and Compiler will be submitted to the Khronos Group, prior to
  the final release, for conformance testing.

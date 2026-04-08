# Automated compilation script for building the 6.6 kernel to the SM8750/MT6991 series universal version
[![STAR](https://img.shields.io/github/stars/palazik/oppo_oplus_realme_sm8750?style=flat&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyByb2xlPSJpbWciIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48dGl0bGU%2BR2l0SHViPC90aXRsZT48cGF0aCBkPSJNMTIgLjI5N2MtNi42MyAwLTEyIDUuMzczLTEyIDEyIDAgNS4zMDMgMy40MzggOS44IDguMjA1IDExLjM4NS42LjExMy44Mi0uMjU4LjgyLS41NzcgMC0uMjg1LS4wMS0xLjA0LS4wMTUtMi4wNC0zLjMzOC43MjQtNC4wNDItMS42MS00LjA0Mi0xLjYxQzQuNDIyIDE4LjA3IDMuNjMzIDE3LjcgMy42MzMgMTcuN2MtMS4wODctLjc0NC4wODQtLjcyOS4wODQtLjcyOSAxLjIwNS4wODQgMS44MzggMS4yMzYgMS44MzggMS4yMzYgMS4wNyAxLjgzNSAyLjgwOSAxLjMwNSAzLjQ5NS45OTguMTA4LS43NzYuNDE3LTEuMzA1Ljc2LTEuNjA1LTIuNjY1LS4zLTUuNDY2LTEuMzMyLTUuNDY2LTUuOTMgMC0xLjMxLjQ2NS0yLjM4IDEuMjM1LTMuMjItLjEzNS0uMzAzLS41NC0xLjUyMy4xMDUtMy4xNzYgMCAwIDEuMDA1LS4zMjIgMy4zIDEuMjMuOTYtLjI2NyAxLjk4LS4zOTkgMy0uNDA1IDEuMDIuMDA2IDIuMDQuMTM4IDMgLjQwNSAyLjI4LTEuNTUyIDMuMjg1LTEuMjMgMy4yODUtMS4yMy42NDUgMS42NTMuMjQgMi44NzMuMTIgMy4xNzYuNzY1Ljg0IDEuMjMgMS45MSAxLjIzIDMuMjIgMCA0LjYxLTIuODA1IDUuNjI1LTUuNDc1IDUuOTIuNDIuMzYuODEgMS4wOTYuODEgMi4yMiAwIDEuNjA2LS4wMTUgMi44OTYtLjAxNSAzLjI4NiAwIC4zMTUuMjEuNjkuODI1LjU3QzIwLjU2NSAyMi4wOTIgMjQgMTcuNTkyIDI0IDEyLjI5N2MwLTYuNjI3LTUuMzczLTEyLTEyLTEyIiBmaWxsPSIjZmZmZmZmIj48L3BhdGg%2BPC9zdmc%2B)](https://github.com/palazik/oppo_oplus_realme_sm8750/stargazers)
[![FORK](https://img.shields.io/github/forks/palazik/oppo_oplus_realme_sm8750?style=flat&logo=greasyfork&color=%2394E61A)](https://github.com/palazik/oppo_oplus_realme_sm8750/forks)
[![COOLAPK](https://img.shields.io/badge/palazik_2-palazik_2?style=flat&logo=android&logoColor=FF4500&label=%E9%85%B7%E5%AE%89&color=FF4500)](http://www.coolapk.com/u/22650293)
[![DISCUSSION](https://img.shields.io/badge/%E8%AE%A8%E8%AE%BA%E5%8C%BA-discussions?logo=livechat&logoColor=FFBBFF&color=3399ff)](https://github.com/palazik/oppo_oplus_realme_sm8750/discussions)

<img alt="Endpoint Badge" src="https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Fcctv18%2Fkernel-workshop%2Frefs%2Fheads%2Fhotfix%2Fnotice.json">

##### 
A more convenient and faster automated universal kernel compilation script for OPPO/OnePlus/Realme series Snapdragon 8 Elite (SM8750)/Dimensity 9400+ (MT6991) models.
##### 
The initial goal of this project was to solve the following problems:
- Green Factory's official stance is to slack off, only releasing half of the open-source code, which has resulted in some kernel code being unable to compile normally using the existing configuration XML, or even without compiling the configuration XML at all;
- The official Bazel compiler is too unstable and inefficient, prone to all sorts of inexplicable errors, and there are almost no effective solutions available online, making it extremely unfriendly to beginners;
- Due to the modified kernel f2fs code by OPPO, the OGA real machine model cannot boot normally after flashing the GKI kernel without clearing the data partition.
## Main contents (and plans) of this project
- Provides dual compilation modes: OKI (official source code) / GKI (Google general kernel source code). OKI retains the official driver/schedule, while GKI has stronger compatibility (it can be flashed without the need for the same kernel minor version).
- Port the official kernel's f2fs source code to GKI, so that the GKI kernel can be flashed like the official OKI kernel, retaining data and booting normally without needing to clear the data folder.
- We switched to LLVM/Clang 18 for compilation and excluded unnecessary vendor source code from the official source code, which greatly optimized the compilation process. Compared with the original bazel compiler, it shortened the compilation time by nearly 2/3 (the original official compiler takes more than 1 hour to complete each compilation), improved the stability of the compilation process, and made the output logs easier to maintain and debug.
- Fixed bugs in the official code/patches that were not updated in time, and introduced support for the Windspeed kernel driver;
- Provides dual-version scripts for online compilation via Github Actions and local compilation via shell.
## Implemented:
- [x] OKI kernel for SM8750 (based on OnePlus 13 source code 6.6.30, OnePlus 13t source code 6.6.56, OnePlus Pad 2 Pro source code 6.6.57, OnePlus 13 source code 6.6.66 and OnePlus 13 source code 6.6.89; other non-SM8750 models with the same kernel version can be tested independently, and some models are fully compatible).
- [x] OKI kernel for MT6991 (based on the official 6.6.50 kernel source code of OnePlus Ace5 Ultra; other non-MT6989 models with the same kernel version can be tested independently; some models are fully compatible)
- [x] The Ougazhen 6.6 series kernel has been fully ported to the official Fengchi SCX speed controller, enabling complete original Fengchi kernel scheduling functions on models with official Fengchi kernel support.
- [x] ReSukiSU/SukiSU Ultra/KernelSU Next/Original KernelSU (Multiple versions of KSU available)
- [x] Introducing ccache caching and numerous proprietary compilation process optimizations, the initial compilation time is approximately 11 minutes, and the subsequent compilation time can be stabilized at approximately 6 minutes. *(The initial compilation will pull the common pre-built ccache. From the second compilation onwards, with the configuration unchanged, the single compilation time is approximately 6 minutes. (Due to the ccache caching mechanism, changing any kernel compilation options will cause the secondary compilation speed to drop to approximately 11 minutes. If the same configuration is used when creating the cache, it can be restored to approximately 6 minutes. If long-term modifications to configuration options are required, it is recommended to enable the "Update ccache cache" option.) The cache will be automatically cleared after two weeks of inactivity, and the compilation will automatically rebuild the cache at this time.)*
- [x] Introducing O2 compilation optimizations to improve kernel performance.
- [x] ~~Optional manual/kprobes/syscall hook modes (kprobes hook mode supports switching to SUS SU mode)~~ Since the latest version of KSU has updated the inline hook, the old manual/syscall hook is obsolete.
- [x] lz4 1.10.0 & zstd 1.5.7 algorithm update & optimization patch (from [@ferstar](https://github.com/ferstar), ported by [@Xiaomichael](https://github.com/Xiaomichael), 6.6 version patch remake by [@cctv18](https://github.com/cctv18))
- [x] Optional addition of BBR/Brutal and a series of TCP congestion control algorithms
- Porting the ADIOS IO Scheduler (https://github.com/firelzrd/adios)
- [x] Added some network connectivity performance optimization configuration options (to provide support for ipset and programs that require kernel support for advanced network functions such as iptables).
- [x] Added support for the [Mountify](https://github.com/backslashxx/mountify) module.
- [x] Added Re:Kernel support, working with software like Freezer and NoActive to reduce power consumption.
- [x] Added kernel anti-format baseband protection (By [@showdo](https://github.com/showdo)), effectively preventing malicious formatting scripts/programs from damaging system partition data.
## To be implemented:
- [ ] OMEGA SM8750 Universal GKI Kernel (Porting OnePlus f2fs source code to achieve data flashing without data wipe)
- [ ] zram is built-in, no need for external zram.ko mounting ~~(Is it really necessary now that there are new lz4 & zstd patches?)~~
- [ ] LXC/Docker feature support
- [ ] Nethunter driver porting
- ~~Integration of multi-version kernel compilation scripts (Due to ease of operation and limitations in the number of options on GitHub Actions, multi-script integration is not currently performed)~~
- Further optimizations and feature porting...
##### 
##### 
##### 
## Credits
- ReSukiSU：[ReSukiSU/ReSukiSU](https://github.com/ReSukiSU/ReSukiSU)
- SukiSU Ultra：[SukiSU-Ultra/SukiSU-Ultra](https://github.com/SukiSU-Ultra/SukiSU-Ultra)
- susfs4ksu：[ShirkNeko/susfs4ksu](https://github.com/ShirkNeko/susfs4ksu)
- SukiSU kernel patch：[SukiSU-Ultra/SukiSU_patch](https://github.com/SukiSU-Ultra/SukiSU_patch)
- KernelSU Next branch maintained by pershoot：[pershoot/KernelSU-Next](https://github.com/pershoot/KernelSU-Next)
- Manual hooks and other patches：[WildKernels/kernel_patches](https://github.com/WildKernels/kernel_patches)
- Original KernelSU: [tiann/KernelSU](https://github.com/tiann/KernelSU)
- Kernel anti-grind baseband protection module：[vc-teahouse/Baseband-guard](https://github.com/vc-teahouse/Baseband-guard)
- GKI kernel build script: (To be determined)
- ~~本地化内核构建脚本（已失效）：[Suxiaoqinx/kernel_manifest_OnePlus_Sukisu_Ultra](https://github.com/Suxiaoqinx/kernel_manifest_OnePlus_Sukisu_Ultra)~~

<!-- 这是一个访客统计，用来看看我的项目主页有多少人访问过 -->
<div align="center">
  <img width="0" height="0" src="https://count.getloli.com/get/@:palazik" />
</div>

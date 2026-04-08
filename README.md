# OPlus (OPPO/OnePlus/Realme) SM8750/MT6991 Series Universal 6.6 Fengchi Ported Kernel Automated Compilation Script

[STAR](https://github.com/palazik/oppo_oplus_realme_sm8750/stargazers)
[FORK](https://github.com/palazik/oppo_oplus_realme_sm8750/forks)
[COOLAPK](http://www.coolapk.com/u/22650293)
[![DISSCUSSION]https://github.com/palazik/oppo_oplus_realme_sm8750/discussions](https://github.com/palazik/oppo_oplus_realme_sm8750/discussions))

\<img alt="Endpoint Badge" src="[https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Fcctv18%2Fkernel-workshop%2Frefs%2Fheads%2Fhotfix%2Fnotice.json](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Fcctv18%2Fkernel-workshop%2Frefs%2Fheads%2Fhotfix%2Fnotice.json)"\>

##### 

A more convenient and faster automated universal kernel compilation script for OPPO/OnePlus/Realme Snapdragon 8 Elite (SM8750) / Dimensity 9400+ (MT6991) devices.

##### 

The original intention of this project is to solve the following problems:

  - The "Green Factory" (OPPO) half-baking their open-source release, causing some kernel code to fail compilation with the existing XML configurations, or completely lacking compilation configuration XMLs entirely;
  - The official Bazel compiler used is too unstable and inefficient, prone to various inexplicable errors with almost no effective solutions online, making it extremely unfriendly to beginners;
  - Because OPPO heavily modified the kernel's f2fs code, flashing a GKI kernel on OPlus devices prevents the device from booting normally unless the data partition is wiped.

## Main Content (and Roadmap) of this Project

  - Provides dual compilation modes: OKI (Official Source) / GKI (Google Generic Kernel Image). OKI retains official drivers/scheduling, while GKI has stronger compatibility (can be flashed without needing the exact same kernel sub-version);
  - Ported the official kernel's f2fs source code for GKI, allowing the GKI kernel to boot normally and retain data after flashing just like the official OKI kernel, without needing to wipe data \~\~("New Folder")\~\~;
  - Switched to LLVM/Clang 18 for compilation and excluded unnecessary vendor source participation from the official code. This significantly optimizes the compilation process, reducing build time by nearly 2/3 compared to the original Bazel compiler (the original official compiler takes over 1 hour per build), improving stability, and producing logs that are easier to maintain and debug;
  - Fixes bugs and out-of-date patches in the official code, and introduces support for Fengchi (WindSpeed) kernel drivers;
  - Provides dual script versions for both Github Actions online compilation and local shell compilation.

## Implemented Features:

  - [x] OPlus SM8750 Universal OKI Kernel (based on OnePlus 13 source 6.6.30, OnePlus 13T source 6.6.56, OnePlus Pad 2 Pro source 6.6.57, OnePlus 13 source 6.6.66, and OnePlus 13 source 6.6.89. Other non-SM8750 devices with the same kernel version can test it themselves, some are fully compatible)
  - [x] OPlus MT6991 Universal OKI Kernel (based on the official 6.6.50 kernel source from OnePlus Ace 5 Pro. Other non-MT6989 devices with the same kernel version can test it themselves, some are fully compatible)
  - [x] Fully ported the official Fengchi scx governor for OPlus 6.6 series kernels, enabling complete original Fengchi kernel scheduling on devices with official Fengchi support
  - [x] Multiple KSU versions optional: ReSukiSU / SukiSU Ultra / KernelSU Next / Original KernelSU
  - [x] Introduced ccache and massive exclusive compilation process optimizations. First compilation takes \~11 mins, subsequent compilations stabilize at \~6 mins *(Pulls a public preset ccache on first run. If the configuration remains unchanged, subsequent builds take \~6 mins. Due to ccache mechanics, changing any kernel compile option drops subsequent speeds back to \~11 minutes; reverting to the config used when the cache was created restores the \~6 minute speed. If you need long-term config changes, it's recommended to enable the "Update ccache cache" option. Caches are automatically cleared after two weeks of inactivity, triggering an automatic cache rebuild on the next compile)*
  - [x] Introduced O2 compilation optimization to improve kernel runtime performance
  - [x] \~\~Optional manual/kprobes/syscall hook modes (supports switching to sus su mode under kprobes hook)\~\~ Since the latest KSU has updated to inline hooks, the old manual/syscall hooks are now deprecated.
  - [x] lz4 1.10.0 & zstd 1.5.7 algorithm updates & optimization patches (from [@ferstar](https://github.com/ferstar), ported by [@Xiaomichael](https://github.com/Xiaomichael), 6.6 version patch remade by [@cctv18](https://github.com/cctv18))
  - [x] Optional addition of BBR/Brutal and a series of TCP congestion control algorithms
  - [x] Ported the [ADIOS IO Scheduler](https://github.com/firelzrd/adios)
  - [x] Added network connection performance optimization config options (to provide kernel support for ipset and programs requiring advanced networking like iptables)
  - [x] Added support for the [Mountify](https://github.com/backslashxx/mountify) module
  - [x] Added Re:Kernel support to reduce power consumption in conjunction with software like Freezer and NoActive
  - [x] Added Kernel Anti-Format Baseband Protection (By [@showdo](https://github.com/showdo)), effectively preventing malicious formatting scripts/programs from destroying system partition data

## To-Do List:

  - [ ] OPlus SM8750 Universal GKI Kernel (Porting OnePlus f2fs source to allow flashing without wiping data)
  - [ ] Built-in zram, eliminating the need for external zram.ko mounting \~\~*(Is this really still necessary with the new lz4 & zstd patches?)*\~\~
  - [ ] LXC/Docker feature support
  - [ ] Nethunter driver ports
  - \~\~Integrate multi-version kernel compilation scripts (Suspended for now due to operational convenience and GitHub Action option limits)\~\~
  - More optimizations and feature ports...

##### 

##### 

##### 

## Acknowledgements

  - ReSukiSU: [ReSukiSU/ReSukiSU](https://github.com/ReSukiSU/ReSukiSU)
  - SukiSU Ultra: [SukiSU-Ultra/SukiSU-Ultra](https://github.com/SukiSU-Ultra/SukiSU-Ultra)
  - susfs4ksu: [ShirkNeko/susfs4ksu](https://github.com/ShirkNeko/susfs4ksu)
  - SukiSU kernel patches: [SukiSU-Ultra/SukiSU\_patch](https://github.com/SukiSU-Ultra/SukiSU_patch)
  - KernelSU Next branch maintained by pershoot: [pershoot/KernelSU-Next](https://github.com/pershoot/KernelSU-Next)
  - Manual hook and other patches: [WildKernels/kernel\_patches](https://github.com/WildKernels/kernel_patches)
  - Original KernelSU: [tiann/KernelSU](https://github.com/tiann/KernelSU)
  - Kernel Anti-Format Baseband Protection module: [vc-teahouse/Baseband-guard](https://github.com/vc-teahouse/Baseband-guard)
  - GKI kernel build script: (TBD)
  - \~\~Localized kernel build script (Deprecated): [Suxiaoqinx/kernel\_manifest\_OnePlus\_Sukisu\_Ultra](https://www.google.com/search?q=https://github.com/Suxiaoqinx/kernel_manifest_OnePlus_Sukisu_Ultra)\~\~

\<\!-- This is a visitor counter to see how many people have visited my project homepage --\>

\<div align="center"\>
\<img width="0" height="0" src="[https://count.getloli.com/get/@:palazik](https://count.getloli.com/get/@:palazik)" /\>
\</div\>

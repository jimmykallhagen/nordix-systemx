# __*Nordix -SystemX*__

---

 > This is a rolling project and I am not currently actively working on this project, what is available now is a setup I have run on the hyprland stack, it works great, however there is some component in the stack that does not like this setup and if I remember correctly it is hyprutils or hyprtools. However, it may be because it is built with LTO=full and changing to LTO=thin may possibly solve the problem, hyprland and aquamarine do work with this setup and I will soon release an aur package with one of the more powerful optimized setups you can get from your desktop environment based on the AUR packages hypr*-.frozen
</br>

 My idea is to eventually produce a highly optimized Custom build where I also intend to produce PGO profiles for system components such as: 

  - [ ] ZFS
  - [ ] Kernel
  - [ ] Drivers
  - [ ] Compositor stack
  - [ ] Ananicy Cpp 

and if I ever succeed then also a custom proton or wine.

---

## ⚠️
> What is currently published has flags specific to zvnver4, so you must have a CPU that has that particular architecture, znver4 or zvner5. However, it is possible to remove the zver4 flags and then run these on v3-v4 architectures.

---

## Nordix znver4 optimizations

## Compiler
- CC=clang
- CXX=clang++

## C-Flags
- -march=znver4
- -mtune=znver4
- -O3
- -pipe
- -fno-plt
- -mavx512f
- -mavx512dq
- -mavx512bw
- -mavx512vl
- -mavx512cd
- -mavx512vbmi
- -mavx512vbmi2
- -mavx512vnni
- -mvaes
- -mvpclmulqdq
- -flto=full
- -fvectorize
- -fslp-vectorize
- -ftree-vectorize
- -funroll-loops
- -falign-functions=64
- -falign-loops=64
- -fno-math-errno
- -fno-trapping-math
- -fmerge-all-constants
- -fno-stack-protector
- -D_FORTIFY_SOURCE=0

## LD-Flags
- -flto=full
- -fuse-ld=lld
- -Wl,-O3,--relax
- -Wl,--lto-O3
- -Wl,--lto-whole-program-visibility"
  
**I will probably replace lto full with lto thin, as I suspect lto thin will be more robust**
**The idea is to also create PGO profiles in the future.**

## Nordix znver4 optimizations

## Compiler
- CC=clang
- CXX=clang++

## C-Flags
- -march=znver4
- -mtune=znver4
- -O3
- -pipe
- -fno-plt
- -mavx512f
- -mavx512dq
- -mavx512bw
- -mavx512vl
- -mavx512cd
- -mavx512vbmi
- -mavx512vbmi2
- -mavx512vnni
- -mvaes
- -mvpclmulqdq
- -flto=full
- -fvectorize
- -fslp-vectorize
- -ftree-vectorize
- -funroll-loops
- -falign-functions=64
- -falign-loops=64
- -fno-math-errno
- -fno-trapping-math
- -fmerge-all-constants

### Performance flags with security impact
- -fstack-protector
- -D_FORTIFY_SOURCE=1

**Read the guide below, so you can decide for yourself what you think is right for you.**
**Personally, I go all in.**

## LD-Flags
- -flto=full
- -fuse-ld=lld
- -Wl,-O3,--relax
- -Wl,--lto-O3
- -Wl,--lto-whole-program-visibility

**I will probably replace lto full with lto thin, as I suspect lto thin will be more robust.**<br>
**The idea is to create PGO profiles in the future.**

### Security vs Performance trade-off

| Level | Flags | Pipeline cost |
|-------|-------|---------------|
| Maximum performance | `-fno-stack-protector -D_FORTIFY_SOURCE=0` | 0 extra instructions |
| Minimal security | `-fstack-protector -D_FORTIFY_SOURCE=1` | ~1 check per risky function |
| Balanced | `-fstack-protector-strong -D_FORTIFY_SOURCE=2` | ~1 check per function with arrays |
| Maximum security | `-fstack-protector-all -D_FORTIFY_SOURCE=3` | Check on every function call |

Choose based on your threat model and performance requirements.











# **Nordix plans for repo**

**I've been thinking of just trying to get a small repo,<br>
 just to get the system's foundation built for performance.<br>
 This will be relevant later on.**

 **What I show here is only to optimize zver4 to the max.<br>
  My idea is to also do this for CPU architectures: v3 and v4.<br>
  Maybe something intel specific too**

## This is tested and is woking with:
- [**Nordix C-Flags**](/CFLAGS.md)

Tests have been performed with lto full but adjustments or switching to lto thin may be needed.<br>
The idea is to also create PGO profiles in the future for kernel, zfs, compositor, and graphics drivers.

**Nordix Custombuilds - Desktop**
- hyprland-protocols-nordix
- hyprwayland-scanner-nordix
- hyprutils-nordix
- hyprgraphics-nordix
- hyprlang-nordix
- hyprcursor-nordix
- aquamarine-nordix
- xdg-desktop-portal-hyprland-nordix
- hyprwire-nordix
- hyprtoolkit-nordix
- hyprland-nordix
- hyprland-qt-support-nordix
- hyprqt6engine-nordix
- hyprpolkitagent-nordix
- hyprpicker-nordix
- hyprland-guiutils-nordix

## I haven't been able to accomplish this yet with:
- [**Nordix C-Flags**](/CFLAGS.md)
- Mesa
- Proton GE Custom

## Kernel
**I would like to be able to get this linux-taychon kernel with the same optimization**

I haven't managed to get a compile done yet with
- [**Kernel Config**](README-nordix-tachyon-kernel.md)

**However, I have performed tests with good results on the linux-tachyon kernel with less advanced optimizations.**
- clang
- -O3
- znver4
- lto thin

### Linux Tachyon is a beast of a kernel

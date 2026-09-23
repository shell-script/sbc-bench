# Radxa Dragon Q8B
 
Tested with sbc-bench v0.9.72 on Tue, 22 Sep 2026 16:14:21 +0000. Full info: [https://pastebin.com/hwhVPt7v](../hwhVPt7v.txt)
 
### General information:
 
    Information courtesy of cpufetch:
 
    SoC:                 Snapdragon 8cx Gen 3
    Technology:          5nm
    CPU 1:
      Microarchitecture: Cortex-A78C
      Max Frequency:     2.438 GHz
      Cores:             4 cores
      Features:          NEON,SHA1,SHA2,AES,CRC32
    CPU 2:
      Microarchitecture: Cortex-X1C
      Max Frequency:     2.995 GHz
      Cores:             4 cores
      Features:          NEON,SHA1,SHA2,AES,CRC32
 
The CPU features 2 clusters of different core types:
 
    Snapdragon 460 rev 1.1, Qualcomm Snapdragon 8cx Gen 3 (SC8280XP), Kernel: aarch64, Userland: arm64
 
    CPU sysfs topology (clusters, cpufreq members, clockspeeds)
                     cpufreq   min    max
     CPU    cluster  policy   speed  speed   core type
      0        0        0      300    2438   Cortex-A78C / r0p0
      1        0        0      300    2438   Cortex-A78C / r0p0
      2        0        0      300    2438   Cortex-A78C / r0p0
      3        0        0      300    2438   Cortex-A78C / r0p0
      4        0        4      826    2995   Cortex-X1C / r0p0
      5        0        4      826    2995   Cortex-X1C / r0p0
      6        0        4      826    2995   Cortex-X1C / r0p0
      7        0        4      826    2995   Cortex-X1C / r0p0
 
7326 KB available RAM
 
### Governors/policies (performance vs. idle consumption):
 
Original governor settings:
 
    cpufreq-policy0: performance / 2438 MHz (ondemand performance schedutil / 300 403 499 595 691 806 902 1018 1114 1210 1325 1440 1555 1670 1786 1882 1997 2112 2227 2342 2438)
    cpufreq-policy4: performance / 2496 MHz (ondemand performance schedutil / 826 941 1056 1171 1286 1402 1517 1632 1747 1862 1978 2074 2170 2285 2400 2496 2592 2688 2803 2899 2995)
    3d00000.gpu: simple_ondemand / 270 MHz (powersave performance userspace simple_ondemand / 270 410 500 547 606 640 655 690)
 
Tuned governor settings:
 
    cpufreq-policy0: performance / 2438 MHz
    cpufreq-policy4: performance / 2496 MHz
    3d00000.gpu: performance / 690 MHz
 
Status of performance related policies found below /sys:
 
    /sys/module/pcie_aspm/parameters/policy: default [performance] powersave powersupersave
 
### Clockspeeds (idle vs. heated up):
 
Before:
 
    cpu0-cpu3 (Cortex-A78C): OPP: 2438, Measured: 2434 
    cpu4-cpu7 (Cortex-X1C): OPP: 2995, Measured: 2492     (-16.8%)
 
After:
 
    cpu0-cpu3 (Cortex-A78C): OPP: 2438, Measured: 2434 
    cpu4-cpu7 (Cortex-X1C): OPP: 2995, Measured: 2491     (-16.8%)
 
### Performance baseline
 
  * cpu0 (Cortex-A78C): memcpy: 14383.3 MB/s, memchr: 23146.8 MB/s, memset: 38694.7 MB/s
  * cpu4 (Cortex-X1C): memcpy: 16776.3 MB/s, memchr: 25002.0 MB/s, memset: 39157.3 MB/s
  * cpu0 (Cortex-A78C) 16M latency: 72.66 50.39 71.81 51.19 66.34 38.41 32.11 51.58 
  * cpu4 (Cortex-X1C) 16M latency: 48.88 33.10 44.15 33.03 43.65 24.78 28.16 48.23 
  * cpu0 (Cortex-A78C) 128M latency: 169.9 185.2 176.5 177.1 176.6 166.2 124.3 105.2 
  * cpu4 (Cortex-X1C) 128M latency: 165.9 181.2 172.9 173.2 172.9 160.2 121.5 104.4 
  * 7-zip MIPS (3 consecutive runs): 33558, 34106, 34098 (33920 avg), single-threaded: 3672
  * `aes-256-cbc     826995.25k  1181709.63k  1319949.48k  1363190.44k  1370546.18k  1371531.95k (Cortex-A78C)`
  * `aes-256-cbc     958551.67k  1264944.04k  1368466.77k  1401351.85k  1409791.32k  1410820.78k (Cortex-X1C)`
 
### PCIe and storage devices:
 
  * Toshiba Device 0220: Speed 8GT/s, Width x4, driver in use: tc956x_pci, 
  * Toshiba Device 0220: Speed 8GT/s, Width x4, driver in use: tc956x_pci, 
  * 58.9GB "Longsys USD00" UHS-I speed SDR104 SDXC card as /dev/mmcblk0: date 08/2024, manfid/oemid: 0x0000ad/0x4c53, hw/fw rev: 0x2/0x1
  * 32MB MTD device, drivers in use: qcom_scm_storage/qcom_scm
 
### Swap configuration:
 
  * /dev/zram0: 3.6G (1128.5M used, lz4, 9.7M streams, 2.8M data, 4.3M compressed,  total, e[0;91mslowed down by zswap)
 
### Software versions:
 
  * Ubuntu 26.04.1 LTS (resolute)
  * Build scripts: Radxa rbuild: architecture: arm64, build_date: '2026-09-03T11:59:57+00:00', distro_mirror: '', suite: 
  * Compiler: /usr/bin/gcc (Ubuntu 15.2.0-16ubuntu1) 15.2.0 / aarch64-linux-gnu
  * OpenSSL 3.5.5, built on 27 Jan 2026 (Library: OpenSSL 3.5.5 27 Jan 2026)    
 
### Kernel info:
 
  * `/proc/cmdline: root=UUID=d7fc41bd-5c07-41e0-a4a3-b92282f2d11a console=ttyMSM0,115200n8 clk_ignore_unused quiet splash loglevel=4 rw earlycon consoleblank=0 console=tty1 coherent_pool=2M irqchip.gicv3_pseudo_nmi=0 cgroup_enable=cpuset cgroup_memory=1 cgroup_enable=memory swapaccount=1 kasan=off plymouth.enable=0`
  * Vulnerability Spec store bypass:         Mitigation; Speculative Store Bypass disabled via prctl
  * Vulnerability Spectre v1:                Mitigation; __user pointer sanitization
  * Vulnerability Spectre v2:                Mitigation; CSV2, BHB
  * Kernel 7.0.11-6-qcom / CONFIG_HZ=1000
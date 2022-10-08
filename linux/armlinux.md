# 임베디드 시스템 개발에서 사용한 리눅스 버전입니다.
- linux-version
- target board : Atmel

```
Linux buildroot 3.18.0-linux4sam_5.0-alpha5-00009-g23d9de4-dirty #41 Tue Sep 15 09:20:24 KST 2020 armv7l GNU/Linux
```


## linux 시스템 명령어
- addgroup
- cp
- echo
- ip
- login
- mt
- rm
- sync
- adduser
- cpio
- egrep
- ipaddr
- ls
- mv
- rmdir
- tar
- ash
- date
- false
- iplink
- lsattr
- netstat
- run-parts
- touch
- busybox
- dd
- fd
- flush
- iproute
- lsblk
- nice
- sed
- true
- cat
- delgroup
- fgrep
- iprule
- mkdir
- pidof
- setarch
- umount
- catv
- deluser
- getopt
- iptunnel
- mknod
- ping
- setserial
- uname
- chattr
- df
- grep
- kill
- mktemp
- pipe_progress  sh
- usleep
- chgrp
- dmesg
- gunzip
- linux32
- more
- printenv
- sleep
- vi
- chmod
- dnsdomainname
- gzip
- linux64
- mount
- ps
- stty
- watch
- chown
- dumpkmap
- hostname
- ln
- mountpoint
- pwd
- su
- zcat


## Boot Log ( 커널 포팅 관련해서 필요한 로그들만 기본적으로 숙지합니다. )
```
Apr 19 16:15:07 buildroot syslog.info syslogd started: BusyBox v1.20.2
Apr 19 16:15:07 buildroot user.notice kernel: klogd started: BusyBox v1.20.2 (2015-09-30 16:47:43 KST)
Apr 19 16:15:07 buildroot user.info kernel: Booting Linux on physical CPU 0x0
Apr 19 16:15:07 buildroot user.notice kernel: Linux version 3.18.0-linux4sam_5.0-alpha5-00009-g23d9de4-dirty (root@brian--Compaq) (gcc version 4.7.3 (Sourcery CodeBench Lite 2013.05-24) ) #41 Tue Sep 15 09:20:24 KST 2020
Apr 19 16:15:07 buildroot user.info kernel: CPU: ARMv7 Processor [410fc051] revision 1 (ARMv7), cr=10c53c7d
Apr 19 16:15:07 buildroot user.info kernel: CPU: PIPT / VIPT nonaliasing data cache, VIPT aliasing instruction cache
Apr 19 16:15:07 buildroot user.info kernel: Machine model: Atmel SAMA5D3 Xplained
Apr 19 16:15:07 buildroot user.info kernel: cma: Reserved 16 MiB at 0x3e800000
Apr 19 16:15:07 buildroot user.info kernel: Memory policy: Data cache writeback
Apr 19 16:15:07 buildroot user.info kernel: AT91: Detected soc type: sama5d3
Apr 19 16:15:07 buildroot user.info kernel: AT91: Detected soc subtype: sama5d36
Apr 19 16:15:07 buildroot user.debug kernel: On node 0 totalpages: 131072
Apr 19 16:15:07 buildroot user.debug kernel: free_area_init_node: node 0, pgdat c06c0640, node_mem_map dfbf2000
Apr 19 16:15:07 buildroot user.debug kernel:   Normal zone: 1024 pages used for memmap
Apr 19 16:15:07 buildroot user.debug kernel:   Normal zone: 0 pages reserved
Apr 19 16:15:07 buildroot user.debug kernel:   Normal zone: 131072 pages, LIFO batch:31
Apr 19 16:15:07 buildroot user.info kernel: CPU: All CPU(s) started in SVC mode.
Apr 19 16:15:07 buildroot user.debug kernel: pcpu-alloc: s0 r0 d32768 u32768 alloc=1*32768
Apr 19 16:15:07 buildroot user.debug kernel: pcpu-alloc: [0] 0
Apr 19 16:15:07 buildroot user.warn kernel: Built 1 zonelists in Zone order, mobility grouping on.  Total pages: 130048
Apr 19 16:15:07 buildroot user.notice kernel: Kernel command line: console=ttyS0,115200 earlyprintk mtdparts=atmel_nand:256k(bootstrap)ro,512k(uboot)ro,256K(env),256k(evn_redundent),256k(spare),512k(dtb),6M(kernel)ro,-(rootfs) rootfstype=ubifs ubi.mtd=7 root=ubi0:rootfs
Apr 19 16:15:07 buildroot user.info kernel: PID hash table entries: 2048 (order: 1, 8192 bytes)
Apr 19 16:15:07 buildroot user.info kernel: Dentry cache hash table entries: 65536 (order: 6, 262144 bytes)
Apr 19 16:15:07 buildroot user.info kernel: Inode-cache hash table entries: 32768 (order: 5, 131072 bytes)
Apr 19 16:15:07 buildroot user.warn kernel: Memory: 496100K/524288K available (4937K kernel code, 228K rwdata, 1524K rodata, 192K init, 169K bss, 28188K reserved)
Apr 19 16:15:07 buildroot user.notice kernel: Virtual kernel memory layout:
Apr 19 16:15:07 buildroot user.notice kernel:     vector  : 0xffff0000 - 0xffff1000   (   4 kB)
Apr 19 16:15:07 buildroot user.notice kernel:     fixmap  : 0xffc00000 - 0xffe00000   (2048 kB)
Apr 19 16:15:07 buildroot user.notice kernel:     vmalloc : 0xe0800000 - 0xff000000   ( 488 MB)
Apr 19 16:15:07 buildroot user.notice kernel:     lowmem  : 0xc0000000 - 0xe0000000   ( 512 MB)
Apr 19 16:15:07 buildroot user.notice kernel:     modules : 0xbf000000 - 0xc0000000   (  16 MB)
Apr 19 16:15:07 buildroot user.notice kernel:       .text : 0xc0008000 - 0xc06577d8   (6462 kB)
Apr 19 16:15:07 buildroot user.notice kernel:       .init : 0xc0658000 - 0xc0688000   ( 192 kB)
Apr 19 16:15:07 buildroot user.notice kernel:       .data : 0xc0688000 - 0xc06c1288   ( 229 kB)
Apr 19 16:15:07 buildroot user.notice kernel:        .bss : 0xc06c1288 - 0xc06eb6f8   ( 170 kB)
Apr 19 16:15:07 buildroot user.info kernel: NR_IRQS:16 nr_irqs:16 16
Apr 19 16:15:07 buildroot user.info kernel: sched_clock: 32 bits at 1kHz, resolution 1000000ns, wraps every 2147483648000000ns
Apr 19 16:15:07 buildroot user.info kernel: Console: colour dummy device 80x30
Apr 19 16:15:07 buildroot user.info kernel: Calibrating delay loop... 348.16 BogoMIPS (lpj=174080)
Apr 19 16:15:07 buildroot user.info kernel: pid_max: default: 32768 minimum: 301
Apr 19 16:15:07 buildroot user.info kernel: Mount-cache hash table entries: 1024 (order: 0, 4096 bytes)
Apr 19 16:15:07 buildroot user.info kernel: Mountpoint-cache hash table entries: 1024 (order: 0, 4096 bytes)
Apr 19 16:15:07 buildroot user.info kernel: CPU: Testing write buffer coherency: ok
Apr 19 16:15:07 buildroot user.info kernel: Setting up static identity map for 0x204aec08 - 0x204aec60
Apr 19 16:15:07 buildroot user.info kernel: devtmpfs: initialized
Apr 19 16:15:07 buildroot user.info kernel: VFP support v0.3: implementor 41 architecture 2 part 30 variant 5 rev 1
Apr 19 16:15:07 buildroot user.info kernel: pinctrl core: initialized pinctrl subsystem
Apr 19 16:15:07 buildroot user.info kernel: regulator-dummy: no parameters
Apr 19 16:15:07 buildroot user.info kernel: NET: Registered protocol family 16
Apr 19 16:15:07 buildroot user.info kernel: DMA: preallocated 256 KiB pool for atomic coherent allocations
Apr 19 16:15:07 buildroot user.info kernel: cpuidle: using governor ladder
Apr 19 16:15:07 buildroot user.info kernel: cpuidle: using governor menu
Apr 19 16:15:07 buildroot user.info kernel: gpio-at91 fffff200.gpio: at address fefff200
Apr 19 16:15:07 buildroot user.info kernel: gpio-at91 fffff400.gpio: at address fefff400
Apr 19 16:15:07 buildroot user.info kernel: gpio-at91 fffff600.gpio: at address fefff600
Apr 19 16:15:07 buildroot user.info kernel: gpio-at91 fffff800.gpio: at address fefff800
Apr 19 16:15:07 buildroot user.info kernel: gpio-at91 fffffa00.gpio: at address fefffa00
Apr 19 16:15:07 buildroot user.info kernel: pinctrl-at91 ahb:apb:pinctrl@fffff200: initialized AT91 pinctrl driver
Apr 19 16:15:07 buildroot user.debug kernel: tcb_clksrc: tc0 at 16.000 MHz
Apr 19 16:15:07 buildroot user.info kernel: at_hdmac ffffe600.dma-controller: Atmel AHB DMA Controller ( cpy slave sg-cpy ), 8 channels
Apr 19 16:15:07 buildroot user.info kernel: at_hdmac ffffe800.dma-controller: Atmel AHB DMA Controller ( cpy slave sg-cpy ), 8 channels
Apr 19 16:15:07 buildroot user.notice kernel: SCSI subsystem initialized
Apr 19 16:15:07 buildroot user.info kernel: usbcore: registered new interface driver usbfs
Apr 19 16:15:07 buildroot user.info kernel: usbcore: registered new interface driver hub
Apr 19 16:15:07 buildroot user.info kernel: usbcore: registered new device driver usb
Apr 19 16:15:07 buildroot user.info kernel: at91_i2c f0018000.i2c: using dma0chan0 (tx) and dma0chan1 (rx) for DMA transfers
Apr 19 16:15:07 buildroot user.info kernel: at91_i2c f0018000.i2c: AT91 i2c bus driver (hw version: 0x402).
Apr 19 16:15:07 buildroot user.info kernel: at91_i2c f801c000.i2c: using dma1chan0 (tx) and dma1chan1 (rx) for DMA transfers
Apr 19 16:15:07 buildroot user.info kernel: at91_i2c f801c000.i2c: AT91 i2c bus driver (hw version: 0x402).
Apr 19 16:15:07 buildroot user.info kernel: Linux video capture interface: v2.00
Apr 19 16:15:07 buildroot user.info kernel: Advanced Linux Sound Architecture Driver Initialized.
Apr 19 16:15:07 buildroot user.info kernel: cfg80211: Calling CRDA to update world regulatory domain
Apr 19 16:15:07 buildroot user.info kernel: Switched to clocksource tcb_clksrc
Apr 19 16:15:07 buildroot user.info kernel: NET: Registered protocol family 2
Apr 19 16:15:07 buildroot user.info kernel: TCP established hash table entries: 4096 (order: 2, 16384 bytes)
Apr 19 16:15:07 buildroot user.info kernel: TCP bind hash table entries: 4096 (order: 2, 16384 bytes)
Apr 19 16:15:07 buildroot user.info kernel: TCP: Hash tables configured (established 4096 bind 4096)
Apr 19 16:15:07 buildroot user.info kernel: TCP: reno registered
Apr 19 16:15:07 buildroot user.info kernel: UDP hash table entries: 256 (order: 0, 4096 bytes)
Apr 19 16:15:07 buildroot user.info kernel: UDP-Lite hash table entries: 256 (order: 0, 4096 bytes)
Apr 19 16:15:07 buildroot user.info kernel: NET: Registered protocol family 1
Apr 19 16:15:07 buildroot user.info kernel: RPC: Registered named UNIX socket transport module.
Apr 19 16:15:07 buildroot user.info kernel: RPC: Registered udp transport module.
Apr 19 16:15:07 buildroot user.info kernel: RPC: Registered tcp transport module.
Apr 19 16:15:07 buildroot user.info kernel: RPC: Registered tcp NFSv4.1 backchannel transport module.
Apr 19 16:15:07 buildroot user.info kernel: futex hash table entries: 256 (order: -1, 3072 bytes)
Apr 19 16:15:07 buildroot user.info kernel: msgmni has been set to 1000
Apr 19 16:15:07 buildroot user.info kernel: io scheduler noop registered (default)
Apr 19 16:15:07 buildroot user.info kernel: atmel_usart f001c000.serial: ttyS1 at MMIO 0xf001c000 (irq = 29, base_baud = 4125000) is a ATMEL_SERIAL
Apr 19 16:15:07 buildroot user.info kernel: atmel_usart f0020000.serial: ttyS2 at MMIO 0xf0020000 (irq = 30, base_baud = 4125000) is a ATMEL_SERIAL
Apr 19 16:15:07 buildroot user.info kernel: atmel_usart f0024000.serial: ttyS3 at MMIO 0xf0024000 (irq = 31, base_baud = 4125000) is a ATMEL_SERIAL
Apr 19 16:15:07 buildroot user.info kernel: atmel_usart f8020000.serial: ttyS5 at MMIO 0xf8020000 (irq = 37, base_baud = 4125000) is a ATMEL_SERIAL
Apr 19 16:15:07 buildroot user.info kernel: atmel_usart f8024000.serial: ttyS4 at MMIO 0xf8024000 (irq = 38, base_baud = 4125000) is a ATMEL_SERIAL
Apr 19 16:15:07 buildroot user.info kernel: atmel_usart ffffee00.serial: ttyS0 at MMIO 0xffffee00 (irq = 44, base_baud = 8250000) is a ATMEL_SERIAL
Apr 19 16:15:07 buildroot user.info kernel: console [ttyS0] enabled
Apr 19 16:15:07 buildroot user.info kernel: atmel_usart f8028000.serial: ttyS6 at MMIO 0xf8028000 (irq = 55, base_baud = 4125000) is a ATMEL_SERIAL
Apr 19 16:15:07 buildroot user.info kernel: [drm] Initialized drm 1.1.0 20060810
Apr 19 16:15:07 buildroot user.info kernel: brd: module loaded
Apr 19 16:15:07 buildroot user.info kernel: loop: module loaded
Apr 19 16:15:07 buildroot user.info kernel: atmel_nand_nfc 70000000.nfc: NFC is probed.
Apr 19 16:15:07 buildroot user.info kernel: atmel_nand 60000000.nand: Use On Flash BBT
Apr 19 16:15:07 buildroot user.info kernel: atmel_nand 60000000.nand: Using dma0chan2 for DMA transfers.
Apr 19 16:15:07 buildroot user.info kernel: nand: device found, Manufacturer ID: 0x2c, Chip ID: 0xda
Apr 19 16:15:07 buildroot user.info kernel: nand: Micron MT29F2G08ABAEAWP
Apr 19 16:15:07 buildroot user.info kernel: nand: 256MiB, SLC, page size: 2048, OOB size: 64
Apr 19 16:15:07 buildroot user.info kernel: atmel_nand 60000000.nand: minimum ECC: 4 bits in 512 bytes
Apr 19 16:15:07 buildroot user.info kernel: atmel_nand 60000000.nand: Initialize PMECC params, cap: 4, sector: 512
Apr 19 16:15:07 buildroot user.info kernel: atmel_nand 60000000.nand: Using NFC Sram read
Apr 19 16:15:07 buildroot user.info kernel: Bad block table found at page 131008, version 0x01
Apr 19 16:15:07 buildroot user.info kernel: Bad block table found at page 130944, version 0x01
Apr 19 16:15:07 buildroot user.notice kernel: 8 cmdlinepart partitions found on MTD device atmel_nand
Apr 19 16:15:07 buildroot user.notice kernel: Creating 8 MTD partitions on "atmel_nand":
Apr 19 16:15:07 buildroot user.notice kernel: 0x000000000000-0x000000040000 : "bootstrap"
Apr 19 16:15:07 buildroot user.notice kernel: 0x000000040000-0x0000000c0000 : "uboot"
Apr 19 16:15:07 buildroot user.notice kernel: 0x0000000c0000-0x000000100000 : "env"
Apr 19 16:15:07 buildroot user.notice kernel: 0x000000100000-0x000000140000 : "evn_redundent"
Apr 19 16:15:07 buildroot user.notice kernel: 0x000000140000-0x000000180000 : "spare"
Apr 19 16:15:07 buildroot user.notice kernel: 0x000000180000-0x000000200000 : "dtb"
Apr 19 16:15:07 buildroot user.notice kernel: 0x000000200000-0x000000800000 : "kernel"
Apr 19 16:15:07 buildroot user.notice kernel: 0x000000800000-0x000010000000 : "rootfs"
Apr 19 16:15:07 buildroot user.info kernel: atmel_spi f0004000.spi: version: 0x213
Apr 19 16:15:07 buildroot user.info kernel: atmel_spi f0004000.spi: Using dma0chan3 (tx) and dma0chan4 (rx) for DMA transfers
Apr 19 16:15:07 buildroot user.info kernel: atmel_spi f0004000.spi: Atmel SPI Controller at 0xf0004000 (irq 26)
Apr 19 16:15:07 buildroot user.info kernel: atmel_spi f8008000.spi: version: 0x213
Apr 19 16:15:07 buildroot user.info kernel: atmel_spi f8008000.spi: Using dma1chan2 (tx) and dma1chan3 (rx) for DMA transfers
Apr 19 16:15:07 buildroot user.info kernel: atmel_spi f8008000.spi: Atmel SPI Controller at 0xf8008000 (irq 34)
Apr 19 16:15:07 buildroot user.info kernel: CAN device driver interface
Apr 19 16:15:07 buildroot user.info kernel: at91_can f000c000.can: device registered (reg_base=e0828000, irq=51)
Apr 19 16:15:07 buildroot user.info kernel: libphy: MACB_mii_bus: probed
Apr 19 16:15:07 buildroot user.info kernel: macb f0028000.ethernet eth0: Cadence GEM rev 0x00020119 at 0xf0028000 irq 52 (04:91:62:fd:7a:d7)
Apr 19 16:15:07 buildroot user.info kernel: macb f0028000.ethernet eth0: attached PHY driver [Micrel KSZ9031 Gigabit PHY] (mii_bus:phy_addr=f0028000.etherne:07, irq=-1)
Apr 19 16:15:07 buildroot user.info kernel: libphy: MACB_mii_bus: probed
Apr 19 16:15:07 buildroot user.info kernel: macb f802c000.ethernet eth1: Cadence MACB rev 0x0001010c at 0xf802c000 irq 53 (04:91:62:fd:dc:ec)
Apr 19 16:15:07 buildroot user.info kernel: macb f802c000.ethernet eth1: attached PHY driver [Micrel KSZ8081 or KSZ8091] (mii_bus:phy_addr=f802c000.etherne:01, irq=-1)
Apr 19 16:15:07 buildroot user.info kernel: ehci_hcd: USB 2.0 'Enhanced' Host Controller (EHCI) Driver
Apr 19 16:15:07 buildroot user.info kernel: ehci-atmel: EHCI Atmel driver
Apr 19 16:15:07 buildroot user.info kernel: atmel-ehci 700000.ehci: EHCI Host Controller
Apr 19 16:15:07 buildroot user.info kernel: atmel-ehci 700000.ehci: new USB bus registered, assigned bus number 1
Apr 19 16:15:07 buildroot user.info kernel: atmel-ehci 700000.ehci: irq 57, io mem 0x00700000
Apr 19 16:15:07 buildroot user.info kernel: atmel-ehci 700000.ehci: USB 2.0 started, EHCI 1.00
Apr 19 16:15:07 buildroot user.info kernel: usb usb1: New USB device found, idVendor=1d6b, idProduct=0002
Apr 19 16:15:07 buildroot user.info kernel: usb usb1: New USB device strings: Mfr=3, Product=2, SerialNumber=1
Apr 19 16:15:07 buildroot user.info kernel: usb usb1: Product: EHCI Host Controller
Apr 19 16:15:07 buildroot user.info kernel: usb usb1: Manufacturer: Linux 3.18.0-linux4sam_5.0-alpha5-00009-g23d9de4-dirty ehci_hcd
Apr 19 16:15:07 buildroot user.info kernel: usb usb1: SerialNumber: 700000.ehci
Apr 19 16:15:07 buildroot user.info kernel: hub 1-0:1.0: USB hub found
Apr 19 16:15:07 buildroot user.info kernel: hub 1-0:1.0: 3 ports detected
Apr 19 16:15:07 buildroot user.info kernel: ohci_hcd: USB 1.1 'Open' Host Controller (OHCI) Driver
Apr 19 16:15:07 buildroot user.info kernel: ohci-atmel: OHCI Atmel driver
Apr 19 16:15:07 buildroot user.info kernel: pdata->vbus_pin[0]=fffffffe
Apr 19 16:15:07 buildroot user.info kernel: pdata->vbus_pin[1]=1e
Apr 19 16:15:07 buildroot user.info kernel: pdata->vbus_pin[2]=19
Apr 19 16:15:07 buildroot user.info kernel: at91_ohci 600000.ohci: USB Host Controller
Apr 19 16:15:07 buildroot user.info kernel: at91_ohci 600000.ohci: new USB bus registered, assigned bus number 2
Apr 19 16:15:07 buildroot user.info kernel: at91_ohci 600000.ohci: irq 57, io mem 0x00600000
Apr 19 16:15:07 buildroot user.info kernel: usb usb2: New USB device found, idVendor=1d6b, idProduct=0001
Apr 19 16:15:07 buildroot user.info kernel: usb usb2: New USB device strings: Mfr=3, Product=2, SerialNumber=1
Apr 19 16:15:07 buildroot user.info kernel: usb usb2: Product: USB Host Controller
Apr 19 16:15:07 buildroot user.info kernel: usb usb2: Manufacturer: Linux 3.18.0-linux4sam_5.0-alpha5-00009-g23d9de4-dirty ohci_hcd
Apr 19 16:15:07 buildroot user.info kernel: usb usb2: SerialNumber: at91
Apr 19 16:15:07 buildroot user.info kernel: hub 2-0:1.0: USB hub found
Apr 19 16:15:07 buildroot user.info kernel: hub 2-0:1.0: 3 ports detected
Apr 19 16:15:07 buildroot user.info kernel: usbcore: registered new interface driver cdc_acm
Apr 19 16:15:07 buildroot user.info kernel: cdc_acm: USB Abstract Control Model driver for USB modems and ISDN adapters
Apr 19 16:15:07 buildroot user.info kernel: usbcore: registered new interface driver usb-storage
Apr 19 16:15:07 buildroot user.info kernel: usbcore: registered new interface driver usbserial
Apr 19 16:15:07 buildroot user.info kernel: usbcore: registered new interface driver usbserial_generic
Apr 19 16:15:07 buildroot user.info kernel: usbserial: USB Serial support registered for generic
Apr 19 16:15:07 buildroot user.info kernel: usbcore: registered new interface driver ftdi_sio
Apr 19 16:15:07 buildroot user.info kernel: usbserial: USB Serial support registered for FTDI USB Serial Device
Apr 19 16:15:07 buildroot user.info kernel: usbcore: registered new interface driver pl2303
Apr 19 16:15:07 buildroot user.info kernel: usbserial: USB Serial support registered for pl2303
Apr 19 16:15:07 buildroot user.info kernel: atmel_usba_udc 500000.gadget: MMIO registers at 0xf8030000 mapped at e0830000
Apr 19 16:15:07 buildroot user.info kernel: atmel_usba_udc 500000.gadget: FIFO at 0x00500000 mapped at e2200000
Apr 19 16:15:07 buildroot user.info kernel: rtc-ds1307 2-0068: rtc core: registered ds1388 as rtc0
Apr 19 16:15:07 buildroot user.info kernel: i2c /dev entries driver
Apr 19 16:15:07 buildroot user.info kernel: AT91: Starting after watchdog reset
Apr 19 16:15:07 buildroot user.info kernel: at91sam9_wdt: enabled (heartbeat=15 sec, nowayout=0)
Apr 19 16:15:07 buildroot user.info kernel: atmel_mci f0000000.mmc: version: 0x505
Apr 19 16:15:07 buildroot user.info kernel: atmel_mci f0000000.mmc: using dma0chan5 for DMA transfers
Apr 19 16:15:07 buildroot user.info kernel: atmel_mci f0000000.mmc: No vmmc regulator found
Apr 19 16:15:07 buildroot user.info kernel: atmel_mci f0000000.mmc: No vqmmc regulator found
Apr 19 16:15:07 buildroot user.info kernel: atmel_mci f0000000.mmc: Atmel MCI controller at 0xf0000000 irq 25, 1 slots
Apr 19 16:15:07 buildroot user.info kernel: atmel_mci f8000000.mmc: version: 0x505
Apr 19 16:15:07 buildroot user.info kernel: atmel_mci f8000000.mmc: using dma1chan4 for DMA transfers
Apr 19 16:15:07 buildroot user.info kernel: atmel_mci f8000000.mmc: No vmmc regulator found
Apr 19 16:15:07 buildroot user.info kernel: atmel_mci f8000000.mmc: No vqmmc regulator found
Apr 19 16:15:07 buildroot user.info kernel: atmel_mci f8000000.mmc: Atmel MCI controller at 0xf8000000 irq 33, 1 slots
Apr 19 16:15:07 buildroot user.info kernel: atmel_aes f8038000.aes: version: 0x135
Apr 19 16:15:07 buildroot user.info kernel: atmel_aes f8038000.aes: Atmel AES - Using dma1chan5, dma1chan6 for DMA transfers
Apr 19 16:15:07 buildroot user.info kernel: atmel_sha f8034000.sha: version: 0x410
Apr 19 16:15:07 buildroot user.info kernel: atmel_sha f8034000.sha: using dma1chan7 for DMA transfers
Apr 19 16:15:07 buildroot user.info kernel: atmel_sha f8034000.sha: Atmel SHA1/SHA256/SHA224/SHA384/SHA512
Apr 19 16:15:07 buildroot user.info kernel: atmel_tdes f803c000.tdes: version: 0x701
Apr 19 16:15:07 buildroot user.warn kernel: atmel_tdes f803c000.tdes: no DMA channel available
Apr 19 16:15:07 buildroot user.err kernel: atmel_tdes f803c000.tdes: initialization failed.
Apr 19 16:15:07 buildroot user.warn kernel: atmel_tdes: probe of f803c000.tdes failed with error -12
Apr 19 16:15:07 buildroot user.info kernel: usbcore: registered new interface driver usbhid
Apr 19 16:15:07 buildroot user.info kernel: usbhid: USB HID core driver
Apr 19 16:15:07 buildroot user.info kernel: iio iio:device0: Resolution used: 12 bits
Apr 19 16:15:07 buildroot user.info kernel: iio iio:device0: ADC Touch screen is disabled.
Apr 19 16:15:07 buildroot user.info kernel: TCP: cubic registered
Apr 19 16:15:07 buildroot user.info kernel: NET: Registered protocol family 10
Apr 19 16:15:07 buildroot user.info kernel: sit: IPv6 over IPv4 tunneling driver
Apr 19 16:15:07 buildroot user.info kernel: NET: Registered protocol family 17
Apr 19 16:15:07 buildroot user.info kernel: can: controller area network core (rev 20120528 abi 9)
Apr 19 16:15:07 buildroot user.info kernel: NET: Registered protocol family 29
Apr 19 16:15:07 buildroot user.info kernel: can: raw protocol (rev 20120528)
Apr 19 16:15:07 buildroot user.info kernel: can: broadcast manager protocol (rev 20120528 t)
Apr 19 16:15:07 buildroot user.info kernel: can: netlink gateway (rev 20130117) max_hops=1
Apr 19 16:15:07 buildroot user.notice kernel: UBI: attaching mtd7 to ubi0
Apr 19 16:15:07 buildroot user.warn kernel: mmc0: host does not support reading read-only switch, assuming write-enable
Apr 19 16:15:07 buildroot user.info kernel: mmc0: new high speed SDHC card at address e624
Apr 19 16:15:07 buildroot user.info kernel: mmcblk0: mmc0:e624 SS08G 7.40 GiB
Apr 19 16:15:07 buildroot user.info kernel:  mmcblk0: p1
Apr 19 16:15:07 buildroot user.warn kernel: mmc1: host does not support reading read-only switch, assuming write-enable
Apr 19 16:15:07 buildroot user.info kernel: mmc1: new high speed SDHC card at address aaaa
Apr 19 16:15:07 buildroot user.info kernel: mmcblk1: mmc1:aaaa SC32G 29.7 GiB
Apr 19 16:15:07 buildroot user.info kernel:  mmcblk1: p1
Apr 19 16:15:07 buildroot user.notice kernel: random: nonblocking pool is initialized
Apr 19 16:15:07 buildroot user.notice kernel: UBI: scanning is finished
Apr 19 16:15:07 buildroot user.notice kernel: UBI: attached mtd7 (name "rootfs", size 248 MiB) to ubi0
Apr 19 16:15:07 buildroot user.notice kernel: UBI: PEB size: 131072 bytes (128 KiB), LEB size: 126976 bytes
Apr 19 16:15:07 buildroot user.notice kernel: UBI: min./max. I/O unit sizes: 2048/2048, sub-page size 2048
Apr 19 16:15:07 buildroot user.notice kernel: UBI: VID header offset: 2048 (aligned 2048), data offset: 4096
Apr 19 16:15:07 buildroot user.notice kernel: UBI: good PEBs: 1980, bad PEBs: 4, corrupted PEBs: 0
Apr 19 16:15:07 buildroot user.notice kernel: UBI: user volume: 1, internal volumes: 1, max. volumes count: 128
Apr 19 16:15:07 buildroot user.notice kernel: UBI: max/mean erase counter: 13/3, WL threshold: 4096, image sequence number: 1184744293
Apr 19 16:15:07 buildroot user.notice kernel: UBI: available PEBs: 0, total reserved PEBs: 1980, PEBs reserved for bad PEB handling: 36
Apr 19 16:15:07 buildroot user.notice kernel: UBI: background thread "ubi_bgt0d" started, PID 635
Apr 19 16:15:07 buildroot user.info kernel: input: gpio_keys as /devices/gpio_keys/input/input0
Apr 19 16:15:07 buildroot user.info kernel: rtc-ds1307 2-0068: setting system clock to 2022-04-19 16:15:06 UTC (1650384906)
Apr 19 16:15:07 buildroot user.info kernel: ALSA device list:
Apr 19 16:15:07 buildroot user.info kernel:   No soundcards found.
Apr 19 16:15:07 buildroot user.notice kernel: UBIFS: recovery needed
Apr 19 16:15:07 buildroot user.notice kernel: UBIFS: recovery deferred
Apr 19 16:15:07 buildroot user.notice kernel: UBIFS: mounted UBI device 0, volume 0, name "rootfs", R/O mode
Apr 19 16:15:07 buildroot user.notice kernel: UBIFS: LEB size: 126976 bytes (124 KiB), min./max. I/O unit sizes: 2048 bytes/2048 bytes
Apr 19 16:15:07 buildroot user.notice kernel: UBIFS: FS size: 244936704 bytes (233 MiB, 1929 LEBs), journal size 9023488 bytes (8 MiB, 72 LEBs)
Apr 19 16:15:07 buildroot user.notice kernel: UBIFS: reserved for root: 0 bytes (0 KiB)
Apr 19 16:15:07 buildroot user.notice kernel: UBIFS: media format: w4/r0 (latest is w4/r0), UUID 54E959B5-BC50-4926-AA69-F2D8EAFB0DE4, small LPT model
Apr 19 16:15:07 buildroot user.info kernel: VFS: Mounted root (ubifs filesystem) readonly on device 0:13.
Apr 19 16:15:07 buildroot user.info kernel: devtmpfs: mounted
Apr 19 16:15:07 buildroot user.info kernel: Freeing unused kernel memory: 192K (c0658000 - c0688000)
Apr 19 16:15:07 buildroot user.notice kernel: UBIFS: completing deferred recovery
Apr 19 16:15:07 buildroot user.notice kernel: UBIFS: background thread "ubifs_bgt0_0" started, PID 647
Apr 19 16:15:07 buildroot user.notice kernel: UBIFS: deferred recovery completed
Apr 19 16:15:08 buildroot user.warn kernel: Registered TMIO character driver
Apr 19 16:15:08 buildroot user.warn kernel: ^M
Apr 19 16:15:08 buildroot user.err kernel: 0>udevd[667]: starting version 182
Apr 19 16:15:08 buildroot daemon.err udevd[667]: specified group 'dialout' unknown
Apr 19 16:15:08 buildroot daemon.err udevd[667]: specified group 'kmem' unknown
Apr 19 16:15:08 buildroot daemon.err udevd[667]: specified group 'video' unknown
Apr 19 16:15:08 buildroot daemon.err udevd[667]: specified group 'lp' unknown
Apr 19 16:15:08 buildroot daemon.err udevd[667]: specified group 'floppy' unknown
Apr 19 16:15:08 buildroot daemon.err udevd[667]: specified group 'cdrom' unknown
Apr 19 16:15:08 buildroot daemon.err udevd[667]: specified group 'tape' unknown
Apr 19 16:15:10 buildroot user.info kernel: IPv6: ADDRCONF(NETDEV_UP): eth1: link is not ready
Apr 19 16:15:10 buildroot user.info kernel: IPv6: ADDRCONF(NETDEV_UP): eth0: link is not ready
Apr 19 16:15:10 buildroot user.info kernel: atmel_nand 60000000.nand: Bit flip in data area, byte_pos: 1323, bit_pos: 7, 0x8e -> 0x0e
Apr 19 16:15:10 buildroot user.info kernel: atmel_nand 60000000.nand: Bit flip in data area, byte_pos: 1323, bit_pos: 7, 0x8e -> 0x0e
Apr 19 16:15:10 buildroot daemon.info init: starting pid 728, tty '': '/app/startup'
Apr 19 16:15:10 buildroot auth.info sshd[726]: Server listening on 0.0.0.0 port 22.
Apr 19 16:15:10 buildroot auth.info sshd[726]: Server listening on :: port 22.
Apr 19 16:15:12 buildroot user.info kernel: macb f0028000.ethernet eth0: link up (100/Full)
Apr 19 16:15:12 buildroot user.info kernel: IPv6: ADDRCONF(NETDEV_CHANGE): eth0: link becomes ready
Apr 19 16:15:14 buildroot user.warn kernel: FAT-fs (mmcblk0p1): Volume was not properly unmounted. Some data may be corrupt. Please run fsck.
Apr 19 16:15:14 buildroot user.warn kernel: FAT-fs (mmcblk1p1): Volume was not properly unmounted. Some data may be corrupt. Please run fsck.
Apr 19 16:15:16 buildroot daemon.info init: starting pid 818, tty '/dev/ttyS0': '/sbin/getty -L ttyS0 115200 vt100 '
Apr 19 16:21:22 buildroot auth.info sshd[1740]: Accepted password for root from 211.221.247.231 port 57833 ssh2
Apr 19 16:21:43 buildroot user.info kernel: atmel_nand 60000000.nand: Bit flip in data area, byte_pos: 860, bit_pos: 6, 0x47 -> 0x07
Apr 19 16:22:17 buildroot user.err kernel: UBI error: ubi_open_volume: cannot open device 0, volume 0, error -16
Apr 19 16:26:53 buildroot user.err kernel: UBI error: ubi_open_volume: cannot open device 0, volume 0, error -16
Apr 19 16:29:48 buildroot user.err kernel: UBI error: ubi_open_volume: cannot open device 0, volume 0, error -16
Apr 19 16:29:48 buildroot user.err kernel: UBI error: ubi_open_volume: cannot open device 0, volume 0, error -16
Apr 19 16:40:01 buildroot auth.info sshd[4618]: Accepted password for root from 211.221.247.231 port 58173 ssh2
Apr 19 16:52:20 buildroot auth.info sshd[6514]: Accepted password for root from 211.221.247.231 port 58361 ssh2
Apr 19 16:53:29 buildroot auth.info sshd[6700]: Accepted password for root from 211.221.247.231 port 58371 ssh2
```

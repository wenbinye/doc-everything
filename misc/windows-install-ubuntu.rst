Windows 硬盘安装 Ubuntu
==============================

1. 下载 grub4dos
2. 下载 ubuntu 安装盘

目录结构 ::

    [-] C:/
     |-[+] $Recycle.Bin
     |-[+] Documents and Settings
     |-[+] Intel
     |-[+] MSOCache
     |-[+] PerfLogs
     |-[+] Program Files
     |-[+] Program Files (x86)
     |-[+] ProgramData
     |-[+] Programs
     |-[+] Recovery
     |-[+] System Volume Information
     |-[+] Users
     |-[+] Windows
     |-  boot.ini
     |-  grldr
     |-  grldr.mbr
     |-  grub.exe
     |-  hiberfil.sys
     |-  initrd.lz
     |-  menu.lst
     |-  pagefile.sys
     |-  ubuntu.iso
     `-  vmlinuz.efi

menu.lst 中加入 ::

    title install ubuntu
    root (hd0,0)
    kernel /vmlinuz.efi boot=casper iso-scan/filename=/ubuntu.iso ro quiet splash locale=zh_CN.UTF-8
    initrd /initrd.lz

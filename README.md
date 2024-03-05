# Here is my approach to protect a PC from common security threats.
1. Replace proprietary BIOS with coreboot (https://github.com/merge/skulls).
2. Secure boot with password and USB stick.
2. OS Gentoo Linux stable relase with open source licensies. Full recompilation. Non systemd. Non root Xorg.
3. Linux kernel compilation with disabled loadable modules and security hardening, such as:
- Strong Stack Protector
- Randomize kernel structures
- Initialize heap memory with zeroes
- Enable debuging kernel data structures
- Other security tweeks, according to hardeing guides such as "Kernel Self Protection Project".
4. Build firmware blobs into the kernel binary, when there is no open source alternative patches for kernel.
5. Full disk encryption with LUKS (Linux Unified Key Setup). Key is a several megabyte file encrypted with AES256 symmetric-key. This key placed at USB stick and used during initramfs loading to decrypt LVM disks with LUKS aes-xts-plain64 algorithm.
6. Hardening /etc/fstab
- proc /proc proc hidepid=2,nosuid,noexec,gid=wheel
- separate partition /home with mount options noexec,nosuid,nodev
7. Simple firewall with iptables or nftables. No log analyzer.
8. Install POSIX Capabilities and active secure computing mode (USE="caps seccomp").
9. Logging under root activated, sudo for root deactivated.
10. Reduce attack surface - look for alterniatives before install libraries and applications with bloated dependencies.
11. Application isolation: Separate user for every big application. Firejail with carefully crafted configurations to prevent keylogging and information gathering. GUI isolation.
12. By timeout, disable USB ports and block screen. Never connect or charge smartphone with USB.
13. Backup of root directory every 6 month with ```tar --exclude-from=backup_exclude.txt --acl --xattrs -cpzvf /mnt/backup/backup-$(date +%F).tar.gz /```

Browser:
- VPN over Tor per application
- Firefox or TorBrowser
- User-Agent changer
- Hide all fingerprints: Canvas, Fonts, TimeZone
- Disable some of the browser functionality (user.json)
- Disable insecure SSL ciphers, rise up version
- Disable JavaScript whenever it is possible

Others:
1. Hide DNS requests with proxy.
2. Never share personal or sensitive information with centralized LLMs like ChatGPT, don't ask it to fix errors in letters.
3. Don't keep sensisitve information or passwords on cheep smartphones, don't install sensitive applications.

Fundamentals of anonymity at the Internet:
1. Anonymous registration.
2. Keeping predefinded fields for personal information clear.

Threat model:
1. Goverments - communication channels, data gathering
2. Corporations - software and hardware backdoors, data gathering
3. Individuals - fake information, vulnerabilities exploitation

# Here is my approach to protect a PC from common security threats.
1. Replace proprietary BIOS with coreboot (https://github.com/merge/skulls).
2. Secure boot with password at USB stick. Main password should not be visible and located at opened machine.
2. OS Gentoo Linux stable relase with open source licensies. Full recompilation. Non systemd. Non root Xorg.
3. Linux kernel compilation with disabled loadable modules and security hardening, such as:
- Strong Stack Protector
- Randomize kernel structures
- Initialize heap memory with zeroes
- Enable debuging kernel data structures
- Other security tweeks, according to hardeing guides such as "Kernel Self Protection Project".
4. Driver installation: find source code and patch sources of kernel. At least disable modules and put firmware driver in kernel.
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
14. Keeping passwords in several encrypted files, unencrypt by necessity with entering password outside of window manager.
15. Solution to problem "Fediverse: how to share personal data and stay anonymous?":
   1) store information at services that don't leak data to anyone expect selected persons (not public) and allow to remove all with one button, sync local copy to remote.
   2) split public anonymous information by several separate platforms, give all contacts together only to selected persons.

# Browser:
- VPN over Tor per application
- Firefox or TorBrowser
- User-Agent changer
- Hide all fingerprints: Canvas, Fonts, TimeZone
- Disable some of the browser functionality (user.json)
- Disable insecure SSL ciphers, rise up version
- Disable JavaScript whenever it is possible

# Smartphones
- To isolate applications use two smartphones one for connection to the Internet and phone calls, other for VPN with applications.
- Consider F-Droid or download APK directly from github with binary comparision from different proxies.

# Fundamentals of privacy at the Internet:
1. Anonymous registration. At least, having two emails for registrations and for conversations.
2. Keeping predefinded fields for personal information clear.
3. Different communication channels for different services.
4. For fingerprints, the best solution is to have different devices and different IP for every activity. It is just costly. From gigh to low: IP address, hardware fingerprints (HTML5 Canvas), connection timestamp, software fingerprints, behaviour fingerprints (mouse).

# Threat model:
1. Goverments - communication channels, data gathering from public sources, highly classified mass surveillance systems.
2. Corporations - software and hardware backdoors, data gathering from private sources
3. Individuals - proxy for surveillance, fake information, vulnerabilities exploitation

# Rings of protecton
Balanced threats:
- Ring 0: brain, hard to keep
- Ring 1: isolated hardward: “USB authenticator”, encrypted backups
- Ring 2: Isolated laptop
- Ring 3: Working laptop root
- Ring 4: Working laptop - working user with Window manager.
- Ring 5: Secure Internet resources.
- Ring 6: Working laptop - applications sandboxes.
- Ring 7: Remote random machines.
- Ring 8: Remote personal machines.

# Others:
1. Hide DNS requests with proxy.
2. Never share personal or sensitive information with centralized LLMs like ChatGPT, don't ask it to fix errors in letters.
3. Don't keep sensisitve information or passwords on cheep smartphones, don't install sensitive applications.

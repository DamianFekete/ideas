# Ansible installation (VirtualBox)
http://mowson.org/karl/2016/2016-05-20_alpinelinux_vm_under_virtualbox/

# Issues
## IPv6 / apk add speed
If for example ```apk add``` is slow try to **disable IPv6** (very slow download starts / installs if the network doesn't support IPv6)

To do this add ```net.ipv6.conf.all.disable_ipv6 = 1``` and run ```sysctl -p``` to activate the option.
To temporarily set it run ```sysctl -w net.ipv6.conf.all.disable_ipv6=1``` (no spaces).
To check if IPv6 is disabled: ```ifconfig``` shouldn't show an IPv6 anymore (no restart needed).

Unfortunately at restart an error will come up: ```sysctl: error: 'net.ipv6.conf.all.disable_ipv6' is an unknown key```
To solve this the ipv6 modules has to be loaded at the time sysctl is called. Do this by adding ```ipv6``` to /etc/modules

## VirtualBox, serial port, /var/log/messages
Comment the (last) line in ```/etc/inittab```:
```
#ttyS0::respawn:/sbin/getty -L 115200 ttyS0 vt100
```

Otherwise every 10 seconds you'll get the following messages:
```
Jun  4 09:24:12 alpine daemon.info init: process '/sbin/getty -L 115200 ttyS0 vt100' (pid 1905) exited. Scheduling for restart.
Jun  4 09:24:12 alpine daemon.info init: starting pid 1906, tty '/dev/ttyS0': '/sbin/getty -L 115200 ttyS0 vt100'
Jun  4 09:24:12 alpine auth.err getty[1906]: tcgetattr: I/O error^M
Jun  4 09:24:12 alpine kern.warn kernel: [  152.014434] ttyS ttyS0: tty_port_close_start: tty->count = 1 port count = 2
```

# Tips
Install dedicated program implementations if the speed is of concern. Some reported that for example the busybox grep is a lot slower than the special implementation.

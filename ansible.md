# IPv6 / apk add speed
Disable IPv6 (very slow download starts / installs if the network doesn't support it)

Add ```net.ipv6.conf.all.disable_ipv6 = 1``` and run ```sysctl -p``` to activate it.
```ifconfig``` shoudln't show an IPv6 anymore (no restart needed).

# VirtualBox, serial port, /var/log/messages
Comment the (last) line in ```/etc/inittab```:
```#ttyS0::respawn:/sbin/getty -L 115200 ttyS0 vt100```

Otherwise every 10 seconds you'll get the following messages:
```
Jun  4 09:24:12 alpine daemon.info init: process '/sbin/getty -L 115200 ttyS0 vt100' (pid 1905) exited. Scheduling for restart.
Jun  4 09:24:12 alpine daemon.info init: starting pid 1906, tty '/dev/ttyS0': '/sbin/getty -L 115200 ttyS0 vt100'
Jun  4 09:24:12 alpine auth.err getty[1906]: tcgetattr: I/O error^M
Jun  4 09:24:12 alpine kern.warn kernel: [  152.014434] ttyS ttyS0: tty_port_close_start: tty->count = 1 port count = 2
```

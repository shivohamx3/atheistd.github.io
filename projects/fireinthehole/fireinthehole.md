# Setup *fireinthehole* ![fireinthehole! image](https://github.com/atheistd/atheistd.github.io/raw/master/assets/fireinthehole/fireinthehole.png)



### updating and installing necessary packages

 - `$ sudo apt update; sudo apt upgrade -y`
 - `$ curl -sSL https://install.pi-hole.net | bash`
 - `$ sudo apt install unbound` &nbsp;&nbsp;&nbsp;&nbsp;*the service won't start right away*



### Configure unbound

**/etc/unbound/unbound.conf.d/pi-hole.conf**

```
server:
	verbosity: 0

	interface: 127.0.0.1
	port: 5335
	do-ip4: yes
	do-udp: yes
	do-tcp: yes

	do-ip6: no
	prefer-ip6: no

	harden-glue: yes
	arden-dnssec-stripped: yes

	use-caps-for-id: no

	dns-buffer-size: 1472
	refetch: yes
	um-threads: 1
	o-rcvbuf: 1m

	private-address: 192.168.0.0/16
	private-address: 169.254.0.0/16
	private-address: 172.16.0.0/12
	private-address: 10.0.0.0/8
	private-address: fd00::/8
	private-address: fe80::/10
```

 - `$ sudo service unbound restart`


### More pi-hole settings

 - Go to *fireinthehole-ip-addr/admin* and remove Google/Cloudfare from DNS servers
 - Enter `127.0.0.1#5335` in *Upstream DNS Servers*

 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `
 - `$ `

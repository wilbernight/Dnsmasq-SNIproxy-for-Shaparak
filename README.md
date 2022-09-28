# Dnsmasq-SNIproxy-for-Shaparak with an Iranian VPS

### Script description:

* Brief description of the principle: use the DNS of [Dnsmasq](http://thekelleys.org.uk/dnsmasq/doc.html) to hijack website resolution to [SNI proxy](https://github.com/dlundquist/sniproxy) on the reverse proxy page.

* Purpose: bypass shaparak and psp ip limitation (Just install it on a Iran vps and use that ip as dns resolver of main server with nano /etc/resolv.conf)

* Feature: The script unlocks `Shaparak bpm` [etc.] by default (https://github.com/wilbernight/Dnsmasq-SNIproxy-for-Shaparak/blob/master/proxy-domains.txt), if you need to add or delete url or media domain names, please edit the file `/etc/sniproxy.conf` and `/etc/dnsmasq.d/custom_borders.conf`

* Script support system: CentOS6+, Debian9+, Ubuntu16+
    * CentOS6/7/8, Debian9/10/11+, Ubuntu16/18/22+ have been tested successfully
    * In theory, there is no limit to the virtualization type, if you have any questions, please feedback
    * If the IP displayed at the end of the script does not match the actual public IP, please modify the IP address in the file `/etc/sniproxy.conf`

### Script usage:

    bash dnsmasq_sniproxy.sh [-h] [-i] [-f] [-id] [-is] [-fs] [-u] [-ud] [-us]
      -h , --help display help information
      -i , --install install Dnsmasq + SNI Proxy
      -f , --fastinstall fast install Dnsmasq + SNI Proxy
      -id, --installdnsmasq install Dnsmasq only
      -is, --installsniproxy install SNI Proxy only
      -fs, --fastinstallsniproxy Quickly install SNI Proxy
      -u , --uninstall uninstall Dnsmasq + SNI Proxy
      -ud, --undnsmasq uninstall Dnsmasq
      -us, --unsniproxy uninstall SNI Proxy

### Quick installation (recommended):
```` Bash
wget --no-check-certificate -O dnsmasq_sniproxy.sh https://raw.githubusercontent.com/wilbernight/Dnsmasq-SNIproxy-for-Shaparak/master/dnsmasq_sniproxy.sh && bash dnsmasq_sniproxy.sh -f
````

### Normal installation:
```` Bash
wget --no-check-certificate -O dnsmasq_sniproxy.sh https://raw.githubusercontent.com/wilbernight/Dnsmasq-SNIproxy-for-Shaparak/master/dnsmasq_sniproxy.sh && bash dnsmasq_sniproxy.sh -i
````

### Uninstall method:
```` Bash
wget --no-check-certificate -O dnsmasq_sniproxy.sh https://raw.githubusercontent.com/wilbernight/Dnsmasq-SNIproxy-for-Shaparak/master/dnsmasq_sniproxy.sh && bash dnsmasq_sniproxy.sh -u
````

### Instructions:
Just change the DNS address of the proxy VPS to the IP of this host. If it doesn't work, remember to keep only one DNS address and try it.

To prevent abuse, it is recommended not to publish IP addresses at will, or use firewalls to do a good job of restricting.

### Debugging and troubleshooting:
- Confirm that sniproxy is running effectively

  View sni status: systemctl status sniproxy

  If sni is not running, check if other services occupy port 80,443, in case of port conflict, change the listening port for other services first, and check the port listening: netstat -tlunp|grep 443

- Confirm that the firewall allows 80,443,53

  Debugging can directly close the firewall systemctl stop firewalld.service

  Testable with other servers telnet vpsip 53 as well as telnet vpsip 443

- resolve domain names

  After trying to configure dns with other servers, resolve the domain name: nslookup shaparak.ir to determine whether the IP is the IP of the Shaparak proxy machine
  If the nslookup command does not exist, CENTOS installation: yum install -y bind-utils DEBIAN installation: apt-get -y install dnsutils

---

___This script is for unlocked shaparak and post only ___

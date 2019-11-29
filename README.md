## Router<->DNS<->PI-Hole

Redirect DNS to Pi-Hole.

* Port:         `53`
* Protocol:     `TCP and UDP`
* SRC Address:   In case you're running a network which uses Pi-Hole's IP in the same range as your clients, you'll need to exclude it! For example `!192.168.1.2`.
Dest Port:      `53`

### Network (example)

* 192.168.1.0/2

### Pi-Hole (DNS Server example)

* 192.168.1.2


## Solution

```bash
iptables -t nat -A PREROUTING ! -s 192.168.1.2 -p tcp --dport 53 -j DNAT --to 192.168.1.2
iptables -t nat -A PREROUTING ! -s 192.168.1.2 -p udp --dport 53 -j DNAT --to 192.168.1.2
```

### DD-WRT

```bash
/usr/sbin/iptables -t nat -A PREROUTING -i br0 -p udp --dport 53 -j DNAT --to 192.168.1.2
/usr/sbin/iptables -t nat -A PREROUTING -i br0 -p tcp --dport 53 -j DNAT --to 192.168.1.2
```

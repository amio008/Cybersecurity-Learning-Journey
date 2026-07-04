# Command Reference – Basic Router Configuration

This file contains the Cisco IOS commands used during this networking exercise.

---

# Reset Router Configuration

```cisco
enable
erase startup-config
reload
```

When prompted:

* Save configuration? → **No**
* Proceed with reload? → **Yes**
* Initial configuration dialog? → **No**

---

# Router R1 Configuration

```cisco
enable
configure terminal

hostname R1
no ip domain-lookup

enable secret class

banner motd &
*** AUTHORIZED ACCESS ONLY ***
&

line console 0
password cisco
login
exit

line vty 0 4
password cisco
login
exit

interface FastEthernet0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

interface Serial0/0/0
ip address 192.168.2.1 255.255.255.0
clock rate 64000
no shutdown
exit

end

copy running-config startup-config
```

---

# Router R2 Configuration

```cisco
enable
configure terminal

hostname R2
no ip domain-lookup

enable secret class

banner motd &
*** AUTHORIZED ACCESS ONLY ***
&

line console 0
password cisco
login
exit

line vty 0 4
password cisco
login
exit

interface Serial0/0/0
ip address 192.168.2.2 255.255.255.0
no shutdown
exit

interface FastEthernet0/0
ip address 192.168.3.1 255.255.255.0
no shutdown
exit

end

copy running-config startup-config
```

---

# Verification Commands

```cisco
show ip interface brief
show ip route
show running-config
ping 192.168.2.2
ping 192.168.2.1
```

These commands were used to verify:

* Interface status
* Assigned IP addresses
* Routing table entries
* Active configuration
* Router-to-router connectivity

---

# Useful Troubleshooting Commands

```cisco
show startup-config
show interfaces
show ip interface brief
show ip route
ping
```

---

# Quick Notes

* `no shutdown` enables an interface.
* The DCE side of the serial connection requires a `clock rate`.
* `enable secret` encrypts the privileged EXEC password.
* `copy running-config startup-config` saves the configuration to NVRAM.
* `show ip route` displays directly connected routes after interfaces are configured and active.

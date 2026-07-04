```markdown
# Command Reference: Basic Router Configuration

## Mode Navigation

| Mode | Prompt | Enter | Exit |
|------|--------|-------|------|
| User EXEC | `Router>` | Default | `exit` |
| Privileged EXEC | `Router#` | `enable` | `disable` |
| Global Config | `Router(config)#` | `configure terminal` | `end` |
| Interface Config | `Router(config-if)#` | `interface [type] [number]` | `exit` |
| Line Config | `Router(config-line)#` | `line [type] [number]` | `exit` |

---

## Router Reset

```cisco
enable
erase startup-config
reload
# Answer: no, no, [Enter]
```

---

## Basic Configuration

```cisco
configure terminal
hostname R1
no ip domain-lookup
enable secret class
banner motd &
!!!AUTHORIZED ACCESS ONLY!!!
&

line console 0
password cisco
login
exit

line vty 0 4
password cisco
login
exit
```

---

## Interface Configuration

### Ethernet (R1)
```cisco
interface fastethernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```

### Serial (R1 - DCE)
```cisco
interface serial 0/0/0
ip address 192.168.2.1 255.255.255.0
clock rate 64000
no shutdown
exit
```

### Serial (R2 - DTE)
```cisco
interface serial 0/0/0
ip address 192.168.2.2 255.255.255.0
no shutdown
exit
```

### Ethernet (R2)
```cisco
interface fastethernet 0/0
ip address 192.168.3.1 255.255.255.0
no shutdown
exit
```

---

## Save Configuration

```cisco
copy running-config startup-config
# or
wr
```

---

## Verification Commands

```cisco
show ip route
show ip interface brief
show running-config
ping 192.168.2.2
```

---

## Full Lab Commands

### R1 Complete
```cisco
enable
configure terminal
hostname R1
no ip domain-lookup
enable secret class
banner motd &!!!AUTHORIZED ACCESS ONLY!!!&
line console 0
password cisco
login
exit
line vty 0 4
password cisco
login
exit
interface fastethernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
interface serial 0/0/0
ip address 192.168.2.1 255.255.255.0
clock rate 64000
no shutdown
end
copy running-config startup-config
```

### R2 Complete
```cisco
enable
configure terminal
hostname R2
no ip domain-lookup
enable secret class
banner motd &!!!AUTHORIZED ACCESS ONLY!!!&
line console 0
password cisco
login
exit
line vty 0 4
password cisco
login
exit
interface serial 0/0/0
ip address 192.168.2.2 255.255.255.0
no shutdown
exit
interface fastethernet 0/0
ip address 192.168.3.1 255.255.255.0
no shutdown
end
copy running-config startup-config
```

---

## Shortcuts

| Command | Shorthand |
|---------|-----------|
| `configure terminal` | `conf t` |
| `interface` | `int` |
| `fastethernet` | `fa` |
| `show running-config` | `sh run` |
| `show ip route` | `sh ip ro` |
| `show ip interface brief` | `sh ip int br` |
| `copy running-config startup-config` | `wr` |

---

## Troubleshooting Checklist

1. **Check physical connections** - Link lights blinking?
2. **Verify interface status** - `show ip interface brief` → Should show `up/up`
3. **Check IP addressing** - Correct IP and subnet mask?
4. **Verify DCE/clock rate** - DCE side must have `clock rate`
5. **Check routing table** - `show ip route` → Should show directly connected routes
6. **Test connectivity** - `ping` from router to router, then host to gateway

---

## Interface Status Indicators

| Status | Meaning |
|--------|---------|
| `up/up` | Working correctly |
| `up/down` | Layer 1 up, Layer 2 down |
| `down/down` | Interface down |
| `administratively down` | Manually shut down |

---

*Created for cybersecurity learning journey - quick reference for Cisco router configuration.*
```

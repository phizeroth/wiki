---
title: ufw firewall
description: 
published: true
date: 2021-07-08T20:33:13.824Z
tags: security
editor: markdown
dateCreated: 2021-07-08T20:33:13.824Z
---

## Using ufw

View firewall status:
```
sudo ufw status [numbered]
```
Silently deny an IP address all access:
```
sudo ufw deny from 123.45.67.890 to any
```
Reject an IP address from all access (sends a reject response to the host):
```
sudo ufw deny from 123.45.67.890 to any
```

UFW (iptables) rules are applied in order of appearance, and the inspection ends immediately when there is a match. Therefore, for example, if a rule is allowing access to tcp port 22 (say using `sudo ufw allow 22`), and afterward another Rule is specified blocking an IP address (say using `ufw deny proto tcp from 202.54.1.1 to any port 22`), the rule to access port 22 is applied and the later rule to block the hacker IP address 202.54.1.1 is not.

Therefore, place deny/reject rules at the **beginning** of the list via:
```
sudo ufw insert 1 deny from 123.45.67.890 to any
```

## References
- https://www.cyberciti.biz/faq/how-to-block-an-ip-address-with-ufw-on-ubuntu-linux-server/
- https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-14-04
- https://help.ubuntu.com/community/UFW
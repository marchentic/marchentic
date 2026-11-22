---
name: nginx-proxy-manager-ssl
description: >-
  Issue or renew NPM SSL certificates with safety gates.
---

# /nginx-proxy-manager-ssl

1. Require an explicit cert issue/renew/attach ask; else stop.
2. Load skill `nginx-proxy-manager-ssl-issue` (and skill
   `nginx-proxy-manager` + ssl/hosts/safety rules).
3. No private keys or DNS tokens in chat.
4. Receipt: cert id + domains + expiry; optional host attach evidence.

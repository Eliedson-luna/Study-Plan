## Redes Básicas para Segurança

### Modelo OSI (7 Camadas) — Foco em Controles de Segurança

| Camada | Nome | Protocolos / Tecnologias | Controles de Segurança Típicos |
|--------|------|--------------------------|--------------------------------|
| **7** | **Aplicação** | HTTP/HTTPS, DNS, SMTP, FTP, SSH, TLS, SNMP, DHCP | WAF, API Gateway, DLP, proxy inspeção TLS, DNSSEC, DMARC/SPF/DKIM |
| **6** | **Apresentação** | TLS/SSL, ASN.1, XDR, compressão, criptografia | Validação de certificado, pinning, inspeção SSL/TLS |
| **5** | **Sessão** | NetBIOS, RPC, PPTP, SIP, TLS session resumption | Timeouts de sessão, secure session cookies, reautenticação |
| **4** | **Transporte** | **TCP**, **UDP**, QUIC, SCTP | Firewall stateful (conexões), rate limiting, SYN flood protection |
| **3** | **Rede** | **IPv4/IPv6**, ICMP, ICMPv6, IPsec, OSPF, BGP | Firewall stateless (pacotes), ACLs, IPsec (VPN), anti-spoofing (uRPF), BGPsec |
| **2** | **Enlace** | Ethernet (802.3), Wi-Fi (802.11), PPP, MAC, VLAN (802.1Q) | Port security, 802.1X (NAC), MACsec, VLAN isolation, DHCP snooping, DAI |
| **1** | **Física** | Cabos, fibra, rádio, conectores, repetidores | Controle de acesso físico, proteção de cabos, TEMPEST |

### Modelo TCP/IP (4 Camadas) — Mapeamento

| TCP/IP | OSI | Protocolos-Chave |
|--------|-----|------------------|
| **Aplicação** | 5-7 | HTTP, DNS, SMTP, SSH, TLS, SNMP |
| **Transporte** | 4 | TCP, UDP, QUIC |
| **Internet** | 3 | IP, ICMP, IPsec |
| **Enlace/Física** | 1-2 | Ethernet, Wi-Fi, MAC |

---

### Portas e Protocolos Essenciais (Must Know)

| Porta | Protocolo | Transporte | Uso | Risco / Controle |
|-------|-----------|------------|-----|------------------|
| **20/21** | FTP | TCP | Transferência arquivos | **Inseguro** (credenciais em claro) → Use SFTP/FTPS |
| **22** | SSH | TCP | Admin remoto seguro | Chaves, disable root login, fail2ban, port knocking |
| **23** | Telnet | TCP | Admin remoto | **Obsoleto/inseguro** → Bloquear |
| **25** | SMTP | TCP | Envio e-mail | STARTTLS obrigatório, SPF/DKIM/DMARC |
| **53** | DNS | UDP/TCP | Resolução nomes | DNSSEC, DoH/DoT, rate limiting, bloquear recursão aberta |
| **67/68** | DHCP | UDP | Endereçamento automático | DHCP snooping, option 82, server guard |
| **80** | HTTP | TCP | Web não criptografada | Redirect para 443, HSTS |
| **110/995** | POP3 / POP3S | TCP | Recebimento e-mail | 995 (TLS) preferido |
| **143/993** | IMAP / IMAPS | TCP | Recebimento e-mail | 993 (TLS) preferido |
| **389/636** | LDAP / LDAPS | TCP | Diretório | 636 (TLS) ou StartTLS em 389 |
| **443** | HTTPS | TCP | Web seguro | TLS 1.2/1.3, HSTS, certificado válido, OCSP stapling |
| **445** | SMB | TCP | Compartilhamento Windows | **Alvo frequente** (EternalBlue) → SMB signing, disable v1, firewall |
| **3389** | RDP | TCP | Remote Desktop | **Alvo frequente** → NLA, MFA, RD Gateway, restrict IP |
| **161/162** | SNMP | UDP | Monitoramento | v3 (auth+priv), community strings fortes, ACL |
| **500/4500** | IPsec/IKE | UDP | VPN site-to-site, remote access | IKEv2, certificados, PFS |
| **1194** | OpenVPN | UDP/TCP | VPN SSL | TLS, certificados, MFA |
| **51820** | WireGuard | UDP | VPN moderna | Chaves Curve25519, roaming, sem handshake visível |

---

### Subnetting e CIDR — Referência Rápida

| CIDR | Máscara | Hosts Úteis | Uso Comum |
|------|---------|-------------|-----------|
| /8 | 255.0.0.0 | 16.777.214 | Classe A (legado) |
| /16 | 255.255.0.0 | 65.534 | Classe B (legado) |
| /24 | 255.255.255.0 | 254 | **Padrão LAN** (192.168.x.0/24, 10.x.y.0/24) |
| /26 | 255.255.255.192 | 62 | Segmentação DMZ, Wi-Fi guests |
| /28 | 255.255.255.240 | 14 | Link ponto-a-ponto, pequenos segmentos |
| /30 | 255.255.255.252 | 2 | Links WAN ponto-a-ponto (IPv4) |
| /32 | 255.255.255.255 | 1 | Host route, loopback |
| /127 | IPv6 | 2 | Link ponto-a-ponto IPv6 (RFC 6164) |
| /64 | IPv6 | 2^64 | **Padrão LAN IPv6** (SLAAC requer /64) |

**Fórmula**: Hosts úteis = 2^(32 - prefixo) - 2 (rede + broadcast). IPv6: /64 = 18 quintilhões.

---

### Segmentação de Rede — Conceitos-Chave

| Conceito | Descrição | Controle de Segurança |
|----------|-----------|----------------------|
| **VLAN (802.1Q)** | Segmentação lógica L2 (tag 12-bit, 4094 VLANs) | Isolamento broadcast, trunk tagged, access untagged |
| **DMZ** | Zona desmilitarizada entre internet e rede interna | Dual firewall (screening router + interno), servidores públicos (web, mail, DNS) |
| **Zero Trust Network Access (ZTNA)** | Não confia em rede — verifica identidade + device + contexto | Microsegmentação, SDP (Software Defined Perimeter), identity-aware proxy |
| **Microsegmentação** | Políticas L3-L7 por workload (não por IP/subnet) | Cisco ACI, VMware NSX, Calico, Cilium, Illumio |
| **East-West Traffic** | Tráfego servidor-servidor dentro do DC | Inspeção L7, mTLS, segmentação por aplicação |
| **North-South Traffic** | Tráfego cliente-internet ↔ DC | Firewall perimetral, WAF, DDoS protection |

---

### Wireless (802.11) — Segurança

| Protocolo | Autenticação | Criptografia | Status |
|-----------|--------------|--------------|--------|
| **WEP** | Open/Shared Key | RC4 | **Quebrado** — não usar |
| **WPA** | PSK / 802.1X (TKIP) | TKIP/RC4 | **Obsoleto** |
| **WPA2** | PSK / 802.1X (Enterprise) | **AES-CCMP** | Mínimo aceitável |
| **WPA3** | SAE (Simultaneous Authentication of Equals) / 802.1X | **AES-GCMP-256** (Enterprise), AES-CCMP (Personal) | **Padrão atual** — forward secrecy, proteção offline dictionary |

**Ataques Wi-Fi comuns**: Rogue AP, Evil Twin, Deauth/Disassociation (DoS), PMKID capture, KRACK (WPA2), Dragonblood (WPA3 early)

**Controles**: 802.1X (EAP-TLS/PEAP), certificados máquina/usuário, WIDS/WIPS, segregação VLAN por SSID, desabilitar WPS.

---

### Resumo — Onde Atuam os Controles

```
Camada 7 (App)     → WAF, DLP, API Gateway, Inspeção TLS, DNSSEC
Camada 6 (Pres)    → Validação Cert, Pinning, TLS Inspection
Camada 4 (Transp)  → Stateful FW, Rate Limit, DDoS (SYN flood)
Camada 3 (Rede)    → Stateless FW/ACL, IPsec, Anti-spoof (uRPF), BGPsec
Camada 2 (Enlace)  → 802.1X (NAC), Port Security, MACsec, VLAN, DHCP Snooping
Camada 1 (Física)  → Acesso físico, TEMPEST, fibra vs cobre
```
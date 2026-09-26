
# 1. Conteúdo Específico 

## Bloco 1 — Segurança Ofensiva
- Conceitos básicos: vulnerabilidades, ameaças e ataques
- Ataques passivos (escuta passiva, inferência) e ativos (escuta ativa, disfarce, repetição, negação de serviço)
- Etapas de um ataque: Footprinting → Varredura → Enumeração → Ganho de acesso → Escalação de privilégios → Backdoor → Encobrimento de rastros → Negação de serviço
- Ataques a protocolos: ARP, IP, ICMP, UDP, TCP, DHCP, SMTP, IMAP, POP3, HTTP, FTP, SMB
- Ataques a redes Wi-Fi: Rogue AP, Evil Twin, SSID Tracking, Jamming, Disassociation
- Man-in-the-Middle: Sniffing e Spoofing
- Engenharia Social: ciclo de ataque e técnicas
- Código malicioso: Vírus, Worm, Trojan, Backdoor, Screenlogger, Keylogger, Injector, Downloader, Flooder, Rootkit, Bot/Botnet, Exploit, Spyware, Ransomware, Cryptojacking, Formjacking
- **MITRE ATT&CK** (matrizes, táticas, técnicas, procedimentos, mitigações) e **MITRE CAPEC** (padrões de ataque)
- Ferramentas de hacking (é bom saber pra que serve cada uma, não decorar sintaxe): amass, aircrack-ng, airgeddon, arpwatch, beef-xss, burpsuite, ettercap, ghidra, hashcat, hydra, john the ripper, nmap, netcat, maltego, steghide, masscan, mimikatz, metasploit-framework, set, smbmap, sqlmap, theharvester, veil, wireshark

## Bloco 2 — Segurança Defensiva
- Defesa em profundidade: filtro de pacotes, firewall de estado, firewall proxy, IDS, IPS, VPN
- Controle de acesso à rede: IEEE 802.1X, EAP, RADIUS
- Segurança em aplicações: OWASP Top 10, OWASP SAMM, CVE, CWE
- Pilares de Segurança da Informação: integridade, autenticidade, confidencialidade, autorização, disponibilidade, irretratabilidade
- Mecanismos: hash/resumo de mensagem, cifragem, assinatura digital, envelope digital, certificado digital, MFA, carimbo do tempo, redundância/tolerância a falhas
- **ICP-Brasil**: autoridade certificadora, autoridade de carimbo do tempo, normas
- Comunicação segura: TLS, SSL, IPsec
- Segurança em endpoint: antimalware, firewall pessoal
- Segurança em SO: CIS Benchmarks, Linux e Windows
- Segurança industrial (OT): ICS Advisory Project, série ISA/IEC 62443, NIST SP 800-82
- Forense digital: evidência digital, processo de análise forense, análise de dispositivos/sites/e-mails, OSINT

## Bloco 3 — Compliance de Segurança e Privacidade
- **Normas ABNT:** ISO/IEC 27001:2022, 27002:2022, 27005:2023, 27035-1:2023 (resposta a incidentes), ISO 22301:2020 e 22313:2020 (continuidade de negócios), ISO/IEC 29100:2024 e 29134:2024 (privacidade), ISO/IEC 27701:2019 (SGPI)
- **Frameworks:** NIST Cybersecurity Framework (CSF) 2.0, CIS Critical Security Controls v8.1
- **Leis/regulamentos:** Marco Civil da Internet (Lei 12.965/2014), LGPD (Lei 13.709/2018), Resolução ANATEL 740/2020 (segurança cibernética em telecom)

---

# 2. Conhecimentos Gerais

**Língua Portuguesa:** compreensão de texto, ortografia, coesão textual, significação de palavras, tempos/modos verbais, classes de palavras, coordenação/subordinação, pontuação, concordância verbal/nominal, regência, crase, colocação pronominal.

**Língua Inglesa:** compreensão de texto técnico + gramática relevante para entender o sentido (não é prova de tradução literal — é interpretação).

---

# 3. Prioridades para 2 meses (8 semanas)

Com pouco tempo, a ordem de prioridade deve seguir o que **mais aparece em provas anteriores da Cesgranrio** e o que **tem maior densidade de peso** no edital:

| Prioridade | Bloco | Por quê |
|---|---|---|
| 🔴 Alta | Segurança Defensiva (pilares, mecanismos, ICP-Brasil, redes/firewall/IDS-IPS) | Base conceitual que sustenta todo o resto; muito cobrado |
| 🔴 Alta | Compliance (ISO 27001/27002, LGPD, NIST CSF) | Normas são "decoráveis" e caem quase sempre; ótimo custo-benefício |
| 🟠 Média | Segurança Ofensiva (ataques, malware, MITRE ATT&CK) | Extenso, mas dá pra estudar por categorias em vez de decorar cada termo |
| 🟠 Média | Português | Curto (10 questões), retorno rápido revisando gramática normativa |
| 🟡 Baixa-mas-não-pule | Inglês técnico | Só 10 questões, mas tem corte próprio — não pode zerar |
| 🟡 Baixa | Ferramentas de hacking específicas | Muito detalhe, baixo retorno relativo — estude o "para que serve", não sintaxe |


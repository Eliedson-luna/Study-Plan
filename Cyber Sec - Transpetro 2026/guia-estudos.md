# Guia de Estudos — TRANSPETRO 2026.4 (Cesgranrio)
## Ênfase 7: Análise de Sistemas – Segurança Cibernética e da Informação

> Fonte oficial: Edital nº 04 – TRANSPETRO/PSP/TERRA/NÍVEL SUPERIOR – 2026.4, Anexo IV.
> Baixe o edital original em www.cesgranrio.org.br para conferir contra este resumo — retificações podem alterar o conteúdo.

---

## 1. Como funciona a prova

- **Data:** provas objetivas em **06/12/2026** (data remarcada; confirme no site da Cesgranrio antes de organizar a reta final).
- **Formato:** caderno único com duas fases:
  - **Fase 1 – Conhecimentos Específicos:** 50 questões (1 ponto cada). Elimina quem tirar menos de 50%.
  - **Fase 2 – Conhecimentos Gerais:** 20 questões — 10 de Português + 10 de Inglês. Elimina quem tirar menos de 50% no total OU zero em qualquer uma das duas matérias.
- **Classificação:** só passa para o ranking quem supera as duas notas de corte. A nota final é a soma das duas fases, mas só é calculada para quem já passou no corte de Específicos.
- **Regra de ouro:** não adianta "compensar" — você precisa acertar pelo menos 25/50 em Específicos, 5/10 em Português e 5/10 em Inglês (aproximado, respeitando o corte de 50% do total de Gerais).

**Implicação prática para o seu plano de 2 meses:** Específicos vale 2,5x mais que Gerais em pontos, mas Gerais tem corte próprio. Não pode zerar Inglês achando que "compensa" com Específicos.

---

## 2. Conteúdo Específico — Ênfase 7 (o que realmente cai)

### Bloco 1 — Segurança Ofensiva
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

### Bloco 2 — Segurança Defensiva
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

### Bloco 3 — Compliance de Segurança e Privacidade
- **Normas ABNT:** ISO/IEC 27001:2022, 27002:2022, 27005:2023, 27035-1:2023 (resposta a incidentes), ISO 22301:2020 e 22313:2020 (continuidade de negócios), ISO/IEC 29100:2024 e 29134:2024 (privacidade), ISO/IEC 27701:2019 (SGPI)
- **Frameworks:** NIST Cybersecurity Framework (CSF) 2.0, CIS Critical Security Controls v8.1
- **Leis/regulamentos:** Marco Civil da Internet (Lei 12.965/2014), LGPD (Lei 13.709/2018), Resolução ANATEL 740/2020 (segurança cibernética em telecom)

---

## 3. Conhecimentos Gerais

**Língua Portuguesa:** compreensão de texto, ortografia, coesão textual, significação de palavras, tempos/modos verbais, classes de palavras, coordenação/subordinação, pontuação, concordância verbal/nominal, regência, crase, colocação pronominal.

**Língua Inglesa:** compreensão de texto técnico + gramática relevante para entender o sentido (não é prova de tradução literal — é interpretação).

---

## 4. Prioridades para 2 meses (8 semanas)

Com pouco tempo, a ordem de prioridade deve seguir o que **mais aparece em provas anteriores da Cesgranrio** e o que **tem maior densidade de peso** no edital:

| Prioridade | Bloco | Por quê |
|---|---|---|
| 🔴 Alta | Segurança Defensiva (pilares, mecanismos, ICP-Brasil, redes/firewall/IDS-IPS) | Base conceitual que sustenta todo o resto; muito cobrado |
| 🔴 Alta | Compliance (ISO 27001/27002, LGPD, NIST CSF) | Normas são "decoráveis" e caem quase sempre; ótimo custo-benefício |
| 🟠 Média | Segurança Ofensiva (ataques, malware, MITRE ATT&CK) | Extenso, mas dá pra estudar por categorias em vez de decorar cada termo |
| 🟠 Média | Português | Curto (10 questões), retorno rápido revisando gramática normativa |
| 🟡 Baixa-mas-não-pule | Inglês técnico | Só 10 questões, mas tem corte próprio — não pode zerar |
| 🟡 Baixa | Ferramentas de hacking específicas | Muito detalhe, baixo retorno relativo — estude o "para que serve", não sintaxe |

---

## 5. Cronograma sugerido (8 semanas)

- **Semana 1-2:** Segurança Defensiva completa (pilares, criptografia, PKI/ICP-Brasil, redes de defesa, forense digital)
- **Semana 3-4:** Compliance (ISO 27001/27002/27005/27035, LGPD, NIST CSF 2.0, CIS Controls) + revisão semanal de Português
- **Semana 5-6:** Segurança Ofensiva (ataques, malware, MITRE ATT&CK/CAPEC, engenharia social) + Inglês técnico 2x/semana
- **Semana 7:** Revisão geral + resolução de provas anteriores da Cesgranrio (mesma banca, procure provas de TI de editais recentes: BB, Petrobras, Liquigás, Transpetro 2023)
- **Semana 8:** Simulados cronometrados + revisão dos pontos fracos identificados

**Dica de método:** a Cesgranrio costuma cobrar de forma **conceitual e comparativa** (ex.: "qual a diferença entre IDS e IPS", "o que garante a norma X que a norma Y não garante"). Priorize entender diferenças entre conceitos parecidos em vez de decorar definições isoladas.

---

## 6. Fontes e materiais recomendados

### Provas e editais oficiais
- **Fundação Cesgranrio** (site oficial, editais, gabaritos, provas anteriores): https://www.cesgranrio.org.br
- **TecConcursos** e **QConcursos**: bancos de questões filtráveis por banca (Cesgranrio) e assunto — essencial para treinar o "estilo" da banca
- Provas anteriores de TI da Cesgranrio para outras estatais (Petrobras, BB, Liquigás, Transpetro 2023) — o padrão de cobrança se repete bastante entre certames da mesma banca

### Normas e frameworks (estude direto na fonte quando possível)
- **NIST Cybersecurity Framework 2.0**: nist.gov/cyberframework (o próprio PDF do framework é curto e direto)
- **OWASP Top 10**: owasp.org/www-project-top-ten
- **MITRE ATT&CK**: attack.mitre.org (navegue pela matriz, não precisa decorar tudo, mas entenda a lógica de táticas x técnicas)
- **ISO 27001/27002**: resumos gratuitos de blogs especializados (ex. ISO.org tem resumos oficiais; buscar "ISO 27002 controles resumo" em português)
- **LGPD**: planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm (leitura direta da lei, é curta)

### Blogs e conteúdo em português
- Blog da **Estratégia Concursos**, **Gran Cursos** e **TecConcursos** — costumam publicar posts gratuitos com "o que estudar" por edital, específicos para Cesgranrio
- **Canal Sec** / blogs de segurança da informação em PT-BR para fixar conceitos com analogias (ex. Manual do Usuário, Segurança Legal)
- YouTube: canais de cursinhos costumam ter aulas avulsas gratuitas de segurança da informação — procure por "Segurança da Informação para concursos Cesgranrio"

### Cursos pagos (se o orçamento permitir, acelera muito dado o prazo curto)
- Estratégia Concursos e Gran Cursos têm cursos específicos para esta ênfase do Transpetro 2026, já organizados por edital, com questões comentadas — dado que você tem só 2 meses, isso evita "garimpar" conteúdo e permite focar 100% em estudar e revisar

---

## 7. Checklist de acompanhamento

- [ ] Baixei o edital oficial e conferi este resumo contra o Anexo IV
- [ ] Segurança Defensiva — teoria revisada
- [ ] Compliance/normas — teoria revisada
- [ ] Segurança Ofensiva — teoria revisada
- [ ] Português — revisão gramatical feita
- [ ] Inglês técnico — pratiquei leitura e vocabulário de TI/segurança
- [ ] Resolvi pelo menos 3 provas anteriores da Cesgranrio (TI)
- [ ] Fiz simulado cronometrado completo (70 questões, 4h30)
- [ ] Verifiquei se houve retificação do edital

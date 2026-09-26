## Resposta a Incidentes — Fundamentos (NIST SP 800-61 / ISO 27035)

### Fases do ciclo de vida (NIST 800-61 Rev. 2)

```
┌─────────────────┐
│  Preparação     │ ← Contínua (políticas, treino, ferramentas, playbooks)
└────────┬────────┘
         ▼
┌─────────────────┐
│ Detecção e      │ ← Alertas, logs, threat hunting, relato de usuários
│ Análise         │    Triagem → Classificação → Priorização
└────────┬────────┘
         ▼
┌─────────────────┐
│ Contenção       │ ← Curto prazo (isolar) → Longo prazo (remediação temporária)
└────────┬────────┘
         ▼
┌─────────────────┐
│ Erradicação     │ ← Remover causa raiz (malware, acesso indevido, vulnerabilidade)
└────────┬────────┘
         ▼
┌─────────────────┐
│ Recuperação     │ ← Restaurar sistemas, validar, monitorar reforçado, retornar à operação
└────────┬────────┘
         ▼
┌─────────────────┐
│ Lições Aprendidas│ ← Pós-incidente (root cause, melhorias, atualizar playbooks)
└─────────────────┘
         │
         └──────► (retorna a Preparação)
```

---

### Preparação (antes do incidente)

| Item | Descrição |
|------|-----------|
| **Política de resposta a incidentes** | Escopo, definições, autoridades, comunicação, retenção de evidências |
| **CSIRT / SOC** | Equipe dedicada (interna, híbrida, terceirizada); roles: Incident Commander, Analyst, Forensics, Comms, Legal, PR |
| **Playbooks / Runbooks** | Cenários: phishing, ransomware, vazamento, DDoS, insider threat, compromise de credencial, supply chain |
| **Ferramentas** | SIEM, EDR/XDR, SOAR, threat intel, sandbox, forense (Volatility, Autopsy, FTK), rede (Zeek, PCAP) |
| **Comunicação** | Canais seguros (Signal, Mattermost), lista de contatos (internos, LE, ANPD, CERT.br, clientes), templates de notificação |
| **Treinamento/Exercícios** | Tabletop trimestral, red team/blue team anual, simulação de ransomware |
| **Evidências / Cadeia de custódia** | Formulários, lacres, hash (SHA-256), log de quem/quando/onde coletou |

---

### Detecção e Análise

| Fonte de detecção | Exemplos |
|-------------------|----------|
| **Automatizada** | SIEM correlation, EDR alert, IDS/IPS, UEBA, DLP, threat intel feed |
| **Manual/Relato** | Help desk, usuário, fornecedor, law enforcement, bug bounty, dark web monitoring |
| **Proativa** | Threat hunting, compromise assessment, purple team |

**Triagem (Triage)** — perguntas-chave:
1. O que aconteceu? (tipo: malware, acesso não autorizado, vazamento, negação, etc.)
2. Quais ativos/sistemas afetados? (criticidade, classificação de dados)
3. Qual o vetor inicial? (phish, exploit, credencial vazada, insider, supply chain)
4. Qual o alcance atual? (contido, lateral movement, exfiltração ativa)
5. Há evidência de persistência? (scheduled tasks, serviços, WMI, registry, kernel modules)
6. Qual a severidade? (Crítico/Alto/Médio/Baixo — base BIA + impacto real)

**Classificação de severidade (exemplo)**

| Severidade | Critérios | SLA resposta | Escalação |
|------------|-----------|--------------|-----------|
| **Crítico (P1)** | Sistema crítico indisponível, vazamento de dados sensíveis confirmado, ransomware ativo, compromisso de admin/domain controller | 15 min | CISO, Direção, Jurídico, DPO, LE |
| **Alto (P2)** | Acesso não autorizado a sistema sensível, malware em endpoint crítico, credencial de admin comprometida | 1 h | Gerente SI, Owner do sistema |
| **Médio (P3)** | Phishing com clique (sem execução), scan de vulnerabilidade, tentativa de brute force bloqueada | 4 h | Analista SOC |
| **Baixo (P4)** | Spam, port scan externo bloqueado, policy violation sem dano | 24 h | Analista SOC |

---

### Contenção

| Tipo | Ações | Cuidados |
|------|-------|----------|
| **Curto prazo (imediato)** | Isolar host da rede (quarentena VLAN), bloquear IP/domínio no firewall/proxy, desabilitar conta comprometida, revogar tokens/sessões, sinkhole DNS | Não desligar o host (perde memória volátil); coletar imagem de memória e disco *antes* se possível |
| **Longo prazo** | Aplicar patches, remover malware, reconstruir sistema (reimage), rotacionar todas as credenciais suspeitas, reforçar regras de detecção | Validar que atacante não tem outro ponto de entrada (persistence) |

---

### Erradicação

- Remover **causa raiz**: malware, webshell, conta rogue, chave SSH não autorizada, vulnerabilidade explorada
- **Sanitização**: Reimage (golden image) > limpeza manual; assumir compromisso total se rootkit/bootkit
- **Patch/Config**: Corrigir falha que permitiu entrada (ex: CVE não patchado, MFA ausente, porta exposta)
- **Validação**: Scan pós-erradicação, verificação de integridade (FIM), threat hunt dirigido

---

### Recuperação

| Passo | Descrição |
|-------|-----------|
| **Restaurar** | De backup limpo (validado, testado, com hash conhecido) ou rebuild from IaC |
| **Validar** | Testes de funcionamento, scan de vulnerabilidade, verificação de integridade de dados |
| **Monitorar reforçado** | Enhanced logging, alertas sensíveis, threat hunt contínuo por 30 dias (minimum) |
| **Retorno à operação** | Aprovação do Owner + CISO; comunicação a stakeholders |
| **Encerramento formal** | Relatório final, evidências arquivadas, lições aprendidas agendadas |

---

### Lições Aprendidas (Post-Incident Review / PIR)

| Perguntas-chave | Artefato |
|-----------------|----------|
| O que aconteceu? (timeline) | Timeline detalhado com timestamps (UTC) |
| Como fomos detectados? (ou por que não fomos?) | Gap de visibilidade |
| A contenção foi eficaz? Tempo para conter? | Métricas: MTTC (Mean Time to Contain) |
| A erradicação removeu a causa raiz? | Root Cause Analysis (5 Whys, Fishbone) |
| Recuperação atendeu RTO/RPO? | Comparativo planejado x real |
| Comunicação funcionou? (internos, clientes, reguladores, imprensa) | Log de comunicações |
| Quais controles falharam/faltaram? | Mapeamento para MITRE ATT&CK (táticas/técnicas) |
| O que melhorar? (política, tooling, treino, arquitetura) | Action items com owner + prazo |

**Métricas-chave (MTTx)**:
- **MTTD** — Mean Time to Detect
- **MTTA** — Mean Time to Acknowledge
- **MTTC** — Mean Time to Contain
- **MTTR** — Mean Time to Recover / Resolve

---

### Cadeia de Custódia (Chain of Custody)

| Elemento | Descrição |
|----------|-----------|
| **Identificação** | Hash SHA-256 da evidência (disco, memória, log, PCAP) no momento da coleta |
| **Coleta** | Quem coletou, quando (UTC), onde, como (ferramenta, write-blocker), testemunha |
| **Transporte/Armazenamento** | Lacres numerados, cofre/sala segura, controle de acesso, log de entrada/saída |
| **Análise** | Quem analisou, quando, ferramentas usadas, hash de verificação pré/pós-análise |
| **Destinação** | Devolução, destruição certificada, entrega a autoridade judicial |

> **Regra de ouro**: Evidência sem cadeia de custódia documentada = inadmissível em processo judicial/administrativo.

---

### Integração com frameworks

| Framework | Mapeamento |
|-----------|------------|
| **NIST CSF 2.0** | Respond (RS) → RP, RS.AN, RS.MI, RS.CO, RC |
| **ISO 27035** | Fases alinhadas; foco em gestão do processo, não só técnico |
| **MITRE ATT&CK** | Mapear técnicas observadas em cada fase (ex: T1059, T1003, T1486) para melhorar detecção |
| **LGPD Art. 48** | Notificação à ANPD e titulares em "prazo razoável" (guia ANPD: ≤ 2 dias úteis para incidente com risco relevante) |
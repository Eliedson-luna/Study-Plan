## Ciclo de Vida da Gestão de Segurança

### PDCA Aplicado à Segurança da Informação (ISO 27001)

| Fase | Atividades de Segurança | Entregáveis |
|------|------------------------|-------------|
| **Plan (Planejar)** | Contexto da organização, partes interessadas, escopo do SGSI, política de SI, análise de risco, plano de tratamento, objetivos de SI, statement of applicability (SoA) | Política de SI, Relatório de Análise de Risco, Plano de Tratamento, SoA, Objetivos de SI |
| **Do (Fazer)** | Implementar controles (Anexo A ISO 27001), gestão de ativos, controle de acesso, criptografia, segurança física, gestão de incidentes, continuidade, treinamento | Controles implementados, procedimentos, registros de treinamento, inventário de ativos |
| **Check (Verificar)** | Monitoramento, medição, análise, avaliação, auditoria interna, análise crítica pela direção | Relatórios de monitoramento, resultados auditoria interna, relatórios de incidentes, KPIs/KRIs |
| **Act (Agir)** | Ações corretivas, melhoria contínua, atualização de riscos/controles/políticas | Planos de ação corretiva, SGSI atualizado, lições aprendidas |

---

### Ciclo de Vida da Informação

```
CRIAÇÃO → CLASSIFICAÇÃO → USO/PROCESSAMENTO → COMPARTILHAMENTO → ARMAZENAMENTO → DESCARTE
   ↑                                                                              ↓
   └────────────────── REVISÃO PERIÓDICA / RECLASSIFICAÇÃO ──────────────────────┘
```

| Fase | Atividades-Chave | Controles |
|------|------------------|-----------|
| **Criação** | Classificação imediata pelo autor, rotulagem | Templates com classificação padrão, DLP preventivo |
| **Classificação** | Definir nível (Público/Interno/Confidencial/Restrito), owner | Matriz de classificação, aprovação do owner |
| **Uso/Processamento** | Acesso por necessidade, integridade, logs | Controle de acesso (RBAC/ABAC), versionamento, watermarking |
| **Compartilhamento** | Avaliar necessidade, canal seguro, NDA, acordos | Criptografia, DLP, rights management (IRM), data sharing agreements |
| **Armazenamento** | Local aprovado, criptografia em repouso, backup, retenção | Criptografia AES-256, backup testado, imutabilidade (WORM), geolocalização |
| **Descarte** | Destruição segura, certificado de destruição, atualização inventário | NIST SP 800-88 (Clear/Purge/Destroy), trituração P-4+, desmagnetização, cripto-shredding |

---

### Gestão de Vulnerabilidades — Ciclo Contínuo

```
IDENTIFICAR → AVALIAR → TRATAR → MONITORAR → (volta a IDENTIFICAR)
```

| Fase | Atividades | Ferramentas / Artefatos |
|------|------------|-------------------------|
| **Identificar** | Inventário de ativos (CMDB), varredura de vulns (credenciada/não credenciada), threat intelligence, code review (SAST/DAST/SCA), bounty | Nessus, OpenVAS, Qualys, Tenable, Nuclei, SonarQube, Checkmarx, Snyk, Dependabot |
| **Avaliar** | CVSS v3.1/v4.0 (Base, Temporal, Environmental), contexto de negócio, exploitabilidade (EPSS), ativo afetado, compensating controls | CVSS Calculator, FIRST EPSS, Kenna, RiskSense, contexto CMDB |
| **Tratar** | **Corrigir** (patch, config), **Mitigar** (WAF, segmentação, regra FW), **Aceitar** (risco residual documentado, aprovação gestor), **Transferir** (seguro cibernético), **Evitar** (descomissionar) | Patch management (WSUS, SCCM, Ansible), WAF rules, firewall rules, risk register |
| **Monitorar** | Re-scan pós-patch, continuous monitoring, threat hunting, KPIs (MTTR, % criticas >30d, cobertura scan) | Dashboards, SLAs, relatórios executivos, threat intel feeds |

### Métricas-Chave (KPIs / KRIs)

| Métrica | Fórmula / Definição | Meta Típica |
|---------|---------------------|-------------|
| **Cobertura de Scan** | Ativos escaneados / Ativos totais no CMDB | ≥ 95% |
| **MTTR (Mean Time To Remediate)** | Média de dias para corrigir por severidade | Crítica ≤ 7d, Alta ≤ 30d, Média ≤ 90d |
| **Vulnerabilidades Abertas > SLA** | Count por severidade fora do prazo | Zero críticas/altas fora SLA |
| **Taxa de Reincidência** | Vulns reabertas / Total corrigidas | < 5% |
| **Cobertura de Patch** | Sistemas patched / Total sistemas | ≥ 95% em 30d (crítico) |

### Integração com Gestão de Mudanças

| Gatilho | Ação de Segurança |
|---------|-------------------|
| Nova vulnerabilidade crítica (ex: Log4Shell) | Change de emergência (CAB exec), patch prioritário, compensating control imediato |
| Mudança de infraestrutura (novo servidor, app, rede) | Threat modeling, hardening baseline, scan pré-produção, atualização CMDB |
| Fim de vida (EOL) de software/hardware | Plano de migração, compensating controls até migração, aceitação de risco documentada |

---

### Responsabilidades (RACI Resumido)

| Atividade | CISO/Segurança | TI/Infra | Donos de Negócio | Auditoria |
|-----------|----------------|----------|------------------|-----------|
| Definir política/objetivos | **R** | C | I | A |
| Análise de risco | **R** | C | **R** (contexto) | I |
| Implementar controles | A | **R** | C | I |
| Scan de vulns | **R** | **R** (execução) | I | I |
| Aprovar aceitação de risco | A | C | **R** | I |
| Auditoria interna | I | C | I | **R** |
| Análise crítica pela direção | **R** | I | A | I |

> **R** = Responsible (executa), **A** = Accountable (aprova/responde), **C** = Consulted (opina), **I** = Informed (informado)
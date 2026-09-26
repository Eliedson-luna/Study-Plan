## Continuidade de Negócios Básica (ISO 22301 / NIST 800-34)

### Conceitos Fundamentais

| Sigla | Nome | Definição |
|-------|------|-----------|
| **BCM** | Business Continuity Management | Gestão holística para identificar ameaças, construir resiliência e garantir resposta efetiva |
| **BCP** | Business Continuity Plan | Plano documentado para **manter/retomar** processos de negócio em nível mínimo aceitável |
| **DRP** | Disaster Recovery Plan | Plano técnico para **recuperar infraestrutura/TI** (sistemas, dados, rede) após desastre |
| **BIA** | Business Impact Analysis | Análise que quantifica impactos de interrupção e define prioridades de recuperação |
| **RTO** | Recovery Time Objective | **Tempo máximo** aceitável para restaurar um processo/sistema após interrupção |
| **RPO** | Recovery Point Objective | **Perda máxima de dados** aceitável (tempo entre último backup e falha) |
| **MTPD** | Maximum Tolerable Period of Disruption | Tempo máximo que o negócio pode ficar parado antes de falência/colapso irrecuperável |
| **MBCO** | Minimum Business Continuity Objective | Nível mínimo de serviço/produção que deve ser mantido durante a interrupção |

> **Relação**: RTO ≤ MTPD. RPO define frequência de backup/replicação.

---

### BIA — Business Impact Analysis (Passos)

1. **Identificar processos críticos** — Entrevistas com donos de processo, mapeamento cadeia de valor
2. **Determinar dependências** — TI (sistemas, rede, dados), pessoas, fornecedores, instalações, equipamentos
3. **Quantificar impactos** por horizonte temporal:
   - **Impacto Financeiro** (receita perdida, multas, custos recuperação)
   - **Impacto Operacional** (clientes afetados, SLA violados)
   - **Impacto Legal/Regulatório** (LGPD, Bacen, CVM, ANP)
   - **Impacto Reputacional** (imagem, confiança)
   - **Impacto Segurança/Vida** (segurança física, saúde)
4. **Definir RTO e RPO** por processo/sistema
5. **Classificar criticidade** (Crítico / Alto / Médio / Baixo)
6. **Validar com stakeholders** e aprovar com direção

---

### Classificação de Criticidade (Exemplo)

| Nível | RTO | RPO | Exemplos | Prioridade Recuperação |
|-------|-----|-----|----------|------------------------|
| **Crítico (Tier 1)** | ≤ 4 horas | ≤ 1 hora | Core banking, trading, SCADA/OT, e-commerce, ERP produção | 1ª — Recuperação imediata (hot site, replicação síncrona) |
| **Alto (Tier 2)** | 4-24 horas | ≤ 4 horas | E-mail corporativo, CRM, RH (folha), portal clientes | 2ª — Warm site, replicação assíncrona frequente |
| **Médio (Tier 3)** | 24-72 horas | ≤ 24 horas | BI/Analytics, file shares, dev/test, sistemas internos | 3ª — Cold site, backup diário |
| **Baixo (Tier 4)** | > 72 horas | ≤ 7 dias | Arquivo morto, sistemas legados sem uso ativo | 4ª — Backup semanal, restore sob demanda |

---

### Estratégias de Recuperação

| Estratégia | RTO Alvo | RPO Alvo | Custo | Descrição |
|------------|----------|----------|-------|-----------|
| **Hot Site** | Minutos - 1h | Near-zero (sync) | $$$$$ | Datacenter espelhado, ativo-ativo ou ativo-passivo quente, replicação síncrona |
| **Warm Site** | 4-24h | 1-4h (async frequente) | $$$ | Infra pré-configurada, dados replicados periodicamente, requer ativação |
| **Cold Site** | Dias | 24h+ (backup) | $$ | Espaço físico + energia + rede, equipamentos sob demanda, restore de backup |
| **Cloud DR / DRaaS** | Minutos-horas | Segundos-horas | $$-$$$ | Replicação para nuvem (AWS/Azure/GCP), failover automatizado, pay-per-use |
| **Backup Only** | Dias-Semanas | RPO do backup | $ | Apenas cópia de dados (3-2-1), restore manual, sem infra prévia |

---

### Backup — Estratégia 3-2-1 (Regra de Ouro)

| Regra | Significado |
|-------|-------------|
| **3** | Três cópias dos dados (original + 2 backups) |
| **2** | Duas mídias/tipos de armazenamento diferentes (ex: disco + fita / disco + cloud / NAS + object storage) |
| **1** | Uma cópia **off-site** (geograficamente separada) — **imutável** (WORM, Object Lock, air-gapped) |

### Tipos de Backup

| Tipo | O que copia | Tempo Backup | Tempo Restore | Espaço | Uso |
|------|-------------|--------------|---------------|--------|-----|
| **Completo (Full)** | Todos os dados | Lento | **Rápido** | Alto | Base semanal/mensal |
| **Incremental** | Só alterados desde último backup (qualquer tipo) | **Rápido** | Lento (cadeia completa) | Baixo | Diário/horário |
| **Diferencial** | Alterados desde último **Full** | Médio | Médio (Full + 1 Diff) | Médio | Diário |
| **Forever Incremental / Synthetic Full** | Incrementais contínuos + full sintético montado no storage | Rápido | Rápido | Otimizado | **Moderno (Veeam, Commvault, Rubrik, AWS Backup)** |
| **Snapshot / CDP** | Point-in-time (storage level) | Instantâneo | Instantâneo | Overhead storage | VMs, bancos, containers (RPO ~minutos) |

### Teste de Continuidade — Tipos e Frequência

| Tipo | Descrição | Frequência Mínima | Participantes |
|------|-----------|-------------------|---------------|
| **Walkthrough / Tabletop** | Revisão teórica do plano em mesa, cenários hipotéticos | Semestral | Gestores, donos de processo, TI, comunicação |
| **Simulação / Drill** | Execução parcial (ex: failover de 1 sistema, restore de 1 DB) | Semestral (críticos) / Anual (demais) | TI, DBAs, Infra, Segurança |
| **Teste de Corte Paralelo (Parallel)** | Ambiente DR roda em paralelo produção por período | Anual (críticos) | TI, Negócio valida dados |
| **Corte Total (Full Cutover)** | Failover real para DR, produção desligada | **Raro** (alto risco) — apenas se exigido por regulador | Todos + Direção |
| **Teste de Backup/Restore** | Restore amostral de sistemas críticos | **Mensal** (críticos) / Trimestral (demais) | DBAs, Infra |

> **Evidência**: Relatório de teste + lições aprendidas + plano de ação corretiva + assinatura dos participantes

---

### Estrutura do BCP (ISO 22301)

1. **Objetivo e Escopo**
2. **Governança e Responsabilidades** (Crisis Management Team, BCP Owner, Equipe Técnica, Comunicação)
3. **Resultados da BIA** (Processos críticos, RTO/RPO, dependências)
4. **Estratégias de Continuidade** (Por processo: workaround manual, site alternativo, terceirização)
5. **Planos de Ação por Cenário** (Perda de site, perda de TI, pandemia, ataque cibernético, fornecedor crítico)
6. **Comunicação de Crise** (Stakeholders internos/externos, templates, porta-voz, mídia, reguladores)
7. **Recursos Necessários** (Pessoas, tecnologia, instalações, fornecedores, contratos SLAs)
8. **Procedimentos de Ativação/Desativação** (Gatilhos, autoridade para declarar desastre, stand-down)
9. **Testes, Manutenção e Melhoria** (Calendário, registros, KPIs)
10. **Anexos** (Listas de contato, inventário, contratos, mapas, checklists)

---

### Integração com Gestão de Incidentes e Riscos

| Evento | Fluxo |
|--------|-------|
| Incidente de segurança (ex: ransomware) | **Resposta a Incidentes** → Contenção/Erradicação → Se exceder RTO → **Ativação BCP/DRP** |
| Risco residual alto identificado | **Tratamento de Risco** → Estratégia de continuidade (ex: replicação) → **Atualiza BCP/DRP** |
| Teste de DRP falha | **Incidente/Problema** → Análise causa raiz → **Atualiza BCP/DRP + Risco** |

---

### Métricas-Chave (KPIs)

| KPI | Meta Típica |
|-----|-------------|
| **% Processos Críticos com RTO/RPO Definidos** | 100% |
| **% Sistemas Críticos com DR Testado (últimos 12m)** | 100% |
| **Taxa de Sucesso Restore Backup (testes)** | ≥ 99% |
| **RTO Real vs RTO Planejado (em teste/incidente real)** | Real ≤ Planejado |
| **RPO Real vs RPO Planejado** | Real ≤ Planejado |
| **Cobertura Backup 3-2-1** | 100% ativos críticos |
| **Tempo para Declarar Desastre (Detection → Declaration)** | ≤ 30 min (críticos) |
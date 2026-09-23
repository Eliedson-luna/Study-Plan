## Gestão de Riscos Básica (ISO 27005 / NIST 800-30)

### Processo de Gestão de Riscos (ISO 27005)

```
ESTABELECER CONTEXTO → IDENTIFICAR RISCOS → ANALISAR RISCOS → AVALIAR RISCOS → TRATAR RISCOS
                                                      ↑                    ↓
                                              MONITORAR E REVISAR ← COMUNICAR E CONSULTAR
```

---

### 1. Estabelecer Contexto

| Elemento | Descrição |
|----------|-----------|
| **Contexto Externo** | Legal (LGPD, Marco Civil, setorial), regulatório, mercado, ameaças setoriais, dependências terceiros |
| **Contexto Interno** | Governança, cultura, recursos, arquitetura, ativos críticos, apetite de risco |
| **Critérios de Risco** | Escalas de probabilidade/impacto, matriz de risco, limites de aceitação, apetite/tolerância |
| **Escopo** | Sistemas, processos, ativos, fronteiras organizacionais incluídos |

---

### 2. Identificação de Riscos

| Entrada | Técnica |
|---------|---------|
| Ativos (CMDB) | Inventário: hardware, software, dados, pessoas, facilities, serviços cloud |
| Ameaças | Catálogo (ISO 27005 Annex B, ENISA Threat Landscape, MITRE ATT&CK, CAPEC) |
| Vulnerabilidades | Scans, pentests, code review, threat modeling, auditorias, incidentes passados |
| Controles Existentes | Políticas, normas, controles técnicos (FW, AV, criptografia, backup, treinamento) |

**Saída**: Lista de cenários de risco — `Ameaça × Vulnerabilidade × Ativo = Cenário de Risco`

Exemplo: `Ransomware (ameaça) × Falha de patch SMBv1 (vuln) × Servidor de arquivos financeiro (ativo) = Risco de criptografia/extorsão de dados financeiros`

---

### 3. Análise de Riscos — Cálculo

#### Escalas (Exemplo 5 Níveis)

| Nível | Probabilidade (Likelihood) | Impacto (Consequência) |
|-------|----------------------------|------------------------|
| **1 - Muito Baixa** | Raro, <1% ao ano | Insignificante, <R$ 10k, sem impacto operacional |
| **2 - Baixa** | Improvável, 1-10%/ano | Menor, R$ 10k-100k, impacto operacional leve |
| **3 - Média** | Possível, 10-50%/ano | Moderado, R$ 100k-1M, parada parcial <4h |
| **4 - Alta** | Provável, 50-90%/ano | Maior, R$ 1M-10M, parada >4h, vazamento dados sensíveis |
| **5 - Muito Alta** | Quase certo, >90%/ano | Catastrófico, >R$ 10M, parada >24h, vazamento massivo, sanção regulatória |

#### Matriz de Risco (Heat Map)

| Prob \ Impacto | 1 Insign. | 2 Menor | 3 Moder. | 4 Maior | 5 Catastr. |
|----------------|-----------|---------|----------|---------|------------|
| **5 Quase Certa** | Média | Alta | **Crítica** | **Crítica** | **Crítica** |
| **4 Provável** | Baixa | Média | Alta | **Crítica** | **Crítica** |
| **3 Possível** | Baixa | Baixa | Média | Alta | **Crítica** |
| **2 Improvável** | Muito Baixa | Baixa | Baixa | Média | Alta |
| **1 Raro** | Muito Baixa | Muito Baixa | Baixa | Baixa | Média |

> **Níveis de Risco**: Muito Baixa → Aceitar | Baixa → Aceitar/Monitorar | Média → Tratar | Alta → Tratar prioritário | Crítica → Tratar IMEDIATO + escalação direção

---

### 4. Avaliação de Riscos — Comparação com Critérios

| Nível de Risco | Ação |
|----------------|------|
| **Crítico / Alto** | **Tratar obrigatoriamente** — plano de ação com dono, prazo, orçamento, aprovação direção |
| **Médio** | Tratar se custo-efetivo; senão aceitar com justificativa documentada e revisão semestral |
| **Baixo / Muito Baixo** | Aceitar (monitorar passivamente) |

**Apetite vs Tolerância vs Limite**:
- **Apetite de Risco**: Quantidade/tipo de risco que a org **busca** para atingir objetivos (ex: "aceitamos risco médio em inovação")
- **Tolerância**: Variação aceitável ao redor do apetite (ex: "até 5 riscos altos simultâneos")
- **Limite (Capacity)**: Risco máximo que a org **pode** absorver sem falhar (ex: "zero risco crítico não tratado")

---

### 5. Tratamento de Riscos — 4 Opções (ISO 27005 / NIST)

| Opção | Descrição | Quando Usar | Exemplo |
|-------|-----------|-------------|---------|
| **Mitigar (Reduzir)** | Reduzir probabilidade e/ou impacto com controles | Risco > apetite, custo-efetivo | Patch, WAF, segmentação, criptografia, MFA, treinamento |
| **Aceitar (Retener)** | Reconhecer risco, não aplicar controle adicional | Risco ≤ apetite, custo > benefício, risco residual aceito | Risco baixo documentado, aprovação do owner |
| **Transferir (Compartilhar)** | Mover impacto para terceiros | Impacto financeiro alto, expertise externa | Seguro cibernético, outsourcing SOC, cláusulas contratuais com fornecedores |
| **Evitar (Eliminar)** | Eliminar a causa (descontinuar ativo/processo) | Risco inaceitável, não mitigável economicamente | Descomissionar sistema legado exposto, não entrar em mercado regulado sem compliance |

> **Risco Residual** = Risco Inerente − Efeito dos Controles. **Nunca zero**.
> Todo risco residual deve ser **documentado, aprovado pelo owner e revisado periodicamente**.

---

### Seleção de Controles (ISO 27001 Anexo A / NIST 800-53)

| Família ISO 27001:2022 (4 Temas, 93 Controles) | Exemplos |
|-----------------------------------------------|----------|
| **Organizacionais (A.5)** | Políticas, papéis, conscientização, gestão fornecedores |
| **Pessoas (A.6)** | Background check, termos confidencialidade, treinamento, disciplina |
| **Físicos (A.7)** | Perímetro seguro, acesso físico, proteção contra ameaças ambientais |
| **Tecnológicos (A.8)** | Controle acesso, criptografia, gestão vulns, logging, rede, desenvolvimento seguro |

**Critério de seleção**: Custo do controle < Redução esperada do risco (ALE - Annualized Loss Expectancy)

---

### Registro de Riscos (Risk Register) — Campos Mínimos

| Campo | Exemplo |
|-------|---------|
| ID | RISK-2026-042 |
| Título | Ransomware em servidor de arquivos financeiro |
| Ativo | SRV-FIN-01 (Windows Server 2019, SMBv1 ativo) |
| Ameaça | Ransomware (ex: LockBit, Cl0p) |
| Vulnerabilidade | CVE-2017-0144 (EternalBlue) — patch MS17-010 não aplicado |
| Probabilidade Inerente | 4 (Provável) |
| Impacto Inerente | 5 (Catastrófico — dados financeiros + PII LGPD) |
| Risco Inerente | **Crítico** |
| Controles Existentes | AV endpoint, backup diário (não testado restore), firewall perimetral |
| Probabilidade Residual | 3 (Possível) |
| Impacto Residual | 4 (Maior) |
| Risco Residual | **Alto** |
| Tratamento Escolhido | **Mitigar**: Aplicar patch MS17-010 (prazo 48h) + Desabilitar SMBv1 + Testar restore backup |
| Dono do Risco | Gerente Financeiro |
| Responsável Tratamento | Coordenador Infra |
| Prazo | 2026-05-15 |
| Status | Em andamento |
| Data Revisão | 2026-06-01 |

---

### Monitoramento e Revisão Contínua

| Gatilho de Revisão | Frequência / Ação |
|--------------------|-------------------|
| **Mudança significativa** (novo ativo, nova ameaça, incidente, lei) | Imediata — reavaliar riscos afetados |
| **Revisão programada** | Semestral (riscos críticos/altos), Anual (todos) |
| **KPIs fora da meta** | MTTR vencido, cobertura scan <95%, novos CVEs críticos |
| **Auditoria / Análise Crítica** | Conforme achados |

### Comunicação e Consulta

- **Interno**: Risk owners, CISO, Comitê de Riscos, Direção, Auditoria Interna
- **Externo**: Reguladores (Bacen, CVM, ANPD), Seguradores, Clientes (questionários segurança), Fornecedores críticos
- **Relatórios**: Heat map executivo, Top 10 riscos, Tendência (melhorando/piorando), Ações em andamento
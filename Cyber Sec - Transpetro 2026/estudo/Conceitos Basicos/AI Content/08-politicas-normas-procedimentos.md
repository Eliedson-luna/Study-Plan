## Políticas, Normas, Procedimentos e Guidelines

### Hierarquia Documental (Top-Down)

```
POLÍTICA (Política de SI)
    │  "O QUÊ" e "POR QUÊ" — direção estratégica, obrigatória, alta gerência aprova
    ▼
NORMA / PADRÃO (Normas/Padrões)
    │  "COMO" — requisitos técnicos mensuráveis, obrigatórios, versão controlada
    ▼
PROCEDIMENTO (Procedimentos/Instruções de Trabalho)
    │  "PASSO A PASSO" — operacional, detalhado, quem/faz/o quê/quando/como
    ▼
GUIDELINE / GUIA (Diretrizes/Orientações)
    │  "RECOMENDAÇÃO" — boas práticas, não obrigatório, flexível
    ▼
BASELINE (Linhas de Base / Baselines)
       Configurações mínimas obrigatórias por tipo de ativo (ex: hardening Windows Server 2022 baseline)
```

---

### Política de Segurança da Informação (Top-Level)

| Atributo | Detalhe |
|----------|---------|
| **Escopo** | Toda a organização, todos os ativos de informação, todas as pessoas |
| **Autoridade** | Alta direção / Conselho / CISO — **assinada pelo CEO/Presidente** |
| **Revisão** | Anual ou mediante mudança significativa (lei, incidente grave, reorganização) |
| **Conteúdo Mínimo (ISO 27001:2022 5.2)** | Objetivos, compromisso gestão, conformidade legal/regulatória, melhoria contínua, responsabilidades, comunicação, exceções (processo formal) |
| **Comunicação** | Disponível a todos (intranet, onboarding), treinamento obrigatório, aceite termo |

---

### Normas / Padrões Técnicos (Exemplos)

| Norma | Foco | Exemplo de Requisito Mensurável |
|-------|------|----------------------------------|
| **Norma de Controle de Acesso** | RBAC, MFA, provisionamento, revisão | "Todos acessos privilegiados exigem MFA FIDO2; revisão trimestral de acessos" |
| **Norma de Criptografia** | Algoritmos, chaves, TLS, dados em repouso | "TLS 1.2+ apenas; AES-256-GCM ou ChaCha20-Poly1305; RSA ≥3072 ou ECC P-256+" |
| **Norma de Gestão de Vulnerabilidades** | SLA por severidade, scan frequency | "Críticas: patch em 72h / compensating control em 24h; Scan mensal credenciado" |
| **Norma de Segurança em Desenvolvimento** | SDLC, SAST/DAST/SCA, secrets | "SAST em todo PR; SCA bloqueia CVE>7.0; secrets scanning obrigatório" |
| **Norma de Classificação e Manuseio** | Níveis, rótulos, descarte | "Dados confidenciais: criptografia em repouso/trânsito; descarte NIST SP 800-88 Purge" |
| **Norma de Continuidade** | RTO/RPO, testes, backup | "RTO 4h / RPO 1h para sistemas críticos; teste DRP semestral; backup 3-2-1" |
| **Norma de Resposta a Incidentes** | Classificação, SLA, comunicação | "Incidente crítico: notificação CISO em 1h, cliente/regulador em 24h (LGPD)" |

---

### Procedimentos — Estrutura Padrão

| Seção | Conteúdo |
|-------|----------|
| **1. Objetivo** | O que o procedimento entrega |
| **2. Escopo** | Aplicável a quais sistemas/processos/pessoas |
| **3. Referências** | Políticas, normas, leis, frameworks relacionados |
| **4. Definições** | Termos técnicos usados |
| **5. Responsabilidades** | Papéis (RACI) — quem executa, aprova, informa |
| **6. Pré-requisitos** | O que deve estar pronto antes de iniciar |
| **7. Passo a Passo** | Numerado, imperativo, com prints/referências a telas/scripts |
| **8. Tratamento de Exceções/Erros | O que fazer se falhar (rollback, escalação) |
| **9. Registros/Evidências** | Logs, assinaturas, tickets, relatórios gerados |
| **10. Métricas/KPIs** | Como medir eficácia |
| **11. Histórico de Versões** | Versão, data, autor, descrição da mudança, aprovação |

**Exemplo**: `PROC-SEC-003 - Provisionamento e Revogação de Acesso Privilegiado`

---

### Guidelines (Diretrizes) — Exemplos

| Guia | Natureza |
|------|----------|
| **Guia de Configuração Segura de Kubernetes** | Recomendações CIS Benchmark + adaptações internas — não obriga, orienta |
| **Guia de Desenvolvimento Seguro (OWASP ASVS)** | Checklist por nível (L1/L2/L3) — uso voluntário por squads |
| **Guia de Phishing e Engenharia Social** | Como identificar, reportar, simulações — educativo |
| **Guia de Classificação Rápida** | Árvore de decisão: "É dado pessoal? → Confidencial no mínimo" |

---

### Baselines (Linhas de Base) — Exemplo

| Ativo | Baseline | Ferramenta Validação |
|-------|----------|---------------------|
| **Windows Server 2022** | CIS Benchmark L1/L2, STIG, sem SMBv1, TLS 1.2+, auditoria 4624/4625/4688 | PowerShell DSC, Ansible, GPO, OpenSCAP |
| **Linux (RHEL/Ubuntu)** | CIS Benchmark, kernel hardening (sysctl), sshd_config (no root, pubkey only), auditd | Lynis, OpenSCAP, Ansible |
| **Kubernetes (EKS/AKS/GKE)** | CIS K8s Benchmark, Pod Security Standards (Restricted), Network Policies, RBAC least priv | kube-bench, Polaris, Kyverno, OPA Gatekeeper |
| **AWS/GCP/Azure** | CIS Foundations Benchmark, SCPs, GuardDuty, Security Hub, IAM least priv | Prowler, ScoutSuite, Cloud Custodian |

---

### Ciclo de Vida do Documento

```
CRIAÇÃO → REVISÃO TÉCNICA → APROVAÇÃO (Owner + CISO + Jurídico se aplicar)
    → PUBLICAÇÃO (intranet, versionamento, notificação partes interessadas)
    → TREINAMENTO/CONSCIENTIZAÇÃO (se mudança relevante)
    → VIGÊNCIA (data efetiva)
    → MONITORAMENTO CONFORMIDADE (auditoria, KPIs)
    → REVISÃO PERIÓDICA (anual ou gatilho) → ATUALIZAÇÃO → (repete)
    → REVOGAÇÃO (se obsoleto/substituído) → ARQUIVAMENTO (retenção legal)
```

### Controle de Versões — Convenção

| Formato | Exemplo | Significado |
|---------|---------|-------------|
| **vM.m.p** | v2.1.0 | **M**ajor (mudança estrutural/escopo), **m**inor (adição requisito), **p**atch (correção textual/formatação) |
| **Data + Versão** | 2026.04-v1.0 | Ano.Mês + versão sequencial |

### Matriz de Aprovação Mínima

| Tipo Documento | Aprovação Mínima |
|----------------|------------------|
| Política de SI | CEO / Presidente + CISO + Jurídico |
| Norma/Padrão Técnico | CISO + Gerente TI + DPO (se dados pessoais) |
| Procedimento Operacional | Gerente da área + CISO (se transversal) |
| Guideline | Autor técnico + revisão par |
| Baseline | Arquitetura Segurança + Infra + Validação automatizada |
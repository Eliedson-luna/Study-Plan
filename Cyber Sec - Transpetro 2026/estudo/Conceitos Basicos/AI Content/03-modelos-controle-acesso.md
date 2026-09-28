# Modelos de Controle de Acesso

## DAC — Discretionary Access Control (Controle Discricionário)

**Quem decide**: Dono do objeto (arquivo, pasta, tabela, recurso).
**Mecanismo**: ACL (Access Control List) — lista de sujeitos (usuários/grupos) × permissões (read, write, execute, delete, take ownership).
**Exemplos**: Permissões NTFS (Windows), `chmod`/`chown`/`setfacl` (Linux), compartilhamentos SMB/NFS, permissões de banco de dados (GRANT/REVOKE).

| Vantagens | Desvantagens |
|-----------|--------------|
| Flexível, intuitivo, fácil de implementar | Propagação de erro: dono pode conceder acesso indevido acidentalmente |
| Baixo custo administrativo inicial | Difícil auditar "quem tem acesso a quê" em escala (espalhamento de ACLs) |
| Adequado para dados de baixo risco, colaboração ad-hoc | Não atende requisitos de conformidade rígidos (governo, defesa, banco central) |
| Modelo padrão da maioria dos FS/SOs | "Confused Deputy" problem — programa age em nome do usuário com privilégios do usuário |

---

## MAC — Mandatory Access Control (Controle Obrigatório)

**Quem decide**: Política de segurança central baseada em **labels/classificações** (sujeito e objeto têm rótulos). O sistema *impede* a decisão do usuário — não há "dono" que possa alterar.
**Modelos Clássicos Teóricos (caem em prova conceitual)**:

| Modelo | Foco | Regra Principal | Mnemônico |
|--------|------|-----------------|-----------|
| **Bell-LaPadula (BLP)** | Confidencialidade | *No read up, no write down* (Simple Security Property, *-Property) | "Não lê segredo acima; não escreve segredo abaixo" |
| **Biba** | Integridade | *No read down, no write up* | "Não lê lixo; não contamina limpo" |
| **Clark-Wilson** | Integridade transacional | Triplas (User, Transformation Procedure, Constrained Data Item) + IVP + Separação de deveres | Foco em transações bem-formadas, não em labels |

**Implementações Reais**: SELinux (Linux), TrustedBSD, Windows Integrity Levels (baixo/médio/alto/sistema), Solaris Trusted Extensions.

| Vantagens | Desvantagens |
|-----------|--------------|
| Garantia forte de confidencialidade/integridade (matemática) | Rigidez operacional — usuários não podem compartilhar legitimamente |
| Atende requisitos governamentais/militares (Classified, Top Secret) | Complexo de configurar, manter, depurar (policy writing) |
| Decisão não depende do usuário (não há "erro humano" de permissão) | Overhead de performance (verificação de label em *todo* acesso ao kernel) |

---

## RBAC — Role-Based Access Control (Baseado em Funções/Papéis)

**Quem decide**: Administrador de segurança atribui **roles** a usuários; permissões atreladas às roles (não ao usuário diretamente).
**Estrutura**: Usuário → Role(s) → Permissões (Objeto + Operação + Contexto opcional).
**Exemplos**: Grupos AD (Domain Admins, Backup Operators), AWS IAM Roles, Kubernetes RBAC (Role/ClusterRole + RoleBinding), Perfis SAP, Oracle Database Roles.

| Vantagens | Desvantagens |
|-----------|--------------|
| Escalável; gestão centralizada (onboarding/offboarding = add/remove role) | **Role Explosion** — roles granulares demais viram pesadelo de manutenção |
| Alinhado a processos de negócio (função = papel no negócio) | Difícil expressar regras contextuais (hora, local, risco, device trust) |
| Auditoria simples: Usuário ↔ Role ↔ Permissão | Não suporta nativamente separação de deveres *dinâmica* (conflito de roles) |
| Padrão de facto em ambientes corporativos e cloud | Herança de role pode criar concessões implícitas não óbvias |

**Extensões Comuns (NIST RBAC Model)**:
- **RBAC0** (Core): Users, Roles, Permissions, Sessions
- **RBAC1** (Hierárquico): Role inheritance (Senior_Admin herda Admin herda Operator)
- **RBAC2** (Com Restrições): Static Separation of Duties (SSD) — roles mutuamente exclusivas
- **RBAC3** (Unificado): RBAC1 + RBAC2
- **ARBAC** (Administrative RBAC): Delegação de administração de roles

---

## ABAC — Attribute-Based Access Control (Baseado em Atributos)

**Quem decide**: **Policy Decision Point (PDP)** avalia atributos em tempo real via linguagem de política (XACML, OPA/Rego, Cedar, ALFA).
**Atributos (4 categorias)**:

| Categoria | Exemplos de Atributos |
|-----------|----------------------|
| **Sujeito** | `user.id`, `user.dept`, `user.clearance`, `user.role`, `user.device_trust_level`, `user.mfa_verified`, `user.location` |
| **Recurso** | `resource.id`, `resource.classification`, `resource.owner`, `resource.sensitivity`, `resource.region` |
| **Ação** | `action.id` (read, write, delete, approve, export, decrypt), `action.purpose` |
| **Ambiente** | `env.time`, `env.network_zone`, `env.threat_level`, `env.compliance_mode` |

**Exemplo de Política (OPA/Rego)**:
```rego
allow if {
    input.user.department == input.resource.owner_department
    input.user.clearance >= input.resource.classification
    input.env.time in business_hours
    input.user.mfa_verified == true
    not input.user.is_terminated
}
```

| Vantagens | Desvantagens |
|-----------|--------------|
| Expressividade máxima; decisões contextuais dinâmicas (Zero Trust) | Complexidade de autoría de políticas; latência de decisão (ms importam) |
| Zero "role explosion" — atributos substituem roles granulares | Requer infra madura: PDP/PEP, fontes de atributo confiáveis (IdP, CMDB, MDM) |
| Suporte nativo a Zero Trust, Continuous Authorization | Curva de aprendizado alta; ferramentas menos maduras que RBAC |
| Auditoria de *por que* decidiu (policy explain) | Teste de regressão de políticas é crítico |

---

## Comparativo Resumido (Para Prova)

| Critério | DAC | MAC | RBAC | ABAC |
|----------|-----|-----|------|------|
| **Granularidade da Decisão** | Objeto × Usuário | Label Sujeito × Label Objeto | Role × Objeto | Atributo Sujeito/Recurso/Ação/Ambiente |
| **Flexibilidade** | Alta | Baixa | Média | **Muito Alta** |
| **Custo Administrativo** | Baixo (inicial) → Alto (escala) | Alto (setup + manutenção) | Médio (gestão de roles) | Alto (setup) → Baixo (operação) |
| **Facilidade de Auditoria** | Difícil (ACLs espalhadas) | Fácil (labels centralizados) | Fácil (role assignment) | Média (precisa de policy explain) |
| **Conformidade Regulatória** | Baixa | **Alta** (gov/mil) | **Alta** (corporativo, SOX, PCI) | **Alta** (Zero Trust, LGPD, NIST 800-207) |
| **Casos de Uso Típicos** | FS locais, compartilhamentos simples, dados baixo risco | Governo, defesa, inteligência, dados classificados | Empresas médias/grandes, ERP, AD, Cloud IAM (AWS/Azure/GCP) | APIs, microsserviços, Zero Trust, context-aware, fintech, healthtech |

---

## Escolha Prática — Guia Rápido

| Cenário | Modelo Recomendado | Justificativa |
|---------|-------------------|---------------|
| Pequena equipe, arquivos locais, colaboração simples | DAC (NTFS/ACL, chmod) | Simplicidade; overhead zero |
| Órgão público, dados sigilosos, classificação formal | MAC (SELinux, BLP/Biba) | Requisito legal; não-confiança no usuário |
| Corporação com AD, ERP, múltiplos sistemas, turnover | RBAC (AD Groups, IAM Roles) | Escalabilidade; alinhamento negócio; ferramentas maduras |
| Arquitetura cloud-native, microsserviços, APIs, Zero Trust | ABAC (OPA, Cedar, AuthZForce) | Decisão contextual; fine-grained; continuous auth |
| Requisitos mistos (legado + cloud + compliance) | **Híbrido**: RBAC base (roles amplas) + ABAC para decisões sensíveis (dados PII, financeiro, admin) | Pragmatismo; transição gradual |
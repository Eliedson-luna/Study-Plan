# Pilares de Segurança da Informação

## CIA Triad (Tríade Clássica)

### Confidencialidade
Garante que a informação só esteja disponível para quem tem autorização. Violação = acesso não autorizado.
- **Controles**: Criptografia (em trânsito e em repouso), Controle de acesso (RBAC/ABAC), Classificação da informação, DLP, Mascaramento de dados.

### Integridade
Garante que a informação não foi alterada de forma não autorizada (acidental ou maliciosa). Violação = modificação não autorizada.
- **Controles**: Hash criptográfico (SHA-256), Assinatura digital, HMAC, Controle de versão, WAF/IPS, Backup íntegro, Blockchain/ledger imutável.

### Disponibilidade
Garante que a informação e os sistemas estejam acessíveis quando necessário. Violação = indisponibilidade (DoS, falha hardware, ransomware).
- **Controles**: Redundância (RAID, cluster, multi-AZ), Backup e restore testado, Balanceamento de carga, Proteção DDoS, Plano de continuidade (BCP/DRP), Monitoramento/alertas.

---

## Pilares Estendidos (ISO 27001 / NBR ISO 27002)

| Pilar | Definição | Exemplo de Controle |
|-------|-----------|---------------------|
| **Autenticidade** | Garante que a identidade do sujeito (pessoa, sistema, processo) é quem diz ser | MFA, Certificados digitais, Autenticação baseada em risco |
| **Autorização** | Define o que um sujeito autenticado *pode* fazer (permissões) | RBAC, ABAC, Menor privilégio, Segregação de funções (SoD) |
| **Irretratabilidade (Não-repúdio)** | Impede que uma parte negue ter realizado uma ação | Assinatura digital (certificado ICP-Brasil), Logs de auditoria imutáveis, Carimbo do tempo |
| **Responsabilidade (Accountability)** | Rastreia ações a um sujeito único para posterior auditoria | Logs centralizados (SIEM), Trilha de auditoria, Identificadores únicos por usuário |

---

## Princípios Fundamentais de Projeto Seguro

| Princípio | Descrição | Aplicação Prática |
|-----------|-----------|-------------------|
| **Menor Privilégio (Least Privilege)** | Conceder apenas o acesso mínimo necessário para a função | Usuários sem admin; service accounts com escopo restrito; just-in-time access |
| **Defesa em Profundidade (Defense in Depth)** | Camadas múltiplas de controle; falha de uma não compromete tudo | Firewall perimetral + IDS/IPS + Host firewall + App sec + Criptografia + Treinamento |
| **Falha Segura (Fail-Safe / Fail-Closed)** | Em caso de falha, o sistema nega acesso por padrão | Firewall bloqueia se regra falha; auth nega se MFA indisponível; default-deny |
| **Separação de Deveres (Separation of Duties - SoD)** | Nenhum indivíduo controla todo um processo crítico | Dev ≠ Prod; Aprovação ≠ Execução; Backup operador ≠ Admin de backup |
| **Economia de Mecanismo (Economy of Mechanism)** | Manter o design o mais simples possível — menos superfície de ataque | Microserviços pequenos; remover código morto; desabilitar serviços não usados |
| **Mediação Completa (Complete Mediation)** | Verificar autorização a *cada* acesso, não só no login | Token JWT com validação contínua; re-autenticação para ações sensíveis (step-up auth) |
| **Psicologicamente Aceitável** | Controles não devem dificultar excessivamente o trabalho legítimo | SSO, MFA adaptativo (push vs SMS), UX de segurança bem desenhada |

---

## Resumo Comparativo

| Pilar | Pergunta-chave | Ameaça Principal | Mecanismo Central |
|-------|----------------|------------------|-------------------|
| Confidencialidade | "Quem pode ver?" | Vazamento, sniffing | Criptografia + Controle de acesso |
| Integridade | "Foi alterado?" | Tampering, injeção | Hash + Assinatura + Controle versão |
| Disponibilidade | "Está acessível?" | DoS, ransomware, falha HW | Redundância + Backup + BCP/DRP |
| Autenticidade | "É quem diz ser?" | Spoofing, credential stuffing | MFA + Certificados |
| Autorização | "Pode fazer isso?" | Escalação de privilégio | RBAC/ABAC + SoD |
| Irretratabilidade | "Pode negar?" | Repúdio de transação | Assinatura digital + Logs imutáveis |
| Responsabilidade | "Quem fez?" | Ação anônima maliciosa | Auditoria + SIEM + Identificador único |
# Autenticação, Autorização e Auditoria (AAA)

## Autenticação (Authentication) — "Quem é você?"

### Fatores de Autenticação

| Categoria | Fator | Exemplos |
|-----------|-------|----------|
| **Conhecimento** (Something you know) | Senha, PIN, frase secreta, padrão | Senha, resposta a pergunta secreta |
| **Posse** (Something you have) | Token, smartcard, celular, OTP hardware | Google Authenticator, YubiKey, SMS/Email OTP, certificado digital |
| **Inerência** (Something you are) | Biometria | Impressão digital, face, íris, voz, geometria da mão |
| **Comportamento** (Something you do) | Padrão comportamental | Keystroke dynamics, mouse dynamics, gait analysis |
| **Localização** (Somewhere you are) | Contexto geográfico/rede | GPS, IP confiável, rede corporativa, beacon BLE |

### MFA / 2FA — Combinações Válidas

| Combinação | Válida? | Exemplo |
|------------|---------|---------|
| Senha + SMS OTP | ✅ (posse) | Bancos, redes sociais |
| Senha + App Authenticator (TOTP) | ✅ (posse) | GitHub, AWS, Google |
| Senha + Certificado digital (A1/A3) | ✅ (posse) | ICP-Brasil, e-CPF, e-CNPJ |
| Senha + Biometria | ✅ (inerência) | Windows Hello, smartphones |
| SMS OTP + Email OTP | ❌ (ambos posse, mesmo canal) | Não recomendado |
| Duas senhas | ❌ (ambos conhecimento) | Não é MFA |

> **Regra**: MFA exige **dois fatores de categorias diferentes**. Dois fatores da mesma categoria = 2SV (Two-Step Verification), não MFA.

---

## Autorização (Authorization) — "O que você pode fazer?"

### Modelos (resumo — ver `03-modelos-controle-acesso.md`)
- **DAC**: Dono decide (ACL)
- **MAC**: Labels/sistema decide (Bell-LaPadula, Biba)
- **RBAC**: Role decide (AD groups, IAM roles)
- **ABAC**: Policy engine decide (atributos + contexto)

### Princípios Aplicados
- **Menor Privilégio**: Acesso mínimo necessário
- **Need-to-Know**: Acesso só se necessário para a tarefa
- **Separação de Deveres (SoD)**: Funções críticas divididas (ex: quem cria não aprova)
- **Just-in-Time (JIT)**: Acesso temporário, elevado sob demanda (PAM)

---

## Auditoria / Accounting — "O que você fez?"

### Objetivos
- **Rastreabilidade**: Vincular ação a identidade autenticada
- **Não-repúdio**: Prova inegável de autoria (logs assinados, carimbo do tempo)
- **Detecção de Anomalias**: Padrões fora do baseline (UEBA)
- **Conformidade**: Evidência para auditorias (LGPD, ISO 27001, SOX, PCI-DSS)

### O que Logar (mínimo)
| Evento | Campos Essenciais |
|--------|-------------------|
| Login/Logout | User, timestamp, IP, device, MFA status, sucesso/falha |
| Acesso a dados sensíveis | User, resource, action (read/export/print), timestamp, classificação |
| Mudança de permissão | Admin, target_user, role_before, role_after, justification |
| Operação privilegiada | User, command, target, timestamp, session_id |
| Falha de segurança | User, event_type, details, timestamp, source_ip |

### Boas Práticas
- **Centralização**: SIEM / Log Aggregator (Elastic, Splunk, Graylog, Wazuh)
- **Imutabilidade**: Write-once storage, assinatura digital de logs, blockchain/merkle tree
- **Retenção**: Conforme política/regulação (ex: LGPD — 6 meses a 5 anos; bancos — 5-10 anos)
- **Correlação**: Regras de alerta (ex: 5 falhas login em 5 min → brute force; acesso fora horário + país diferente → conta comprometida)
- **Cadeia de Custódia**: Hash do log original + assinatura do coletor → integridade probatória

---

## Protocolos e Padrões AAA

| Protocolo/Padrão | Camada | Uso Principal | Autenticação | Autorização | Auditoria |
|------------------|--------|---------------|--------------|-------------|-----------|
| **RADIUS** | Aplicação (UDP 1812/1813) | Acesso rede (VPN, Wi-Fi 802.1X, dial-up) | ✅ (PAP, CHAP, EAP) | ✅ (AVPs) | ✅ (Accounting) |
| **TACACS+** | Aplicação (TCP 49) | Admin de dispositivos de rede (Cisco) | ✅ | ✅ (granular, por comando) | ✅ |
| **Kerberos** | Aplicação (TCP/UDP 88) | SSO domínio Windows/AD, Linux | ✅ (tickets) | ✅ (PAC/SPNEGO) | ✅ (KDC logs) |
| **SAML 2.0** | Aplicação (HTTP/POST) | Federation/SSO empresarial (IdP → SP) | ✅ (Assertion) | ✅ (Attributes) | ✅ (IdP logs) |
| **OIDC / OAuth 2.0** | Aplicação (HTTPS) | SSO moderno, APIs, mobile, SPA | ✅ (ID Token) | ✅ (Access Token + scopes) | ✅ (Token introspection) |
| **LDAP / LDAPS** | Aplicação (TCP 389/636) | Diretório, autenticação bind | ✅ (Simple bind, SASL) | ❌ (não é autorização nativa) | ✅ (Access logs) |
| **DIAMETER** | Aplicação (TCP/SCTP 3868) | Sucessor RADIUS (4G/5G, IMS) | ✅ | ✅ | ✅ |

---

## Fluxo Típico AAA (ex: VPN corporativa)

```
User → [Credenciais + MFA] → RADIUS Server → [Valida AD/LDAP + Policy] 
    → Access-Accept (com AVPs: VLAN, ACL, session-timeout) 
    → NAS/VPN Gateway aplica políticas 
    → Accounting-Start → [Sessão ativa] → Accounting-Interim (periódico) 
    → Accounting-Stop → Logs no SIEM
```

---

## Checklist de Maturidade AAA

- [ ] MFA obrigatório para acesso remoto, admin, dados sensíveis
- [ ] Senhas: política de complexidade + rotação + bloqueio + hash forte (bcrypt/Argon2)
- [ ] Contas de serviço: gerenciadas (PAM), rotação automática, sem login interativo
- [ ] RBAC/ABAC implementado; revisão trimestral de acessos (recertificação)
- [ ] Logs AAA centralizados, imutáveis, retidos conforme política
- [ ] Alertas de anomalia configurados (geo-impossível, horário, volume, privilege escalation)
- [ ] Acesso JIT para admin; sessões gravadas (PAM)
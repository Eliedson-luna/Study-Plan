## PKI Básico (Public Key Infrastructure)

### Componentes da PKI

| Componente | Função | Detalhes |
|------------|--------|----------|
| **CA Raiz (Root CA)** | Confiança absoluta, auto-assinada | Offline, air-gapped, longa vida (10-25 anos), assina CAs subordinadas |
| **CA Subordinada / Emissora (Issuing CA)** | Emite certificados finais | Online, vida média (3-5 anos), assinada pela Root, pode ter múltiplas (por finalidade) |
| **RA (Registration Authority)** | Valida identidade antes de emitir | Verifica documentos, aprova/rejeita solicitações, não assina certs |
| **Repositório de Certificados** | Armazena e publica certificados | LDAP, HTTP, AD CS, banco de dados |
| **Serviço de Revogação** | Indica certs inválidos antes do vencimento | **CRL** (Certificate Revocation List) — lista periódica; **OCSP** (Online Certificate Status Protocol) — tempo real |
| **Usuários Finais / Entidades** | Solicitam e usam certificados | Pessoas, servidores, dispositivos, serviços, código |

### Certificado X.509 v3 — Campos Principais

| Campo | Descrição |
|-------|-----------|
| **Version** | v3 (value=2) — suporta extensões |
| **Serial Number** | Único por CA emissora (inteiro positivo, ≤20 octetos) |
| **Signature Algorithm** | Ex: `sha256WithRSAEncryption`, `ecdsa-with-SHA256` |
| **Issuer** | DN da CA emissora (ex: `CN=AC Transpetro, O=Transpetro, C=BR`) |
| **Validity** | `NotBefore` / `NotAfter` (UTCTime ou GeneralizedTime) |
| **Subject** | DN do titular (ou vazio se SAN usado) |
| **Subject Public Key Info** | Algoritmo + chave pública (RSA 2048+/3072+, ECC P-256/P-384, Ed25519) |
| **Extensions (críticas)** | |
| `Basic Constraints` | `CA:TRUE/FALSE`, `pathlen` (profundidade cadeia) |
| `Key Usage` | `digitalSignature`, `keyEncipherment`, `keyCertSign`, `cRLSign`, `nonRepudiation`, `dataEncipherment` |
| `Extended Key Usage (EKU)` | `serverAuth`, `clientAuth`, `codeSigning`, `emailProtection`, `timeStamping`, `OCSPSigning` |
| `Subject Alternative Name (SAN)` | DNS, IP, email, UPN, URI — **obrigatório para TLS moderno** |
| `Authority Key Identifier (AKI)` | Hash da chave pública da CA emissora (liga cadeia) |
| `Subject Key Identifier (SKI)` | Hash da chave pública do certificado |
| `CRL Distribution Points` | URL(s) para baixar CRL |
| `Authority Information Access (AIA)` | URL da CA emissora + OCSP responder |
| `Certificate Policies` | OID da política de certificação (ex: ICP-Brasil N3) |

### Cadeia de Confiança (Chain of Trust)

```
Root CA (auto-assinada, trust anchor no trust store)
    │ assina
    ▼
Subordinate CA 1 (ex: AC TLS)
    │ assina
    ▼
Certificado Final (ex: servidor web *.transpetro.gov.br)
```

**Validação do cliente**:
1. Verifica assinatura de cada cert com a chave pública do emissor
2. Verifica validade (notBefore/notAfter)
3. Verifica revogação (CRL/OCSP)
4. Verifica EKU compatível com uso (ex: `serverAuth` para HTTPS)
5. Verifica nome (SAN/CN) corresponde ao host acessado
6. Verifica caminho até trust anchor conhecido (Root CA no trust store do OS/navegador)

### Tipos de Certificados

| Tipo / EKU | Uso | Validade Típica |
|------------|-----|-----------------|
| **TLS/SSL Server** (`serverAuth`) | HTTPS, LDAPS, SMTPS, IMAPS | 90-398 dias (padrão CA/B Forum: 398 máx) |
| **TLS Client** (`clientAuth`) | mTLS, VPN, 802.1X (EAP-TLS) | 1-3 anos |
| **Assinatura Digital** (`nonRepudiation` + `emailProtection`) | Documentos, e-mails (S/MIME) | 1-3 anos |
| **Code Signing** (`codeSigning`) | Executáveis, scripts, drivers, containers | 1-3 anos (EV: 2 anos, hardware token) |
| **Time Stamping** (`timeStamping`) | Carimbo do tempo (RFC 3161) | 5-10 anos |
| **OCSP Responder** (`OCSPSigning`) | Respostas OCSP assinadas | Curta (dias/semanas) ou delegada |
| **Document Signing (Adobe CDS)** | PDFs confiáveis no Adobe | 1-3 anos |

### ICP-Brasil (Infraestrutura de Chaves Públicas Brasileira)

| Nível | Garantia | Uso | Requisitos Principais |
|-------|----------|-----|----------------------|
| **N1** | Básico | Assinatura simples, e-mail | Validação por e-mail/CPF, software |
| **N2** | Médio | Documentos com validade jurídica | Validação presencial ou videoconferência, certificado em token/smartcard |
| **N3** | Alto | Documentos de alto valor, procuração, saúde | Validação presencial obrigatória, token criptográfico certificado (FIPS 140-2 Nível 2/3), HSM na CA |
| **N4** | Muito Alto | Transações financeiras de altíssimo risco | HSM certificado, múltiplos fatores, auditoria contínua |

**Estrutura ICP-Brasil**:
```
AC-Raiz (ITI) → ACs de 1º Nível (ex: Serasa, Valid, Certisign) → ACs de 2º Nível / ACTs
                                    ↓
                              ACT (Autoridade de Carimbo do Tempo) — RFC 3161
```

**Normas ICP-Brasil**: DOC-ICP-01 (Política de Certificação), DOC-ICP-02 (Procedimentos), DOC-ICP-03 (Requisitos de HSM), DOC-ICP-15 (Carimbo do Tempo)

### Formatos de Arquivo

| Extensão | Formato | Conteúdo |
|----------|---------|----------|
| `.pem` | Base64 + headers (`-----BEGIN CERTIFICATE-----`) | Cert, chave privada, cadeia, CSR |
| `.der` / `.cer` / `.crt` | Binário DER | Cert único |
| `.p7b` / `.p7c` | PKCS#7 | Cadeia de certs (sem chave privada) |
| `.pfx` / `.p12` | PKCS#12 | Cert + chave privada + cadeia (protegido por senha) |
| `.csr` | PKCS#10 | Certificate Signing Request (chave pública + subject + assinatura) |

### Boas Práticas Operacionais

| Prática | Detalhe |
|---------|---------|
| **Chaves privadas em HSM** | FIPS 140-2 Nível 2+ para CAs; Nível 3 para Root |
| **Renovação antecipada** | Reemitir 30-60 dias antes do vencimento (evita expiração) |
| **Rotação de chaves** | Nova chave a cada renovação (não reusar par) |
| **Monitoramento de expiração** | Alertas 90/60/30/14/7/1 dias |
| **Pinning / Expect-CT** | HPKP (depreciado) → Expect-CT + CT logs públicos |
| **CT Logs (Certificate Transparency)** | Obrigatório para TLS público — monitorar emissão indevida |
| **CA/B Forum Baseline Requirements** | Seguir para certificados TLS públicos (válido para navegadores) |
# Classificação da Informação

## Níveis de Classificação (Modelo 4 Níveis — Comum em Governo/Corporações)

| Nível | Critério Principal | Exemplos Típicos | Controles Mínimos Obrigatórios |
|-------|-------------------|------------------|--------------------------------|
| **Público** | Divulgável externamente sem risco | Site institucional, material de marketing, relatórios anuais publicados | Integridade básica; disponibilidade |
| **Interno** | Uso interno; vazamento causa dano baixo/médio | Organogramas, políticas internas, memorandos, diretório corporativo | Controle de acesso (funcionários/terceiros com NDA); não compartilhar externamente |
| **Confidencial** | Vazamento causa dano significativo (financeiro, reputacional, operacional, legal) | Contratos, dados financeiros, estratégias, código-fonte, PII, dados bancários | Criptografia em trânsito (TLS 1.2+) e repouso (AES-256); Need-to-know; Logs de acesso; DLP; Classificação em metadados |
| **Restrito / Sigiloso** | Vazamento causa dano grave/irreparável; acesso extremamente limitado | Segredos industriais, chaves criptográficas mestras (root CA, HSM), dados biométricos/saúde, segredos de Estado | Isolamento de rede (air-gap ou VLAN dedicada); MFA obrigatório (certificado A3/token); Dual control; Auditoria completa; Carimbo do tempo; Destino final controlado |

> **Nota**: O edital cita "classificação da informação" genericamente. Alguns modelos usam 3 níveis (Público, Interno, Confidencial) ou 5 (adicionando "Secreto"/"Ultra-secreto"). **Entenda a lógica**, não decore rótulos.

---

## Critérios para Definição do Nível

| Critério | Pergunta Orientadora |
|----------|---------------------|
| **Valor do Ativo** | Quanto vale para a organização? (Receita, vantagem competitiva, custo de recriação) |
| **Sensibilidade** | Qual o impacto se tornado público? (Imagem, multas, perda de contratos, segurança física) |
| **Criticidade Operacional** | Quão essencial para continuidade do negócio? (RTO/RPO baixos = mais crítico) |
| **Requisitos Legais/Regulatórios** | LGPD (dado pessoal/sensível), Sigilo bancário, Propriedade intelectual, Segurança nacional, PCI-DSS |
| **Obrigacionais Contratuais** | Cláusulas de NDA, contratos com governo/defesa, requisitos de clientes |

---

## Processo de Gestão da Classificação

1. **Inventário de Ativos de Informação** — Documentos, sistemas, bases de dados, mídias, backup, e-mails.
2. **Avaliação e Rotulagem** — Aplicar critérios → definir nível → rotular (físico: cabeçalho/rodapé/capa; lógico: metadados, tags, extended attributes, DLP).
3. **Definição de Regras de Manuseio** — Por nível: armazenamento, transmissão, cópia, impressão, compartilhamento, descarte, retenção.
4. **Implementação de Controles Técnicos** — DLP, IRM (Information Rights Management), DRM, criptografia, watermarking.
5. **Treinamento e Conscientização** — Todos os colaboradores devem saber classificar e manusear.
6. **Revisão Periódica** — Reclassificar quando contexto muda (ex: projeto tornado público, fim de contrato NDA).
7. **Desclassificação Formal** — Processo documentado e aprovado pelo dono da informação para reduzir nível.

---

## Tabela de Manuseio por Nível (Resumo Operacional)

| Ação | Público | Interno | Confidencial | Restrito |
|------|---------|---------|--------------|----------|
| **Armazenamento** | Qualquer repositório corporativo | Repositório corporativo (SharePoint, GDrive corporativo) | Criptografado (AES-256), acesso controlado (ACL/RBAC), logs | HSM / Cofre isolado / Air-gap; criptografia forte; dual control |
| **Transmissão** | E-mail, web, redes sociais | E-mail corporativo, Teams/Slack corporativo, SharePoint | TLS 1.2+; S/MIME ou PGP para e-mail; SFTP/HTTPS para arquivos | Canal dedicado ponto-a-ponto; criptografia quantum-resistente (híbrida); certificado mútuo |
| **Cópia / Impressão** | Livre | Controlada (watermark com usuário/data) | Registrada (log), autorizada pelo dono, watermark | Proibida sem dual control e registro em ata |
| **Descarte / Sanitização** | Lixeira comum / exclusão lógica | Trituração padrão (NIST 800-88 Clear) | Trituração Nível 3+ (P-4/P-5) / Cripto-shredding (destruir chave) | Incineração / Desmagnetização certificada / Destruição física testemunhada |
| **Compartilhamento Externo** | Livre | NDA + aprovação gestor | NDA + aprovação gerencial + criptografia + DLP | Proibido (exceto autoridade competente com termo de responsabilidade) |

---

## Responsabilidades (RACI)

| Papel | Responsável (R) | Aprova (A) | Consultado (C) | Informado (I) |
|-------|-----------------|------------|----------------|---------------|
| **Dono da Informação (Owner / Business Owner)** | Classificar, definir regras, aprovar acesso, revisar periodicidade | ✅ | | |
| **Custodiante (Custodian / TI / Segurança)** | Implementar controles técnicos (backup, criptografia, logs, DLP) | | ✅ | |
| **Usuário / Colaborador** | Respeitar nível, não reclassificar por conta própria, reportar incidente | | | ✅ |
| **DPO / Comitê de Segurança / CISO** | Definir política, auditar conformidade, aprovar exceções | | | ✅ |

---

## Referências Normativas (para prova)

- **ISO/IEC 27001:2022** — Anexo A, Controle 5.12 (Classificação da informação) e 5.13 (Rotulagem)
- **ISO/IEC 27002:2022** — Controles 5.12, 5.13, 8.10 (Eliminação de informação)
- **NIST SP 800-53 Rev.5** — MP-3 (Marcação de mídia), MP-4 (Armazenamento), MP-5 (Transporte), MP-6 (Sanitização)
- **LGPD (Lei 13.709/2018)** — Art. 6º (Princípios), Art. 46 (Segurança), Art. 48 (Comunicação de incidente)
- **ABNT NBR ISO/IEC 27001/27002** — Versões em português das normas acima
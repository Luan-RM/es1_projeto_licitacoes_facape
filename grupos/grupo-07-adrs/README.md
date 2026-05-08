# Grupo 07 — Registros de Decisão Arquitetural (ADRs)

## 🎯 Responsabilidade

Documentar as **principais decisões arquiteturais** do sistema usando o formato **MADR (Markdown Any Decision Record)**, justificando as escolhas técnicas com base nos requisitos funcionais, não-funcionais e nas restrições do domínio de licitações públicas.

---

## 📋 O que entregar

### Artefatos: Um arquivo `.md` por ADR (mínimo 5)

| Arquivo | Decisão |
|---------|---------|
| `ADR-001-estilo-arquitetural.md` | Monolito modular vs Microsserviços |
| `ADR-002-estrategia-integracao-pncp.md` | Como integrar com o PNCP |
| `ADR-003-autenticacao-autorizacao.md` | Estratégia de auth (papéis e permissões) |
| `ADR-004-armazenamento-documentos.md` | Como armazenar PDFs/documentos do processo |
| `ADR-005-notificacoes.md` | Estratégia de notificações (e-mail, push, in-app) |

---

## 📄 Template MADR

```markdown
# ADR-XXX — [Título da Decisão]

**Data:** YYYY-MM-DD  
**Status:** Proposta | Aceita | Substituída por ADR-XXX | Obsoleta  
**Autores:** [Nomes do grupo]

---

## Contexto

> Descreva o problema ou situação que exige uma decisão. 
> O que está em jogo? Quais são as forças em tensão?
> Cite os requisitos funcionais ou não-funcionais que motivam esta decisão.

## Decisão

> Descreva claramente o que foi decidido.
> Use linguagem declarativa: "Adotamos X" ou "Optamos por Y".

## Opções Consideradas

### Opção A: [Nome]
- **Descrição:** ...
- **Prós:** ...
- **Contras:** ...

### Opção B: [Nome]
- **Descrição:** ...
- **Prós:** ...
- **Contras:** ...

### Opção C: [Nome] *(se houver)*
- ...

## Critérios de Decisão

| Critério | Peso | Opção A | Opção B | Opção C |
|---------|------|---------|---------|---------|
| Manutenibilidade | Alto | ✅ | ⚠️ | ❌ |
| Custo de implantação | Médio | ✅ | ✅ | ⚠️ |
| Aderência a requisitos | Alto | ✅ | ⚠️ | ✅ |

## Consequências

### Positivas
- ...

### Negativas / Riscos
- ...

### Neutras / Trade-offs
- ...

## Conformidade com a Lei 14.133/2021

> Se aplicável: como esta decisão impacta a rastreabilidade, auditoria ou compliance exigidos pela lei de licitações?

---

*Referências:* [links, artigos, documentação]
```

---

## 🔍 Guia por ADR

### ADR-001: Estilo Arquitetural
Considere: monolito modular, microsserviços, serverless.  
Contexto chave: equipe pequena (universidade pública), necessidade de auditoria, integração com sistemas externos legados.

### ADR-002: Integração com PNCP
Considere: polling periódico, webhook (se disponível), integração manual assistida.  
Contexto chave: PNCP tem API REST pública. O sistema precisa consultar preços e publicar PCA.

### ADR-003: Autenticação e Autorização
Considere: SSO institucional (LDAP/AD da prefeitura), JWT próprio, OAuth2.  
Contexto chave: múltiplos perfis (secretaria, almoxarifado, compras, licitações, jurídico) com permissões distintas.

### ADR-004: Armazenamento de Documentos
Considere: banco de dados (BLOB), sistema de arquivos, S3-compatível, GED externo.  
Contexto chave: processos geram PDFs oficiais que precisam de integridade e rastreabilidade por lei.

### ADR-005: Notificações
Considere: e-mail SMTP, notificações in-app, WhatsApp Business API, sem notificação (fluxo pull).  
Contexto chave: prazos críticos (vencimento de ata, prazo de entrega) exigem ação rápida.

---

## 🛠️ Ferramentas Recomendadas

| Ferramenta | Link | Observação |
|-----------|------|------------|
| **Markdown** | qualquer editor | Formato padrão dos ADRs |
| **adr-tools** | [github.com/npryce/adr-tools](https://github.com/npryce/adr-tools) | CLI para criar ADRs automaticamente |
| **Log4brains** | [github.com/thomvaill/log4brains](https://github.com/thomvaill/log4brains) | Visualizador web de ADRs |

---

## 📁 Estrutura esperada da pasta

```
grupo-07-adrs/
├── README.md
├── ADR-001-estilo-arquitetural.md
├── ADR-002-estrategia-integracao-pncp.md
├── ADR-003-autenticacao-autorizacao.md
├── ADR-004-armazenamento-documentos.md
└── ADR-005-notificacoes.md
```

---

## ✏️ Seção de Entrega (preencher pelo grupo)

**Integrantes:**
- ...

**Decisões tomadas:**
> ...

**Limitações identificadas:**
> ...

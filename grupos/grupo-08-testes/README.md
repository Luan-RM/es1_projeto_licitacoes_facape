# Grupo 08 — Plano e Casos de Teste

## 🎯 Responsabilidade

Elaborar o **Plano de Testes** e os **Casos de Teste** do sistema, cobrindo os fluxos críticos identificados no contexto do domínio, com foco especial nas **regras de negócio** da lei de licitações.

---

## 📋 O que entregar

### Artefato 1: `plano-de-testes.md`
Documento descrevendo a estratégia geral de testes:
- Objetivos e escopo
- Pirâmide de testes adotada
- Critérios de entrada e saída
- Ambientes de teste
- Riscos de qualidade identificados

### Artefato 2: `casos-de-teste/CT-XX.md` (mínimo 12 casos)
Casos de teste individuais, organizados por funcionalidade.

### Artefato 3: `matriz-rastreabilidade.md`
Matriz que vincula Casos de Teste ↔ User Stories ↔ Regras de Negócio.

---

## 🔍 Funcionalidades Prioritárias para Teste

Com base nos gargalos identificados no contexto do sistema, priorize:

| Prioridade | Funcionalidade | Regra de Negócio |
|-----------|---------------|-----------------|
| 🔴 Alta | Verificação de fracionamento de despesa | RN-03 |
| 🔴 Alta | Validação de cota ME/EPP por item | RN-01, RN-02 |
| 🔴 Alta | Emissão de OF com verificação de saldo da ata | RN-04 |
| 🔴 Alta | Cotação com mínimo de 3 fornecedores | RN-10 |
| 🟡 Média | Alerta de vencimento de ata (30 dias antes) | RN-04 |
| 🟡 Média | Bloqueio de adesão acima de 50% do quantitativo | RN-08 |
| 🟡 Média | Prazo mínimo de entrega por categoria | - |
| 🟢 Baixa | Notificação de prazo de entrega expirado | - |

---

## 📄 Template de Caso de Teste

```markdown
# CT-XX — [Nome do Caso de Teste]

## Identificação

| Campo | Valor |
|-------|-------|
| **ID** | CT-XX |
| **User Story** | US-XX |
| **Regra de Negócio** | RN-XX |
| **Prioridade** | Alta / Média / Baixa |
| **Tipo de Teste** | Funcional / Borda / Negativo / Integração |
| **Nível** | Unitário / Integração / Sistema / Aceite |

## Pré-condições

- (estado do sistema antes do teste)

## Dados de Entrada

| Campo | Valor |
|-------|-------|
| | |

## Passos de Execução

1. ...
2. ...
3. ...

## Resultado Esperado

> (descreva o comportamento esperado do sistema)

## Resultado Obtido

> (preencher durante a execução)

## Status

[ ] Não executado | [ ] Passou | [ ] Falhou | [ ] Bloqueado
```

---

## 📋 Casos de Teste Obrigatórios

### Bloco 1: Regras de Cota ME/EPP

**CT-01**: Item com valor total = R$ 79.999 → deve ser exclusivo ME/EPP  
**CT-02**: Item com valor total = R$ 80.001 → deve ter cota exclusiva de 25%  
**CT-03**: Item com valor total = R$ 80.000 → caso de borda — qual regra se aplica?  
**CT-04**: Cota ME/EPP calculada como 25% do valor → arredondamento para menos  

### Bloco 2: Fracionamento de Despesa

**CT-05**: Criar DFD de Expediente quando já existe outro aberto → sistema deve alertar e mesclar  
**CT-06**: Criar dois processos de expediente no mesmo exercício → sistema deve bloquear  

### Bloco 3: Ata SRP e Ordens de Fornecimento

**CT-07**: Emitir OF de 100 unidades com saldo de ata = 100 → deve permitir  
**CT-08**: Emitir OF de 101 unidades com saldo de ata = 100 → deve bloquear  
**CT-09**: Emitir OF em ata com validade vencida → deve bloquear com mensagem  
**CT-10**: Adesão de 50% do quantitativo da ata → deve permitir  
**CT-11**: Adesão de 51% do quantitativo da ata → deve bloquear (RN-08)  

### Bloco 4: Cotação

**CT-12**: Iniciar cotação com 2 fornecedores → deve exigir mínimo de 3  
**CT-13**: Cotação com 3 fornecedores → deve calcular e sugerir média corretamente  

---

## 🛠️ Ferramentas Recomendadas

| Ferramenta | Link | Observação |
|-----------|------|------------|
| **Markdown** | qualquer editor | Formato dos casos de teste |
| **TestLink** | [testlink.org](https://testlink.org) | Gestão de casos de teste open-source |
| **Zephyr Scale** | Integrado ao Jira | Para times que usam Jira |
| **Excel/Google Sheets** | - | Alternativa simples para matriz de rastreabilidade |

---

## 📁 Estrutura esperada da pasta

```
grupo-08-testes/
├── README.md
├── plano-de-testes.md
├── matriz-rastreabilidade.md
└── casos-de-teste/
    ├── CT-01-cota-mepp-abaixo-80k.md
    ├── CT-02-cota-mepp-acima-80k.md
    ├── CT-03-cota-mepp-borda-80k.md
    ├── CT-04-arredondamento-cota.md
    ├── CT-05-fracionamento-alerta.md
    ├── CT-06-fracionamento-bloqueio.md
    ├── CT-07-of-saldo-exato.md
    ├── CT-08-of-saldo-insuficiente.md
    ├── CT-09-of-ata-vencida.md
    ├── CT-10-adesao-50pct.md
    ├── CT-11-adesao-51pct.md
    ├── CT-12-cotacao-2-fornecedores.md
    └── CT-13-cotacao-media.md
```

---

## ✏️ Seção de Entrega (preencher pelo grupo)

**Integrantes:**
- ...

**Decisões tomadas:**
> ...

**Limitações identificadas:**
> ...

# Grupo 05 — Modelagem de Processos (BPMN)

## 🎯 Responsabilidade

Modelar os **processos de negócio** do domínio de licitações usando a notação **BPMN 2.0**, representando o fluxo completo de atividades, decisões, eventos e raias (swimlanes) por ator.

---

## 📋 O que entregar

### Artefatos: Um diagrama BPMN por processo (mínimo 2, ideal 3)

| Arquivo | Processo |
|---------|----------|
| `BPMN-01-fase-interna-completa.bpmn` + `.png` | Fluxo completo da fase interna (DFD → envio TR) |
| `BPMN-02-coleta-demandas.bpmn` + `.png` | Sub-processo: coleta e consolidação de demandas |
| `BPMN-03-gestao-ata-srp.bpmn` + `.png` | Sub-processo: gestão de Ata SRP e emissão de OF |

---

## 🗺️ Guia de Modelagem

### Processo 1: Fase Interna Completa

**Raias (Pools/Lanes):**
- Secretaria / Colegiado
- Almoxarifado
- Setor de Compras
- Setor de Licitações
- Jurídico Interno
- Prefeitura *(pool externo — processo continua lá)*

**Elementos obrigatórios:**
- Evento de início: "Necessidade de compra identificada"
- Gateways de decisão:
  - "Valor estimado ≤ R$ 57k?" → Dispensa ou processo normal
  - "Processo exclusivo ME/EPP ou ampla concorrência?"
  - "Documentação completa?"
- Evento de fim: "Processo autuado na Prefeitura"
- Tarefas de serviço (automatizadas): consulta PNCP, consulta Banco de Preços
- Tarefas de usuário (manuais): preenchimento DFD, ETP, TR

### Processo 2: Coleta de Demandas

**Raias:**
- Gestor do PCA
- Secretarias (múltiplas — agrupe em uma raia)
- Almoxarifado

**Gateways:**
- "Prazo de coleta atingido?"
- "Secretaria não respondeu?" → Notificação / encerramento compulsório
- "Item já no estoque?" → Excluir da demanda

### Processo 3: Gestão de Ata SRP e Emissão de OF

**Raias:**
- Setor de Compras
- Contabilidade

**Eventos intermediários:**
- Timer: "Ata próxima do vencimento (30 dias)" → notificação
- Timer: "Prazo de entrega expirado" → acionar cláusula de multa

---

## 🛠️ Ferramentas Recomendadas

| Ferramenta | Link | Observação |
|-----------|------|------------|
| **Camunda Modeler** | [camunda.com/download/modeler](https://camunda.com/download/modeler/) | **Recomendado** — desktop, padrão BPMN 2.0, salva `.bpmn` |
| **bpmn.io** | [bpmn.io](https://bpmn.io) | Online, gratuito, exporta SVG e BPMN |
| **draw.io** | [app.diagrams.net](https://app.diagrams.net) | Tem formas BPMN, exporta XML |
| **Bizagi Modeler** | [bizagi.com](https://www.bizagi.com/pt/plataforma/modeler) | Desktop gratuito, rico em recursos |

> 💡 **Dica**: Prefira o Camunda Modeler ou bpmn.io pois geram arquivos `.bpmn` (XML padrão), que devem ser commitados junto às imagens PNG/SVG. Isso torna o artefato editável e versionável.

---

## 📋 Checklist de Qualidade BPMN

- [ ] Todos os fluxos têm início e fim definidos
- [ ] Gateways têm todas as saídas rotuladas
- [ ] Raias representam atores reais do domínio
- [ ] Tarefas automáticas vs manuais estão distinguidas (ícone de engrenagem vs usuário)
- [ ] Eventos de tempo (timer) usados para prazos
- [ ] Sub-processos expandidos quando necessário
- [ ] Fluxo de exceção para documentação incompleta

---

## 📁 Estrutura esperada da pasta

```
grupo-05-modelagem-processos/
├── README.md
├── BPMN-01-fase-interna-completa.bpmn
├── BPMN-01-fase-interna-completa.png
├── BPMN-02-coleta-demandas.bpmn
├── BPMN-02-coleta-demandas.png
├── BPMN-03-gestao-ata-srp.bpmn
└── BPMN-03-gestao-ata-srp.png
```

---

## ✏️ Seção de Entrega (preencher pelo grupo)

**Integrantes:**
- ...

**Decisões tomadas:**
> ...

**Limitações identificadas:**
> ...

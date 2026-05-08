# Grupo 06 — Backlog de Produto (Épicos, User Stories e Critérios de Aceite)

## 🎯 Responsabilidade

Elaborar o **backlog de produto** completo do sistema, organizado em **épicos** e **user stories**, com **critérios de aceite** escritos no formato Given/When/Then (Gherkin), refletindo as regras de negócio do domínio de licitações.

---

## 📋 O que entregar

### Artefato 1: `epicos.md`
Lista dos épicos com descrição, objetivos e prioridade.

### Artefato 2: `user-stories.md`
Todas as user stories, organizadas por épico, com:
- ID único
- Título
- Narrativa: "Como [ator], quero [ação], para [valor]"
- Critérios de aceite (Given/When/Then)
- Estimativa de complexidade (S/M/L/XL)
- Prioridade (Alta/Média/Baixa)

### Artefato 3: `backlog-priorizado.md`
Backlog na ordem de implementação sugerida (produto mínimo viável primeiro).

---

## 🗂️ Épicos Sugeridos

| ID | Épico | Descrição |
|----|-------|-----------|
| EP-01 | Gestão de Demandas | Coleta e consolidação de necessidades de todas as secretarias |
| EP-02 | Plano de Contratação Anual | Elaboração e publicação do PCA |
| EP-03 | Elaboração de Documentos | ETP, Mapa de Riscos e Termo de Referência |
| EP-04 | Pesquisa de Preços | Integração com Banco de Preços e cotação manual |
| EP-05 | Gestão de Atas SRP | Controle de atas vigentes, saldos e vencimentos |
| EP-06 | Ordens de Fornecimento | Emissão, rastreamento e notificação de OF |
| EP-07 | Integração Externa | PNCP e sistema 1doc da Prefeitura |
| EP-08 | Notificações e Alertas | Prazos, vencimentos e pendências |

---

## 📄 Exemplos de User Stories

### EP-01: Gestão de Demandas

```
US-01: Registrar demanda de material
Como Secretaria/Colegiado
Quero registrar uma demanda de materiais ou serviços no sistema
Para que minha necessidade seja incluída no processo licitatório do ano

Critérios de Aceite:
  Cenário 1: Registro bem-sucedido
    Dado que estou autenticada como representante de secretaria
    E o período de coleta de demandas está aberto
    Quando preencho: descrição, justificativa, itens com catmat e quantidade
    E submeto o formulário
    Então o sistema registra a demanda com status "Aguardando Consolidação"
    E notifica o Almoxarifado sobre nova demanda

  Cenário 2: Período de coleta fechado
    Dado que o período de coleta de demandas está encerrado
    Quando tento registrar uma demanda
    Então o sistema exibe mensagem: "Período de coleta encerrado. Contate o Almoxarifado."
    E não permite o registro

Estimativa: M | Prioridade: Alta | Épico: EP-01
```

```
US-04: Verificar fracionamento de despesa
Como Almoxarifado
Quero que o sistema me alerte quando houver risco de fracionamento de despesa
Para que eu não abra dois processos do mesmo tipo no mesmo exercício

Critérios de Aceite:
  Cenário 1: Fracionamento detectado
    Dado que já existe um DFD aberto para "Material de Expediente" em 2026
    Quando uma secretaria registra nova demanda de "Material de Expediente"
    Então o sistema exibe alerta: "Já existe DFD aberto para esta categoria. A demanda será incluída no processo vigente."
    E adiciona automaticamente a demanda ao DFD existente

Estimativa: M | Prioridade: Alta | Épico: EP-01
```

---

## 🛠️ Ferramentas Recomendadas

| Ferramenta | Link | Observação |
|-----------|------|------------|
| **Markdown + VS Code** | local | Simples e versionável — **recomendado** |
| **Trello** | [trello.com](https://trello.com) | Visualização de backlog em kanban |
| **GitHub Projects** | No próprio repo | Integra com o repositório |
| **Notion** | [notion.so](https://notion.so) | Bom para tabelas e templates |

---

## 📋 Checklist de Qualidade

- [ ] Toda US tem ator, ação e valor claramente expressos
- [ ] Critérios de aceite cobrem o caminho feliz e pelo menos um fluxo alternativo
- [ ] Regras de negócio (RN-XX) estão referenciadas nas USs relevantes
- [ ] Backlog priorizado distingue MVP de funcionalidades futuras
- [ ] Estimativas de complexidade são relativas entre si (não absolutas)

---

## 📁 Estrutura esperada da pasta

```
grupo-06-backlog/
├── README.md
├── epicos.md
├── user-stories.md
└── backlog-priorizado.md
```

---

## ✏️ Seção de Entrega (preencher pelo grupo)

**Integrantes:**
- ...

**Decisões tomadas:**
> ...

**Limitações identificadas:**
> ...

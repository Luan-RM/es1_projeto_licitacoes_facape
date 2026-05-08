# 🏛️ Sistema de Gestão de Licitações — FACAPE

> Projeto aplicado da disciplina **Engenharia de Software I**  
> Curso de Engenharia de Software · Professor: Mateus Silva
> Semestre: 2026.1

---

## 📋 Contexto

Este repositório centraliza os artefatos de modelagem do **Sistema de Gestão de Licitações da FACAPE**, com base no contexto do domínio e nas regras de negócio da disciplina.

O sistema visa digitalizar e integrar o processo interno de compras públicas, eliminando gargalos manuais identificados no levantamento de domínio:

- Coleta descentralizada de demandas (DFD) de múltiplas secretarias
- Geração manual de Ordens de Fornecimento em papel
- Ausência de rastreabilidade interna entre demanda e empenho
- Falta de integração com portais externos (PNCP, Banco de Preços)

O sistema **não** cobre a execução do pregão eletrônico (que ocorre na plataforma da Prefeitura), mas cobre toda a fase interna: da formalização da demanda à emissão da ordem de fornecimento.

---

## 🗂️ Estrutura do Repositório

```text
sistema-licitacao-facape/
│
├── README.md                        ← este arquivo (mantido pelo professor)
├── CONTRIBUTING.md                  ← regras de contribuição e fluxo de PR
│
├── .github/
│   ├── PULL_REQUEST_TEMPLATE.md     ← checklist obrigatório no PR
│   └── ISSUE_TEMPLATE/
│       └── entrega-grupo.md         ← template de issue de entrega
│
├── docs/
│   ├── contexto-do-sistema.md       ← visão geral do domínio (professor)
│   └── glossario-base.md            ← glossário inicial do domínio (professor)
│
└── grupos/
    ├── grupo-01-casos-de-uso/       ← Atores + Diagrama de Casos de Uso
    ├── grupo-02-especificacao-uc/   ← Especificação Narrativa de UCs
    ├── grupo-03-diagrama-classes/   ← Diagrama de Classes do Domínio
    ├── grupo-04-diagramas-sequencia/← Diagramas de Sequência
    ├── grupo-05-modelagem-processos/← Modelagem BPMN de Processos
    ├── grupo-06-backlog/            ← Épicos, User Stories e Critérios de Aceite
    ├── grupo-07-adrs/               ← Registros de Decisão Arquitetural (ADRs)
    ├── grupo-08-testes/             ← Plano e Casos de Teste
    └── grupo-09-auditoria-compliance-bi/ ← Auditoria, Compliance e Indicadores
```

> ⚠️ **Cada grupo trabalha EXCLUSIVAMENTE dentro da sua pasta.** Qualquer modificação fora dela resultará em reprovação do PR.

---

## 👥 Grupos e Responsabilidades

| Grupo | Pasta | Responsabilidade |
| ----- | ----- | ---------------- |
| G01 | `grupo-01-casos-de-uso` | Atores e Diagrama de Casos de Uso |
| G02 | `grupo-02-especificacao-uc` | Especificação Narrativa de UCs |
| G03 | `grupo-03-diagrama-classes` | Diagrama de Classes do Domínio |
| G04 | `grupo-04-diagramas-sequencia` | Diagramas de Sequência |
| G05 | `grupo-05-modelagem-processos` | Modelagem de Processos (BPMN) |
| G06 | `grupo-06-backlog` | Backlog: Épicos, Stories e Critérios de Aceite |
| G07 | `grupo-07-adrs` | Decisões Arquiteturais (ADRs) |
| G08 | `grupo-08-testes` | Plano e Casos de Teste |
| G09 | `grupo-09-auditoria-compliance-bi` | Auditoria, Compliance e Indicadores |

---

## 🔄 Fluxo de Trabalho

```text
1. Fork deste repositório para a conta do grupo
2. Clone o fork localmente
3. Trabalhe APENAS dentro da pasta do seu grupo
4. Commit e push com mensagens no padrão: [G0X] feat: descrição
5. Abra um Pull Request apontando para este repositório (branch: main)
6. Preencha o PULL_REQUEST_TEMPLATE obrigatoriamente
7. Aguarde revisão e aprovação do professor
```

Veja o [CONTRIBUTING.md](CONTRIBUTING.md) para detalhes completos.

## 📄 Artefato Opcional por Grupo

Cada grupo pode, opcionalmente, incluir na propria pasta um arquivo
`.md` voltado a agentes de IA, como `contexto-agente.md` ou `AGENTS.md`.
Esse arquivo deve apenas resumir o contexto tecnico do grupo e nao
substitui nenhuma entrega obrigatoria da disciplina.

---

## 📚 Referências do Domínio

- Lei Federal nº 14.133/2021 (Nova Lei de Licitações)
- Lei Complementar nº 123/2006 (Estatuto das ME/EPP)
- Portal Nacional de Compras Públicas: [https://www.gov.br/compras](https://www.gov.br/compras)
- Contexto do domínio: [`docs/contexto-do-sistema.md`](docs/contexto-do-sistema.md)

---

## 🙏 Agradecimento

Agradecemos a **CARLA VANESSA MEDEIROS SOARES**, chefe de compras da
FACAPE, pela aula ministrada sobre o processo de licitações, que
contribuiu de forma essencial para o entendimento do domínio e para a
construção deste projeto acadêmico.

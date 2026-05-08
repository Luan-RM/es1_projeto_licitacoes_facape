# Requisitos do Projeto AV2

Este documento define a organização do trabalho da disciplina sobre o
sistema de licitações. Ele complementa `contexto-do-sistema.md`: não
repete a descrição completa do domínio, mas traduz esse contexto em
diretrizes de execução, integração entre grupos e critérios mínimos de
entrega.

Fonte de verdade para o domínio:

- `contexto-do-sistema.md`: visão conceitual, escopo, atores e regras de negócio.
- Referências normativas e materiais validados em sala: exemplos e detalhes operacionais.

## Contexto e Objetivo

Este projeto AV2 foi definido a partir do levantamento de domínio
validado com o setor de licitações da instituição. O foco é modelar e
especificar um sistema único, com módulos interligados, para reduzir
gargalos do processo interno e melhorar rastreabilidade, qualidade de
dados e tempo de tramitação.

Objetivo principal: entregar uma solução integrada para o ciclo interno
da licitação, desde a demanda interna até a preparação do processo para
tramitação externa, com acompanhamento interno de ata, ordem de
fornecimento e interface com empenho.

## Escopo do Projeto

**Tipo de escopo:** prático, modelagem e codificação orientada a
processos.

**Domínio funcional coberto:**

- planejamento anual de contratações (PCA) e consolidação de demandas;
- elaboração de DFD, ETP, termo de referência e mapa de risco;
- tramitação interna e integração de fronteira com fluxo externo da
  prefeitura;
- acompanhamento de status externo (sem implementar motor de
  pregão/julgamento);
- controle de ata/SRP, ordem de fornecimento e interface com empenho;
- trilha de auditoria, compliance e indicadores.

**Fora do escopo de implementação:**

- motor de lances do pregão eletrônico;
- julgamento externo de propostas e recursos em plataforma de
  terceiros;
- homologação/adjudicação executada diretamente no sistema externo.

## Organização das Equipes (9 grupos, 9 módulos)

**Quantidade de equipes:** 9  
**Formato:** Modular e paralelo (cada grupo desenvolve UM MÓDULO completo com todos os artefatos de ES)

### Abordagem de Desenvolvimento: Modular e Paralelo

Cada grupo fica responsável por **UM MÓDULO** completo do sistema. Dentro de seu módulo, o grupo desenvolve:

- **Casos de uso** próprios do módulo
- **Diagrama UML** (entidades, atributos, relacionamentos)
- **Diagramas de sequência** (fluxos internos do módulo)
- **BPMN** (processo do módulo, quando aplicável)
- **Backlog** (histórias de usuário do módulo)
- **ADRs** (decisões arquiteturais do módulo)
- **Testes** (unitários, integração com módulos vizinhos)
- **Auditoria** (eventos do módulo + integração com G09)

**Vantagem:** 9 grupos trabalham **em paralelo**, sem bloqueios sequenciais. As interfaces entre módulos são bem definidas: "o módulo X precisa receber ISSO e entrega AQUILO".

| Grupo | Módulo                                  | Entrada Esperada         | Saída Esperada                                    | Responsabilidade principal |
| :---- | :-------------------------------------- | :----------------------- | :------------------------------------------------ | :------------------------- |
| G1    | Consolidação de Demandas (DFD)          | Formulários secretarias  | DFD consolidado                                   | Coleta, validação e consolidação de demandas de múltiplas secretarias |
| G2    | Estudo Técnico Preliminar (ETP)         | DFD                      | ETP com cotações e análise de mercado             | Análise técnica, cotação de preços (Banco de Preços), especificação refinada |
| G3    | Pesquisa e Gestão de Atas SRP           | ETP                      | Relatório de atas (recomendação: adesão vs novo) | Pesquisar atas vigentes, avaliar competitividade, calcular limite de adesão |
| G4    | Elaboração de Termo de Referência (TR)  | ETP + decisão de ata     | TR formatado                                      | Compilar ETP com regras da Lei 123/2006, divisão de cotas, prazos |
| G5    | Mapa de Riscos                          | TR                       | Mapa de Riscos                                    | Analisar riscos (preço, especificação, ambiental, mercado, manutenção) |
| G6    | Preparação para Edital e Envio          | TR + Mapa de Risco       | Edital enviado à Prefeitura                       | Formatar edital, validar, enviar para a Prefeitura, registrar envio |
| G7    | Acompanhamento de Processo Externo      | Edital enviado           | Status do pregão atualizado                       | Consultar plataforma da Prefeitura, registrar status, notificações |
| G8    | Controle de Ordem de Fornecimento (OF)  | Resultado do pregão      | OF gerada e enviada                               | Gerar OF após resultado do pregão, acompanhar entrega |
| G9    | Auditoria, Compliance e Indicadores     | Eventos G01-G08          | Logs de auditoria, relatórios de compliance, indicadores | Registrar trilha imutável, validar Lei 14.133, calcular indicadores, alertas |

### Dependências entre Módulos (Fluxo)

```text
G01 (DFD)
  ↓
G02 (ETP) ← também consulta G03
  ↓
G03 (Atas SRP)
  ↓
G04 (TR)
  ↓
G05 (Mapa de Risco)
  ↓
G06 (Edital)
  ↓ [FORA DO SISTEMA: Prefeitura faz pregão]
G07 (Acompanhamento)
  ↓
G08 (OF)
  ↓
G09 (Auditoria) ← conectado a TODOS para registros imutáveis
```

Todos os eventos de G01-G08 alimentam **G09 (Auditoria, Compliance, BI)** para trilha centralizada.

- G5 envia pacote de processo para G6 (fronteira externa) e aciona G7
  para checklist documental.
- G6 sincroniza status externo e retorna eventos de estado para G5, G7
  e G8.
- G7 valida consistência documental e libera etapa de execução para
  G8.
- G8 publica execução e saldos para G9.
- G9 retroalimenta indicadores para G2 e G3 (melhoria contínua de
  planejamento e cotação).

## Requisitos Mínimos Obrigatórios

### RQ-INT-01 (Integração)

Todos os módulos devem documentar contrato interno de entrada e saída
(dados recebidos, validações, regras de processamento e dados
produzidos).

### RQ-INT-02 (Rastreabilidade)

Cada processo deve ter rastreabilidade ponta a ponta: Demanda
-> ETP/TR -> Tramitação Interna -> Status Externo -> Execução.

### RQ-INT-03 (Compliance)

Toda decisão relevante deve registrar fundamento normativo e
justificativa técnica (ex.: escolha de modalidade, parcelamento, cota
ME/EPP).

### RQ-INT-04 (Qualidade)

Cada grupo deve entregar plano de testes do módulo e testes de
integração com ao menos 2 módulos vizinhos.

### RQ-INT-05 (Observabilidade)

O sistema deve registrar logs estruturados de transições de estado e
disponibilizar indicadores de desempenho do processo.

## Estrutura Sugerida de Repositório

```text
es-av2-licitacao/
  README.md
  docs/
    visao-geral.md
    arquitetura/
      contexto-c4.md
      containers-c4.md
      componentes-c4.md
    requisitos/
      dicionario-dominio.md
      matriz-rastreabilidade.md
    integracao/
      entradas-saidas-modulos.md
      regras-validacao-fluxo.md
    processo/
      dfd-modelo.md
      etp-modelo.md
      tr-modelo.md
      mapa-risco-modelo.md
    governanca/
      rubrica.md
      plano-comunicacao.md
  modules/
    g1-demandas/
    g2-pca-consolidacao/
    g3-etp-cotacao/
    g4-termo-referencia/
    g5-tramitacao/
    g6-integracao-fronteira/
    g7-conformidade-documental/
    g8-ata-contrato-empenho/
    g9-auditoria-bi/
  shared/
    schemas/
    auth/
    logging/
  tests/
    integration/
    e2e/
```

## Matriz de Entradas e Saídas por Módulo

| Grupo | Entrada principal                                       | Saída principal                                      | Destino da saída |
| :---- | :------------------------------------------------------ | :--------------------------------------------------- | :--------------- |
| G1    | Solicitações dos setores/colegiados                     | DFD preliminar consolidado por setor                 | G2               |
| G2    | DFDs preliminares + histórico de consumo                | Plano consolidado de demanda (PCA interno)           | G3               |
| G3    | PCA interno + parâmetros de mercado                     | ETP + cotação + recomendação de modalidade           | G4               |
| G4    | ETP/cotação + regras legais                             | Termo de Referência estruturado por item/lote        | G5               |
| G5    | TR + anexos de suporte                                  | Processo autuado com trilha de tramitação interna    | G6 e G7          |
| G6    | Processo autuado + pacote de publicação                 | Status externo sincronizado e histórico de retorno   | G5, G7 e G8      |
| G7    | Processo autuado + status externo + documentos internos | Parecer de conformidade e liberação interna          | G8               |
| G8    | Resultado final + dados orçamentários                   | Ordens de fornecimento, saldos e execução financeira | G9               |
| G9    | Dados de execução + logs de processo                    | Indicadores, alertas de risco e relatório de compliance | G2 e G3          |

## Artefatos Esperados por Grupo

- Documento de escopo do módulo (problema, fronteira, entradas,
  saídas).
- Modelo de domínio (entidades, regras e estados).
- Contrato interno de entrada/saída do módulo (campos, regras e
  transformações).
- Plano de testes (unitário, integração e critério de aceite).
- Evidências de execução (prints, logs, relatório de testes).
- Relatório técnico final com trade-offs e riscos.
- Opcional: arquivo `.md` de contexto para agentes, restrito ao escopo
  do próprio grupo.

## Cronograma Sugerido

| Marco             | Prazo    | Entrega                                                                                               |
| :---------------- | :------- | :---------------------------------------------------------------------------------------------------- |
| Kickoff do AV2    | Semana 1 | Definição final dos 9 grupos, módulo de cada grupo e interfaces iniciais.                           |
| Checkpoint 1      | Semana 2 | Escopo, backlog e modelo de domínio por módulo.                                                       |
| Checkpoint 2      | Semana 3 | Matriz de entradas/saídas dos módulos e teste de integração de fronteira com sistema externo (mock). |
| Checkpoint 3      | Semana 4 | Fluxo ponta a ponta parcial com rastreabilidade mínima funcionando.                                   |
| Pré-banca técnica | Semana 5 | Demo integrada + relatório de riscos + ajustes de compliance.                                         |
| Entrega final     | Semana 6 | Monorepo completo, documentação, testes e apresentação.                                               |

## Rubrica de Avaliação (sugestão)

| Critério                                                                                     | Peso |
| :------------------------------------------------------------------------------------------- | :--- |
| Aderência ao domínio de licitação e correções conceituais                                   | 20%  |
| Qualidade técnica do módulo (modelo, regras, clareza)                                        | 20%  |
| Integração entre equipes (entradas/saídas, interoperabilidade interna e fronteira externa)  | 20%  |
| Rastreabilidade, compliance e auditabilidade                                                  | 15%  |
| Testes e evidências de validação                                                              | 15%  |
| Comunicação técnica e apresentação final                                                      | 10%  |

## Riscos Comuns e Mitigação

- Risco: módulos desconectados. Mitigação: matriz de entradas/saídas
  congelada no Checkpoint 2.
- Risco: confusão entre fronteira e implementação do sistema externo.
  Mitigação: manter lista explícita de fora de escopo e usar mock de
  retorno externo.
- Risco: sobreposição de responsabilidade entre grupos. Mitigação:
  matriz RACI e fronteiras de módulo no kickoff.
- Risco: baixa aderência ao processo real. Mitigação: validar
  artefatos com base no contexto do sistema e revisar termos do domínio.
- Risco: atraso na integração final. Mitigação: teste E2E incremental
  desde a Semana 3.

## Checklist Final de Entrega

- Monorepo da turma com 9 módulos interligados.
- Documento de arquitetura do monolito modular e matriz de
  entradas/saídas por módulo.
- Matriz de rastreabilidade ponta a ponta.
- Plano e evidências de testes por grupo e integração global.
- Relatório técnico final de cada grupo.
- Apresentação final com demonstração do fluxo integrado.

**Observação Importante**

Este AV2 não é um conjunto de trabalhos independentes. A nota do projeto
considera fortemente o comportamento do sistema integrado. Uma entrega
técnica boa em módulo isolado, sem integração real, será penalizada no
critério de interoperabilidade.

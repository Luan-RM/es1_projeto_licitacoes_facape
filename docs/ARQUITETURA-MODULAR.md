# 🏗️ Arquitetura Modular — 9 Grupos, 9 Módulos

## Visão Geral

Cada grupo fica **responsável por UM MÓDULO** do sistema e desenvolve **todos os artefatos de Engenharia de Software** para esse módulo:
- Casos de uso próprios
- Diagrama de classe (entidades do módulo)
- Diagramas de sequência (fluxos internos)
- BPMN (processos do módulo, quando aplicável)
- Histórias de usuário (backlog do módulo)
- ADRs (decisões do módulo)
- Testes (unitários, integração)
- Auditoria e conformidade (próprias do módulo)

**Vantagem:** Grupos trabalham em paralelo, sem bloqueios. As interfaces entre módulos são definidas de forma clara: "o módulo X precisa receber ISSO e entrega AQUILO".

---

## 🔄 Os 9 Módulos (Fluxo de Processo)

### **G01 — Consolidação de Demandas (DFD)**
**Responsabilidade:** Coleta demandas de múltiplas secretarias e consolida em um único documento de formalização da demanda.

**Entrada:** Demandas textuais/formulários das secretarias (tipo, quantidade, justificativa)  
**Saída:** Documento DFD consolidado com:
  - Lista de itens solicitados (código, descrição, quantidade, secretaria solicitante)
  - Data de consolidação
  - Responsável de cada secretaria

**Atores:** Coordenadores das secretarias, Chefe de Almoxarifado, Chefe de Compras  
**Artefatos Esperados:**
- Casos de uso: "Cadastrar Demanda", "Consolidar Demanda", "Validar Demanda", "Gerar DFD"
- Diagrama de classe: Demanda, Secretaria, Item, DFD
- Diagrama de sequência: fluxo de coleta → consolidação → geração
- BPMN: swimlane por secretaria, prazos de coleta
- Backlog com histórias: "Como coordenador, quero submeter demanda", "Como chefe de compras, quero consolidar todas as demandas"
- ADR: decisão sobre formato de consolidação (JSON? XML? CSV?)
- Testes: validação de consolidação, detecção de duplicatas
- Auditoria: quem criou cada demanda, quando, alterações

---

### **G02 — Estudo Técnico Preliminar (ETP)**
**Responsabilidade:** Análise técnica do DFD: cotação de preços via Banco de Preços, análise de mercado, especificação técnica detalhada.

**Entrada:** DFD do módulo G01 (lista de itens consolidados)  
**Saída:** ETP com:
  - Cotações de 3+ fornecedores por item
  - Análise de viabilidade de mercado
  - Especificação técnica refinada (normas, padrões, garantias)
  - Justificativa de valores estimados
  - Recomendação de parcelamento de itens

**Atores:** Analista de Compras, Especialista Técnico  
**Artefatos Esperados:**
- Casos de uso: "Consultar Banco de Preços", "Fazer Cotação", "Validar Especificação", "Gerar ETP"
- Diagrama de classe: Cotacao, Fornecedor, Especificacao, ETP
- Diagrama de sequência: integração com Banco de Preços, análise de propostas
- BPMN: fluxo de análise técnica, validação por especialista
- Backlog: "Como analista, quero consultar histórico de preços", "Como especialista, quero validar especificação"
- ADR: qual sistema usar para Banco de Preços? Integração com API gov.br ou manual?
- Testes: validação de cotações, detecção de outliers de preço
- Auditoria: quem fez cada cotação, quando, qual foi o critério de seleção dos 3 fornecedores

---

### **G03 — Pesquisa e Gestão de Atas SRP**
**Responsabilidade:** Verifica se há atas de SRP (Sistema de Registro de Preço) ou processos anteriores que podem ser "carona" — reutilizados com adesão.

**Entrada:** ETP do módulo G02 (especificação técnica e valores estimados)  
**Saída:** Relatório de atas disponíveis com:
  - Lista de atas vigentes que cobrem os itens
  - Análise de preço: a ata existente é competitiva vs. nova cotação?
  - Viabilidade de adesão (50% do quantitativo da ata, aceitação de empresa e detentor)
  - Recomendação: usar ata existente ou abrir novo processo?

**Atores:** Pesquisador de Atas, Chefe de Licitações  
**Artefatos Esperados:**
- Casos de uso: "Pesquisar Ata Existente", "Validar Competitividade de Ata", "Calcular Limite de Adesão", "Gerar Relatório de Atas"
- Diagrama de classe: Ata, ProcessoLicitatorio, Adesao, Fornecedor
- Diagrama de sequência: busca em base de atas, validação de elegibilidade
- BPMN: fluxo de pesquisa → validação → decisão (adesão vs. novo processo)
- Backlog: "Como pesquisador, quero filtrar atas por tipo de item", "Como chefe, quero ver análise de preço"
- ADR: onde armazenar dados de atas? Base local? Portal da Prefeitura?
- Testes: cálculo correto de 50%, validação de vigência de ata
- Auditoria: quais atas foram consultadas, qual foi a decisão (adesão ou novo processo)

---

### **G04 — Elaboração de Termo de Referência (TR)**
**Responsabilidade:** Compila ETP (especificação técnica) com todas as regras da Lei Complementar 123/2006 (divisão de cotas para ME/EPP), cria documento formal para edital.

**Entrada:** ETP do módulo G02, decisão de ata (G03)  
**Saída:** TR (documento) com:
  - Objeto da compra (descrição, quantidade, valor estimado)
  - Especificação técnica detalhada
  - Divisão de cotas (se item > R$ 80k: 25% exclusivo para ME/EPP, 75% para todos)
  - Benefícios Lei 123/2006 (empate com 10% de diferença favor ME/EPP)
  - Prazo de entrega e local
  - Critérios de aceitação
  - Contratações correlatas (se aplicável)

**Atores:** Especialista em Lei de Licitações, Chefe de Compras  
**Artefatos Esperados:**
- Casos de uso: "Compilar ETP em TR", "Calcular Divisão de Cotas", "Validar Conformidade com Lei", "Gerar TR"
- Diagrama de classe: TermoReferencia, Cota, CriterioAceitacao, ContrataçãoCorrelata
- Diagrama de sequência: validação de conformidade com Lei 123
- BPMN: fluxo de compilação e validação jurídica
- Backlog: "Como especialista, quero aplicar regras da Lei 123", "Como chefe, quero validar o TR"
- ADR: qual versão da Lei 123/2006 usar? Como lidar com atualizações?
- Testes: cálculo correto de cotas, validação de percentuais
- Auditoria: versão da Lei aplicada, quem validou o TR, data de criação

---

### **G05 — Mapa de Riscos**
**Responsabilidade:** Análise de riscos do produto/serviço que será adquirido (não do fornecedor, mas do item em si).

**Entrada:** TR do módulo G04  
**Saída:** Mapa de Riscos com:
  - Risco de preço elevado (probabilidade: baixa/média/alta, impacto)
  - Risco de especificação inadequada
  - Risco ambiental (se aplicável)
  - Risco de falta de fornecedores (deserta de processo)
  - Risco de falta de manutenção/suporte
  - Mitigação para cada risco

**Atores:** Analista de Risco, Especialista Técnico  
**Artefatos Esperados:**
- Casos de uso: "Identificar Riscos", "Avaliar Probabilidade e Impacto", "Definir Mitigação", "Gerar Mapa"
- Diagrama de classe: Risco, Categoria, Probabilidade, Impacto, Mitigacao
- Diagrama de sequência: análise de risco passo a passo
- BPMN: fluxo de identificação → avaliação → mitigação
- Backlog: "Como analista, quero identificar riscos ambientais", "Como especialista, quero avaliar viabilidade"
- ADR: qual matriz de risco usar? 3x3, 4x4, 5x5?
- Testes: cálculo correto de probabilidade × impacto
- Auditoria: quem fez a avaliação, data, versão do mapa

---

### **G06 — Preparação para Edital e Envio à Prefeitura**
**Responsabilidade:** Formata TR + Mapa de Risco em documento oficial (edital), envia para a Prefeitura que conduzirá o pregão eletrônico.

**Entrada:** TR do módulo G04, Mapa de Risco do módulo G05  
**Saída:** Edital formatado e enviado com:
  - Edital em formato oficial
  - Termo de Referência anexado
  - Mapa de Riscos anexado
  - Registro de envio à Prefeitura
  - Data prevista do pregão

**Atores:** Chefe de Licitações, Servidor responsável por tramitação  
**Artefatos Esperados:**
- Casos de uso: "Formatar Edital", "Validar Edital", "Enviar para Prefeitura", "Registrar Envio"
- Diagrama de classe: Edital, EditalFormatado, Anexo, TramiteExterno
- Diagrama de sequência: formatação → validação → envio
- BPMN: fluxo de tramitação interna e externa
- Backlog: "Como chefe de licitações, quero validar edital antes de envio", "Como servidor, quero registrar envio"
- ADR: qual formato oficial usar? PDF? Assinado digitalmente?
- Testes: validação de formato, completude de anexos
- Auditoria: quem enviou, quando, qual versão foi enviada, confirmação de recebimento na Prefeitura

---

### **G07 — Acompanhamento de Processo Externo**
**Responsabilidade:** Acompanha o pregão eletrônico na plataforma da Prefeitura (SEM implementar o motor de lances, apenas leitura de status).

**Entrada:** Edital enviado do módulo G06, informações do pregão da plataforma externa  
**Saída:** Status atualizado com:
  - Data/hora de abertura do pregão
  - Número de lances recebidos
  - Empresa vencedora por item
  - Valor final por item
  - Status: aberto, em julgamento, adjudicado, fracassado, deserto

**Atores:** Acompanhador de Processo, Chefe de Compras (leitura)  
**Artefatos Esperados:**
- Casos de uso: "Consultar Status Pregão", "Receber Resultado Pregão", "Validar Vencedor", "Atualizar Status"
- Diagrama de classe: ProcessoExterno, StatusPregao, EmpresaVencedora, ResultadoItem
- Diagrama de sequência: integração com plataforma da Prefeitura (leitura)
- BPMN: fluxo de acompanhamento, notificações de mudança de status
- Backlog: "Como acompanhador, quero receber notificações de mudança de status", "Como chefe, quero consultar resultado"
- ADR: qual API da Prefeitura usar? Polling ou webhooks?
- Testes: validação de dados vindos da plataforma externa, detecção de inconsistências
- Auditoria: quando cada consulta foi feita, qual foi o resultado, mudanças de status ao longo do tempo

---

### **G08 — Controle de Ordem de Fornecimento (OF)**
**Responsabilidade:** Gera Ordem de Fornecimento após resultado do pregão, envia para fornecedor vencedor.

**Entrada:** Resultado do pregão do módulo G07 (empresa vencedora, valor final)  
**Saída:** OF com:
  - Número da OF
  - Empresa, CNPJ, contato
  - Itens (descrição, quantidade, preço unitário, preço total)
  - Local de entrega
  - Prazo de entrega
  - Condições de pagamento
  - Assinatura digital
  - Status de envio ao fornecedor

**Atores:** Gestor de OF, Fornecedor (recepção)  
**Artefatos Esperados:**
- Casos de uso: "Gerar OF", "Validar OF", "Enviar OF a Fornecedor", "Acompanhar Entrega"
- Diagrama de classe: OrdemFornecimento, ItemOF, Fornecedor, EntregaPrograma
- Diagrama de sequência: geração → envio → acompanhamento
- BPMN: fluxo de OF, ciclo de entrega
- Backlog: "Como gestor, quero gerar OF automaticamente", "Como fornecedor, quero receber OF"
- ADR: como registrar a assinatura digital? Qual padrão?
- Testes: cálculo de totais, validação de prazos
- Auditoria: quem gerou a OF, quando foi enviada, confirmação de recebimento pelo fornecedor

---

### **G09 — Auditoria, Compliance e Indicadores de Negócio**
**Responsabilidade:** Centraliza trilha de auditoria de TODOS os eventos do sistema, valida conformidade com Lei 14.133/2021, gera indicadores de desempenho.

**Entrada:** Eventos de todos os módulos (G01–G08): criação, modificação, envio, recepção, resultado  
**Saída:** 
  - Log auditoria com todas as operações (quem, quando, o quê, resultado)
  - Relatório de conformidade: todos os DFDs seguem Lei 14.133?
  - Indicadores: tempo médio de processamento, taxa de sucesso de pregões, comparação de preços (cotado vs. final)
  - Alertas: processo travado? Prazo ultrapassado?

**Atores:** Auditor, Chefe de Licitações (leitura de relatórios), Gestor de Compliance  
**Artefatos Esperados:**
- Casos de uso: "Registrar Evento de Auditoria", "Gerar Relatório de Conformidade", "Calcular Indicadores", "Enviar Alertas"
- Diagrama de classe: EventoAuditoria, LogOperacao, ConformidadeItem, Indicador
- Diagrama de sequência: integração com todos os módulos, geração de relatórios
- BPMN: fluxo de auditoria contínua, geração periódica de relatórios
- Backlog: "Como auditor, quero ver trilha completa de cada DFD", "Como gestor, quero dashboard de indicadores"
- ADR: qual banco de dados para auditoria imutável? EventSourcing?
- Testes: integridade de logs, cálculo correto de indicadores
- Auditoria: auto-auditoria interna (quem acessou os logs, quando)

---

## 🔗 Matriz de Integração (Entradas e Saídas)

| Módulo | Entrada | Saída | Depende de |
|--------|---------|-------|-----------|
| G01 | Demandas das secretarias (formulário/texto) | **DFD** (document) | Nenhum |
| G02 | **DFD** (G01) | **ETP** (document) | G01 |
| G03 | **ETP** (G02) | **Relatório de Atas** (decision) | G02 |
| G04 | **ETP** (G02), Decisão Ata (G03) | **TR** (document) | G02, G03 |
| G05 | **TR** (G04) | **Mapa de Risco** (document) | G04 |
| G06 | **TR** (G04), **Mapa de Risco** (G05) | **Edital** (enviado) | G04, G05 |
| G07 | **Edital** enviado (G06), API Prefeitura | **Status Pregão** (dados) | G06 |
| G08 | **Status Pregão** (G07) | **OF** (document) | G07 |
| G09 | Eventos de todos (G01–G08) | **Logs, Relatórios, Indicadores** | Todos |

---

## ✅ Benefícios dessa Abordagem

1. **Paralelismo:** 9 grupos trabalham ao mesmo tempo, sem bloqueios de dependência sequencial.
2. **Clareza:** Cada grupo sabe exatamente o que precisa receber e o que deve entregar.
3. **Integração:** As interfaces são bem definidas (formato de entrada/saída esperado).
4. **Realismo:** Cada grupo desenvolve um módulo **completo** (UC, diagramas, BPMN, testes, auditoria).
5. **Escalabilidade:** Mais fácil para cada grupo debugar seu módulo isoladamente e depois integrar.

---

## 🎯 Próximos Passos para Cada Grupo

1. Ler este documento (compreender seu módulo e as dependências).
2. Ler [contexto-do-sistema.md] para entender o domínio.
3. Definir suas entidades principais (diagrama de classe do módulo).
4. Escrever casos de uso **do seu módulo** (não de todo o sistema).
5. Desenhar fluxo BPMN **do seu módulo**.
6. Escrever histórias de usuário **do seu módulo**.
7. Documentar decisões arquiteturais (ADR) **do seu módulo**.
8. Implementar testes **do seu módulo**.
9. Garantir auditoria e compliance **do seu módulo**.
10. Integrar com G09 (auditoria centralizada).

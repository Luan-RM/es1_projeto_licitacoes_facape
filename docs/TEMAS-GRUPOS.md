# 👥 Temas dos 9 Grupos — Módulos do Sistema

Cada grupo fica responsável por **UM MÓDULO DO SISTEMA** e desenvolve **todos os artefatos de Engenharia de Software** para esse módulo: casos de uso, diagramas, BPMN, backlog, ADRs, testes e auditoria.

Os grupos trabalham **em paralelo**, com interfaces bem definidas.

---

## G01 — Consolidação de Demandas (DFD)

**O que fazer:** Modelar o módulo de coleta e consolidação de demandas das secretarias em um Documento de Formalização da Demanda (DFD) único.

**Responsabilidade:**
- Receber demandas textuais/formulários das secretarias
- Validar e consolidar itens (eliminar duplicatas, normalizar especificações)
- Gerar DFD com lista consolidada de itens solicitados

**Entradas esperadas:** Formulários/demandas das secretarias (tipo, quantidade, justificativa, secretaria)  
**Saídas esperadas:** DFD (document) com lista consolidada de itens

**Entregas mínimas:**
- 4+ casos de uso (cadastrar demanda, consolidar, validar, gerar DFD)
- Diagrama UML de classes: Demanda, Secretaria, Item, DFD
- Diagrama de sequência: fluxo de coleta → consolidação → geração de DFD
- BPMN: processo com swimlanes por secretaria, prazos de coleta
- Histórias de usuário para seu backlog (mínimo 5)
- 2+ ADRs (ex: formato de armazenamento, detecção de duplicatas)
- Testes unitários e de integração (validação de consolidação)
- Auditoria: log de quem criou/modificou cada demanda

---

## G02 — Estudo Técnico Preliminar (ETP)

**O que fazer:** Modelar o módulo que faz análise técnica do DFD: cotação de preços (via Banco de Preços), especificação refinada, análise de mercado.

**Responsabilidade:**
- Receber DFD consolidado (G01)
- Consultar Banco de Preços para obter 3+ cotações por item
- Refinar especificação técnica (normas, padrões, garantias)
- Gerar ETP com recomendações de parcelamento

**Entradas esperadas:** DFD (G01)  
**Saídas esperadas:** ETP (document) com cotações, especificação, análise de mercado

**Entregas mínimas:**
- 4+ casos de uso (consultar Banco de Preços, fazer cotação, validar especificação, gerar ETP)
- Diagrama UML: Cotacao, Fornecedor, Especificacao, AnaliseETP
- Diagrama de sequência: integração com Banco de Preços, análise de propostas
- BPMN: fluxo de análise técnica com pontos de validação
- Histórias de usuário (mínimo 5)
- 2+ ADRs (ex: API vs. manual para Banco de Preços, critérios de seleção de fornecedores)
- Testes: validação de cotações, detecção de outliers de preço
- Auditoria: quem fez cada cotação, critério de seleção

---

## G03 — Pesquisa e Gestão de Atas SRP

**O que fazer:** Modelar o módulo que verifica se há atas de SRP (Sistema de Registro de Preço) já existentes que podem ser "reutilizadas" (adesão/carona) em vez de abrir novo processo.

**Responsabilidade:**
- Receber ETP (G02)
- Pesquisar atas de SRP vigentes que cobrem os itens solicitados
- Comparar competitividade: preço da ata vs. cotação nova
- Calcular viabilidade de adesão (50% limite do quantitativo da ata)
- Gerar recomendação: adesão a ata existente ou novo processo

**Entradas esperadas:** ETP (G02)  
**Saídas esperadas:** Relatório de atas com recomendação de ação

**Entregas mínimas:**
- 4+ casos de uso (pesquisar ata, validar competitividade, calcular limite de adesão, gerar relatório)
- Diagrama UML: Ata, ProcessoLicitatorio, Adesao, Fornecedor, AnalisePrecoConcorrencia
- Diagrama de sequência: busca em base de atas, validação de elegibilidade
- BPMN: fluxo de pesquisa → validação → decisão (adesão vs. novo processo)
- Histórias de usuário (mínimo 5)
- 2+ ADRs (ex: onde armazenar dados de atas? Local vs. Portal da Prefeitura?)
- Testes: cálculo correto de 50%, validação de vigência
- Auditoria: quais atas foram consultadas, qual foi a decisão final

---

## G04 — Elaboração de Termo de Referência (TR)

**O que fazer:** Modelar o módulo que compila ETP com todas as regras de Lei Complementar 123/2006 e cria o Termo de Referência (documento formal).

**Responsabilidade:**
- Receber ETP (G02) e decisão de ata (G03)
- Aplicar regras da Lei 123/2006:
  - Itens ≤ R$ 80k: exclusivo para ME/EPP
  - Itens > R$ 80k: 25% exclusivo para ME/EPP, 75% para todos
  - Empate: ME/EPP tem vantagem de 10% de diferença
- Compilar TR com especificação, divisão de cotas, prazos, critérios de aceitação

**Entradas esperadas:** ETP (G02), Decisão de Ata (G03)  
**Saídas esperadas:** TR (document) formatado e validado

**Entregas mínimas:**
- 4+ casos de uso (compilar ETP em TR, calcular cotas, validar Lei 123, gerar TR)
- Diagrama UML: TermoReferencia, CotaExclusiva, CotaAberta, RegrasLei123, Criterio
- Diagrama de sequência: compilação e validação de conformidade legal
- BPMN: fluxo de TR com validações jurídicas obrigatórias
- Histórias de usuário (mínimo 5)
- 2+ ADRs (ex: qual versão da Lei 123 aplicar? Como lidar com atualizações?)
- Testes: cálculo correto de cotas, validação de percentuais
- Auditoria: versão da Lei aplicada, quem validou, data de criação

---

## G05 — Mapa de Riscos

**O que fazer:** Modelar o módulo que analisa riscos do PRODUTO (não do fornecedor): preço, especificação, ambiente, mercado, manutenção.

**Responsabilidade:**
- Receber TR (G04)
- Identificar riscos: preço elevado, especificação inadequada, risco ambiental, falta de fornecedores (deserta), falta de manutenção
- Avaliar probabilidade (baixa/média/alta) e impacto
- Definir mitigação para cada risco
- Gerar Mapa de Riscos

**Entradas esperadas:** TR (G04)  
**Saídas esperadas:** Mapa de Riscos (document)

**Entregas mínimas:**
- 4+ casos de uso (identificar riscos, avaliar probabilidade/impacto, definir mitigação, gerar mapa)
- Diagrama UML: Risco, Categoria, Probabilidade, Impacto, Mitigacao
- Diagrama de sequência: análise de risco passo a passo
- BPMN: fluxo de identificação → avaliação → mitigação
- Histórias de usuário (mínimo 5)
- 2+ ADRs (ex: qual matriz de risco usar? 3x3, 4x4, 5x5?)
- Testes: cálculo correto de probabilidade × impacto
- Auditoria: quem fez avaliação, data, versão do mapa

---

## G06 — Preparação para Edital e Envio à Prefeitura

**O que fazer:** Modelar o módulo que formata TR + Mapa de Risco em documento oficial (edital), envia para a Prefeitura.

**Responsabilidade:**
- Receber TR (G04) e Mapa de Risco (G05)
- Formatar edital em padrão oficial
- Anexar TR e Mapa de Risco
- Validar completude do edital
- Enviar para Prefeitura (que conduzirá o pregão eletrônico)
- Registrar data/hora/confirmação de envio

**Entradas esperadas:** TR (G04), Mapa de Risco (G05)  
**Saídas esperadas:** Edital formatado e enviado para Prefeitura

**Entregas mínimas:**
- 4+ casos de uso (formatar edital, validar, enviar para Prefeitura, registrar envio)
- Diagrama UML: Edital, EditalFormatado, Anexo, TramiteExterno, Destinatario
- Diagrama de sequência: formatação → validação → envio
- BPMN: fluxo de tramitação interna e externa
- Histórias de usuário (mínimo 5)
- 2+ ADRs (ex: qual formato oficial? PDF assinado digitalmente?)
- Testes: validação de formato, completude de anexos
- Auditoria: quem enviou, quando, qual versão, confirmação de recebimento

---

## G07 — Acompanhamento de Processo Externo

**O que fazer:** Modelar o módulo que acompanha o pregão eletrônico na plataforma da Prefeitura (SEM implementar motor de lances, apenas leitura de status).

**Responsabilidade:**
- Receber edital enviado (G06)
- Consultar plataforma da Prefeitura para obter status do pregão
- Registrar datas de abertura, empresa vencedora, valor final
- Atualizar status: aberto, em julgamento, adjudicado, fracassado, deserto
- Gerar notificações de mudança de status

**Entradas esperadas:** Edital enviado (G06), API da plataforma da Prefeitura  
**Saídas esperadas:** Status atualizado, resultado do pregão (empresa vencedora, valores finais)

**Entregas mínimas:**
- 4+ casos de uso (consultar status pregão, receber resultado, validar vencedor, atualizar status)
- Diagrama UML: ProcessoExterno, StatusPregao, EmpresaVencedora, ResultadoItem
- Diagrama de sequência: integração com API/plataforma da Prefeitura
- BPMN: fluxo de acompanhamento com notificações
- Histórias de usuário (mínimo 5)
- 2+ ADRs (ex: API vs. polling? Webhooks?)
- Testes: validação de dados da plataforma, detecção de inconsistências
- Auditoria: quando cada consulta foi feita, qual foi o resultado

---

## G08 — Controle de Ordem de Fornecimento (OF)

**O que fazer:** Modelar o módulo que gera Ordem de Fornecimento após resultado do pregão e acompanha entrega do fornecedor.

**Responsabilidade:**
- Receber resultado do pregão (G07): empresa vencedora, valor final
- Gerar OF com número, itens, preços, local de entrega, prazo, condições de pagamento
- Enviar OF ao fornecedor (assinado digitalmente)
- Acompanhar confirmação de recebimento da OF
- Acompanhar status de entrega

**Entradas esperadas:** Resultado do pregão (G07)  
**Saídas esperadas:** OF gerada e enviada ao fornecedor

**Entregas mínimas:**
- 4+ casos de uso (gerar OF, validar, enviar ao fornecedor, acompanhar entrega)
- Diagrama UML: OrdemFornecimento, ItemOF, Fornecedor, Entrega, Pagamento
- Diagrama de sequência: geração → envio → acompanhamento
- BPMN: ciclo completo de OF
- Histórias de usuário (mínimo 5)
- 2+ ADRs (ex: assinatura digital? Qual padrão?)
- Testes: cálculo de totais, validação de prazos
- Auditoria: quem gerou OF, quando foi enviada, confirmação de recebimento

---

## G09 — Auditoria, Compliance e Indicadores de Negócio

**O que fazer:** Modelar o módulo centralizado que registra TODOS os eventos de todos os módulos (G01–G08), valida conformidade com Lei 14.133/2021 e gera indicadores de desempenho.

**Responsabilidade:**
- Receber eventos de todos os módulos: criação, modificação, envio, recepção, resultado
- Registrar trilha de auditoria imutável (quem, quando, o quê, resultado)
- Validar conformidade: todas as operações seguem Lei 14.133/2021?
- Calcular indicadores: tempo médio de processamento, taxa de sucesso, variação de preços
- Gerar alertas: processo travado? Prazo ultrapassado?

**Entradas esperadas:** Eventos de G01–G08 (logs, mudanças de estado)  
**Saídas esperadas:** Logs auditoria, relatórios de conformidade, indicadores, alertas

**Entregas mínimas:**
- 4+ casos de uso (registrar evento, gerar relatório de conformidade, calcular indicadores, enviar alertas)
- Diagrama UML: EventoAuditoria, LogOperacao, ConformidadeItem, Indicador, Alerta
- Diagrama de sequência: integração com todos os módulos
- BPMN: fluxo de auditoria contínua, geração periódica de relatórios
- Histórias de usuário (mínimo 5)
- 2+ ADRs (ex: EventSourcing? Qual banco para logs imutáveis?)
- Testes: integridade de logs, cálculo correto de indicadores
- Auditoria: meta-auditoria (quem acessou os logs de auditoria)

---

## 🔗 Integração entre Módulos

```
G01 (DFD)
  ↓
G02 (ETP) ← também recebe sugestão de G03
  ↓
G03 (Atas SRP) ← consulta
  ↓↑
G04 (TR)
  ↓
G05 (Mapa de Risco)
  ↓
G06 (Edital) ← envia para Prefeitura
  ↓ [FORA DO SISTEMA]
Prefeitura faz o pregão
  ↓ [Retorna para cá]
G07 (Acompanhamento) ← consulta status
  ↓
G08 (OF)
  ↓
Fornecedor entrega
  ↓
G09 (Auditoria, Compliance, BI) ← conectado a TODOS
```

Todos os eventos passam por **G09 (Auditoria)** para registro centralizado.

---

## ✅ Benefícios dessa Abordagem

1. **Paralelismo:** 9 grupos trabalham ao mesmo tempo, sem bloqueios sequenciais.
2. **Clareza:** Cada grupo sabe exatamente o que precisa receber e o que deve entregar.
3. **Integração:** As interfaces são bem definidas (formato de entrada/saída esperado).
4. **Realismo:** Cada grupo desenvolve um módulo **completo** (UC, diagramas, BPMN, testes, auditoria).
5. **Escalabilidade:** Mais fácil debugar cada módulo isoladamente e depois integrar.

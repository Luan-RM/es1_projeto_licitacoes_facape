# Contexto do Sistema — Gestão de Licitações FACAPE

> Documento-base de domínio para o projeto da disciplina.  
> Este arquivo consolida o contexto do problema, o escopo funcional, os atores e as regras de negócio extraídos da aula com a equipe de licitações.  
> Ele deve ser tratado como referência conceitual comum para todos os grupos, e não como documento de planejamento da execução do trabalho.

## Como usar este documento

- Use este arquivo para entender o processo real de licitações da FACAPE.
- Use `Requisitos-Projeto-AV2-ES.md` para regras de organização do projeto, integração entre grupos e entregas.
- Use o glossário e as regras de negócio deste projeto para esclarecer dúvidas, validar interpretações e resolver ambiguidades.

---

## 1. Visão Geral

O sistema a ser modelado é um **sistema interno de apoio ao processo de compras públicas** da FACAPE (Faculdade de Petrolina), vinculada à Prefeitura Municipal de Petrolina-PE.

O processo de compras da FACAPE é regido pela **Lei Federal nº 14.133/2021** e segue um fluxo que envolve múltiplos atores internos (secretarias, almoxarifado, setor de licitações) e externos (Prefeitura de Petrolina, portal PNCP, Banco de Preços gov.br, empresas fornecedoras).

O sistema **NÃO** executa o pregão eletrônico — essa etapa ocorre no portal da Prefeitura. O sistema cobre exclusivamente a **fase interna**: da identificação da necessidade até o envio do Termo de Referência à Prefeitura e o controle de Ordens de Fornecimento.

---

## 2. Problema Central

Hoje, todo o processo interno é **manual e fragmentado**:

| Gargalo | Impacto |
|---------|---------|
| Coleta de demandas por e-mail/papel de múltiplas secretarias | DFD incompleto, itens esquecidos, fracionamento indevido de despesa |
| Cotação de preços feita individualmente em planilhas | Erros de valor que levam à deserção ou fracasso do processo |
| Especificações técnicas sem validação | Impugnações de empresas, republicações custosas (~R$ 5.000/processo) |
| Ordens de Fornecimento em papel | Sem rastreabilidade entre demanda → ata → empenho |
| Empenho feito manualmente pela contabilidade | Atraso no bloqueio orçamentário |

---

## 3. Escopo do Sistema

### ✅ Dentro do escopo

- Formalização de demandas (DFD) por secretarias/colegiados
- Consolidação e validação de demandas no almoxarifado
- Suporte à elaboração do Estudo Técnico Preliminar (ETP)
- Suporte à cotação e pesquisa de preços
- Elaboração e validação do Mapa de Riscos
- Elaboração do Termo de Referência (TR)
- Geração e rastreamento de Ordens de Fornecimento
- Controle de Atas de Registro de Preços vigentes
- Notificação de prazos (entrega, validade de ata, empenho)
- Integração com PNCP (Portal Nacional de Compras Públicas) — consulta
- Integração com Banco de Preços gov.br — consulta de cotações

### ❌ Fora do escopo

- Execução do pregão eletrônico
- Sistema financeiro/contábil da prefeitura (empenho)
- Gestão de contratos após assinatura
- Portal de transparência pública

---

## 4. Atores do Sistema

| Ator | Papel |
|------|-------|
| **Secretaria / Colegiado** | Registra demandas de materiais e serviços |
| **Almoxarifado (Xarifado)** | Consolida demandas, verifica estoque, elabora DFD |
| **Chefe de Compras** | Coordena o processo, valida ETP e TR |
| **Chefe de Licitações** | Elabora documentos licitatórios, faz cotação |
| **Gestor do PCA** | Responsável pelo Plano de Contratação Anual |
| **Jurídico Interno** | Valida documentos antes do envio à Prefeitura |
| **Prefeito / Ordenador de Despesas** | Autoriza o processo (assinatura) |
| **Sistema Externo: PNCP** | Portal Nacional de Compras Públicas |
| **Sistema Externo: Banco de Preços** | Software de cotação de preços de mercado |
| **Sistema Externo: Prefeitura (1doc)** | Recebe e tramita o processo licitatório |

---

## 5. Fluxo Macro do Processo

```
[Planejamento]
PCA (Plano de Contratação Anual) → publicado no PNCP até novembro do ano anterior

[Fase Interna — ESCOPO DO SISTEMA]
1. Secretarias registram demandas
2. Almoxarifado consolida → gera DFD
3. Setor de Compras elabora ETP + Mapa de Riscos + Cotação
4. Setor de Licitações elabora Termo de Referência
5. Jurídico interno valida
6. Envio à Prefeitura (via 1doc)

[Fase Externa — FORA DO ESCOPO]
7. Prefeitura autua o processo e elabora Edital
8. Jurídico da Prefeitura + Controladoria validam
9. Publicação no PNCP (mín. 8 dias úteis)
10. Sessão do Pregão Eletrônico
11. Adjudicação e Homologação
12. Geração de Ata de Registro de Preços ou Contrato

[Fase de Execução — PARCIALMENTE NO ESCOPO]
13. Setor emite Ordem de Fornecimento → sistema rastreia
14. Empresa entrega → nota fiscal
15. Contabilidade empenha → fora do escopo
16. Pagamento → fora do escopo
```

---

## 6. Documentos Chave do Domínio

| Sigla | Nome Completo | Descrição |
|-------|---------------|-----------|
| **PCA** | Plano de Contratação Anual | Previsão anual de compras, publicado no PNCP |
| **DFD** | Documento de Formalização da Demanda | Consolida necessidades de todas as secretarias |
| **ETP** | Estudo Técnico Preliminar | Justifica a compra, analisa opções de mercado |
| **TR** | Termo de Referência | Especificação técnica completa; parte do edital |
| **SRP** | Sistema de Registro de Preços | Ata com preços registrados; compra sob demanda |
| **OF** | Ordem de Fornecimento | Pedido formal à empresa vencedora |
| **PNCP** | Portal Nacional de Compras Públicas | Portal gov. obrigatório para publicações |

---

## 7. Regras de Negócio Críticas (para modelagem)

- **RN-01**: Itens com valor estimado ≤ R$ 80.000 são exclusivos para ME/EPP (Lei Complementar 123/2006)
- **RN-02**: Itens com valor > R$ 80.000 devem ter cota de 25% reservada para ME/EPP
- **RN-03**: Fracionamento de despesa é proibido — todos os itens do mesmo tipo devem ser consolidados em um único processo por ano
- **RN-04**: Contratos SRP não obrigam a comprar o quantitativo total licitado (0% a 100% no prazo de 12 meses)
- **RN-05**: Contratos diretos (sem SRP) obrigam a adquirir ≥ 75% do quantitativo licitado
- **RN-06**: Compras por dispensa de valor são permitidas até o limite anual vigente (≈ R$ 57.000 em 2026)
- **RN-07**: O prazo mínimo de divulgação do edital antes do pregão é de 8 dias úteis
- **RN-08**: Adesão a ata alheia (carona) é limitada a 50% do quantitativo da ata original
- **RN-09**: Subcontratação não é permitida nos processos da FACAPE
- **RN-10**: Todo processo deve ter cotação com mínimo de 3 fornecedores distintos

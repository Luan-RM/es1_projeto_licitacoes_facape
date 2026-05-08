# Grupo 03 — Diagrama de Classes do Domínio

## 🎯 Responsabilidade

Modelar o **diagrama de classes UML** do domínio do sistema, capturando as entidades, atributos, relacionamentos, multiplicidades e restrições identificadas no processo de licitações.

---

## 📋 O que entregar

### Artefato 1: `diagrama-classes-dominio.png` + fonte (`.puml` ou `.drawio`)
Diagrama UML de Classes com:
- Mínimo de 12 classes de domínio
- Atributos com tipos de dados
- Relacionamentos completos (associação, composição, agregação, herança)
- Multiplicidades corretas
- Sem classes de infraestrutura (sem `Repository`, `Service`, `Controller`)

### Artefato 2: `dicionario-de-dados.md`
Para cada classe, descreva:
- Responsabilidade da classe
- Atributos (nome, tipo, restrição, exemplo)
- Invariantes relevantes

---

## 🗂️ Classes-Chave para Modelar

Baseadas no contexto do sistema:

| Classe | Descrição |
|--------|-----------|
| `PCA` | Plano de Contratação Anual |
| `Demanda` | Necessidade registrada por uma secretaria |
| `DFD` | Documento de Formalização da Demanda |
| `ItemDemanda` | Item específico dentro de uma demanda |
| `ETP` | Estudo Técnico Preliminar |
| `MapaDeRisco` | Riscos identificados para a contratação |
| `Cotacao` | Pesquisa de preços com fornecedores |
| `ItemCotacao` | Preço de um item junto a um fornecedor |
| `TermoDeReferencia` | Especificação técnica completa |
| `ProcessoLicitatorio` | Registro do processo enviado à Prefeitura |
| `AtaRegistroPrecos` | Ata SRP vigente com itens e preços |
| `OrdemFornecimento` | Pedido emitido à empresa vencedora |
| `Secretaria` | Unidade demandante (colegiado, setor) |
| `Fornecedor` | Empresa participante |

> ⚠️ Cuidado com as **regras de negócio** ao definir multiplicidades:
> - Uma `DFD` pode ter N `Demandas` de N `Secretarias`
> - Uma `AtaRegistroPrecos` pode gerar 0..N `OrdemFornecimento`
> - Um `ProcessoLicitatorio` tem exatamente 1 `TermoDeReferencia`

---

## 🛠️ Ferramentas Recomendadas

| Ferramenta | Link | Observação |
|-----------|------|------------|
| **PlantUML** | [plantuml.com](https://plantuml.com) | Preferencial — código versionável |
| **draw.io** | [app.diagrams.net](https://app.diagrams.net) | Boa UX, exporta XML |
| **StarUML** | [staruml.io](https://staruml.io) | Desktop, rico em recursos UML |
| **Mermaid** | [mermaid.live](https://mermaid.live) | Integra bem com GitHub MD |

### Exemplo PlantUML — Classe básica:

```plantuml
@startuml diagrama-classes-dominio
skinparam classAttributeIconSize 0

class DFD {
  - id: UUID
  - dataAbertura: Date
  - status: StatusDFD
  - valorEstimadoTotal: Decimal
  --
  + consolidarDemandas(): void
  + gerarResumo(): String
}

enum StatusDFD {
  ABERTO
  CONSOLIDADO
  ENVIADO
  ENCERRADO
}

class Demanda {
  - id: UUID
  - descricao: String
  - justificativa: String
  - dataRegistro: Date
}

class ItemDemanda {
  - id: UUID
  - catmat: String
  - descricao: String
  - quantidadeSolicitada: Integer
  - unidadeMedida: String
}

DFD "1" *-- "1..*" Demanda : contém
Demanda "1" *-- "1..*" ItemDemanda : possui
DFD --> StatusDFD
@enduml
```

---

## 📁 Estrutura esperada da pasta

```
grupo-03-diagrama-classes/
├── README.md
├── diagrama-classes-dominio.puml    ← fonte PlantUML (ou .drawio)
├── diagrama-classes-dominio.png     ← exportação
└── dicionario-de-dados.md           ← descrição detalhada das classes
```

---

## ✏️ Seção de Entrega (preencher pelo grupo)

**Integrantes:**
- ...

**Decisões tomadas:**
> ...

**Limitações identificadas:**
> ...

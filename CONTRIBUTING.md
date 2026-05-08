# 🤝 Guia de Contribuição

## Regras Fundamentais

### ❶ Cada grupo toca APENAS sua pasta

```
grupos/grupo-XX-nome-do-grupo/
```

Qualquer commit que modifique arquivos **fora** desta pasta será **rejeitado automaticamente** no PR e o grupo deverá corrigir antes da avaliação.

### ❷ Padrão de commits

Use o prefixo do grupo em todas as mensagens de commit:

```
[G01] feat: adiciona diagrama de casos de uso v1
[G01] fix: corrige ator "Pregoeiro" no diagrama
[G01] docs: atualiza README do grupo com instruções de uso
```

Verbos permitidos: `feat`, `fix`, `docs`, `refactor`, `chore`

### ❸ Nomeação de arquivos

- Use **kebab-case**: `diagrama-casos-de-uso.png`, não `DiagramaCasosDeUso.PNG`
- Inclua fontes editoráveis junto com exportações (`.puml` + `.png`, `.bpmn` + `.png`)
- Sem espaços, acentos ou caracteres especiais nos nomes de arquivo

---

## Fluxo Passo a Passo

### 1. Fork do repositório

No GitHub, clique em **Fork** no repositório do professor.  
Isso cria uma cópia em `github.com/SEU_USUARIO/sistema-licitacao-facape`.

### 2. Clone local

```bash
git clone https://github.com/SEU_USUARIO/sistema-licitacao-facape.git
cd sistema-licitacao-facape
```

### 3. Configure o upstream (repositório original)

```bash
git remote add upstream https://github.com/PROFESSOR/sistema-licitacao-facape.git
git fetch upstream
```

Isso permite que você sincronize com mudanças do professor:

```bash
git pull upstream main
```

### 4. Crie uma branch para seu trabalho

```bash
git checkout -b grupo-01/casos-de-uso
```

Padrão: `grupo-XX/descricao-curta`

### 5. Trabalhe na sua pasta

```bash
# Navegue até sua pasta
cd grupos/grupo-01-casos-de-uso/

# Faça suas modificações...

# Commit
git add .
git commit -m "[G01] feat: adiciona diagrama de casos de uso v1"
```

### 6. Push para o fork

```bash
git push origin grupo-01/casos-de-uso
```

### 7. Abra o Pull Request

- Acesse seu fork no GitHub
- Clique em **Compare & pull request**
- **Base repository**: repositório do professor, branch `main`
- **Head repository**: seu fork, branch `grupo-01/casos-de-uso`
- Preencha o template de PR **completamente**
- Adicione o professor e os membros do grupo como reviewers

---

## Resolução de Conflitos

Como cada grupo trabalha em pastas separadas, conflitos são improváveis. Se ocorrerem (geralmente no `README.md` do grupo):

```bash
git fetch upstream
git rebase upstream/main
# Resolva conflitos manualmente
git add .
git rebase --continue
git push --force-with-lease origin grupo-01/casos-de-uso
```

---

## Checklist antes do PR

- [ ] Todos os artefatos estão na pasta correta do grupo
- [ ] Nenhum arquivo foi modificado fora da pasta do grupo
- [ ] Exportações em imagem (PNG/SVG) estão presentes
- [ ] Fontes editoráveis estão presentes
- [ ] README do grupo está preenchido com decisões e justificativas
- [ ] Commits seguem o padrão `[G0X] tipo: descrição`
- [ ] Template de PR está completamente preenchido

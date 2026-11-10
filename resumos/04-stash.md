# 🎀 Git Stash

> ୨୧ Meu caderno de estudos — Git & GitHub  
> Aprendendo a guardar alterações temporariamente e recuperar meu trabalho quando precisar!

---

## 🌷 1. O que é Git Stash?

O **Git Stash** é um recurso que permite guardar temporariamente alterações que ainda não foram commitadas.

Ele é muito útil quando estamos trabalhando em uma tarefa e precisamos interromper o que estamos fazendo para mudar de branch, corrigir um problema ou realizar outra atividade.

Em vez de criar um commit incompleto, podemos guardar nossas alterações em uma espécie de área temporária.

### Quando utilizar?

Imagine a seguinte situação:

Estou trabalhando em uma funcionalidade na branch `feature/login`, mas meu supervisor solicita uma correção urgente na branch `main`.

Ainda não terminei minha funcionalidade e não quero criar um commit incompleto.

Nesse caso, posso utilizar o `git stash` para guardar minhas alterações, trocar de branch e depois recuperar meu trabalho.

---

## 🩷 2. Principais comandos

### Guardar alterações

```bash
git stash
```

Guarda temporariamente as alterações rastreadas que estão na área de trabalho e na Staging Area, deixando o diretório limpo.

Também podemos adicionar uma descrição:

```bash
git stash push -m "Descrição das alterações"
```

A mensagem ajuda a identificar o conteúdo guardado.

### Listar alterações guardadas

```bash
git stash list
```

Exibe a lista de stashes existentes.

Exemplo:

```text
stash@{0}: On main: Rascunho do README
stash@{1}: On feature/login: Ajustes no formulário
```

Cada stash possui um identificador, como `stash@{0}`.

O índice `0` representa o stash mais recente.

### Recuperar alterações sem remover o stash

```bash
git stash apply
```

Recupera as alterações do stash mais recente, mas mantém o registro na lista.

Também podemos escolher um stash específico:

```bash
git stash apply stash@{1}
```

### Recuperar alterações e remover o stash

```bash
git stash pop
```

Recupera as alterações do stash mais recente e remove esse registro da lista caso a aplicação seja concluída com sucesso.

Também podemos especificar um stash:

```bash
git stash pop stash@{1}
```

### Excluir um stash

```bash
git stash drop stash@{0}
```

Remove um stash específico sem recuperar suas alterações.

### Excluir todos os stashes

```bash
git stash clear
```

Remove todos os registros de stash.

**Atenção:** esse comando é destrutivo. Utilize somente quando tiver certeza de que não precisa mais das alterações guardadas.

---

## 💻 3. Diferença entre Apply e Pop

Embora os dois comandos recuperem alterações, existe uma diferença importante:

| Comando | Recupera alterações | Remove da lista |
|---|---|---|
| `git stash apply` | Sim | Não |
| `git stash pop` | Sim | Sim, se aplicado com sucesso |

**Exemplo:**

Se utilizarmos `git stash apply`, poderemos recuperar as alterações novamente no futuro.

Se utilizarmos `git stash pop`, o Git recupera as alterações e remove o registro da lista quando a operação é concluída com sucesso.

---

## ✨ 4. Guardando alterações que não foram rastreadas

Por padrão, o `git stash` não inclui arquivos novos que ainda não foram rastreados pelo Git.

Para incluir esses arquivos, podemos utilizar:

```bash
git stash -u
```

Ou:

```bash
git stash push -u -m "Inclui arquivos novos"
```

A opção `-u` significa *untracked files*.

Também existe:

```bash
git stash -a
```

A opção `-a` inclui arquivos não rastreados e arquivos ignorados pelo `.gitignore`.

**Atenção:** arquivos ignorados podem conter informações locais ou arquivos gerados automaticamente. Verifique o conteúdo antes de utilizar essa opção.

---

## 🌸 5. Criando uma branch a partir de um Stash

Existe também uma opção interessante: criar uma nova branch utilizando as alterações guardadas.

```bash
git stash branch nome-da-branch
```

O Git cria uma branch a partir do commit em que o stash foi originalmente criado e tenta aplicar as alterações nela.

Isso pode ser útil quando percebemos que as alterações guardadas pertencem a outra tarefa.

---

## 🎀 6. Exemplo prático completo

Imagine que estamos trabalhando no README da branch `main`, mas precisamos interromper a atividade.

### Etapa 1 — Fazer uma alteração

Adicionar um texto temporário ao arquivo:

```bash
Add-Content README.md "`nRascunho temporário."
```

### Etapa 2 — Verificar as alterações

```bash
git status
```

Podemos visualizar o conteúdo modificado com:

```bash
git diff
```

### Etapa 3 — Guardar as alterações

```bash
git stash push -m "Rascunho temporário do README"
```

### Etapa 4 — Conferir se o diretório está limpo

```bash
git status
```

As alterações foram guardadas e não aparecem mais como modificações pendentes.

### Etapa 5 — Consultar os stashes

```bash
git stash list
```

### Etapa 6 — Recuperar as alterações

```bash
git stash pop
```

As alterações voltam para o diretório de trabalho.

Pronto! Conseguimos interromper nossa atividade e recuperar o trabalho depois, sem precisar criar um commit.

---

## 🩷 7. Cuidados importantes

- O stash é temporário, não substitui commits.
- Por padrão, arquivos novos não rastreados não são incluídos.
- Utilize mensagens descritivas para organizar seus stashes.
- Confira a lista antes de excluir algum registro.
- `git stash clear` remove todos os stashes.
- A aplicação de um stash também pode gerar conflitos se o conteúdo atual for incompatível com as alterações guardadas.

### E se ocorrer um conflito ao recuperar um stash?

Podemos verificar os arquivos conflitantes:

```bash
git status
```

Depois, resolvemos os conflitos manualmente, adicionamos os arquivos corrigidos e continuamos normalmente com o trabalho.

---

## 🌷 8. O que preciso lembrar?

| Comando | Função |
|---|---|
| `git stash` | Guarda alterações temporariamente. |
| `git stash push -m "mensagem"` | Guarda alterações com descrição. |
| `git stash list` | Lista os stashes. |
| `git stash apply` | Recupera sem remover da lista. |
| `git stash pop` | Recupera e remove da lista se aplicado com sucesso. |
| `git stash drop` | Exclui um stash específico. |
| `git stash clear` | Exclui todos os stashes. |
| `git stash -u` | Inclui arquivos não rastreados. |
| `git stash -a` | Inclui também arquivos ignorados. |
| `git stash branch nome` | Cria uma branch a partir de um stash. |

---

## 🎀 9. Minhas anotações

- 
- 
- 

---

<sub>♡ Nem toda alteração precisa virar um commit imediatamente. Às vezes, guardar o progresso e continuar depois é a melhor escolha! ♡</sub>
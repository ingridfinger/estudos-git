# 🌷 Git Reset

O `git reset` é utilizado para reposicionar o HEAD e a branch atual em outro commit. Dependendo da opção utilizada, também pode modificar a Staging Area e o diretório de trabalho.

É muito útil quando precisamos desfazer commits ou reorganizar alterações antes de enviá-las ao repositório remoto.

## ✨ 1. Como funciona o Git Reset?

O comando possui três modos principais:

- `--soft`
- `--mixed`
- `--hard`

A diferença entre eles está no que acontece com as alterações depois que o HEAD é reposicionado.

## 🎀 2. Git Reset --soft

```bash
git reset --soft HEAD~1
```

Desfaz o último commit, mas mantém todas as alterações correspondentes na **Staging Area**.

Isso significa que:
- O commit deixa de ser o topo da branch.
- As alterações continuam preparadas para commit.
- Os arquivos do diretório de trabalho não são modificados.

**Quando utilizar?**

Quando queremos desfazer um commit, mas manter suas alterações preparadas para criar outro commit.

## 🌸 3. Git Reset --mixed

```bash
git reset --mixed HEAD~1
```

Desfaz o último commit e retira suas alterações da Staging Area, mantendo-as no diretório de trabalho.

Isso significa que:
- O HEAD volta para o commit anterior.
- As alterações ficam fora da Staging Area.
- Os arquivos continuam modificados.

**Quando utilizar?**

Quando queremos desfazer um commit e reorganizar as alterações antes de adicioná-las novamente.

O `--mixed` é o modo padrão do `git reset`. Portanto, estes comandos são equivalentes:

```bash
git reset --mixed HEAD~1
git reset HEAD~1
```

## 🩷 4. Git Reset --hard

```bash
git reset --hard HEAD~1
```

Desfaz o último commit e atualiza a Staging Area e os arquivos rastreados para corresponderem ao commit de destino.

Isso significa que:
- O HEAD volta para o commit anterior.
- As alterações rastreadas que não existem no commit de destino são descartadas.
- O diretório de trabalho fica igual ao commit de destino.

**Quando utilizar?**

Quando queremos realmente descartar alterações e retornar ao estado de um commit anterior.

⚠️ **Cuidado!** O `--hard` pode causar perda de alterações locais. Antes de utilizá-lo, confira se não existe nenhum trabalho importante que ainda não foi salvo.

Arquivos não rastreados (*untracked*) não são necessariamente removidos pelo `git reset --hard`.

## 🔎 5. Entendendo o HEAD

O `HEAD` representa a posição atual da branch, normalmente apontando para o commit mais recente.

Podemos utilizar referências relativas:

```bash
HEAD~1
```
Indica o commit imediatamente anterior.

```bash
HEAD~2
```
Indica dois commits anteriores.

Exemplo:

```bash
git reset --soft HEAD~1
```

Desfaz o último commit, mantendo suas alterações na Staging Area.

## 📚 6. Comparação entre os modos

| Comando | HEAD | Staging Area | Diretório de trabalho |
|---|---|---|---|
| `--soft` | Reposiciona | Mantém alterações | Mantém alterações |
| `--mixed` | Reposiciona | Atualiza para o destino | Mantém alterações rastreadas |
| `--hard` | Reposiciona | Atualiza para o destino | Atualiza para o destino |

## 💻 7. Comandos úteis

```bash
# Desfazer o último commit mantendo as alterações staged
git reset --soft HEAD~1

# Desfazer o último commit mantendo as alterações unstaged
git reset --mixed HEAD~1

# Descartar alterações rastreadas e voltar ao commit anterior
git reset --hard HEAD~1

# Consultar o estado atual do repositório
git status

# Consultar o histórico de commits
git log --oneline
```

## 💡 8. Git Reset x Git Revert

Embora os dois comandos possam ser utilizados para desfazer commits, eles funcionam de maneiras diferentes:

- **Git Reset:** reposiciona o histórico da branch, podendo retirar commits do histórico atual.
- **Git Revert:** cria um novo commit que desfaz as alterações de um commit anterior, preservando o histórico.

Em projetos compartilhados, o `git revert` costuma ser mais seguro para desfazer commits que já foram publicados.

---

🌷 **Dica final:** antes de executar qualquer comando de reset, confira o `git status` e o histórico com `git log`. Tenha cuidado especialmente com o `--hard` e evite reescrever histórico que outras pessoas já estão utilizando.
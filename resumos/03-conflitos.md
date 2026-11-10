# 🎀 Conflitos e Resolução no Git

> ୨୧ Meu caderno de estudos — Git & GitHub  
> Aprendendo a identificar, entender e resolver conflitos durante o desenvolvimento!

---

## 🌷 1. O que são conflitos no Git?

Um **conflito (merge conflict)** acontece quando o Git não consegue combinar automaticamente duas ou mais alterações.

Isso geralmente ocorre quando duas branches modificam a mesma parte de um arquivo de maneiras diferentes.

Imagine a seguinte situação:

- Na branch `main`, uma frase foi alterada para: "Estou aprendendo Git".
- Na branch `feature/documentacao`, a mesma frase foi alterada para: "Estou estudando Git e GitHub".

Quando tentamos unir essas alterações, o Git não sabe qual versão deve permanecer.

Por isso, ele solicita que o desenvolvedor resolva o conflito manualmente.

### Por que os conflitos acontecem?

- Duas branches modificam a mesma linha de um arquivo.
- Uma pessoa altera um arquivo enquanto outra também está trabalhando nele.
- Uma alteração é feita em uma branch e outra alteração incompatível é feita em outra.
- Durante operações de merge, rebase ou cherry-pick, o Git encontra mudanças que não consegue combinar automaticamente.

**Importante:** conflitos são situações normais no desenvolvimento colaborativo. Eles não significam que o repositório está corrompido.

---

## 🩷 2. Como identificar um conflito?

Quando o Git encontra um conflito, ele interrompe a operação e informa quais arquivos precisam de atenção.

Podemos verificar a situação com:

```bash
git status
```

O resultado pode apresentar algo semelhante a:

```text
On branch main
You have unmerged paths.

Unmerged paths:
  both modified: README.md
```

Isso indica que o arquivo `README.md` foi modificado nas duas versões e precisa ser resolvido.

---

## 💻 3. Entendendo os marcadores de conflito

Ao abrir um arquivo com conflito, podemos encontrar uma estrutura parecida com esta:

```text
<<<<<<< HEAD
Estou aprendendo Git.
=======
Estou estudando Git e GitHub.
>>>>>>> feature/documentacao
```

Esses símbolos são marcadores adicionados pelo Git para mostrar as partes conflitantes.

### O que cada marcador significa?

| Marcador | Significado |
|---|---|
| `<<<<<<< HEAD` | Início da versão da referência atual. |
| `=======` | Separa as duas versões. |
| `>>>>>>> branch` | Final da outra versão apresentada no conflito. |

No exemplo:

- O conteúdo acima de `=======` representa a versão atual.
- O conteúdo abaixo de `=======` representa a outra versão.

**Atenção:** durante um rebase, a interpretação de `HEAD` e da outra versão pode ser diferente da que encontramos em um merge. Por isso, sempre analise o conteúdo e o contexto antes de escolher o que manter.

---

## 🌸 4. Como resolver um conflito?

A resolução é feita manualmente, escolhendo qual conteúdo deve permanecer.

Podemos seguir estes passos:

1. Identificar os arquivos com conflito usando `git status`.
2. Abrir os arquivos no VS Code.
3. Analisar as alterações de cada versão.
4. Escolher uma das versões ou combinar os conteúdos.
5. Remover todos os marcadores de conflito.
6. Salvar o arquivo.
7. Continuar ou finalizar a operação que gerou o conflito.

### Exemplo de resolução

Antes:

```text
<<<<<<< HEAD
Estou aprendendo Git.
=======
Estou estudando Git e GitHub.
>>>>>>> feature/documentacao
```

Depois de resolver:

```text
Estou aprendendo Git e GitHub.
```

O conteúdo final deve conter apenas o texto desejado, sem os marcadores de conflito.

### Resolvendo pelo VS Code

O VS Code possui ferramentas visuais para facilitar esse processo.

Quando identifica um conflito, pode apresentar opções como:

- **Accept Current Change:** mantém a alteração atual.
- **Accept Incoming Change:** mantém a alteração recebida.
- **Accept Both Changes:** mantém as duas alterações.
- **Compare Changes:** permite comparar as versões.

Também é possível editar o arquivo manualmente.

**Importante:** aceitar as duas alterações não significa necessariamente que o resultado ficará correto. Sempre revise o conteúdo final.

---

## ✨ 5. Finalizando um conflito de Merge

Quando o conflito acontece durante um `merge`, precisamos adicionar os arquivos resolvidos à Staging Area.

Por exemplo:

```bash
git add README.md
```

Depois, finalizamos o merge:

```bash
git commit
```

O Git poderá abrir o editor para confirmar a mensagem do merge commit.

Também podemos utilizar:

```bash
git merge --continue
```

Esse comando continua o merge depois que os conflitos foram resolvidos e adicionados.

### Cancelando um Merge

Se decidirmos desistir da operação:

```bash
git merge --abort
```

Esse comando tenta retornar o repositório ao estado anterior ao início do merge.

---

## 💻 6. Resolvendo conflitos durante um Rebase

O rebase também pode gerar conflitos quando o Git tenta reaplicar commits sobre outra base.

Exemplo:

```bash
git switch feature/documentacao
git rebase main
```

Se houver conflito, o Git interromperá a operação.

Podemos verificar os arquivos:

```bash
git status
```

Depois de resolver o conflito e salvar o arquivo:

```bash
git add README.md
git rebase --continue
```

Se outros conflitos aparecerem, repetimos o processo.

### Cancelando um Rebase

Se quisermos desistir da operação:

```bash
git rebase --abort
```

Esse comando tenta retornar ao estado anterior ao início do rebase.

**Atenção:** durante um rebase, não utilizamos `git commit` para finalizar cada conflito. O comando apropriado é `git rebase --continue`.

---

## 🎀 7. Resolvendo conflitos durante um Cherry-pick

O `cherry-pick` também pode gerar conflitos quando tentamos aplicar um commit que possui alterações incompatíveis com o conteúdo atual da branch.

Exemplo:

```bash
git cherry-pick ID_DO_COMMIT
```

Se ocorrer um conflito:

1. Verificar os arquivos com `git status`.
2. Resolver os conflitos manualmente.
3. Adicionar os arquivos resolvidos.

```bash
git add README.md
```

4. Continuar a operação:

```bash
git cherry-pick --continue
```

### Cancelando um Cherry-pick

```bash
git cherry-pick --abort
```

Esse comando cancela a operação em andamento e tenta restaurar o estado anterior.

---

## 🌷 8. Diferenças entre os comandos de continuação

Cada operação possui seu próprio comando para continuar depois da resolução dos conflitos.

| Operação | Comando para continuar |
|---|---|
| Merge | `git merge --continue` |
| Rebase | `git rebase --continue` |
| Cherry-pick | `git cherry-pick --continue` |

Para cancelar:

| Operação | Comando para cancelar |
|---|---|
| Merge | `git merge --abort` |
| Rebase | `git rebase --abort` |
| Cherry-pick | `git cherry-pick --abort` |

---

## 📝 9. Boas práticas

- Leia as alterações antes de resolver um conflito.
- Não escolha automaticamente uma versão sem entender o que ela contém.
- Revise o arquivo depois de remover os marcadores.
- Utilize `git status` para acompanhar o processo.
- Faça testes depois de resolver conflitos, principalmente em projetos maiores.
- Comunique-se com a equipe quando as alterações envolverem arquivos compartilhados.
- Evite deixar conflitos pendentes por muito tempo.

---

## 🩷 10. O que preciso lembrar?

- Conflitos acontecem quando o Git não consegue combinar alterações automaticamente.
- Eles podem ocorrer durante merge, rebase e cherry-pick.
- O desenvolvedor precisa analisar e resolver manualmente as diferenças.
- Os marcadores de conflito devem ser removidos antes de continuar.
- `git status` ajuda a identificar arquivos conflitantes.
- Cada operação possui comandos próprios para continuar ou cancelar.

---

## 🌸 11. Minhas anotações

- 
- 
- 

---

<sub>♡ Resolver conflitos também faz parte de programar. O importante é entender as mudanças e escolher a melhor solução! ♡</sub>
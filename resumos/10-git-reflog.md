# 🎀 10 — Git Reflog

> 🌷 **Encontrando o caminho de volta para commits aparentemente perdidos!**

O `git reflog` é um recurso muito importante para recuperação no Git. Ele registra movimentações de referências, permitindo localizar commits que não aparecem mais no histórico normal da branch.

---

## 💗 1. O que é Git Reflog?

O `git reflog` (Reference Logs) registra as movimentações de referências do repositório local, principalmente do `HEAD`.

Ele mantém um histórico de operações como:

- Commits realizados;
- `git reset`;
- Trocas de branches com `git checkout` ou `git switch`;
- Rebase;
- Revert;
- Outras movimentações de referências.

✨ Sua principal utilidade é ajudar a encontrar commits que deixaram de aparecer no histórico atual depois de alguma operação.

## 🌸 2. Sintaxe básica

Para consultar o reflog:

```bash
git reflog
```

Também podemos visualizar uma versão mais compacta:

```bash
git reflog --oneline
```

Para consultar especificamente as movimentações de uma branch:

```bash
git reflog show main
```

**Lembrete:** o reflog é local. Ele não funciona como um histórico compartilhado no GitHub.

## 🧁 3. Entendendo a diferença entre Git Log e Git Reflog

Embora os dois comandos mostrem informações sobre o histórico, eles têm finalidades diferentes.

| 🎀 Git Log | 🌷 Git Reflog |
|---|---|
| Mostra o histórico de commits alcançáveis a partir da referência consultada. | Mostra o histórico de movimentações de referências locais. |
| Ajuda a acompanhar a evolução do projeto. | Ajuda a localizar commits após operações como reset. |
| Não mostra necessariamente commits que deixaram de ser alcançáveis. | Pode mostrar commits que não aparecem mais no `git log` da branch atual. |

**Resumindo:**

- `git log`: consulta o histórico de commits.
- `git reflog`: consulta o histórico de movimentações do Git.

## 🎀 4. Entendendo as referências do Reflog

Ao executar `git reflog`, podemos encontrar algo parecido com:

```text
abc1234 HEAD@{0}: commit: Atualiza README
def5678 HEAD@{1}: reset: moving to HEAD~1
ghi9012 HEAD@{2}: commit: Adiciona arquivo
```

Vamos entender cada parte:

- **ID do commit:** identificador do commit relacionado à movimentação.
- **HEAD@{0}:** movimentação mais recente registrada.
- **HEAD@{1}:** movimentação imediatamente anterior.
- **HEAD@{2}:** movimentação anterior à de número 1.
- **Descrição:** informa qual operação foi realizada.

⚠️ Os números de `HEAD@{n}` representam posições no reflog, não a quantidade de commits anteriores. Eles também mudam conforme novas operações são realizadas.

## 🪄 5. Recuperando commits com Git Reflog

Imagine que você executou:

```bash
git reset --hard HEAD~2
```

Depois percebeu que precisava de um commit que deixou de aparecer no histórico atual da branch.

Em vez de entrar em pânico, podemos consultar:

```bash
git reflog
```

Localizamos o identificador do commit que queremos recuperar.

Uma maneira segura de preservá-lo é criar uma nova branch:

```bash
git branch recuperacao ID_DO_COMMIT
```

Por exemplo:

```bash
git branch recuperacao abc1234
```

Isso cria uma branch chamada `recuperacao` apontando para o commit escolhido, sem alterar a branch atual.

Para conferir:

```bash
git branch
```

E para verificar o commit guardado:

```bash
git log recuperacao --oneline -1
```

💗 **Importante:** criar uma branch de recuperação não move a branch atual. Apenas cria uma referência para o commit desejado.

## 🌷 6. Nosso exercício prático

Durante os estudos, praticamos os comandos `git reset` e `git revert`.

Primeiro, criamos commits de teste e utilizamos:

```bash
git reset --soft HEAD~1
```

Depois:

```bash
git reset --mixed HEAD~1
```

E, por fim:

```bash
git reset --hard HEAD~1
```

Como consequência, alguns commits deixaram de aparecer no histórico normal da branch.

Para encontrá-los, executamos:

```bash
git reflog
```

Localizamos o commit `21479b0`, que havia sido criado durante o exercício de reset.

Em seguida, criamos uma branch para preservá-lo:

```bash
git branch recuperacao 21479b0
```

Conferimos o resultado:

```bash
git log recuperacao --oneline -1
```

E encontramos:

```text
21479b0 (recuperacao) Adiciona arquivo para praticar reset
```

✨ Assim, conseguimos preservar o commit mesmo depois de termos realizado um `reset --hard`.

## ⚠️ 7. Cuidados importantes

- 🌸 O reflog é armazenado localmente e não é enviado automaticamente ao GitHub.
- 🌸 Suas entradas têm prazo de expiração e podem ser removidas pela limpeza interna do Git.
- 🌸 Nem sempre um commit encontrado no reflog poderá ser recuperado indefinidamente.
- 🌸 Antes de executar comandos destrutivos, procure preservar commits importantes.
- 🌸 Criar uma branch de recuperação é uma alternativa segura para guardar um commit localizado.

**Atenção:** o `git reflog` ajuda a localizar commits, mas não é um substituto para backups.

## 💻 8. Comandos importantes

| Comando | Para que serve |
|---|---|
| `git reflog` | Exibe o histórico de movimentações de referências. |
| `git reflog --oneline` | Exibe o reflog de forma compacta. |
| `git reflog show main` | Exibe o reflog da branch main. |
| `git log` | Consulta o histórico de commits. |
| `git branch nome ID` | Cria uma branch apontando para um commit específico. |
| `git log nome --oneline -1` | Confere o último commit de uma branch. |
| `git --no-pager reflog` | Exibe o reflog sem abrir o paginador do terminal. |

## ✨ 9. O que aprendi?

O `git reflog` permite consultar o histórico de movimentações das referências locais e localizar commits que deixaram de aparecer no histórico atual de uma branch.

Com ele, podemos encontrar commits após operações como `git reset --hard` e preservá-los criando uma nova branch com `git branch`.

---

<blockquote>

🎀 **Para guardar:**

`git reflog` = histórico de movimentações e uma grande ajuda para recuperar commits aparentemente perdidos!

</blockquote>

*Mais um conhecimento documentado na nossa jornada com Git! 🌷*
# 🎀 09 — Git Revert

> 🌷 **Desfazendo alterações sem apagar o histórico do projeto!**

O `git revert` é um comando muito útil quando cometemos algum erro em um commit e queremos desfazer suas alterações sem comprometer o histórico do repositório.

---

## 💗 1. O que é Git Revert?

O `git revert` permite desfazer as alterações introduzidas por um commit específico.

A diferença é que ele **não apaga o commit original**. Em vez disso, cria um novo commit que aplica as alterações inversas.

Assim, o histórico continua preservado e conseguimos visualizar tanto a alteração original quanto sua reversão.

## 🌸 2. Sintaxe básica

```bash
git revert ID_DO_COMMIT
```

Para reverter o commit mais recente:

```bash
git revert HEAD
```

**Lembrete:** `HEAD` representa o commit em que estamos atualmente.

## 🧁 3. Entendendo na prática

Imagine que nosso histórico esteja assim:

```text
A → B → C → D
```

O commit `C` introduziu um erro e queremos desfazer suas alterações.

Executamos:

```bash
git revert ID_DO_COMMIT_C
```

O Git cria um novo commit, chamado `E`:

```text
A → B → C → D → E
```

Perceba que o commit `C` continua existindo! O novo commit `E` é responsável por desfazer suas alterações.

## 🎀 4. Nosso exercício prático

Durante os estudos, criamos um arquivo chamado `teste-revert.txt`:

**1. Criamos o arquivo:**

```powershell
echo "Arquivo para praticar revert" > teste-revert.txt
```

**2. Adicionamos à área de preparação:**

```bash
git add teste-revert.txt
```

**3. Criamos o commit:**

```bash
git commit -m "Adiciona arquivo para praticar revert"
```

**4. Conferimos o histórico:**

```bash
git log --oneline
```

**5. Revertimos o último commit:**

```bash
git revert HEAD
```

O Git criou um novo commit que desfez a criação do arquivo.

✨ O resultado foi que o arquivo deixou de existir no estado atual do projeto, mas o commit original continuou registrado no histórico.

## 🌷 5. Git Revert x Git Reset

Os dois comandos podem ser usados para desfazer alterações, mas funcionam de maneiras diferentes.

| 🎀 Git Revert | 🌸 Git Reset |
|---|---|
| Cria um novo commit. | Move a referência da branch para outro commit. |
| Preserva o histórico original. | Pode retirar commits do histórico atual da branch. |
| Desfaz as alterações de um commit. | Pode alterar o histórico e o estado dos arquivos. |
| Indicado para commits compartilhados. | Muito utilizado para reorganizar o histórico local. |

**Quando usar?**

- 💗 `git revert`: quando queremos desfazer um commit sem reescrever o histórico, especialmente se ele já foi compartilhado.
- 💗 `git reset`: quando queremos voltar a um commit anterior e reorganizar o histórico local.

## 🪄 6. Revertendo um commit específico

Não precisamos reverter somente o último commit. Podemos escolher qualquer commit que desejamos desfazer.

Primeiro, consultamos o histórico:

```bash
git log --oneline
```

Depois, utilizamos o identificador do commit:

```bash
git revert ID_DO_COMMIT
```

Por exemplo, considerando este histórico:

```text
D (HEAD)
C
B
A
```

Para reverter o commit `C`, podemos executar:

```bash
git revert HEAD~1
```

Isso funciona porque `HEAD~1` representa o primeiro commit anterior ao atual nesse histórico linear.

## ⚠️ 7. Resolvendo conflitos durante o Revert

Assim como em outras operações do Git, um `revert` pode apresentar conflitos.

Isso acontece quando o Git não consegue aplicar automaticamente as alterações inversas.

Para resolver:

**1.** Verifique quais arquivos apresentam conflitos.

**2.** Abra os arquivos e corrija os trechos conflitantes.

**3.** Adicione os arquivos corrigidos:

```bash
git add .
```

**4.** Continue a operação:

```bash
git revert --continue
```

Se quiser cancelar a operação em andamento:

```bash
git revert --abort
```

## 🌼 8. Revert de um Merge Commit

Também é possível reverter um merge commit, mas precisamos informar qual dos pais será considerado a linha principal.

```bash
git revert -m 1 ID_DO_MERGE
```

O parâmetro `-m 1` indica que o primeiro pai será tratado como a linha principal.

⚠️ Essa operação exige atenção, pois pode influenciar a forma como merges futuros serão realizados.

## 💻 9. Comandos importantes

| Comando | Para que serve |
|---|---|
| `git revert HEAD` | Reverte o commit mais recente. |
| `git revert ID` | Reverte um commit específico. |
| `git revert HEAD~1` | Reverte o commit anterior ao atual. |
| `git revert --continue` | Continua após resolver conflitos. |
| `git revert --abort` | Cancela o revert em andamento. |
| `git revert -m 1 ID` | Reverte um merge commit usando o primeiro pai como referência principal. |

## ✨ 10. Boas práticas

- 🌷 Confira o histórico antes de executar o comando.
- 🌷 Identifique corretamente o commit que deseja reverter.
- 🌷 Prefira `git revert` para desfazer commits que já foram compartilhados.
- 🌷 Verifique os arquivos depois da reversão.
- 🌷 Execute testes para garantir que tudo continua funcionando.

## 💗 11. O que aprendi?

O `git revert` permite desfazer as alterações de um commit criando um novo commit que registra essa reversão.

Sua principal diferença em relação ao `git reset` é que ele preserva o histórico original, sendo uma alternativa mais segura para desfazer commits que já foram compartilhados com outras pessoas.

---

<blockquote>

🎀 **Para guardar:**

`git revert` = desfaz as alterações, mas mantém o commit original no histórico.

</blockquote>

*Mais um conceito aprendido e documentado! 🌷*
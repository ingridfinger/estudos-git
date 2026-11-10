# 🎀 Git Rebase

> ୨୧ Meu caderno de estudos — Git & GitHub  
> Aprendendo a reorganizar o histórico de commits e integrar alterações entre branches!

---

## 🌷 1. O que é Git Rebase?

O **Git Rebase** é um comando que permite reaplicar os commits de uma branch sobre outra base.

Ele é utilizado para atualizar uma branch com as alterações de outra, reorganizando o histórico do projeto.

Imagine que estamos desenvolvendo uma funcionalidade na branch `feature/login`, enquanto a branch `main` recebe novas alterações.

Podemos utilizar o rebase para reaplicar nossos commits sobre a versão mais recente da `main`.

### Por que utilizar Rebase?

- Manter o histórico de commits mais linear.
- Atualizar uma branch com as alterações de outra.
- Organizar o histórico antes de integrar uma funcionalidade.
- Facilitar a leitura e compreensão da sequência de desenvolvimento.

---

## 🩷 2. Como funciona o Rebase?

Imagine que temos duas branches:

```text
      C---D  feature/login
     /
A---B---E---F  main
```

A branch `feature/login` foi criada a partir do commit `B`, mas a `main` recebeu dois novos commits: `E` e `F`.

Ao executar o rebase da branch `feature/login` sobre `main`, o Git reaplica os commits `C` e `D` depois do commit `F`.

Resultado:

```text
A---B---E---F---C'---D'  feature/login
                main
```

Os commits `C'` e `D'` representam as alterações reaplicadas.

**Importante:** os novos commits possuem identificadores diferentes dos originais, pois o rebase cria novos commits.

---

## 💻 3. Principais comandos

### Iniciar um Rebase

Primeiro, precisamos estar na branch que receberá a atualização:

```bash
git switch feature/login
```

Depois, executamos:

```bash
git rebase main
```

Isso reaplica os commits da branch atual sobre a `main`.

### Verificar o histórico

```bash
git log --oneline --graph --all
```

Permite visualizar a organização do histórico após o rebase.

### Continuar após resolver conflitos

```bash
git add README.md
git rebase --continue
```

Depois de resolver e adicionar os arquivos conflitantes, utilizamos esse comando para continuar a operação.

### Cancelar um Rebase

```bash
git rebase --abort
```

Cancela o rebase em andamento e tenta retornar ao estado anterior à operação.

### Pular um commit

```bash
git rebase --skip
```

Ignora o commit que está sendo reaplicado e continua o processo.

**Atenção:** esse comando descarta a aplicação daquele commit durante o rebase. Utilize somente quando entender por que ele deve ser ignorado.

---

## ✨ 4. Diferença entre Merge e Rebase

Os dois comandos permitem integrar alterações entre branches, mas trabalham de maneiras diferentes.

### Merge

O merge une as alterações das branches e preserva a história original de ambas.

Quando necessário, cria um merge commit.

Exemplo:

```text
      C---D  feature/login
     /     \
A---B---E---F---M  main
```

### Rebase

O rebase reaplica os commits de uma branch sobre outra base, criando novos identificadores para os commits reaplicados.

Exemplo:

```text
A---B---E---F---C'---D'  feature/login
```

### Comparação

| Característica | Merge | Rebase |
|---|---|---|
| Preserva os commits originais | Sim | Não, quando são reaplicados |
| Cria novos commits | Pode criar merge commit | Cria novos commits ao reaplicar |
| Mantém a estrutura das ramificações | Sim | Produz histórico mais linear |
| Reescreve histórico | Não | Sim |
| Pode gerar conflitos | Sim | Sim |

**Resumindo:**

- `merge`: integra as alterações preservando a história das branches.
- `rebase`: reaplica os commits sobre uma nova base, reorganizando o histórico.

---

## 🌸 5. Conflitos durante o Rebase

Assim como no merge, o rebase pode encontrar conflitos quando tenta reaplicar alterações incompatíveis.

Quando isso acontece, o Git interrompe a operação.

### Como resolver?

Primeiro, verificamos o estado do repositório:

```bash
git status
```

Depois, abrimos os arquivos conflitantes e resolvemos as alterações manualmente.

Após salvar os arquivos:

```bash
git add README.md
```

Continuamos o rebase:

```bash
git rebase --continue
```

Se surgirem novos conflitos, repetimos o processo.

### Cancelando em caso de problemas

Se decidirmos desistir da operação:

```bash
git rebase --abort
```

---

## 🎀 6. Rebase Interativo

Existe também o **Interactive Rebase**, que permite modificar a sequência e o conteúdo dos commits.

Ele é útil para organizar o histórico antes de compartilhar alterações.

Para iniciar:

```bash
git rebase -i HEAD~3
```

Nesse exemplo, o Git apresenta os últimos três commits para edição.

### Principais opções

| Opção | Função |
|---|---|
| `pick` | Mantém o commit como está. |
| `reword` | Altera a mensagem do commit. |
| `edit` | Pausa para permitir alterações no commit. |
| `squash` | Combina o commit com o anterior, permitindo editar a mensagem final. |
| `fixup` | Combina o commit com o anterior, descartando sua mensagem. |
| `drop` | Remove o commit do histórico reescrito. |

**Atenção:** o rebase interativo reescreve o histórico. Tenha cuidado ao utilizá-lo em commits que já foram compartilhados com outras pessoas.

---

## 💻 7. Exemplo prático completo

Imagine que estamos trabalhando em uma funcionalidade na branch `feature/rebase`, mas a `main` recebeu novas alterações.

### Etapa 1 — Criar uma branch de trabalho

```bash
git switch -c feature/rebase
```

### Etapa 2 — Fazer uma alteração e criar um commit

```bash
git add README.md
git commit -m "Adiciona documentação de rebase"
```

### Etapa 3 — Voltar para a main

```bash
git switch main
```

### Etapa 4 — Criar uma nova alteração na main

```bash
git add README.md
git commit -m "Atualiza documentação na main"
```

### Etapa 5 — Voltar para a branch de trabalho

```bash
git switch feature/rebase
```

### Etapa 6 — Executar o Rebase

```bash
git rebase main
```

Se houver conflitos, resolvemos os arquivos e executamos:

```bash
git add README.md
git rebase --continue
```

### Etapa 7 — Conferir o histórico

```bash
git log --oneline --graph --all
```

Assim, podemos observar como os commits foram reorganizados sobre a nova base.

---

## 🩷 8. Cuidados e boas práticas

- Utilize rebase para organizar branches locais e atualizar seu trabalho.
- Evite fazer rebase em branches compartilhadas que outras pessoas já utilizam.
- Lembre-se de que o rebase altera os identificadores dos commits reaplicados.
- Verifique o histórico depois da operação.
- Resolva os conflitos com atenção.
- Utilize `git rebase --abort` se precisar cancelar uma operação em andamento.
- Antes de utilizar o rebase interativo, tenha certeza de quais commits deseja modificar.

### Por que evitar Rebase em branches compartilhadas?

Imagine que várias pessoas já baixaram uma branch e estão trabalhando com seus commits.

Se alguém fizer rebase nessa branch, os identificadores dos commits poderão mudar.

Isso pode gerar divergências e dificuldades para os demais desenvolvedores sincronizarem o histórico.

Por isso, uma regra importante é:

**Não reescreva o histórico de branches compartilhadas sem combinar isso com a equipe.**

---

## 🌷 9. O que preciso lembrar?

| Comando | Função |
|---|---|
| `git rebase main` | Reaplica os commits da branch atual sobre a main. |
| `git rebase --continue` | Continua após resolver conflitos. |
| `git rebase --abort` | Cancela o rebase em andamento. |
| `git rebase --skip` | Pula o commit atual durante o rebase. |
| `git rebase -i HEAD~3` | Inicia rebase interativo dos últimos três commits. |
| `git log --oneline --graph --all` | Visualiza o histórico de commits. |

---

## 🎀 10. Minhas anotações

- 
- 
- 

---

<sub>♡ Um histórico organizado facilita entender a evolução de um projeto. Aprender Git também é aprender a cuidar da história do código! ♡</sub>
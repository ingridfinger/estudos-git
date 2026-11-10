# 🎀 Branches e Merge

> ୨୧ Meu caderno de estudos — Git & GitHub  
> Aprendendo a criar caminhos independentes de desenvolvimento e unir alterações!

---

## 🌷 1. O que são Branches?

Uma **branch** (ramificação) é uma linha independente de desenvolvimento dentro de um repositório Git.

Ela permite trabalhar em uma funcionalidade, correção ou melhoria sem modificar diretamente a branch principal.

Por exemplo, imagine que temos um projeto com a seguinte estrutura:

- `main`: versão principal do projeto.
- `feature/login`: desenvolvimento de uma funcionalidade de login.
- `feature/cadastro`: desenvolvimento de uma funcionalidade de cadastro.
- `fix/erro-menu`: correção de um erro.

Cada branch pode ter seus próprios commits e alterações.

### Por que utilizar branches?

- Desenvolver funcionalidades separadamente.
- Corrigir erros sem interferir diretamente na versão principal.
- Testar ideias antes de incorporá-las ao projeto.
- Facilitar o trabalho em equipe.
- Organizar o histórico de desenvolvimento.

---

## 🩷 2. Principais comandos de Branch

### Visualizar branches

Listar as branches locais:

```bash
git branch
```

Listar branches locais e remotas:

```bash
git branch -a
```

A branch atual aparece com um `*` ao lado do nome.

### Criar uma branch

```bash
git branch nome-da-branch
```

Esse comando cria uma branch, mas não muda para ela.

### Criar e trocar de branch

```bash
git switch -c nome-da-branch
```

Esse comando cria uma nova branch e já muda para ela.

### Trocar de branch

```bash
git switch nome-da-branch
```

Também existe a forma antiga:

```bash
git checkout nome-da-branch
```

Atualmente, `git switch` é uma opção mais específica e clara para trocar de branch.

### Renomear uma branch

```bash
git branch -m novo-nome
```

### Excluir uma branch

Excluir uma branch local já integrada:

```bash
git branch -d nome-da-branch
```

Forçar a exclusão:

```bash
git branch -D nome-da-branch
```

**Atenção:** a opção `-D` pode excluir uma branch mesmo que ela tenha alterações ainda não integradas.

---

## 💻 3. O que é Merge?

O **merge** é a operação utilizada para unir as alterações de uma branch em outra.

Por exemplo, imagine que desenvolvemos uma funcionalidade na branch `feature/login` e queremos incorporá-la à `main`.

O merge permite trazer os commits dessa funcionalidade para a branch principal.

### Como realizar um Merge?

Primeiro, precisamos estar na branch que receberá as alterações:

```bash
git switch main
```

Depois, executamos:

```bash
git merge feature/login
```

Pronto! O Git tentará integrar as alterações da branch `feature/login` à `main`.

**Importante:** o merge não exclui automaticamente a branch de origem.

---

## ✨ 4. Tipos de Merge

### Fast-forward

Acontece quando a branch de destino não recebeu novos commits desde a criação da branch que será integrada.

Nesse caso, o Git simplesmente avança a referência da branch de destino.

Exemplo:

```text
A---B---C  main
         \
          D---E  feature/login
```

Após um merge fast-forward:

```text
A---B---C---D---E  main
```

Não é necessário criar um commit de merge.

### Three-way merge

Acontece quando as duas branches possuem commits diferentes desde o ponto em que se separaram.

Exemplo:

```text
      D---E  feature/login
     /
A---B
     \
      C---F  main
```

O Git utiliza três pontos para realizar a integração:

- O ancestral comum.
- O estado atual da branch de destino.
- O estado atual da branch que será integrada.

O resultado pode gerar um **merge commit**, registrando a união das duas linhas de desenvolvimento.

### Merge com commit explícito

Podemos solicitar que o Git crie um commit de merge mesmo quando seria possível fazer fast-forward:

```bash
git merge --no-ff feature/login
```

Isso ajuda a preservar visualmente a integração da funcionalidade no histórico.

---

## 🌸 5. Conflitos de Merge

Um conflito acontece quando o Git não consegue combinar automaticamente determinadas alterações.

Um exemplo comum é quando duas branches modificam a mesma parte de um arquivo de maneiras diferentes.

Quando isso acontece, o Git solicita que o desenvolvedor resolva o conflito manualmente.

### Como identificar um conflito?

Após executar:

```bash
git merge feature/login
```

Podemos receber uma mensagem indicando que existem conflitos.

Ao abrir o arquivo, podemos encontrar algo parecido com:

```text
<<<<<<< HEAD
Conteúdo da branch atual
=======
Conteúdo da outra branch
>>>>>>> feature/login
```

Esses marcadores indicam as partes conflitantes:

- `<<<<<<< HEAD`: início do conteúdo da branch atual.
- `=======`: separação entre as versões.
- `>>>>>>> feature/login`: final do conteúdo da outra branch.

### Como resolver?

1. Abrir o arquivo com conflito.
2. Analisar as duas versões.
3. Escolher o conteúdo que deve permanecer ou combinar as alterações.
4. Remover os marcadores de conflito.
5. Salvar o arquivo.

Depois:

```bash
git add README.md
git commit
```

O commit finaliza o merge quando ele ficou pendente por causa dos conflitos.

### Cancelar um Merge

Se quisermos desistir da operação antes de concluí-la:

```bash
git merge --abort
```

Esse comando tenta retornar ao estado anterior ao início do merge.

---

## 💻 6. Exemplo prático completo

Imagine que estamos trabalhando em um projeto e precisamos criar uma funcionalidade de login.

### Etapa 1 — Criar a branch

```bash
git switch -c feature/login
```

### Etapa 2 — Fazer alterações

Modificar os arquivos necessários e preparar as alterações:

```bash
git add .
```

### Etapa 3 — Criar um commit

```bash
git commit -m "Adiciona funcionalidade de login"
```

### Etapa 4 — Voltar para a branch principal

```bash
git switch main
```

### Etapa 5 — Integrar as alterações

```bash
git merge feature/login
```

### Etapa 6 — Conferir o resultado

```bash
git log --oneline --graph --all
```

Esse comando permite visualizar o histórico de commits e as ramificações do projeto.

---

## 🎀 7. Boas práticas

- Crie branches para funcionalidades e correções específicas.
- Utilize nomes descritivos, como `feature/login` e `fix/menu`.
- Evite desenvolver tudo diretamente na `main`.
- Faça commits pequenos e com mensagens claras.
- Antes de realizar um merge, confira o estado do repositório.
- Resolva os conflitos com atenção, sem apagar alterações importantes.
- Exclua branches que não são mais necessárias depois de confirmar que foram integradas.

---

## 📝 8. O que preciso lembrar?

| Comando | Função |
|---|---|
| `git branch` | Lista branches locais. |
| `git branch nome` | Cria uma branch. |
| `git switch nome` | Troca de branch. |
| `git switch -c nome` | Cria e troca de branch. |
| `git branch -d nome` | Exclui uma branch integrada. |
| `git merge nome` | Integra uma branch à atual. |
| `git merge --no-ff nome` | Cria um merge commit explícito. |
| `git merge --abort` | Cancela um merge em andamento. |
| `git log --oneline --graph --all` | Exibe o histórico visualmente. |

---

## 🌷 9. Minhas anotações

- 
- 
- 

---

<sub>♡ Cada branch é um caminho de desenvolvimento, e o merge permite reunir esses caminhos. Um passo de cada vez! ♡</sub>
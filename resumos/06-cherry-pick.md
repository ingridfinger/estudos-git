# 🎀 Git Cherry-pick

> ୨୧ Meu caderno de estudos — Git & GitHub  
> Aprendendo a selecionar e aplicar commits específicos entre branches!

---

## 🌷 1. O que é Git Cherry-pick?

O **Git Cherry-pick** é um comando que permite selecionar um commit específico de uma branch e aplicar suas alterações na branch atual.

Diferentemente do merge, que integra o histórico de uma branch, o cherry-pick permite escolher apenas os commits que queremos aproveitar.

O nome vem da expressão em inglês *cherry-pick*, que significa escolher cuidadosamente.

### Quando utilizar?

Imagine que estamos desenvolvendo duas funcionalidades:

- `feature/login`: desenvolvimento do sistema de login.
- `feature/cadastro`: desenvolvimento do cadastro de usuários.

Durante o desenvolvimento do login, encontramos uma correção que também precisa ser aplicada ao cadastro.

Em vez de integrar toda a branch de login, podemos selecionar apenas o commit que contém a correção e aplicá-lo na branch de cadastro.

---

## 🩷 2. Como funciona o Cherry-pick?

Imagine que temos o seguinte histórico:

```text
      C---D---E  feature/login
     /
A---B
     \
      F---G  main
```

O commit `D` contém uma alteração que também queremos na branch `main`.

Podemos utilizar:

```bash
git switch main
git cherry-pick ID_DO_COMMIT
```

Depois da operação, o histórico ficará semelhante a:

```text
      C---D---E  feature/login
     /
A---B
     \
      F---G---D'  main
```

O commit `D'` representa a aplicação das alterações de `D` na branch atual.

**Importante:** o cherry-pick cria um novo commit com um identificador diferente. O commit original continua existindo na branch de origem.

---

## 💻 3. Principais comandos

### Identificar o commit desejado

Para visualizar o histórico:

```bash
git log --oneline
```

Para visualizar o histórico de todas as branches:

```bash
git log --oneline --graph --all
```

Esses comandos ajudam a encontrar o identificador do commit que queremos aplicar.

### Aplicar um commit específico

```bash
git cherry-pick ID_DO_COMMIT
```

Aplica as alterações do commit selecionado na branch atual.

Exemplo:

```bash
git cherry-pick 5992ce7
```

### Aplicar vários commits

Podemos selecionar vários identificadores:

```bash
git cherry-pick ID1 ID2 ID3
```

O Git aplica os commits na ordem informada.

Também podemos selecionar um intervalo:

```bash
git cherry-pick ID_INICIAL^..ID_FINAL
```

O símbolo `^` permite incluir o commit inicial no intervalo.

### Continuar após resolver conflitos

```bash
git add README.md
git cherry-pick --continue
```

Depois de resolver os conflitos e adicionar os arquivos, esse comando continua a operação.

### Cancelar um Cherry-pick

```bash
git cherry-pick --abort
```

Cancela a operação em andamento e tenta retornar ao estado anterior.

### Pular um commit

```bash
git cherry-pick --skip
```

Ignora o commit atual durante uma sequência de cherry-pick e continua com os próximos, se houver.

---

## ✨ 4. Cherry-pick x Merge x Rebase

Os três comandos permitem trabalhar com alterações entre branches, mas possuem objetivos diferentes.

| Operação | Principal finalidade |
|---|---|
| Merge | Integrar o histórico de uma branch em outra. |
| Rebase | Reaplicar commits sobre uma nova base. |
| Cherry-pick | Selecionar commits específicos e aplicar suas alterações. |

### Merge

Integra uma branch inteira, preservando a história das ramificações.

### Rebase

Reaplica os commits de uma branch sobre outra base, reorganizando o histórico.

### Cherry-pick

Copia as alterações de commits selecionados para a branch atual, sem integrar necessariamente a branch de origem.

**Resumindo:** merge integra branches, rebase reorganiza commits e cherry-pick seleciona alterações específicas.

---

## 🌸 5. Conflitos durante o Cherry-pick

Assim como no merge e no rebase, o cherry-pick pode gerar conflitos.

Isso acontece quando as alterações do commit selecionado não podem ser aplicadas automaticamente ao conteúdo atual.

### Como resolver?

Primeiro, verificamos a situação:

```bash
git status
```

Depois:

1. Abrimos os arquivos conflitantes.
2. Analisamos as alterações.
3. Escolhemos ou combinamos os conteúdos.
4. Removemos os marcadores de conflito.
5. Salvamos os arquivos.

Adicionamos os arquivos resolvidos:

```bash
git add README.md
```

Continuamos a operação:

```bash
git cherry-pick --continue
```

Se quisermos desistir:

```bash
git cherry-pick --abort
```

---

## 🎀 6. Exemplo prático completo

Imagine que temos uma branch chamada `feature/correcao`, na qual foi realizada uma correção que também precisamos na `main`.

### Etapa 1 — Criar uma branch de trabalho

```bash
git switch main
git switch -c feature/correcao
```

### Etapa 2 — Fazer uma alteração

Modificar um arquivo do projeto.

Depois, adicionar e registrar a alteração:

```bash
git add README.md
git commit -m "Corrige informação na documentação"
```

### Etapa 3 — Identificar o commit

```bash
git log --oneline
```

Anotamos o identificador do commit criado.

### Etapa 4 — Voltar para a main

```bash
git switch main
```

### Etapa 5 — Aplicar o commit selecionado

```bash
git cherry-pick ID_DO_COMMIT
```

### Etapa 6 — Conferir o resultado

```bash
git log --oneline --graph --all
```

Podemos observar que a alteração foi aplicada à `main` por meio de um novo commit.

---

## 🩷 7. Boas práticas e cuidados

- Verifique o identificador do commit antes de executar o comando.
- Confira se a alteração selecionada realmente faz sentido na branch de destino.
- Lembre-se de que o cherry-pick cria um novo commit.
- Evite aplicar várias vezes o mesmo commit sem necessidade.
- Resolva os conflitos com atenção.
- Utilize mensagens de commit claras.
- Tenha cuidado ao aplicar commits que dependem de outras alterações anteriores.

### Uma observação importante

O cherry-pick pode ser muito útil para correções urgentes.

Por exemplo, se uma correção foi desenvolvida em uma branch de funcionalidades, mas também precisa ser aplicada à versão de produção, podemos selecionar somente o commit responsável pela correção.

Entretanto, precisamos verificar se ele não depende de outras alterações que ainda não foram integradas.

---

## 🌷 8. O que preciso lembrar?

| Comando | Função |
|---|---|
| `git cherry-pick ID` | Aplica um commit específico. |
| `git cherry-pick ID1 ID2` | Aplica vários commits selecionados. |
| `git cherry-pick ID_INICIAL^..ID_FINAL` | Aplica um intervalo de commits, incluindo o inicial. |
| `git cherry-pick --continue` | Continua após resolver conflitos. |
| `git cherry-pick --abort` | Cancela a operação em andamento. |
| `git cherry-pick --skip` | Pula o commit atual durante uma sequência. |
| `git log --oneline` | Exibe o histórico resumido. |

---

## 🎀 9. Minhas anotações

- 
- 
- 

---

<sub>♡ Nem sempre precisamos de uma branch inteira. Às vezes, uma única alteração já resolve o problema! ♡</sub>
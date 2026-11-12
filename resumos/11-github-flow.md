# 🎀 Aula 11 — GitHub Flow

> 🌷 **Tema:** Fluxo de trabalho colaborativo com Git e GitHub  
> 💻 **Objetivo:** Aprender a desenvolver funcionalidades em branches separadas, utilizar Pull Requests e revisar alterações antes de integrá-las à branch principal.

---

## 🌸 1. O que é GitHub Flow?

O **GitHub Flow** é um fluxo de trabalho utilizado para organizar o desenvolvimento de projetos com Git e GitHub.

Ele permite que cada funcionalidade ou correção seja desenvolvida em uma branch separada, sem modificar diretamente a branch principal (`main`).

✨ **Por que utilizar?**

- Evita alterações diretas na versão principal.
- Permite desenvolver e testar funcionalidades isoladamente.
- Facilita a revisão do código.
- Organiza o trabalho em equipe.
- Ajuda a manter a versão principal estável.

---

## 🩷 2. Etapas do GitHub Flow

O fluxo básico funciona da seguinte maneira:

| Etapa | Descrição |
|---|---|
| 🌷 Main | Branch principal do projeto. |
| 🌱 Branch | Criar uma ramificação para desenvolver uma funcionalidade. |
| 💻 Alterações | Desenvolver e testar as modificações. |
| 📝 Commit | Registrar as alterações realizadas. |
| ☁️ Push | Enviar a branch para o GitHub. |
| 💌 Pull Request | Solicitar a integração das alterações. |
| 🔍 Code Review | Revisar o código antes da integração. |
| 🎀 Merge | Integrar as alterações à branch principal. |

---

## 🌱 3. Branch

Uma **branch** é uma ramificação do projeto que permite trabalhar em alterações de maneira isolada.

Isso evita que modificações em desenvolvimento afetem diretamente a versão estável do projeto.

**Criar uma branch e mudar para ela:**

```bash
git switch -c feature/nova-funcionalidade
```

💡 O parâmetro `-c` cria a branch e já muda para ela.

**Listar as branches:**

```bash
git branch
```

O asterisco (`*`) indica a branch em que estamos trabalhando atualmente.

---

## 💌 4. Pull Request (PR)

Um **Pull Request** é uma solicitação para integrar as alterações de uma branch em outra.

Geralmente, é utilizado para que outras pessoas possam analisar o código antes de sua integração.

### ✨ Principais campos:

- **Base:** branch que receberá as alterações (ex.: `main`).
- **Compare:** branch que contém as alterações (ex.: `feature/nova-funcionalidade`).
- **Title:** título que resume o objetivo do PR.
- **Description:** descrição das modificações realizadas.

💡 O Pull Request não realiza o merge automaticamente. Ele permite que as alterações sejam analisadas antes da integração.

---

## 🔍 5. Code Review

O **Code Review** é o processo de revisão do código antes de sua integração.

No GitHub, a aba `Files changed` permite visualizar as modificações realizadas.

**Como identificar as alterações:**

- 🟢 Linhas verdes (`+`): conteúdo adicionado.
- 🔴 Linhas vermelhas (`-`): conteúdo removido.

Durante a revisão, é possível identificar erros, sugerir melhorias e comentar trechos específicos do código.

---

## 🎀 6. Merge

O **Merge** é a integração das alterações de uma branch em outra.

Quando um Pull Request é integrado, suas alterações passam a fazer parte da branch de destino.

O GitHub também verifica se existem conflitos entre as branches antes de permitir a integração automática.

💡 A mensagem `No conflicts with base branch` indica que não foram encontrados conflitos entre as alterações e a branch de destino.

---

## 💻 7. Comandos utilizados

| Comando | Função |
|---|---|
| `git status` | Verifica o estado do repositório. |
| `git switch -c nome-da-branch` | Cria e acessa uma nova branch. |
| `git branch` | Lista as branches locais. |
| `git add arquivo` | Adiciona um arquivo à Staging Area. |
| `git commit -m "mensagem"` | Registra as alterações. |
| `git push -u origin nome-da-branch` | Envia uma nova branch ao GitHub e configura o acompanhamento remoto. |
| `git push` | Envia novos commits para a branch remota vinculada. |
| `git switch main` | Retorna à branch principal. |
| `git pull origin main` | Atualiza a branch local com as alterações do repositório remoto. |

---

## 🧁 8. Diferença entre os principais conceitos

| Conceito | Significado |
|---|---|
| 🌱 Branch | Espaço isolado para desenvolver alterações. |
| 💌 Pull Request | Solicitação para integrar alterações. |
| 🔍 Code Review | Revisão das alterações antes da integração. |
| 🎀 Merge | Integração das alterações entre branches. |

---

## 🧸 9. Prática realizada

Foi realizada uma simulação completa do GitHub Flow no repositório `estudos-git`.

**Etapas executadas:**

- [x] Criação da branch `feature/github-flow`.
- [x] Criação e edição do arquivo `github-flow.md`.
- [x] Adição do arquivo à Staging Area.
- [x] Criação de um commit.
- [x] Envio da branch ao GitHub.
- [x] Abertura de um Pull Request com destino à `main`.
- [x] Revisão das alterações pela aba `Files changed`.
- [x] Verificação de ausência de conflitos.
- [x] Realização do Merge.
- [x] Exclusão da branch remota após a integração.
- [x] Atualização da branch `main` local.

<details>
<summary>🌷 Resultado da prática</summary>

Alterações integradas com sucesso e repositório local sincronizado com o GitHub!

</details>

---

## 💗 10. Resumo final

O **GitHub Flow** organiza o desenvolvimento de projetos por meio de branches, Pull Requests, Code Review e Merge.

Esse fluxo permite desenvolver funcionalidades de forma isolada, revisar as alterações antes da integração e manter a branch principal mais estável.

É uma prática muito importante para o desenvolvimento colaborativo e para o trabalho em equipes de programação.

---

<p align="center">
  🌷 ──── ⋆｡°✩｡°⋆ ──── 🌷
  <br>
  <strong>Mais uma etapa concluída!</strong>
  <br>
  Estudando um pouquinho todos os dias. 🎀
</p>
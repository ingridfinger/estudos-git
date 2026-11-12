# 🎀 Aula 12 — Pull Requests e Code Review aprofundado

## 🌷 1. O que é Pull Request (PR)?

Um **Pull Request** é uma solicitação para integrar as alterações de uma branch em outra, geralmente uma branch de funcionalidade (`feature`) na branch principal (`main`).

Ele permite que outras pessoas analisem o código antes da integração.

**Principais objetivos:**
- Revisar alterações antes do merge.
- Identificar erros e possíveis melhorias.
- Discutir soluções com a equipe.
- Manter o histórico de desenvolvimento organizado.
- Garantir maior qualidade ao código.

## 💗 2. O que é Code Review?

**Code Review** é o processo de revisão do código realizado antes de sua integração.

Durante a revisão, o responsável analisa:
- Se o código funciona corretamente.
- Se está organizado e legível.
- Se segue boas práticas.
- Se existem possíveis erros ou melhorias.
- Se as alterações atendem ao objetivo do PR.

O Code Review ajuda a prevenir problemas e compartilhar conhecimento entre desenvolvedores.

## 🎀 3. Tipos de revisão no GitHub

Ao finalizar uma revisão, o GitHub disponibiliza três opções principais:

| Opção | Significado |
|---|---|
| **Comment** | Envia comentários sem aprovar ou bloquear o PR. |
| **Approve** | Aprova as alterações revisadas. |
| **Request changes** | Solicita alterações antes da integração. |

**Importante:** o autor de um Pull Request não pode aprovar o próprio PR nem solicitar alterações nele mesmo.

## 🌸 4. Comentários e sugestões

Durante o Code Review, é possível adicionar comentários diretamente em linhas específicas do código.

### Tipos de interação

- **Review Comment:** comentário sobre uma alteração específica.
- **Suggestion:** sugestão de alteração diretamente no código.
- **Conversation:** espaço para discutir e responder aos comentários.
- **Resolve conversation:** marca uma discussão como resolvida quando o assunto foi tratado.

Uma conversa resolvida não significa que o Pull Request foi aprovado ou integrado.

## 🐰 5. Como funciona o ciclo de revisão?

Um fluxo comum de Code Review funciona assim:

1. Desenvolvedor cria uma branch.
2. Implementa uma funcionalidade.
3. Envia as alterações ao GitHub.
4. Abre um Pull Request.
5. Reviewer analisa o código.
6. Reviewer adiciona comentários ou solicita alterações.
7. Desenvolvedor realiza as correções.
8. Novos commits são enviados para a mesma branch.
9. O Pull Request é atualizado automaticamente.
10. Reviewer verifica as alterações novamente.
11. O PR é aprovado e integrado por meio do merge.

**Atenção:** não é necessário criar outro Pull Request quando novas alterações são enviadas para a mesma branch. O PR existente é atualizado automaticamente.

## 💻 6. Merge Pull Request

O **Merge** é o processo de integrar as alterações de uma branch à branch de destino.

Antes de realizar o merge, é importante verificar:

- Se as revisões necessárias foram concluídas.
- Se as verificações automatizadas passaram.
- Se existem conflitos com a branch de destino.
- Se as regras de proteção da branch foram atendidas.

### Tipos de merge

| Tipo | Funcionamento |
|---|---|
| **Merge commit** | Cria um commit de merge, preservando o histórico das branches. |
| **Squash and merge** | Reúne os commits do PR em um único commit. |
| **Rebase and merge** | Reaplica os commits sobre a branch de destino, sem criar um merge commit tradicional. |

## 🌷 7. Excluir branches após o merge

Depois que um Pull Request é integrado, a branch de funcionalidade geralmente pode ser excluída.

Existem duas operações diferentes:

**No GitHub — branch remota:**
- Utilizar o botão `Delete branch` na página do PR.

**No computador — branch local:**

```powershell
git switch main
git pull origin main
git branch -d nome-da-branch
```

O parâmetro `-d` realiza uma exclusão segura: o Git verifica se a branch já foi integrada antes de removê-la.

## 🧠 8. Comandos utilizados

| Comando | Função |
|---|---|
| `git switch main` | Alterna para a branch main. |
| `git pull origin main` | Atualiza a main local com as alterações do repositório remoto. |
| `git push` | Envia os novos commits para a branch remota configurada. |
| `git status` | Mostra o estado atual do repositório. |
| `git branch` | Lista as branches locais. |
| `git branch -d nome` | Exclui uma branch local já integrada. |

## 🧪 9. Nossa prática — Code Review na prática

Criamos uma simulação de revisão utilizando o repositório `estudos-git`.

### Etapas realizadas

- [x] Criamos a branch `feature/code-review`.
- [x] Criamos o arquivo `calculadora.py`.
- [x] Implementamos funções de soma, subtração e multiplicação.
- [x] Criamos um Pull Request para a `main`.
- [x] Analisamos as alterações em `Files changed`.
- [x] Publicamos um comentário de revisão sugerindo uma demonstração de uso das funções.
- [x] Simulamos o atendimento ao feedback adicionando exemplos com `print()`.
- [x] Criamos o commit `44e3491`.
- [x] Enviamos as alterações com `git push`.
- [x] Conferimos a atualização no mesmo Pull Request.
- [x] Resolvemos a conversa de revisão.
- [x] Realizamos o merge do Pull Request.
- [x] Excluímos a branch remota e a local.
- [x] Atualizamos a `main` local.

### Resultado final

O arquivo `calculadora.py` foi integrado à branch `main`.

A última verificação retornou:

```text
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

Isso confirma que o repositório estava sincronizado com o GitHub e sem alterações pendentes.

---

## ✨ 10. O que preciso guardar desta aula?

1. Pull Request é uma solicitação de integração de alterações, não a integração em si.
2. Code Review é a análise do código antes de sua integração.
3. Comentários de revisão permitem discutir melhorias em linhas específicas.
4. Novos commits enviados à mesma branch atualizam o PR existente.
5. Resolver uma conversa não significa aprovar ou integrar o PR.
6. Merge é o processo que integra as alterações à branch de destino.
7. Após o merge, branches de funcionalidade podem ser excluídas com segurança.

**Conclusão:** Pull Requests e Code Review são fundamentais para o trabalho colaborativo, pois ajudam a manter o código organizado, revisado e com maior qualidade. 💗

🌷 *Aprendendo um commit de cada vez!*

# 🎀 Aula 13 — Proteção de Branches e Regras de Aprovação

## 🌷 1. O que são proteções de branches?

As proteções de branches são regras que ajudam a evitar alterações indevidas em branches importantes, como `main`.

Elas permitem controlar:
- Como as alterações podem chegar à branch principal.
- Quem pode aprovar Pull Requests.
- Quais verificações precisam passar antes do merge.
- Quais operações são permitidas ou bloqueadas.

**Objetivo:** manter o código mais seguro, organizado e confiável, especialmente em projetos com várias pessoas trabalhando juntas.

---

## 💗 2. Branch Rulesets

Os **Branch Rulesets** permitem reunir várias regras de proteção em uma configuração.

No GitHub, acessamos por:

`Settings → Rules → Rulesets`

Criamos um ruleset chamado:

`Protecao da branch main`

Configurações utilizadas:

| Configuração | Estado |
|---|---|
| Enforcement status | Active |
| Branch de destino | `main` |
| Require a pull request before merging | Ativado |
| Block force pushes | Ativado |
| Restrict deletions | Ativado |
| Require linear history | Ativado |

### O que cada regra faz?

**Require a pull request before merging**

Exige que as alterações sejam enviadas por Pull Requests antes de chegarem à branch protegida.

Isso impede que alguém faça alterações diretamente na `main`.

**Block force pushes**

Bloqueia o uso de force push na branch protegida, evitando sobrescrever o histórico remoto dessa branch.

**Restrict deletions**

Impede que a branch protegida seja excluída.

---

## 🌸 3. Pull Requests e aprovações

Também configuramos regras específicas para Pull Requests:

| Regra | Configuração |
|---|---|
| Required approvals | 1 aprovação |
| Dismiss stale pull request approvals | Ativado |
| Require approval of the most recent reviewable push | Ativado |
| Require conversation resolution | Ativado |
| Require review from Code Owners | Desativado |

### Entendendo as regras

**Required approvals**

Exige pelo menos uma aprovação de um revisor com permissão de escrita no repositório.

**Dismiss stale pull request approvals when new commits are pushed**

Se novos commits forem enviados depois de uma aprovação, essa aprovação pode ser descartada, exigindo uma nova revisão.

**Require approval of the most recent reviewable push**

Exige que a última alteração revisável seja aprovada por alguém diferente de quem fez o último push.

**Require conversation resolution before merging**

Exige que as conversas e os comentários de revisão sejam resolvidos antes do merge.

### Uma observação importante

O autor do Pull Request não pode aprovar o próprio PR. Em um projeto individual, sem outro colaborador com permissão adequada, a regra de aprovação pode impedir o merge.

---

## 💻 4. Testando a proteção da branch main

Fizemos um teste prático para verificar se a regra de Pull Request estava funcionando.

Primeiro, criamos um commit vazio:

```powershell
git commit --allow-empty -m "Teste de protecao da main"
```

Depois, tentamos enviar diretamente para a `main`:

```powershell
git push origin main
```

O GitHub rejeitou o envio e apresentou:

```text
GH013: Repository rule violations found
Changes must be made through a pull request.
```

Isso confirmou que a proteção estava funcionando!

Em seguida, removemos o commit local de teste e sincronizamos o repositório:

```powershell
git reset --hard origin/main
```

**Resultado:** a branch `main` permaneceu limpa e sincronizada com o GitHub.

---

## 🦋 5. Histórico linear — Require linear history

Essa regra exige que o histórico da branch protegida permaneça linear, sem commits de merge tradicionais.

Ela é útil para manter o histórico mais simples e fácil de acompanhar.

Existem três métodos comuns de merge no GitHub:

| Método | Como funciona |
|---|---|
| Merge commit | Cria um commit de merge |
| Squash and merge | Junta os commits do PR em um único commit |
| Rebase and merge | Reaplica os commits sobre a branch de destino |

Quando `Require linear history` está ativado, o método **Merge Commit** não é compatível com a branch protegida.

Os métodos Squash e Rebase continuam compatíveis.

**Importante:** histórico linear não impede a criação de Pull Requests. Ele controla a forma como as alterações são incorporadas à branch.

---

## 🔐 6. Regras avançadas

Conhecemos outras regras disponíveis nos Rulesets e entendemos para que servem.

### Require signed commits

Exige commits com assinaturas criptográficas verificadas.

Essas assinaturas ajudam a confirmar a autenticidade e a origem dos commits.

Exemplos de mecanismos de assinatura:
- GPG;
- SSH.

### Require status checks to pass

Exige que verificações automatizadas sejam aprovadas antes do merge.

Exemplo: um projeto pode executar testes automatizados com `pytest` usando GitHub Actions.

Se um teste obrigatório falhar, o GitHub pode bloquear o merge.

**Atenção:** é necessário ter verificações disponíveis e adicionar pelo menos uma como obrigatória. Apenas ativar a regra sem configurar os checks não cria testes automaticamente.

A opção `Require branches to be up to date before merging` exige que a branch esteja atualizada com a branch de destino antes de permitir o merge, quando há verificações obrigatórias configuradas.

### Require deployments to succeed

Permite exigir que determinados ambientes de implantação tenham um deployment bem-sucedido antes do merge.

Depende de ambientes e processos de deployment configurados.

### Require code scanning results

Permite exigir resultados de análise de segurança do código.

Um exemplo é o CodeQL, ferramenta do GitHub que identifica possíveis vulnerabilidades.

### Require code quality results

Permite exigir resultados de análise da qualidade do código, com critérios de severidade.

### Restrict code coverage

Permite estabelecer requisitos de cobertura de testes.

Podemos definir:
- Cobertura mínima de linhas;
- Queda máxima permitida na cobertura em relação à branch principal.

### Automatically request Copilot code review

Permite solicitar automaticamente revisões do GitHub Copilot em Pull Requests, conforme as opções configuradas e a disponibilidade do recurso.

**Observação:** estudamos essas regras, mas não ativamos todas. Algumas dependem de ferramentas, verificações ou ambientes previamente configurados.

---

## 🎯 7. Simulação prática de proteção

Criamos uma branch para testar o fluxo:

```powershell
git switch -c feature/documentacao-projeto
```

Criamos o arquivo `documentacao-projeto.md`, adicionamos o conteúdo e fizemos o commit:

```powershell
git add documentacao-projeto.md
git commit -m "Adiciona documentacao do projeto"
```

Depois, enviamos a branch:

```powershell
git push -u origin feature/documentacao-projeto
```

No GitHub, criamos um Pull Request para a `main`.

O GitHub apresentou:

```text
Review required
At least 1 approving review is required by reviewers with write access.

Merging is blocked
New changes require approval from someone other than the last pusher.
```

Isso confirmou que as regras de aprovação estavam funcionando.

Como não havia outro colaborador disponível para aprovar, fechamos o PR sem fazer o merge.

---

## 🧹 8. Limpeza após a prática

Depois de concluir os testes, removemos a branch remota pelo GitHub e limpamos a branch local.

Comandos utilizados:

```powershell
git switch main
git branch -D feature/documentacao-projeto
git status
```

O resultado final foi:

```text
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

Assim, terminamos a aula sem deixar branches de teste ou alterações pendentes.

---

## 📌 9. Resumo para consulta rápida

| Recurso | Finalidade |
|---|---|
| Branch Rulesets | Agrupar regras de proteção |
| Require PR before merging | Exigir Pull Requests |
| Block force pushes | Bloquear force push |
| Restrict deletions | Impedir exclusão da branch protegida |
| Required approvals | Exigir aprovações |
| Dismiss stale approvals | Descartar aprovações antigas após novas alterações |
| Conversation resolution | Exigir resolução dos comentários |
| Linear history | Impedir merge commits na branch protegida |
| Signed commits | Exigir assinaturas verificadas |
| Status checks | Exigir verificações automatizadas aprovadas |
| Deployments | Exigir deployments bem-sucedidos |
| Code scanning | Exigir resultados de análise de segurança |
| Code coverage | Estabelecer requisitos de cobertura de testes |

---

## 🌷 10. O que pratiquei nesta aula?

- [x] Criei um Branch Ruleset no GitHub.
- [x] Configurei proteções para a branch `main`.
- [x] Testei o bloqueio de push direto.
- [x] Configurei regras de aprovação de Pull Requests.
- [x] Entendi como funciona a exigência de aprovação.
- [x] Estudei histórico linear e métodos de merge.
- [x] Conheci regras avançadas de segurança e qualidade.
- [x] Criei uma branch e um Pull Request para testar as proteções.
- [x] Fechei o PR de teste e limpei as branches.
- [x] Finalizei a prática com o repositório limpo.

**Resultado do quiz:** 4 de 5 questões corretas — 80%.

### 💖 Conclusão

Nesta aula, aprendi a proteger branches importantes e a controlar como as alterações chegam à branch principal de um projeto.

Também compreendi como as regras de aprovação, verificações automatizadas e histórico linear contribuem para a segurança e a qualidade do desenvolvimento colaborativo.

Mais do que conhecer as configurações, consegui testar seu funcionamento diretamente no meu repositório do GitHub.

**Aula 13 concluída! 🎀**

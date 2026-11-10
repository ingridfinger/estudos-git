# 🎀 Tags e Versionamento no Git

> ୨୧ Meu caderno de estudos — Git & GitHub  
> Aprendendo a identificar versões importantes de um projeto e organizar seu histórico!

---

## 🌷 1. O que são Tags no Git?

As **Tags** são referências utilizadas para marcar pontos específicos do histórico de um repositório.

Geralmente, são utilizadas para identificar versões importantes de um projeto, como lançamentos oficiais e versões estáveis.

Por exemplo:

- `v1.0.0`: primeira versão estável.
- `v1.1.0`: versão com novas funcionalidades.
- `v1.1.1`: versão com correções.
- `v2.0.0`: nova versão principal, com mudanças significativas.

### Para que servem?

- Identificar versões importantes.
- Facilitar a consulta de versões anteriores.
- Marcar lançamentos oficiais.
- Organizar o histórico do projeto.
- Facilitar a criação de Releases no GitHub.

**Importante:** uma tag não é uma branch. Ela funciona como uma referência a um commit específico e, normalmente, não acompanha novos commits automaticamente.

---

## 🩷 2. Tipos de Tags

O Git possui dois tipos principais de tags: *Lightweight* e *Annotated*.

### Lightweight Tag

É uma tag simples que funciona como uma referência direta para um commit.

Não possui informações adicionais próprias, como autor da tag, data ou mensagem.

Para criar:

```bash
git tag v1.0.0
```

É útil para marcações simples e temporárias.

### Annotated Tag

É uma tag anotada que possui um objeto próprio no Git, armazenando informações adicionais, como:

- Nome de quem criou a tag.
- Data de criação.
- Mensagem descritiva.
- Referência ao commit marcado.

Para criar:

```bash
git tag -a v1.0.0 -m "Primeira versão do projeto"
```

É recomendada para identificar versões oficiais e lançamentos de projetos.

### Comparação

| Característica | Lightweight | Annotated |
|---|---|---|
| Referencia um commit | Sim | Sim |
| Possui mensagem própria | Não | Sim |
| Registra autor da tag | Não | Sim |
| Registra data da tag | Não | Sim |
| Possui objeto próprio | Não | Sim |
| Indicada para Releases | Menos comum | Sim |

**Minha dica:** para versões oficiais de um projeto, prefira utilizar tags anotadas.

---

## 💻 3. Principais comandos

### Listar Tags

```bash
git tag
```

Exibe as tags existentes no repositório local.

Para pesquisar tags por padrão:

```bash
git tag -l "v1.*"
```

### Criar uma Tag Lightweight

```bash
git tag v1.0.0
```

### Criar uma Tag Annotated

```bash
git tag -a v1.0.0 -m "Primeira versão"
```

### Consultar os detalhes de uma Tag

```bash
git show v1.0.0
```

Exibe informações da tag, do commit associado e das alterações registradas.

### Marcar um commit específico

Por padrão, a tag é criada no commit atual (`HEAD`).

Para marcar outro commit, podemos informar seu identificador:

```bash
git tag -a v1.0.0 ID_DO_COMMIT -m "Primeira versão"
```

### Excluir uma Tag local

```bash
git tag -d v1.0.0
```

Remove a tag do repositório local, mas não exclui o commit.

### Enviar uma Tag para o GitHub

```bash
git push origin v1.0.0
```

Envia uma tag específica para o repositório remoto.

### Enviar todas as Tags

```bash
git push origin --tags
```

Envia todas as tags locais que ainda não estão no repositório remoto.

### Baixar Tags do Repositório Remoto

```bash
git fetch --tags
```

Busca as tags disponíveis no repositório remoto.

### Excluir uma Tag Remota

```bash
git push origin --delete v1.0.0
```

Remove a referência da tag no repositório remoto.

**Atenção:** excluir uma tag não apaga o commit associado. Tenha cuidado ao remover tags de versões já publicadas.

---

## 🌸 4. O que é Versionamento Semântico?

O **Semantic Versioning**, também conhecido como SemVer, é um padrão utilizado para organizar os números das versões de um software.

Sua estrutura tradicional é:

```text
MAJOR.MINOR.PATCH
```

Exemplo:

```text
2.4.1
```

Cada número possui um significado.

### MAJOR

Representa mudanças incompatíveis com versões anteriores.

Exemplo:

```text
1.0.0 → 2.0.0
```

Pode indicar mudanças importantes na estrutura ou no funcionamento do sistema que exigem adaptações.

### MINOR

Representa a adição de funcionalidades compatíveis com versões anteriores.

Exemplo:

```text
1.0.0 → 1.1.0
```

Indica que novas funcionalidades foram adicionadas sem quebrar a compatibilidade.

### PATCH

Representa correções de erros e melhorias compatíveis com a versão anterior.

Exemplo:

```text
1.0.0 → 1.0.1
```

Indica uma atualização com correções, sem adicionar uma nova funcionalidade principal.

### Resumo

| Tipo | Quando incrementar? | Exemplo |
|---|---|---|
| MAJOR | Mudanças incompatíveis | 1.0.0 → 2.0.0 |
| MINOR | Novas funcionalidades compatíveis | 1.0.0 → 1.1.0 |
| PATCH | Correções compatíveis | 1.0.0 → 1.0.1 |

---

## ✨ 5. Diferença entre Tag e Release

Apesar de estarem relacionadas, Tag e Release não são a mesma coisa.

### Tag

É uma referência criada no Git para identificar um commit específico.

Exemplo:

```text
v1.0.0
```

### Release

É um recurso do GitHub utilizado para apresentar e distribuir uma versão do projeto.

Uma Release pode conter:

- Título da versão.
- Descrição das alterações.
- Tag associada.
- Arquivos para download.
- Informações sobre o lançamento.

### Exemplo prático

Podemos criar uma tag chamada `v1.0.0` no Git e depois utilizar essa tag para criar uma Release no GitHub.

Assim, a versão fica identificada no histórico do repositório e apresentada de maneira organizada na plataforma.

---

## 🎀 6. Criando uma Release no GitHub

Depois de criar e publicar uma tag, podemos criar uma Release.

### Etapa 1 — Acessar o repositório

Entrar no repositório no GitHub.

### Etapa 2 — Abrir a área de Releases

Acessar a seção **Releases** e selecionar a opção para criar uma nova Release.

### Etapa 3 — Selecionar a Tag

Escolher a tag que identifica a versão, por exemplo:

```text
v1.0.0
```

### Etapa 4 — Adicionar o título

Exemplo:

```text
v1.0.0 — Primeira versão
```

### Etapa 5 — Escrever a descrição

A descrição deve apresentar o que foi desenvolvido ou atualizado naquela versão.

Exemplo:

```markdown
## Primeira versão do projeto — v1.0.0

Primeira versão organizada do repositório.

### Conteúdo
- Fundamentos de Git e GitHub.
- Gerenciamento de branches.
- Merge e resolução de conflitos.
- Git Stash, Rebase e Cherry-pick.
- Tags e versionamento.
```

### Etapa 6 — Publicar

Depois de conferir as informações, podemos clicar em **Publish release**.

Pronto! A versão estará disponível na área de Releases do GitHub.

---

## 💻 7. Exemplo prático completo

Imagine que finalizamos uma etapa importante do nosso projeto e queremos identificá-la como versão `v1.0.0`.

### Etapa 1 — Conferir o histórico

```bash
git log --oneline
```

Identificamos o commit que representa a versão desejada.

### Etapa 2 — Criar uma Tag Annotated

```bash
git tag -a v1.0.0 -m "Primeira versão do projeto"
```

### Etapa 3 — Conferir as Tags

```bash
git tag
```

### Etapa 4 — Consultar os detalhes

```bash
git show v1.0.0
```

### Etapa 5 — Publicar a Tag

```bash
git push origin v1.0.0
```

### Etapa 6 — Criar uma Release

No GitHub, selecionamos a tag `v1.0.0`, adicionamos um título e uma descrição e publicamos a Release.

Assim, temos uma versão identificada no Git e apresentada oficialmente no GitHub.

---

## 🩷 8. Cuidados e boas práticas

- Utilize tags anotadas para versões oficiais.
- Escolha nomes padronizados para suas versões.
- Utilize o versionamento semântico quando fizer sentido para o projeto.
- Confira o commit associado antes de publicar uma tag.
- Evite reutilizar ou alterar tags de versões já publicadas.
- Escreva descrições claras nas Releases.
- Mantenha um histórico organizado das versões.
- Não confunda publicar uma tag com atualizar a branch principal.

**Importante:** ao executar `git push origin v1.0.0`, o Git envia a referência da tag e os objetos necessários para que o commit marcado esteja disponível no remoto. Isso não atualiza a referência da branch `main`, mas os commits alcançados pela tag podem ficar acessíveis por meio dela.

---

## 🌷 9. O que preciso lembrar?

| Comando | Função |
|---|---|
| `git tag` | Lista as tags locais. |
| `git tag v1.0.0` | Cria uma tag Lightweight. |
| `git tag -a v1.0.0 -m "mensagem"` | Cria uma tag Annotated. |
| `git show v1.0.0` | Exibe os detalhes de uma tag. |
| `git tag -d v1.0.0` | Exclui uma tag local. |
| `git push origin v1.0.0` | Publica uma tag específica. |
| `git push origin --tags` | Publica todas as tags locais. |
| `git fetch --tags` | Busca tags do remoto. |
| `git push origin --delete v1.0.0` | Exclui uma tag remota. |

---

## 🎀 10. Minhas anotações

- 
- 
- 

---

<sub>♡ Cada versão representa uma etapa da evolução de um projeto. Registrar essa evolução também faz parte de desenvolver com qualidade! ♡</sub>
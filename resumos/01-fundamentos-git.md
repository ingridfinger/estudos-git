# 🎀 Fundamentos do Git

> ୨୧ Meu caderno de estudos — Git & GitHub  
> Anotações, conceitos e comandos para consultar sempre que precisar!

---

## 🌷 1. O que é Git?

O **Git** é um sistema de controle de versão distribuído. Ele permite acompanhar as alterações realizadas em arquivos ao longo do tempo, registrar diferentes versões de um projeto e recuperar estados anteriores quando necessário.

Com ele, podemos trabalhar com segurança, organizar o desenvolvimento e colaborar com outras pessoas.

### Git x GitHub

Apesar de trabalharem juntos, eles não são a mesma coisa:

- **Git:** ferramenta que controla as versões do projeto.
- **GitHub:** plataforma online que hospeda repositórios Git e facilita a colaboração entre desenvolvedores.

---

## 🩷 2. Conceitos importantes

| Conceito | Significado |
|---|---|
| Repositório | Local onde o Git acompanha os arquivos e o histórico do projeto. |
| Commit | Registro de um conjunto de alterações. |
| Branch | Linha independente de desenvolvimento. |
| Working Directory | Diretório onde trabalhamos nos arquivos. |
| Staging Area | Área onde selecionamos alterações que entrarão no próximo commit. |
| HEAD | Referência que indica a posição atual no histórico do Git. |

### Como funciona o fluxo básico?

O Git possui três áreas principais:

1. **Working Directory:** onde fazemos as alterações.
2. **Staging Area:** onde selecionamos o que será registrado.
3. **Repository:** onde os commits ficam armazenados.

Fluxo:

`Working Directory → Staging Area → Repository`

---

## 💻 3. Principais comandos

### Configuração inicial

Configura a identidade utilizada nos commits:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
```

Consultar as configurações:

```bash
git config --list
```

### Criando ou obtendo um repositório

Inicializar um repositório:

```bash
git init
```

Clonar um repositório existente:

```bash
git clone URL_DO_REPOSITORIO
```

### Verificando alterações

Verificar o estado dos arquivos:

```bash
git status
```

Visualizar as alterações ainda não adicionadas:

```bash
git diff
```

Visualizar o histórico de commits:

```bash
git log
```

Versão resumida do histórico:

```bash
git log --oneline
```

### Preparando alterações

Adicionar um arquivo específico à Staging Area:

```bash
git add README.md
```

Adicionar todas as alterações:

```bash
git add .
```

Retirar um arquivo da Staging Area, mantendo suas alterações:

```bash
git restore --staged README.md
```

### Registrando alterações

Criar um commit:

```bash
git commit -m "Mensagem explicando a alteração"
```

Consultar o último commit:

```bash
git show
```

### Desfazendo alterações

Descartar alterações não adicionadas à Staging Area:

```bash
git restore README.md
```

**Atenção:** esse comando descarta as alterações locais do arquivo. Utilize com cuidado!

---

## ✨ 4. Exemplo de fluxo na prática

Imagine que estamos desenvolvendo um projeto e modificamos o arquivo `README.md`.

Podemos seguir esta sequência:

```bash
# Verificar o estado do projeto
git status

# Adicionar o arquivo à Staging Area
git add README.md

# Registrar as alterações
git commit -m "Atualiza documentação"

# Conferir o histórico
git log --oneline
```

Pronto! As alterações foram registradas em um novo commit.

---

## 🌸 5. Boas práticas

- Utilize mensagens de commit claras e objetivas.
- Faça commits pequenos e relacionados a uma alteração específica.
- Verifique o `git status` antes de executar operações importantes.
- Não inclua arquivos desnecessários no repositório.
- Utilize um arquivo `.gitignore` para ignorar arquivos que não devem ser versionados.
- Evite utilizar comandos destrutivos sem entender seus efeitos.

---

## 🎀 6. O que preciso lembrar?

- Git controla versões de arquivos e projetos.
- GitHub hospeda repositórios Git online.
- `git add` prepara alterações.
- `git commit` registra alterações no histórico.
- `git status` mostra a situação atual do repositório.
- `git log` permite consultar o histórico de commits.
- A Staging Area permite escolher o que será incluído em um commit.

---

## 📝 7. Minhas anotações

- 
- 
- 

---

<sub>♡ Estudando um pouquinho todos os dias e construindo meu caminho na Engenharia de Computação. ♡</sub>
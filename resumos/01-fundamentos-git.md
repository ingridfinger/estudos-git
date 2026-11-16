

# 🎀 Fundamentos do Git

୨୧ Meu caderno de estudos — Git & GitHub

## 🌷 1. O que é Git?

O **Git** é um sistema de controle de versão distribuído, utilizado para acompanhar as alterações feitas em arquivos e projetos ao longo do tempo.

Com ele, é possível registrar versões do projeto, recuperar estados anteriores, trabalhar com diferentes branches e colaborar com outras pessoas.

Uma diferença importante:

- **Git:** ferramenta responsável pelo controle de versão.
- **GitHub:** plataforma online que hospeda repositórios Git e oferece recursos para colaboração.

## 🩷 2. Conceitos importantes

| Conceito | O que significa |
|---|---|
| Repositório | Local onde ficam armazenados os arquivos e o histórico do projeto. |
| Commit | Registro de um conjunto de alterações. |
| Branch | Linha independente de desenvolvimento dentro do projeto. |
| Working Directory | Diretório onde os arquivos são editados. |
| Staging Area | Área onde são selecionadas as alterações que entrarão no próximo commit. |
| HEAD | Referência que indica o commit ou branch atualmente selecionado. |

O fluxo básico do Git funciona assim:

**Working Directory → Staging Area → Repository**

Primeiro, as alterações são feitas nos arquivos. Depois, elas são selecionadas para a Staging Area e, por fim, registradas em um commit no repositório.

## 💻 3. Principais comandos

### ⚙️ Configuração inicial

| Comando | Função |
|---|---|
| `git config --global user.name "Nome"` | Define o nome do usuário. |
| `git config --global user.email "email"` | Define o e-mail do usuário. |
| `git config --list` | Exibe as configurações do Git. |

### 📁 Criar ou obter um repositório

| Comando | Função |
|---|---|
| `git init` | Inicializa um repositório Git na pasta atual. |
| `git clone URL` | Clona um repositório remoto para o computador. |

### 🔎 Verificar alterações

| Comando | Função |
|---|---|
| `git status` | Mostra o estado atual do repositório. |
| `git diff` | Exibe as diferenças entre as alterações e a versão registrada. |
| `git log` | Exibe o histórico de commits. |

### 📌 Preparar alterações

| Comando | Função |
|---|---|
| `git add arquivo` | Adiciona um arquivo específico à Staging Area. |
| `git add .` | Adiciona as alterações da pasta atual à Staging Area. |
| `git restore --staged arquivo` | Remove um arquivo da Staging Area sem apagar suas alterações. |

### 💾 Registrar alterações

| Comando | Função |
|---|---|
| `git commit -m "mensagem"` | Registra as alterações preparadas em um novo commit. |
| `git show` | Exibe informações sobre um commit. |

### ↩️ Desfazer alterações

| Comando | Função |
|---|---|
| `git restore arquivo` | Descarta alterações ainda não preparadas, recuperando a versão registrada. |

**Atenção:** o comando `git restore` pode descartar alterações feitas nos arquivos. É importante verificar o estado do projeto antes de utilizá-lo.

## ✨ 4. Exemplo de fluxo na prática

Imagine que você criou um arquivo `README.md` e deseja registrar essa alteração no Git.

**1. Verificar o estado do repositório:**

```bash
git status
```

**2. Adicionar o arquivo à Staging Area:**

```bash
git add README.md
```

**3. Registrar a alteração:**

```bash
git commit -m "Adiciona README"
```

**4. Conferir o histórico:**

```bash
git log
```

Esse é um fluxo básico de trabalho: verificar, adicionar, registrar e conferir as alterações.

## 🌸 5. Boas práticas

- Escrever mensagens de commit claras e objetivas.
- Fazer commits pequenos, agrupando alterações relacionadas.
- Verificar o estado do repositório antes de executar comandos.
- Evitar registrar arquivos desnecessários.
- Manter o histórico organizado para facilitar a identificação de alterações.

## 📝 6. Resumo da aula

O Git permite controlar as versões de um projeto e acompanhar seu histórico de alterações.

Os conceitos fundamentais são:

- **Working Directory:** local onde os arquivos são modificados.
- **Staging Area:** área onde as alterações são preparadas.
- **Repository:** local onde os commits são armazenados.
- **Commit:** registro das alterações realizadas.
- **Branch:** linha independente de desenvolvimento.

O fluxo básico de trabalho é:

```bash
git status
git add .
git commit -m "Descrição das alterações"
git log
```


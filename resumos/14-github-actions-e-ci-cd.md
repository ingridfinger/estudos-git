# 🎀 Aula 14 — GitHub Actions e CI/CD

> Automatizando tarefas, executando testes e garantindo mais qualidade ao código! 💗

## 🌷 1. O que é CI/CD?

**CI (Continuous Integration — Integração Contínua)** é uma prática que permite integrar alterações de código frequentemente, executando verificações e testes automaticamente para identificar problemas.

**CD (Continuous Delivery / Continuous Deployment)** está relacionado à entrega e publicação do software:

- **Continuous Delivery:** mantém o código pronto para ser publicado, dependendo de uma aprovação para a implantação.
- **Continuous Deployment:** publica automaticamente as alterações aprovadas, sem precisar de uma etapa manual de implantação.

## 💻 2. O que é GitHub Actions?

O **GitHub Actions** é uma ferramenta de automação integrada ao GitHub. Com ela, podemos executar tarefas automaticamente quando determinados eventos acontecem no repositório.

Alguns exemplos:
- Executar testes quando um código é enviado.
- Verificar alterações em uma Pull Request.
- Automatizar processos de integração e entrega.
- Executar scripts e outras tarefas.

### Estrutura de um workflow

Os workflows são arquivos escritos em YAML e ficam dentro da pasta:

```text
.github/
└── workflows/
    └── primeiro-workflow.yml
```

Principais elementos:

| Elemento | Função |
|---|---|
| `name` | Nome do workflow |
| `on` | Eventos que iniciam a execução |
| `jobs` | Conjunto de tarefas |
| `runs-on` | Ambiente onde o job será executado |
| `steps` | Etapas executadas pelo job |
| `uses` | Utiliza uma Action existente |
| `run` | Executa um comando no terminal |

## ⚙️ 3. Eventos e execução automática

Um workflow pode ser iniciado por diferentes eventos.

Os dois que utilizamos foram:

- `push`: executa o workflow quando alterações são enviadas ao repositório.
- `pull_request`: executa o workflow quando uma Pull Request é aberta ou atualizada.

Exemplo:

```yaml
on:
  push:
  pull_request:
    branches:
      - main
```

Nesse exemplo, o workflow será executado em eventos de `push` e em Pull Requests direcionadas à branch `main`.

## 🧪 4. Testes automatizados com Python e pytest

O **pytest** é uma ferramenta utilizada para executar testes automatizados em Python.

Criamos um pequeno projeto de calculadora para aprender como os testes funcionam na prática.

### Estrutura do projeto

```text
estudos-git/
├── .github/
│   └── workflows/
│       └── primeiro-workflow.yml
└── testes-python/
    ├── calculadora.py
    └── test_calculadora.py
```

### Arquivo `calculadora.py`

Criamos quatro funções:

```python
def somar(a, b):
    return a + b


def subtrair(a, b):
    return a - b


def multiplicar(a, b):
    return a * b


def dividir(a, b):
    if b == 0:
        raise ValueError("Não é possível dividir por zero.")

    return a / b
```

### Arquivo `test_calculadora.py`

Criamos cinco testes para verificar o funcionamento das funções:

```python
import pytest

from calculadora import somar, subtrair, multiplicar, dividir


def test_somar():
    assert somar(2, 3) == 5


def test_subtrair():
    assert subtrair(5, 3) == 2


def test_multiplicar():
    assert multiplicar(4, 3) == 12


def test_dividir():
    assert dividir(10, 2) == 5


def test_dividir_por_zero():
    with pytest.raises(ValueError):
        dividir(10, 0)
```

### Comandos importantes

Instalar o pytest:

```powershell
py -m pip install pytest
```

Verificar a versão instalada:

```powershell
py -m pytest --version
```

Entrar na pasta dos testes:

```powershell
cd .\testes-python
```

Executar os testes:

```powershell
py -m pytest -v
```

O parâmetro `-v` apresenta os resultados individualmente.

**Resultado obtido:**

```text
5 passed in 0.06s
```

Todos os cinco testes foram aprovados! 🎉

## 🤖 5. Executando testes com GitHub Actions

Depois de verificar que os testes funcionavam localmente, configuramos o GitHub Actions para executá-los automaticamente.

### Workflow utilizado

Arquivo: `.github/workflows/primeiro-workflow.yml`

```yaml
name: Testes automatizados

on:
  push:
  pull_request:
    branches:
      - main

jobs:
  testes:
    runs-on: ubuntu-latest

    steps:
      - name: Baixar código do repositório
        uses: actions/checkout@v4

      - name: Configurar Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"

      - name: Instalar pytest
        run: python -m pip install pytest

      - name: Executar testes
        working-directory: testes-python
        run: python -m pytest -v
```

### Entendendo as etapas

1. `actions/checkout@v4`: disponibiliza o código do repositório no ambiente de execução.
2. `actions/setup-python@v5`: configura o Python 3.12.
3. `pip install pytest`: instala a ferramenta de testes.
4. `python -m pytest -v`: executa os testes automatizados.

O `working-directory` define a pasta na qual o comando será executado.

### Resultado no GitHub

Na Pull Request, os dois checks foram aprovados:

- `Testes automatizados / testes (push)`
- `Testes automatizados / testes (pull_request)`

Assim, confirmamos que os testes funcionavam tanto no envio de código quanto na abertura da Pull Request. 💗

## 🔒 6. Integração com proteção de branches

Além de executar os testes automaticamente, podemos configurar o GitHub para exigir que eles sejam aprovados antes de permitir o merge.

Para isso, utilizamos as regras de proteção da branch `main`, em:

**Settings → Rules → Rulesets**

### Regras configuradas

| Regra | Finalidade |
|---|---|
| Restrict deletions | Impede a exclusão da branch por usuários sem permissão de bypass. |
| Require linear history | Impede a criação de merges com histórico não linear. |
| Require a pull request before merging | Exige Pull Request para integrar alterações. |
| Block force pushes | Impede envios forçados. |
| Require status checks to pass | Exige que os checks selecionados sejam aprovados. |
| Require branches to be up to date before merging | Exige que a branch da Pull Request esteja atualizada com a branch de destino. |

### Check obrigatório

Adicionamos o seguinte check:

```text
Testes automatizados / testes
```

Com isso, o GitHub exige que o job de testes seja aprovado antes de permitir a integração da Pull Request.

**Na prática:** se os testes falharem, o merge ficará bloqueado até que o problema seja corrigido e os testes passem.

## 📝 7. Fluxo prático realizado

Durante a aula, seguimos este fluxo:

1. Criamos a branch `feature/testes-automatizados`.
2. Criamos uma calculadora em Python.
3. Escrevemos cinco testes com pytest.
4. Executamos os testes localmente.
5. Configuramos o GitHub Actions.
6. Criamos um commit e enviamos a branch ao GitHub.
7. Abrimos uma Pull Request.
8. Conferimos os checks automáticos.
9. Fizemos o Squash and merge.
10. Excluímos a branch remota e a local.
11. Atualizamos a `main` com `git pull origin main`.
12. Configuramos os testes como uma verificação obrigatória na proteção da branch.

## 💡 8. O que aprendi nesta aula?

Nesta aula, aprendi a utilizar o GitHub Actions para automatizar tarefas e executar testes em projetos.

Também compreendi a diferença entre CI e CD, conheci a estrutura dos workflows e aprendi a configurar eventos como `push` e `pull_request`.

Na prática, desenvolvi uma pequena calculadora em Python, criei testes automatizados com pytest e configurei uma pipeline para executar esses testes diretamente no GitHub.

Por fim, aprendi a integrar os checks do GitHub Actions às regras de proteção da branch `main`, impedindo que alterações sejam integradas sem a aprovação dos testes.

## 🌸 9. Anotações importantes

- CI/CD ajuda a automatizar processos e reduzir erros.
- Workflows do GitHub Actions são escritos em YAML.
- Os arquivos de workflow ficam em `.github/workflows/`.
- `push` e `pull_request` são eventos que podem iniciar workflows.
- O pytest permite executar testes automatizados em Python.
- Checks podem ser utilizados como requisitos para permitir um merge.
- Uma branch protegida ajuda a manter a qualidade e a organização do repositório.

---

<sub>🎀 Estudos de Git e GitHub — Engenharia de Computação | UCDB</sub>

<sub>Feito com dedicação, prática e muitos commits! 💗</sub>
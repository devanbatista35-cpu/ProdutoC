# ProdutosC

> Sistema de gerenciamento de produtos para a linha de comando, desenvolvido em **C**, com persistência de dados em arquivo **CSV**.

![Linguagem](https://img.shields.io/badge/linguagem-C-00599C?logo=c&logoColor=white)
![Interface](https://img.shields.io/badge/interface-terminal-black)
![Armazenamento](https://img.shields.io/badge/armazenamento-CSV-orange)
![Plataforma](https://img.shields.io/badge/plataforma-Windows%20%7C%20Linux-lightgrey)

Projeto acadêmico da disciplina **Algoritmos e Pensamento Computacional**, sob orientação da **Profª Andrea Ono Sakai**.

---

## Sumário

- [Demonstração em vídeo](#demonstração-em-vídeo)
- [Sobre o projeto](#sobre-o-projeto)
- [Funcionalidades](#funcionalidades)
- [Interface](#interface)
- [Tecnologias](#tecnologias)
- [Como executar](#como-executar)
- [Estrutura de dados](#estrutura-de-dados)
- [Validações implementadas](#validações-implementadas)
- [Organização do código](#organização-do-código)
- [Integrantes](#integrantes)

---

## Demonstração em vídeo


**Link do vídeo:** [https://www.youtube.com/watch?v=MXVzC7ynqQ8](https://www.youtube.com/watch?v=MXVzC7ynqQ8)

---

## Sobre o projeto

O **ProdutosC** é um sistema de loja que permite cadastrar, consultar, atualizar e remover produtos direto pelo terminal. Os dados ficam salvos no arquivo `produtos.csv`, então continuam disponíveis mesmo depois de fechar o programa.

O projeto aplica, na prática, conceitos fundamentais de programação em C: estruturas (`struct`), ponteiros, manipulação de arquivos, funções, modularização e validação de entradas.

## Funcionalidades

| Opção | Funcionalidade | Descrição |
|:-----:|----------------|-----------|
| 1 | Cadastrar produto | Registra nome, categoria e preço. O ID é gerado automaticamente. |
| 2 | Listar produtos | Exibe todos os produtos cadastrados e o total. |
| 3 | Buscar por nome | Localiza um produto pelo nome exato. |
| 4 | Buscar por categoria | Lista todos os produtos de uma categoria. |
| 5 | Buscar por faixa de preços | Lista os produtos entre um preço mínimo e um máximo. |
| 6 | Atualizar produto | Altera nome, categoria e preço de um produto, escolhido pelo ID. |
| 7 | Remover produto | Exclui um produto pelo ID, com confirmação (S/N). |
| 0 | Sair | Encerra o sistema. |

## Interface

### Menu principal

<p align="center">
  <img src="img/tela-inicial.png" alt="Menu principal do sistema" width="420">
</p>

### Cadastro e listagem

<table>
  <tr>
    <td align="center"><b>Cadastrar produto</b></td>
    <td align="center"><b>Listar produtos</b></td>
  </tr>
  <tr>
    <td align="center"><img src="img/cadastro.png" alt="Tela de cadastro de produto" width="380"></td>
    <td align="center"><img src="img/listagem.png" alt="Tela de listagem de produtos" width="330"></td>
  </tr>
</table>

### Buscas

<table>
  <tr>
    <td align="center"><b>Por nome</b></td>
    <td align="center"><b>Por categoria</b></td>
    <td align="center"><b>Por faixa de preços</b></td>
  </tr>
  <tr>
    <td align="center"><img src="img/busca-nome.png" alt="Busca por nome" width="300"></td>
    <td align="center"><img src="img/busca-categoria.png" alt="Busca por categoria" width="300"></td>
    <td align="center"><img src="img/busca-preco.png" alt="Busca por faixa de preços" width="300"></td>
  </tr>
</table>

### Atualização e remoção

<table>
  <tr>
    <td align="center"><b>Atualizar produto</b></td>
    <td align="center"><b>Remover produto</b></td>
  </tr>
  <tr>
    <td align="center"><img src="img/atualizar.png" alt="Tela de atualização de produto" width="400"></td>
    <td align="center"><img src="img/remover.png" alt="Tela de remoção de produto" width="430"></td>
  </tr>
</table>

## Tecnologias

- **Linguagem:** C (padrão ANSI/C99)
- **Bibliotecas:** `stdio.h`, `stdlib.h`, `string.h`, `locale.h`
- **Persistência:** arquivo de texto no formato CSV
- **Compilador sugerido:** GCC (MinGW no Windows) ou Dev-C++

## Como executar

### Pré-requisitos

- Um compilador C instalado (por exemplo, [GCC](https://gcc.gnu.org/))

### Passo a passo

```bash
# 1. Clone o repositório
git clone https://github.com/SEU_USUARIO/ProdutosC.git
cd ProdutosC

# 2. Compile
gcc Produtos.c -o produtos

# 3. Execute
./produtos          # Linux / macOS
produtos.exe        # Windows
```

> **Observação:** o arquivo `produtos.csv` é criado automaticamente no primeiro cadastro, na mesma pasta de execução do programa.

## Estrutura de dados

Cada produto é representado pela seguinte `struct`:

```c
typedef struct {
    int   id;
    char  nome[100];
    char  categoria[100];
    float preco;
} Produto;
```

No arquivo `produtos.csv`, cada linha guarda um produto, com campos separados por ponto e vírgula:

```
id;nome;categoria;preco
1;Caneta;Escolar;7,00
2;Borracha;Escolar;7,00
```

## Validações implementadas

- **Campos de texto:** não aceitam valor vazio nem o caractere `;`, que quebraria o formato do CSV.
- **Preço:** aceita apenas números não negativos, com vírgula ou ponto como separador decimal.
- **Faixa de preços:** o preço mínimo não pode ser maior que o máximo.
- **ID:** deve ser um número inteiro positivo; o sistema avisa quando o ID não existe.
- **Menu:** entradas que não são números são recusadas.
- **Remoção:** pede confirmação antes de excluir e permite cancelar.
- **IDs automáticos:** o novo ID é sempre o maior ID existente mais 1, sem repetição.
- **Atualização e remoção seguras:** o programa grava as alterações em um arquivo temporário (`temp.csv`) e só substitui o original ao final da operação.

## Organização do código

| Grupo | Funções |
|-------|---------|
| **CRUD** | `cadastrarProduto`, `listarProduto`, `buscarPorNome`, `buscarPorCategoria`, `buscarPorFaixa`, `atualizarProduto`, `removerProduto` |
| **Validação de entrada** | `lerTexto`, `lerPreco`, `lerId` |
| **Arquivo CSV** | `lerLinhaCSV`, `verificarProdutos`, `gerarId` |
| **Auxiliares** | `menu`, `mostrarProduto`, `confirmarRemocao`, `limparBuffer`, `pausar` |

## Integrantes

| Nome |
|------|
| Vanessa Vieira dos Santos |
| Gustavo Sacomani Rafael |
| João Pedro Camargo de Souza |
| Pamela Nunes de Campos |
| Henrique de Oliveira Granso |


**Professora orientadora:** Profª Andrea Ono Sakai
**Disciplina:** Algoritmos e Pensamento Computacional

---

<p align="center">Desenvolvido por estudantes como projeto acadêmico.</p>

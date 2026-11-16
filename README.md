# C06 - Projeto-2

Sistema de **controle de estoque** feito em Java, executado pelo terminal. Ele permite cadastrar produtos, adicionar e retirar unidades e ver quais itens estão com estoque baixo. Os dados ficam salvos em um arquivo de texto, então continuam disponíveis da próxima vez que o programa for aberto.

## Funcionalidades

```
=== CONTROLE DE ESTOQUE ===
1 - Cadastrar produto
2 - Listar produtos
3 - Adicionar estoque
4 - Retirar estoque
5 - Verificar estoque baixo
0 - Sair
```

- **Cadastrar produto:** pede o nome, a quantidade inicial e o tipo (Comum ou Perecível). Não aceita nome vazio, nome repetido ou quantidade negativa.
- **Listar produtos:** mostra todos os produtos e marca os que estão com estoque baixo.
- **Adicionar / Retirar estoque:** altera a quantidade de um produto já cadastrado. Não deixa retirar mais do que existe.
- **Verificar estoque baixo:** lista só os produtos abaixo do mínimo.

### Estoque mínimo por tipo

| Tipo      | Mínimo | Estoque baixo quando |
|-----------|--------|----------------------|
| Comum     | 5      | quantidade < 5       |
| Perecível | 5      | quantidade < 5       |

## Como executar

É preciso ter o **JDK 11 ou mais recente** instalado.

```bash
cd ControleEstoque
javac *.java
java Main
```

O arquivo `produtos.txt` é criado e lido na pasta de onde o programa é executado.

## Estrutura do projeto

```
ControleEstoque/
├── Alertavel.java         # Interface com o método estoqueBaixo()
├── Produto.java           # Classe abstrata com nome, quantidade e regras de estoque
├── ProdutoComum.java      # Produto com estoque mínimo 5
├── ProdutoPerecivel.java  # Produto com estoque mínimo 5
├── Estoque.java           # Lista de produtos: cadastrar, buscar, listar, salvar e carregar
└── Main.java              # Menu e leitura das opções do usuário
```

## Conceitos de POO utilizados

- **Interface:** `Alertavel` define o comportamento `estoqueBaixo()`, que todo produto precisa ter.
- **Classe abstrata:** `Produto` reúne o que é comum a todos os produtos, mas não pode ser instanciada diretamente.
- **Herança:** `ProdutoComum` e `ProdutoPerecivel` herdam de `Produto`.
- **Polimorfismo:** cada tipo implementa `getMinimo()` e `getTipo()` do seu jeito, e o `Estoque` trata todos como `Produto`.
- **Encapsulamento:** `nome` e `quantidade` são privados e só mudam pelos métodos `adicionar()` e `retirar()`, que validam os valores.
- **Tratamento de exceções:** entradas inválidas geram `IllegalArgumentException`, e o menu mostra a mensagem de erro sem encerrar o programa.

## Arquivo de dados

Os produtos são salvos em `produtos.txt`, um por linha, no formato:

```
Tipo;Nome;Quantidade
```

Exemplo:

```
Perecivel;Arroz;8
Comum;Feijao;6
```

O arquivo é lido ao abrir o programa e gravado ao escolher a opção **0 - Sair**. Ao carregar, linhas com formato inválido são ignoradas e avisadas no terminal.

## Uso de Inteligência Artificial

Durante o desenvolvimento deste projeto foi utilizado o **ChatGPT** como apoio para:

- revisar conceitos básicos da matéria;
- entender o funcionamento do código;
- auxiliar nos testes do programa.

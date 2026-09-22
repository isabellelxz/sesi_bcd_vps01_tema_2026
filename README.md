# Prova-Desafio Banco de Dados 

## Desafio: Estoque da Loja

## Atividade Mer e Der:

![Atividade](./AtividadeMEReDER.drawio.png)

## Dicionário de Dados: 

| Entidade                | Atributo          | Tipo    | Tamanho | Descrição                                                     |
| ----------------------- | ----------------- | ------- | ------- | ------------------------------------------------------------- |
| Categoria               | id                | Inteiro | 11      | Identificador, PK, Auto incrementável                         |
| Categoria               | nome              | Texto   | 100     | Nome da categoria                                             |
| Categoria               | descricao         | Texto   | 255     | Descrição da categoria                                        |
| Fornecedor              | id                | Inteiro | 11      | Identificador, PK, Auto incrementável                         |
| Fornecedor              | razao_social      | Texto   | 150     | Nome oficial da empresa                                       |
| Fornecedor              | nome_fantasia     | Texto   | 150     | Nome comercial da empresa                                     |
| Fornecedor              | cnpj              | Texto   | 18      | Documento da empresa                                          |
| Fornecedor              | telefone          | Texto   | 20      | Número da empresa                                             |
| Fornecedor              | email             | Texto   | 150     | Email da empresa                                              |
| Fornecedor              | endereco          | Texto   | 255     | Localização da empresa                                        |
| Produto                 | id                | Inteiro | 11      | Identificador, PK, Auto incrementável                         |
| Produto                 | nome              | Texto   | 150     | Nome do produto                                               |
| Produto                 | descricao         | Texto   | 255     | Descrição do produto                                          |
| Produto                 | preco             | Decimal | 10,2    | Valor do produto                                              |
| Produto                 | marca             | Texto   | 100     | Marca do produto                                              |
| Produto                 | id_categoria      | Inteiro | 11      | Identificador da categoria, FK referenciando Categoria (id)   |
| Produto                 | id_fornecedor     | Inteiro | 11      | Identificador do fornecedor, FK referenciando Fornecedor (id) |
| Estoque                 | id                | Inteiro | 11      | Identificador, PK, Auto incrementável                         |
| Estoque                 | id_produto        | Inteiro | 11      | Identificador do produto, FK referenciando Produto (id)       |
| Estoque                 | quantidade        | Inteiro | 11      | Quantidade de produto no estoque                              |
| Estoque                 | quantidade_minima | Inteiro | 11      | Quantidade mínima de produtos no estoque                      |
| Estoque                 | localizacao       | Texto   | 100     | Localização do produto na loja                                |
| Movimentacao de Estoque | id_movimentacao   | Inteiro | 11      | Identificador, PK, Auto incrementável                         |
| Movimentacao de Estoque | id_produto        | Inteiro | 11      | Identificador do produto, FK referenciando Produto (id)       |
| Movimentacao de Estoque | tipo              | Enum    | —       | Tipo de movimentação: Entrada ou Saída                        |
| Movimentacao de Estoque | quantidade        | Inteiro | 11      | Quantidade de produtos movimentados                           |
| Movimentacao de Estoque | data              | Data    | —       | Data em que ocorreu a movimentação                            |

## Dados em CSV:
- ![Categoria.csv](./Categoria.csv)
- ![Fornecedor.csv](./estoque.csv)
- ![produto.csv](./produto.csv)
- ![estoque.csv](./estoque.csv)
- ![movimentação.csv](./movimentação.csv)

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

## DDL:

````
CREATE DATABASE IF NOT EXISTS loja_roupas
    CHARACTER SET utf8mb4
    COLLATE utf8mb4_unicode_ci;

USE loja_roupas;

CREATE TABLE categoria (
    id INT(11) AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    descricao VARCHAR(255)
);

CREATE TABLE fornecedor (
    id INT(11) AUTO_INCREMENT PRIMARY KEY,
    razao_social VARCHAR(150) NOT NULL,
    nome_fantasia VARCHAR(150) NOT NULL,
    cnpj VARCHAR(18) NOT NULL UNIQUE,
    telefone VARCHAR(20),
    email VARCHAR(150),
    endereco VARCHAR(255)
);

CREATE TABLE produto (
    id INT(11) AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(150) NOT NULL,
    descricao VARCHAR(255),
    preco DECIMAL(10,2) NOT NULL,
    marca VARCHAR(100),
    id_categoria INT(11) NOT NULL,
    id_fornecedor INT(11) NOT NULL,

    CONSTRAINT fk_produto_categoria
        FOREIGN KEY (id_categoria)
        REFERENCES categoria(id),

    CONSTRAINT fk_produto_fornecedor
        FOREIGN KEY (id_fornecedor)
        REFERENCES fornecedor(id),

    CONSTRAINT chk_produto_preco
        CHECK (preco >= 0)
);

CREATE TABLE estoque (
    id_estoque INT(11) AUTO_INCREMENT PRIMARY KEY,
    id_produto INT(11) NOT NULL UNIQUE,
    quantidade INT(11) NOT NULL DEFAULT 0,
    quantidade_minima INT(11) NOT NULL DEFAULT 0,
    localizacao VARCHAR(100),

    CONSTRAINT fk_estoque_produto
        FOREIGN KEY (id_produto)
        REFERENCES produto(id),

    CONSTRAINT chk_estoque_quantidade
        CHECK (quantidade >= 0),

    CONSTRAINT chk_estoque_quantidade_minima
        CHECK (quantidade_minima >= 0)
);

CREATE TABLE movimentacao_estoque (
    id_movimentacao INT(11) AUTO_INCREMENT PRIMARY KEY,
    id_produto INT(11) NOT NULL,
    tipo ENUM('Entrada', 'Saída') NOT NULL,
    quantidade INT(11) NOT NULL,
    data DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_movimentacao_produto
        FOREIGN KEY (id_produto)
        REFERENCES produto(id),

    CONSTRAINT chk_movimentacao_quantidade
        CHECK (quantidade > 0)
);
```


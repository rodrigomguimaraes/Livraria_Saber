# 📚 Livraria Saber - Implementação e Manipulação de Dados SQL

Este projeto consiste na implementação e manipulação de um banco de dados relacional (`livraria_saber`) utilizando SQL, com foco em comandos DML (Data Manipulation Language). O trabalho integra a modelagem lógica de uma livraria e papelaria com práticas de versionamento e garantia da integridade referencial.

## 🎯 Objetivos
* **Aplicar:** Executar comandos SQL para manipulação de dados em ferramentas reais (MySQL Workbench/PGAdmin).
* **Criar:** Desenvolver scripts SQL completos e estruturados.
* **Integrar:** Combinar modelagem lógica e integridade com DML.

## 🛠️ Tecnologias Utilizadas
* **SGBD:** MySQL (ou compatível)
* **Linguagem:** SQL (Structured Query Language)
* **Ferramentas:** MySQL Workbench, DBeaver ou outro cliente SQL
* **Versionamento:** Git e GitHub

## 📂 Estrutura do Repositório

O banco de dados é formado pelos seguintes arquivos SQL:

| Arquivo | Conteúdo | Observação |
| :--- | :--- | :--- |
| `livraria_saber_schema_full.sql` | Script completo de criação do DB e tabelas. | Contém todos os `CREATE` e `INSERT`. |
| `livraria_saber_autor.sql` | Tabela `autor` | |
| `livraria_saber_cliente.sql` | Tabela `cliente` | |
| `livraria_saber_editora.sql` | Tabela `editora` | |
| `livraria_saber_fornecedor.sql` | Tabela `fornecedor` | |
| `livraria_saber_livro.sql` | Tabela `livro` | Depende de `editora`. |
| `livraria_saber_papelaria.sql` | Tabela `papelaria` | Depende de `fornecedor`. |
| `livraria_saber_vendedor.sql` | Tabela `vendedor` | Necessário criar/incluir. |
| `livraria_saber_venda.sql` | Tabela `venda` | Depende de `cliente` e `vendedor`. |
| `livraria_saber_item_venda.sql` | Tabela `item_venda` | Depende de `venda`, `livro` e `papelaria`. |
| `livraria_saber_dml_exemplos.sql` | Script de manipulação DML. | Contém `SELECT`, `UPDATE` e `DELETE`. |

## ⚙️ Instruções de Execução

1.  **Configuração:** Instale o MySQL Server e um cliente SQL (ex: MySQL Workbench).
2.  **Criação do Banco:**
    ```sql
    CREATE DATABASE livraria_saber;
    USE livraria_saber;
    ```
   
3.  **População das Tabelas:**
    Execute o script `livraria_saber_schema_full.sql` ou os arquivos individuais na seguinte ordem para respeitar as chaves estrangeiras:
    1.  `autor.sql`
    2.  `cliente.sql`
    3.  `editora.sql`
    4.  `fornecedor.sql`
    5.  `vendedor.sql`
    6.  `livro.sql`
    7.  `papelaria.sql`
    8.  `livro_autor.sql`
    9.  `venda.sql`
    10. `item_venda.sql`

## 📝 Exemplos de Manipulação de Dados (DML)

O arquivo `livraria_saber_dml_exemplos.sql` contém os seguintes testes:

### Consultas (SELECT)
```sql
-- Listar títulos de livros e seus autores (JOIN)
SELECT l.titulo, a.nome AS autor_nome FROM livro l
JOIN livro_autor la ON l.id_livro = la.id_livro
JOIN autor a ON la.id_autor = a.id_autor ORDER BY l.titulo;

-- Valor total de vendas por forma de pagamento (GROUP BY)
SELECT forma_pagamento, SUM(valor_total) AS total_por_pagamento
FROM venda GROUP BY forma_pagamento WITH ROLLUP;

-- Cliente com a maior compra
SELECT c.nome, v.valor_total FROM venda v
JOIN cliente c ON v.id_cliente = c.id_cliente
ORDER BY v.valor_total DESC LIMIT 1;

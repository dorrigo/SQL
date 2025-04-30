# Como Utilizar SQL

### Criando um Banco de Dados e Tabela

```sql
CREATE DATABASE nome_do_banco;

CREATE TABLE clientes (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    data_nascimento DATE,
    saldo DECIMAL(10,2) DEFAULT 0,
    ativo BOOLEAN DEFAULT TRUE
);

```

```sql
INSERT INTO clientes (nome, email, data_nascimento)
VALUES 
    ('1', 'Maria Souza', 'maria@email.com', '1985-08-20', 200.30, TRUE),
    ('2','Carlos Oliveira', 'carlos@email.com', '1995-03-10', 123.00, FALSE),
    ('3','Jonatas Silva', 'jonatas@email.com', '1994-05-15', 10.50, FALSE),
    ('4','Sabrina Castro', 'sabrina@email.com', '1990-11-22', 534.25, TRUE),
    ('5','Eduardo Lima', 'eduardo@email.com', '1989-09-01', 55.00, TRUE);
```

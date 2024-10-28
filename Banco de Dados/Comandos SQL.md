SQL (_Structured Query Language_) é a linguagem padrão para manipulação e gerenciamento de bancos de dados relacionais. Ela permite a criação, consulta, modificação e exclusão de dados armazenados. Abaixo estão os principais comandos SQL organizados por categorias.

#### **DDL (Data Definition Language)**

Os comandos DDL são usados para definir a estrutura do banco de dados, como criar ou modificar tabelas e outros objetos.

- **CREATE**: Cria um novo objeto no banco de dados, como uma tabela ou uma view.    
    ```sql
    CREATE TABLE usuarios (
	    id INT PRIMARY KEY,
	    nome VARCHAR(100),
	    email VARCHAR(100) UNIQUE
	);
    ```
    
- **ALTER**: Modifica a estrutura de um objeto existente, como adicionar uma nova coluna a uma tabela.
    ```sql
    ALTER TABLE usuarios ADD idade INT;
    ```
    
- **DROP**: Exclui um objeto do banco de dados permanentemente.
    ```sql
    DROP TABLE usuarios;
    ```
    
- **TRUNCATE**: Remove todos os dados de uma tabela, mas mantém a estrutura da tabela intacta.    
    ```sql
    TRUNCATE TABLE usuarios;
    ```
    

#### **DML (Data Manipulation Language)**
Os comandos DML são usados para manipular os dados em uma tabela. Eles são responsáveis por inserir, atualizar e deletar registros.
- **INSERT**: Insere novos dados em uma tabela.
    ```sql
    INSERT INTO usuarios (id, nome, email)
    VALUES (1, 'Caio Malvezzi', 'caio@example.com');
    ```
    
- **UPDATE**: Atualiza dados existentes em uma tabela.
    ```sql
    UPDATE usuarios
    SET email = 'caio.malvezzi@example.com'
    WHERE id = 1;
    ```
    
- **DELETE**: Remove dados de uma tabela.
    ```sql
    DELETE FROM usuarios WHERE id = 1;
	```
    
#### **DQL (Data Query Language)**

Comandos DQL são usados para realizar consultas e obter dados de uma tabela.

- **SELECT**: Consulta dados de uma ou mais tabelas.    
    ```sql
    SELECT nome, email
    FROM usuarios
    WHERE idade > 25;
    ```
    
- **Aliases**: Cria apelidos temporários para colunas ou tabelas.
    ```sql
    SELECT
	    u.nome AS usuario_nome,
	    u.email AS usuario_email
	FROM usuarios AS u;
	```
    
- **JOINS**: Combina dados de várias tabelas com base em uma condição.
    - **INNER JOIN**: Retorna registros que têm correspondência em ambas as tabelas.
        ```sql
        SELECT
	        u.nome,
		    p.produto
		FROM usuarios u 
		INNER JOIN pedidos p
		ON u.id = p.usuario_id;
		```
        
    - **LEFT JOIN**: Retorna todos os registros da tabela à esquerda e os registros correspondentes da tabela à direita, se existirem.
        ```sql
        SELECT
	        u.nome,
	        p.produto
		FROM usuarios u
		LEFT JOIN pedidos p
		ON u.id = p.usuario_id;
        ```
        
    - **RIGHT JOIN**: Retorna todos os registros da tabela à direita e os registros correspondentes da tabela à esquerda, se existirem.        
        ```sql
        SELECT 
	        u.nome, 
		    p.produto 
		FROM usuarios u 
		RIGHT JOIN pedidos p 
		ON u.id = p.usuario_id;
		```
        
    - **FULL JOIN**: Retorna todos os registros quando há uma correspondência em uma das tabelas ou em ambas.
        ```sql
        SELECT 
	        u.nome, 
	        p.produto 
		FROM usuarios u 
		FULL JOIN pedidos p
		ON u.id = p.usuario_id;
        ```
        

#### **DCL (Data Control Language)**
Comandos DCL são usados para controlar o acesso aos dados no banco de dados.
- **GRANT**: Concede permissões a usuários.
    ```sql
    GRANT SELECT, INSERT ON usuarios TO 'caio';
    ```
    
- **REVOKE**: Remove permissões de usuários.    
    ```sql
    REVOKE INSERT ON usuarios FROM 'caio';
    ```
    

#### **TCL (Transaction Control Language)**
Comandos TCL são usados para gerenciar transações no banco de dados.

- **BEGIN TRANSACTION**: Inicia uma nova transação.    
    ```sql
    BEGIN TRANSACTION;
    ```
    
- **COMMIT**: Confirma a transação e persiste as alterações no banco de dados.
    ```sql
    COMMIT;
    ```
    
- **ROLLBACK**: Reverte uma transação, desfazendo as alterações feitas desde o último `BEGIN TRANSACTION`.
    ```sql
    ROLLBACK;
    ```
    

#### **Funções Agregadas**
As funções agregadas permitem realizar cálculos sobre um conjunto de registros.

- **COUNT**: Retorna o número de registros.    
    ```sql
    SELECT COUNT(*) 
    FROM usuarios;
    ```
    
- **SUM**: Calcula a soma de valores numéricos.    
    ```sql
    SELECT SUM(idade) 
    FROM usuarios;
    ```
    
- **AVG**: Calcula a média de valores numéricos.
    ```sql
    SELECT AVG(idade) 
    FROM usuarios;
    ```
    
- **MAX**: Retorna o maior valor.
    ```sql
    SELECT MAX(idade) 
    FROM usuarios;
    ```
    
- **MIN**: Retorna o menor valor.
    ```sql
    SELECT MIN(idade)
    FROM usuarios;
    ```
    

#### **Subqueries**
Subqueries são consultas aninhadas dentro de outra consulta.
- **Exemplo de Subquery**: Obtém todos os usuários que fizeram pedidos.    
    ```sql
    SELECT nome 
    FROM usuarios 
    WHERE id IN (SELECT usuario_id FROM pedidos);
    ```
    
#### **Views**
Views são consultas salvas que podem ser tratadas como tabelas.
- **CREATE VIEW**: Cria uma view.    
    ```sql
    CREATE VIEW usuarios_ativos AS SELECT nome, email 
    FROM usuarios 
    WHERE status = 'ativo';
    ```
    
- **DROP VIEW**: Exclui uma view.
    ```sql
    DROP VIEW usuarios_ativos;
    ```
    
#### **Index**
Os índices são usados para acelerar as consultas em tabelas.
- **CREATE INDEX**: Cria um índice em uma ou mais colunas de uma tabela.
    ```sql
    CREATE INDEX idx_nome ON usuarios (nome);
    ```
    
- **DROP INDEX**: Exclui um índice.
    ```sql
    DROP INDEX idx_nome;
    ```
    
---

### **Boas Práticas em SQL**

1. **Use JOINs adequadamente**: Evite o uso excessivo de subqueries quando um JOIN bem planejado pode ser mais eficiente.
2. **Limite o uso de SELECT ***: Sempre especifique as colunas que você precisa para evitar a sobrecarga de dados desnecessários.
3. **Use índices com cuidado**: Embora índices acelerem consultas, eles também aumentam o tempo de inserção e atualização de dados.
4. **Normalize suas tabelas**: Aplique normalização para evitar redundância de dados e melhorar a consistência.
5. **Cuidado com o ROLLBACK**: Sempre confirme transações importantes com `COMMIT` para evitar perder dados em um ROLLBACK acidental.
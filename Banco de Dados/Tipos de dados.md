### **Tipos de Dados em Bancos de Dados**
Os **tipos de dados** definem que tipo de valor cada coluna pode armazenar. Abaixo estão os tipos mais comuns, encontrados em bancos de dados como MySQL, PostgreSQL e SQL Server.

#### **Tipos Numéricos**
1. **Inteiros**:
    - **INT**: Armazena números inteiros. Exemplo: `42`, `-15`.
        - Variações: `TINYINT`, `SMALLINT`, `MEDIUMINT`, `BIGINT`.
    - **SMALLINT**: Inteiros menores (geralmente até ±32 mil).
    - **BIGINT**: Inteiros maiores, utilizado para números grandes.
2. **Ponto Flutuante**:
    - **FLOAT**: Armazena números decimais com precisão menor. Exemplo: `3.14`.
    - **DOUBLE**: Armazena números decimais com maior precisão.
3. **Decimais Fixos**:
    - **DECIMAL(precision, scale)**: Armazena números com precisão exata. `precision` define o total de dígitos e `scale` define quantos são após a vírgula. Exemplo: `DECIMAL(10, 2)` armazenaria números como `12345.67`.

#### **Tipos de Texto**
1. **VARCHAR**: Armazena texto de comprimento variável. Você define o limite, por exemplo, `VARCHAR(255)`.
2. **CHAR**: Armazena texto de comprimento fixo. Por exemplo, `CHAR(10)` sempre ocupará 10 caracteres, completando com espaços se necessário.
3. **TEXT**: Armazena grandes quantidades de texto. Dependendo do banco de dados, pode haver variações como `TINYTEXT`, `MEDIUMTEXT` e `LONGTEXT`.

#### **Tipos de Data e Hora**
1. **DATE**: Armazena apenas datas. Exemplo: `2024-10-11`.
2. **TIME**: Armazena apenas o horário. Exemplo: `14:30:00`.
3. **DATETIME**: Armazena tanto a data quanto a hora. Exemplo: `2024-10-11 14:30:00`.
4. **TIMESTAMP**: Similar ao `DATETIME`, mas também inclui informações sobre fusos horários. Exemplo: `2024-10-11 14:30:00`.
5. **YEAR**: Armazena apenas o ano. Exemplo: `2024`.

#### **Tipos Booleanos**
- **BOOLEAN** ou **BOOL**: Armazena valores de `true` (1) ou `false` (0).

#### **Tipos Binários**
1. **BLOB (Binary Large Object)**: Armazena grandes quantidades de dados binários, como imagens ou arquivos.
    - Variações: `TINYBLOB`, `BLOB`, `MEDIUMBLOB`, `LONGBLOB` (dependendo do tamanho).

---
### **Primary Key (PK) – Chave Primária**
A **Chave Primária** (Primary Key) é uma coluna (ou conjunto de colunas) que **identifica exclusivamente** cada registro em uma tabela. Ela deve seguir algumas regras:
1. **Única**: O valor da chave primária deve ser único para cada registro. Não pode haver dois registros com o mesmo valor na coluna da chave primária.
2. **Não Nulo**: Uma chave primária não pode ter valor nulo (`NULL`), já que ela deve identificar exclusivamente um registro.

**Exemplo**:
```sql
CREATE TABLE Cliente (
	id_cliente INT PRIMARY KEY, -- Chave primária
	nome_cliente VARCHAR(100),
	email_cliente VARCHAR(100)
);
```

No exemplo acima, `id_cliente` é a chave primária, o que significa que cada cliente terá um identificador único.

---

### **Foreign Key (FK) – Chave Estrangeira**
A **Chave Estrangeira** (Foreign Key) é uma coluna (ou conjunto de colunas) que cria um **relacionamento** entre duas tabelas, referenciando a chave primária de outra tabela. Sua função é **garantir a integridade referencial** no banco de dados, o que significa que uma linha com uma chave estrangeira só pode existir se a linha correspondente na outra tabela existir.

1. **Referência**: A chave estrangeira deve referenciar uma chave primária de outra tabela.
2. **Integridade**: Ela garante que não haja registros "soltos". Ou seja, se uma tabela depende de outra, um registro que tenha uma chave estrangeira não pode existir sem uma referência válida.

**Exemplo**:

```sql
CREATE TABLE Pedido (
	id_pedido INT PRIMARY KEY, -- Chave Primária da tabela Pedido
	data_pedido DATE,
	id_cliente INT, -- Chave Estrangeira que referencia a tabela Cliente
	FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente)
);
```

No exemplo acima:

- A tabela `Pedido` tem uma chave estrangeira `id_cliente`, que faz referência à coluna `id_cliente` da tabela `Cliente`.
- Isso significa que um pedido só pode existir se houver um cliente correspondente na tabela `Cliente`.

---

### **Exemplo de Relacionamento**

Aqui está um exemplo prático de como uma **Chave Primária** e uma **Chave Estrangeira** funcionam juntas:

1. **Tabela Cliente**:    
    ```sql
    CREATE TABLE Cliente (
	    id_cliente INT PRIMARY KEY,
	    nome_cliente VARCHAR(100),
	    email_cliente VARCHAR(100)
	);
    ```
    
2. **Tabela Pedido**:    
    ```sql
    CREATE TABLE Pedido (
	    id_pedido INT PRIMARY KEY,
	    data_pedido DATE,
	    id_cliente INT,
	    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente)
	);
	```
    
Neste caso, o `id_cliente` é a **Primary Key** na tabela `Cliente` e uma **Foreign Key** na tabela `Pedido`. Isso garante que cada pedido está associado a um cliente existente, e nenhum pedido pode ser inserido sem um cliente correspondente.

---

### **Resumo dos Conceitos**
- **Tipos de Dados**:
    - **Numéricos**: INT, FLOAT, DECIMAL.
    - **Texto**: VARCHAR, CHAR, TEXT.
    - **Data e Hora**: DATE, TIME, DATETIME.
    - **Booleanos**: BOOLEAN.
    - **Binários**: BLOB.
- **Chave Primária (Primary Key)**:
    - Identifica unicamente um registro na tabela.
    - Deve ser única e não nula.
- **Chave Estrangeira (Foreign Key)**:
    - Cria um relacionamento entre duas tabelas.
    - Referencia a chave primária de outra tabela.
    - Garante a integridade referencial.

### **Restrições em SQL**

As restrições (ou **constraints**) são regras que definimos nas colunas das tabelas para garantir a integridade dos dados. Aqui estão as mais comuns:

1. **NOT NULL**: Garante que a coluna não aceite valores nulos.
2. **UNIQUE**: Garante que todos os valores na coluna sejam únicos.
3. **DEFAULT**: Define um valor padrão para a coluna quando nenhum valor é especificado.
4. **CHECK**: Define uma condição que os valores na coluna devem atender.
5. **AUTO_INCREMENT** (ou **SERIAL** no PostgreSQL): Faz com que o valor da coluna seja gerado automaticamente, normalmente utilizado para chaves primárias.

### **Exemplo Completo de Criação de Tabela com Restrições**
Aqui vai um exemplo de como criar uma tabela utilizando várias dessas restrições.

#### **Tabela Cliente**

```sql
	CREATE TABLE Cliente (
		id_cliente INT AUTO_INCREMENT PRIMARY KEY,  -- Chave Primária com auto-incremento
		nome_cliente VARCHAR(100) NOT NULL,         -- Não pode ser nulo 
		email_cliente VARCHAR(100) NOT NULL UNIQUE, -- Deve ser único
		data_cadastro DATE NOT NULL DEFAULT CURRENT_DATE,  -- Valor padrão é a data atual
		telefone_cliente VARCHAR(15),               -- Pode ser nulo (não tem NOT NULL)
		CHECK (LENGTH(telefone_cliente) >= 8)       -- Checa que o telefone tem pelo menos 8 caracteres
);```
- **id_cliente**: Esta coluna é a **Primary Key**, com **AUTO_INCREMENT**, ou seja, o valor será incrementado automaticamente à medida que novos registros forem adicionados.
- **nome_cliente**: Esta coluna tem a restrição **NOT NULL**, o que significa que não pode haver registros sem o nome do cliente.
- **email_cliente**: Além de **NOT NULL**, também tem a restrição **UNIQUE**, ou seja, cada email registrado precisa ser único.
- **data_cadastro**: Usa a restrição **DEFAULT**, que define um valor padrão se nenhum valor for fornecido. Neste caso, a data de cadastro será automaticamente definida como a data atual.
- **telefone_cliente**: Não tem a restrição **NOT NULL**, portanto, pode aceitar valores nulos. A coluna também possui uma condição de **CHECK**, que garante que, se houver um telefone informado, ele terá pelo menos 8 caracteres.

#### **Tabela Pedido com Foreign Key**
```sql
	CREATE TABLE Pedido (
		id_pedido INT AUTO_INCREMENT PRIMARY KEY,  -- Chave Primária com auto-incremento
		data_pedido DATE NOT NULL DEFAULT CURRENT_DATE,  -- Data padrão é a atual
		valor_total DECIMAL(10, 2) NOT NULL,  -- Valor total do pedido, não pode ser nulo
		id_cliente INT NOT NULL,  -- Chave estrangeira para a tabela Cliente 
		FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente)  -- Definindo a chave estrangeira
	);```

- **id_pedido**: Assim como na tabela Cliente, essa coluna é uma chave primária com **AUTO_INCREMENT**.
- **data_pedido**: Armazena a data do pedido, com **NOT NULL** e o valor padrão sendo a data atual.
- **valor_total**: Deve ser um valor decimal (com até 10 dígitos no total e 2 casas decimais) e não pode ser nulo (**NOT NULL**).
- **id_cliente**: Esta coluna é uma **Foreign Key** que referencia a tabela `Cliente`. Ela não pode ser nula porque um pedido precisa sempre estar vinculado a um cliente.

### **Exemplo de Inserção de Dados**
Agora que criamos as tabelas com suas restrições, aqui estão exemplos de como inserir dados nelas:

```sql
-- Inserindo um cliente na tabela Cliente
	INSERT INTO Cliente (
		nome_cliente,
		email_cliente,
		telefone_cliente
	) VALUES (
		'João Silva',
		'joao.silva@email.com',
		'11987654321');  -- Inserindo um pedido na tabela Pedido, referenciando o id_cliente do cliente que acabamos de inserir
	INSERT INTO Pedido (
		valor_total,
		id_cliente
	) VALUES (150.00, 1);
```

- Na tabela **Cliente**, o campo `id_cliente` será automaticamente incrementado. O `data_cadastro` será definido automaticamente como a data atual, já que não especificamos um valor para ele.
- Na tabela **Pedido**, o `id_cliente` do cliente que fizemos o pedido é `1`, porque esse foi o valor gerado automaticamente na tabela `Cliente`.

### **Resumo Final**

- **NOT NULL**: Garante que a coluna não aceite valores nulos.
- **UNIQUE**: Garante que todos os valores na coluna sejam únicos.
- **DEFAULT**: Define um valor padrão quando nenhum é fornecido.
- **CHECK**: Define uma condição que os valores na coluna devem atender.
- **AUTO_INCREMENT**: Faz com que os valores da coluna sejam gerados automaticamente.
- **PRIMARY KEY**: Identifica unicamente um registro em uma tabela.
- **FOREIGN KEY**: Cria um relacionamento entre duas tabelas, referenciando a chave primária de outra tabela.
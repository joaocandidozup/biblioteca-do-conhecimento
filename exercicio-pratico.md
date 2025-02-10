## Exercício Prático: Manipulação de Tabelas e Filtragem no PostgreSQL
Cenário: Você foi contratado por uma empresa fictícia chamada TechCorp para gerenciar o banco de dados de seus funcionários e projetos.
Sua tarefa é criar e manipular tabelas no PostgreSQL para organizar as informações da empresa.
### Passo 1: Criar o Banco de Dados

Crie um banco de dados chamado techcorp
````sql
CREATE DATABASE techcorp;
````
Acesse o banco de dados
````sql
\c techcorp
````
Criar um novo usuario
````sql
CREATE USER nome_do_usuario WITH PASSWORD 'senha_segura'; 
````
Conceder permissão para o usuario criar tabelas
````sql
GRANT CREATE ON SCHEMA public TO nome_do_usuario;
````
Garantir que o usuário possa se conectar ao banco de dados
````sql
GRANT CONNECT ON DATABASE techcorp TO nome_do_usuario;
````
Acessar o banco de dados com o novo usuario
```sql
\c techcorp nome_do_usuario;
````

### Passo 2: Criar as Tabelas
Crie uma tabela chamada funcionarios com as seguintes colunas:
id (chave primária, numeração automática)<br>
nome (nome do funcionário, texto com até 50 caracteres)<br>
cargo (cargo do funcionário, texto com até 50 caracteres)<br>
salario (salário do funcionário, número com duas casas decimais)<br>
data_admissao (data de admissão do funcionário)
```sql
CREATE TABLE funcionarios(
id SERIAL PRIMARY KEY,
nome VARCHAR(50),
cargo VARCHAR(50),
salario DECIMAL (10,2),
data_admisao DATE);

````
Crie uma tabela chamada projetos com as seguintes colunas:
id (chave primária, numeração automática)<br>
nome_projeto (nome do projeto, texto com até 100 caracteres)<br>
id_funcionario (chave estrangeira que referencia o id da tabela funcionarios)<br>
data_inicio (data de início do projeto)<br>
data_fim (data de término do projeto)

````sql
CREATE TABLE projetos (
id SERIAL PRIMARY KEY,
nome_projeto VARCHAR(100),
id_funcionario INT, data_inicio DATE,
data_fim DATE,
FOREIGN KEY (id_funcionario) REFERENCES funcionarios(id));
````
listar as tabelas
````sql
\dt
````
listar todos os usuarios
```sql
\du
````
### Passo 3: Inserir Dados
Insira os seguintes funcionários na tabela funcionarios:
    ('João Silva', 'Analista', 3500.00, '2023-01-15'),<br>
    ('Maria Oliveira', 'Gerente', 7500.00, '2022-05-10'),<br>
    ('Carlos Santos', 'Desenvolvedor', 4500.00, '2023-03-01'),<br>
    ('Ana Costa', 'Desenvolvedor', 4000.00, '2023-02-20'),<br>
    ('Pedro Lima', 'Estagiário', 1500.00, '2023-04-01');

```sql
INSERT INTO funcionarios(nome,cargo,salario,data_admisao)
VALUES('Maria Oliveira', 'Gerente', 7500.00, '2022-05-10'),
('Carlos Santos', 'Desenvolvedor', 4500.00, '2023-03-01'),
('Ana Costa', 'Desenvolvedor', 4000.00, '2023-02-20'),
('Pedro Lima', 'Estagiário', 1500.00, '2023-04-01');

````

Insira os seguintes projetos na tabela projetos:
    ('Sistema de Gestão', 1, '2023-02-01', '2023-06-30'),<br>
    ('E-commerce', 3, '2023-03-15', '2023-09-15'),<br>
    ('Aplicativo Mobile', 4, '2023-04-01', '2023-12-31'),<br>
    ('Relatório Financeiro', 2, '2023-01-01', '2023-05-31');

  ```sql
    INSERT INTO projetos(nome_projeto,id_funcionario,data_inicio,data_fim)
     VALUES ('Sistema de Gestão', 1, '2023-02-01', '2023-06-30'),
    ('E-commerce', 3, '2023-03-15', '2023-09-15'),
    ('Aplicativo Mobile', 4, '2023-04-01', '2023-12-31'),
    ('Relatório Financeiro', 2, '2023-01-01', '2023-05-31');

  ```
### Passo 4: Consultas e Filtragem
Agora, para cada pergunta abaixo, escreva a query correspondente e execute no PostgreSQL.
- Exibir todos os funcionários e seus respectivos cargos.
  
  ```sql
   SELECT nome,cargo FROM funcionarios;

  ````
- Filtrar os funcionários com salário maior que R$ 4.000,00.
  
  ````sql
  SELECT nome,cargo,salario FROM funcionarios Where SALARIO > 4000.00;
  ````
- Exibir os projetos que terminam após 30/06/2023.
  
  ````sql
  SELECT nome_projeto, data_fim FROM projetos  WHERE data_fim > '2023-06-30';

  ````
- Listar os funcionários que possuem o cargo de "Desenvolvedor" e salário maior ou igual a R$ 4.000,00.

  ````sql
   SELECT nome, cargo, salario FROM funcionarios WHERE cargo = 'Desenvolvedor' AND salario >= 4000.00;

  ````
- Exibir os funcionários que foram admitidos antes de 01/03/2023.
```sql
SELECT nome, cargo, data_admisao FROM funcionarios WHERE data_admisao < '2023-03-01';

````
  ### Passo 5: Atualizar e Deletar Dados
- Atualize o salário do funcionário "Ana Costa" para R$ 4.500,00

  ````sql
  UPDATE funcionarios SET salario = 4500.00  WHERE nome = 'Ana Costa';

  ````
- Delete o projeto "Relatório Financeiro".

  ````sql
  DELETE FROM projetos WHERE nome_projeto = 'Relatório Financeiro';
  ````

Desafio Extra
- Liste os funcionários que possuem salário entre R$ 3.000,00 e R$ 5.000,00

  ````sql
  SELECT nome, cargo, salario
  FROM funcionarios
  WHERE salario BETWEEN 3000.00 AND 5000.00;
  
  ````
- Exiba o tempo total (em dias) de cada projeto

  ````sql
  SELECT nome_projeto,
  (data_fim - data_inicio) AS tempo_total_em_dias
  FROM projetos;

  ````

















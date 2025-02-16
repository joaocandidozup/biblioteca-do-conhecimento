## Exercício Prático: Imagine que você está criando um banco de dados para uma escola de música. Siga os passos abaixo:
Identifique as entidades principais (exemplo: Alunos, Professores, Aulas).<br>
Liste os atributos de cada entidade.<br>
Defina os relacionamentos entre as entidades.<br>
Crie o modelo lógico e implemente as tabelas no PostgreSQL.<br>
Dica: Pense em perguntas como:<br>
O que precisamos saber sobre os alunos?<br>
Como registramos as aulas?<br>
Como conectamos os professores às aulas?
----

### Passo 1: Identificar as Entidades Principais
As entidades principais para um banco de dados de uma escola de música podem ser:
- alunos
- Professores
- Aulas
- Instrumentos

### Passo 2: Listar os Atributos de Cada Entidade
Alunos
````yml
nome: (nome completo do aluno)
data de nascimento: (data de nascimento do aluno)
email: (e-mail do aluno)
telefone: (telefone de contato do aluno)
````
Professores
````yml
nome: (nome completo do professor)
especialidade: (instrumento ou área de especialização)
email: (e-mail do professor)
telefone: (telefone de contato do professor)
````
Aulas
````yml
data e hora: (data e hora da aula)
duracao: (duração da aula em minutos)
````
Instrumentos
````yml
nome: (nome do instrumento)
````
### Passo 3: Definir os Relacionamentos Entre as Entidades
````yml
Alunos e Instrumentos: Um aluno pode aprender varios instrumentos e um instrumento pode ser aprendido por vários alunos. 
(Relacionamento N:N)

Professores e Aulas: Um professor pode ministrar várias aulas, mas cada aula é ministrada por apenas um professor.
(Relacionamento 1:N)

Alunos e Aulas: Um aluno pode participar de várias aulas, mas cada aula é associada a apenas um aluno.
(Relacionamento 1:N)
````
### Passo 4: Criar o Modelo Lógico
Alunos
````yml
id (chave primária)
nome 
data_nascimento 
email 
telefone 
instrumento_id (chave estrangeira)
````
Professores
````yml
id (chave primária)
nome 
especialidade 
email 
telefone 

````
Aulas
````yml
id (chave primária)
data_hora 
duracao 
professor_id (chave estrangeira )
aluno_id (chave estrangeira )
````
Instrumentos
````yml
id (chave primária)
nome 
````
Alunos_Instrumentos (tabela intermediaria para o relacionamento N:N)

### Passo 5: Criar o Banco de Dados

Crie um banco de dados chamado techcorp
````sql
CREATE DATABASE escola_de_musica;
````
Acesse o banco de dados
````sql
\c escola_de_musica;
````

### Passo 6: Criar um novo usuario
verificar todos os usuarios existentes
````sql
\du
````
Criar um novo usuario
```sql
CREATE USER usuario1 WITH PASSWORD '123';
````
Conceder permissão para o usuario criar tabelas
````sql
GRANT CREATE ON SCHEMA public TO usuario1;
````
Garantir que o usuário possa se conectar ao banco de dados
````sql
GRANT CONNECT ON DATABASE escola_de_musica TO usuario1;
````
Acessar o banco de dados com o novo usuario
```sql
\c escola_de_musica usuario1;
````
### Passo 7: Implementar as Tabelas no PostgreSQL
Tabela de Instrumentos
````sql
CREATE TABLE instrumentos (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(50) NOT NULL
);

````
Tabela de Alunos
````sql
CREATE TABLE alunos (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    data_nascimento DATE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    telefone VARCHAR(15),
    instrumento_id INT REFERENCES instrumentos(id)
);
````
 Tabela de Professores
````sql
CREATE TABLE professores (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    especialidade VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    telefone VARCHAR(15)
);

````
Tabela de Aulas
```sql
CREATE TABLE aulas (
    id SERIAL PRIMARY KEY,
    data_hora TIMESTAMP NOT NULL,
    duracao INT NOT NULL,
    professor_id INT REFERENCES professores(id),
    aluno_id INT REFERENCES alunos(id)
);

````
 Tabela intermediária para o relacionamento N:N entre Alunos e Instrumentos  
 
````sql
CREATE TABLE alunos_instrumentos (
   aluno_id INT NOT NULL REFERENCES alunos(id),
   instrumento_id INT NOT NULL REFERENCES instrumentos(id),
   PRIMARY KEY (aluno_id, instrumento_id)
);
````
### Passo 8: Inserindo Dados nas Tabelas
Inserindo dados na tabela de Instrumentos
````sql
INSERT INTO instrumentos (nome) VALUES 
('Violão'),
('Piano'),
('Bateria'),
('Guitarra'),
('Flauta');
````
Inserindo dados na tabela de Alunos
````sql
INSERT INTO alunos (nome, data_nascimento, email, telefone, instrumento_id) VALUES 
('João Silva', '2005-03-15', 'joao.silva@email.com', '11999999999', 1),
('Maria Oliveira', '2007-07-22', 'maria.oliveira@email.com', '11988888888', 2),
('Carlos Santos', '2006-11-10', 'carlos.santos@email.com', '11977777777', 3),
('Ana Costa', '2008-01-05', 'ana.costa@email.com', '11966666666', 4);
````
Inserindo dados na tabela de Professores
````sql
INSERT INTO professores (nome, especialidade, email, telefone) VALUES 
('Pedro Almeida', 'Cordas', 'pedro.almeida@email.com', '11955555555'),
('Fernanda Lima', 'Teclas', 'fernanda.lima@email.com', '11944444444'),
('Rafael Souza', 'Percussão', 'rafael.souza@email.com', '11933333333');
````
Inserindo dados na tabela de Aulas
````sql
INSERT INTO aulas (data_hora, duracao, professor_id, aluno_id) VALUES 
('2023-10-15 10:00:00', 60, 1, 1),
('2023-10-16 14:00:00', 45, 2, 2),
('2023-10-17 16:00:00', 90, 3, 3),
('2023-10-18 09:00:00', 60, 1, 4);
````
Inserindo dados na tabela intermediária Alunos_Instrumentos
````sql
INSERT INTO alunos_instrumentos (aluno_id, instrumento_id) VALUES 
(1, 1),
(2, 2), 
(3, 3), 
(4, 4), 
(1, 3), 
(2, 4); 
````
## Exemplos de Consultas ao Banco de Dados

Quais alunos estão aprendendo piano?
````sql
SELECT a.nome 
FROM alunos a
JOIN instrumentos i ON a.instrumento_id = i.id
WHERE i.nome = 'Piano';

````
Quais aulas um professor específico está ministrando?
````sql
SELECT a.data_hora, a.duracao, al.nome AS aluno
FROM aulas a
JOIN professores p ON a.professor_id = p.id
JOIN alunos al ON a.aluno_id = al.id
WHERE p.nome = 'Pedro Almeida';
````
 Quantos alunos estão aprendendo cada instrumento?
 ````sql
SELECT i.nome AS instrumento, COUNT(a.id) AS total_alunos
FROM instrumentos i
LEFT JOIN alunos a ON i.id = a.instrumento_id
GROUP BY i.nome;

````
 Quais são os contatos dos professores?
 ````sql
SELECT nome, email, telefone 
FROM professores;

````

  

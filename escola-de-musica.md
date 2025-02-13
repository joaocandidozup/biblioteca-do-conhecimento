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
data_nascimento: (data de nascimento)
email: (e-mail do aluno)
telefone: (telefone de contato)
````
Professores
````yml
nome: (nome completo do professor)
especialidade: (instrumento ou área de especialização)
email: (e-mail do professor)
telefone: (telefone de contato)
````
Aulas
````yml
data_hora: (data e hora da aula)
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


  

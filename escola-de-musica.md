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
id: (chave primária)
nome: (nome completo do aluno)
data_nascimento: (data de nascimento)
email: (e-mail do aluno)
telefone: (telefone de contato)
instrumento_id: (instrumento que o aluno está aprendendo, chave estrangeira)
````
Professores
````yml
id: (chave primária)
nome: (nome completo do professor)
especialidade: (instrumento ou área de especialização)
email: (e-mail do professor)
telefone: (telefone de contato)
````
Aulas
````yml
id: (chave primária)
data_hora: (data e hora da aula)
duracao: (duração da aula em minutos)
professor_id: (chave estrangeira para o professor que ministra a aula)
aluno_id: (chave estrangeira para o aluno que participa da aula)
````
Instrumentos
````yml
id: (chave primária)
nome: (nome do instrumento)
````


  

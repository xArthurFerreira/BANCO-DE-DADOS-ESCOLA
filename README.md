# PROVA-BANCO-DE-DADOS


Uma disciplina pode ter várias notas, mas uma nota está associada a apenas uma disciplina.
Este modelo de banco de dados reflete e espelha a estrutura de um cenário escolar, permitindo uma adaptação fácil para diferentes contextos educacionais. Ele fornece uma base  para o gerenciamento  de informações acadêmicas, independentemente dos detalhes específicos de cada instituição.


Relacionamentos:

Aluno - Turma (1:N):
Um aluno pode pertencer a várias turmas, mas uma turma pertence a apenas um aluno.

Professor - Turma (1:N):
Um professor pode lecionar várias turmas, mas uma turma é lecionada por apenas um professor.

Disciplina - Turma (1:N):
Uma disciplina pode pertencer a várias turmas, mas uma turma está associada a apenas uma disciplina.

Aluno - Nota (1:N):
Um aluno pode ter várias notas, mas uma nota pertence a apenas um aluno.

Disciplina - Nota (1:N):
Uma disciplina pode ter várias notas, mas uma nota está associada a apenas uma disciplina.



# Modelagem física:

Tabela: Aluno
Matricula (PK, int)
Nome (varchar)
DataNascimento (date)
Endereco (varchar)
Telefone (varchar)
Email (varchar)
Atributos Compostos:
Nome (Composto: PrimeiroNome, Sobrenome)
Tabela: Professor

Professores:
IDProfessor (PK, int)
Nome (varchar)
DataNascimento (date)
Endereco (varchar)
Telefone (varchar)
Email (varchar)
Especialidade (varchar)
Atributos Compostos:
Nome (Composto: PrimeiroNome, Sobrenome)
Tabela: Disciplina

Disciplina:
CodigoDisciplina (PK, int)
Nome (varchar)
CargaHoraria (int)
Sala (varchar)
Tabela: Turma

Turma:
CodigoTurma (PK, int)
AnoLetivo (int)
Periodo (varchar)
CodigoDisciplina (FK, int, referenciando CodigoDisciplina)
IDProfessor (FK, int, referenciando IDProfessor)
Atributos Multivalorados:
AlunosMatriculas (Multivalorado: Lista de Matriculas de Aluno)
Tabela: Nota

Nota:
IDNota (PK, int)
Matricula (FK, int, referenciando Matricula de Aluno)
CodigoDisciplina (FK, int, referenciando CodigoDisciplina)
Valor (decimal)
DataLancamento (date)
Atributo Derivado:
Status (Derivado: Calculado com base no Valor)

# Modelo-Lógico:
![BANCO DE DADOS ESCOLA](https://github.com/xArthurFerreira/BANCO-DE-DADOS-ESCOLA/assets/141787340/c79fd31f-e4b8-4833-89fc-03fcc4b5e249)


# Modelo-Conceitual: 
![Diagrama em branco](https://github.com/xArthurFerreira/BANCO-DE-DADOS-ESCOLA/assets/141787340/2dd25b57-412a-447c-b13e-527e30eb9a1c)


# Criação-Tabelas: 
-- Criação da tabela Aluno
CREATE TABLE Aluno (
    ID INT PRIMARY KEY,
    Nome VARCHAR(255),
    DataNascimento DATE,
    Endereco VARCHAR(255),
    Telefone VARCHAR(15),
    Email VARCHAR(255)
);

-- Criação da tabela Professor
CREATE TABLE Professor (
    ID INT PRIMARY KEY,
    Nome VARCHAR(255),
    DataNascimento DATE,
    Endereco VARCHAR(255),
    Telefone VARCHAR(15),
    Email VARCHAR(255),
    Especialidade VARCHAR(255)
);

-- Criação da tabela Disciplina
CREATE TABLE Disciplina (
    ID INT PRIMARY KEY,
    Nome VARCHAR(255),
    CargaHoraria INT,
    Sala VARCHAR(255)
);

-- Criação da tabela Turma
CREATE TABLE Turma (
    ID INT PRIMARY KEY,
    AnoLetivo INT,
    Periodo VARCHAR(50),
    IDDisciplina INT FOREIGN KEY REFERENCES Disciplina(ID),
    IDProfessor INT FOREIGN KEY REFERENCES Professor(ID)
);

-- Criação da tabela Nota
CREATE TABLE Nota (
    ID INT PRIMARY KEY,
    IDAluno INT FOREIGN KEY REFERENCES Aluno(ID),
    IDDisciplina INT FOREIGN KEY REFERENCES Disciplina(ID),
    Valor DECIMAL(5, 2),
    DataLancamento DATE,
    Status AS CASE WHEN Valor >= 5.0 THEN 'Aprovado' ELSE 'Reprovado' END
);







# Inserção de dados na tabela Aluno
-- Inserção de dados na tabela Aluno
INSERT INTO Aluno (ID, Nome, DataNascimento, Endereco, Telefone, Email)
VALUES
    (1, 'João', '1990-05-15', 'Rua A, 123', '123456789', 'joao@email.com'),
    
    (2, 'Maria', '1988-08-21', 'Rua B, 456', '987654321', 'maria@email.com'),

    (3, 'Ana Souza', '1992-02-28', 'Rua E, 789', '555666777', 'ana_souza@email.com'),
    
    (4, 'Pedro Santos', '1995-09-10', 'Rua F, 456', '888999000', 'pedro@email.com'),
    
    (5, 'Mariana Lima', '1993-07-15', 'Rua G, 321', '111222333', 'mariana@email.com'),
    
    (6, 'Lucas Oliveira', '1994-11-20', 'Rua H, 654', '444555666', 'lucas@email.com'),
    
    (7, 'Beatriz Silva', '1991-04-05', 'Rua I, 987', '777888999', 'beatriz@email.com'),
    
    (8, 'Rafaela Pereira', '1990-12-18', 'Rua J, 111', '222333444', 'rafaela@email.com'),
    
    (9, 'Roberto Santos', '1993-06-25', 'Rua K, 222', '999000111', 'roberto@email.com'),
    
    (10, 'Fernanda Lima', '1989-08-30', 'Rua L, 333', '333444555', 'fernanda@email.com'),
    
    (11, 'Gustavo Oliveira', '1992-03-12', 'Rua M, 444', '666777888', 'gustavo@email.com'),
    
    (12, 'Patrícia Souza', '1988-01-22', 'Rua N, 555', '222333444', 'patricia@email.com'),
    
    (13, 'Anderson Pereira', '1994-07-08', 'Rua O, 666', '999000111', 'anderson@email.com'),
    
    (14, 'Camila Lima', '1991-09-19', 'Rua P, 777', '444555666', 'camila@email.com'),
    
    (15, 'Vinícius Santos', '1987-05-14', 'Rua Q, 888', '777888999', 'vinicius@email.com'),
    
    (16, 'Isabela Oliveira', '1996-12-01', 'Rua R, 999', '111222333', 'isabela@email.com'),
    
    (17, 'Felipe Souza', '1990-10-28', 'Rua S, 1010', '555666777', 'felipe@email.com'),
    
    (18, 'Larissa Lima', '1989-04-02', 'Rua T, 1111', '888999000', 'larissa@email.com'),
    
    (19, 'Bruno Santos', '1993-06-07', 'Rua U, 1212', '111222333', 'bruno@email.com'),
    
    (20, 'Carolina Oliveira', '1995-08-15', 'Rua V, 1313', '444555666', 'carolina@email.com');
    
    
![image](https://github.com/xArthurFerreira/BANCO-DE-DADOS-ESCOLA/assets/141787340/ee79dc53-6a02-40a4-9fa6-0628bc3ba937)




# Inserção de dados na tabela Professor
INSERT INTO Professor (ID, Nome, DataNascimento, Endereco, Telefone, Email, Especialidade)
VALUES
    (1, 'Carlos Santos', '1975-03-10', 'Rua C, 789', '111222333', 'carlos@email.com', 'Matemática'),
    
    (2, 'Ana Lima', '1982-11-05', 'Rua D, 101', '444555666', 'ana@email.com', 'História'),
    
    (3, 'Fernando Silva', '1980-08-15', 'Rua E, 222', '555666777', 'fernando@email.com', 'Física'),
    
    (4, 'Patrícia Oliveira', '1978-04-25', 'Rua F, 333', '888999000', 'patricia@email.com', 'Química'),
    
    (5, 'Roberto Lima', '1985-12-30', 'Rua G, 444', '111222333', 'roberto@email.com', 'Biologia'),
    
    (6, 'Mariana Santos', '1979-07-05', 'Rua H, 555', '444555666', 'mariana@email.com', 'Geografia'),
    
    (7, 'Gustavo Oliveira', '1982-03-12', 'Rua I, 666', '777888999', 'gustavo@email.com', 'Artes'),
    
    (8, 'Carla Lima', '1981-11-18', 'Rua J, 777', '222333444', 'carla@email.com', 'Educação Física'),
    
    (9, 'Lucas Souza', '1984-06-25', 'Rua K, 888', '999000111', 'lucas@email.com', 'Inglês'),
    
    (10, 'Bianca Santos', '1989-08-30', 'Rua L, 999', '333444555', 'bianca@email.com', 'História da Arte'),
    
    (11, 'Ricardo Lima', '1987-03-12', 'Rua M, 1010', '666777888', 'ricardo@email.com', 'Espanhol'),
    
    (12, 'Cristina Oliveira', '1978-01-22', 'Rua N, 1111', '222333444', 'cristina@email.com', 'Matemática Financeira'),
    
    (13, 'Alexandre Pereira', '1984-07-08', 'Rua O, 1212', '999000111', 'alexandre@email.com', 'Filosofia'),
    
    (14, 'Camila Lima', '1981-09-19', 'Rua P, 1313', '444555666', 'camila@email.com', 'Sociologia'),
    
    (15, 'Vinícius Santos', '1977-05-14', 'Rua Q, 1414', '777888999', 'vinicius@email.com', 'Literatura'),
    
    (16, 'Isabela Oliveira', '1986-12-01', 'Rua R, 1515', '111222333', 'isabela@email.com', 'Química Orgânica'),
    
    (17, 'Felipe Souza', '1980-10-28', 'Rua S, 1616', '555666777', 'felipe@email.com', 'Economia'),
    
    (18, 'Larissa Lima', '1979-04-02', 'Rua T, 1717', '888999000', 'larissa@email.com', 'Psicologia'),
    
    (19, 'Bruno Santos', '1983-06-07', 'Rua U, 1818', '111222333', 'bruno@email.com', 'Marketing'),
    
    (20, 'Carolina Oliveira', '1985-08-15', 'Rua V, 1919', '444555666', 'carolina@email.com', 'Comunicação Social');

![image](https://github.com/xArthurFerreira/BANCO-DE-DADOS-ESCOLA/assets/141787340/1de46e1d-2d85-4156-8e59-02658bb804c4)




# Inserção de dados na tabela Disciplina
    -- Inserção de dados na tabela Disciplina
INSERT INTO Disciplina (ID, Nome, CargaHoraria, Sala)
VALUES
    (1, 'Matemática', 60, 'Sala 101'),
    (2, 'História', 45, 'Sala 202'),
    (3, 'Física', 50, 'Sala 303'),
    (4, 'Química', 55, 'Sala 404'),
    (5, 'Biologia', 40, 'Sala 505'),
    (6, 'Geografia', 60, 'Sala 606'),
    (7, 'Artes', 30, 'Sala 707'),
    (8, 'Educação Física', 40, 'Sala 808'),
    (9, 'Inglês', 45, 'Sala 909'),
    (10, 'História da Arte', 35, 'Sala 1010'),
    (11, 'Espanhol', 40, 'Sala 1111'),
    (12, 'Matemática Financeira', 50, 'Sala 1212'),
    (13, 'Filosofia', 30, 'Sala 1313'),
    (14, 'Sociologia', 30, 'Sala 1414'),
    (15, 'Literatura', 40, 'Sala 1515'),
    (16, 'Química Orgânica', 55, 'Sala 1616'),
    (17, 'Economia', 45, 'Sala 1717'),
    (18, 'Psicologia', 35, 'Sala 1818'),
    (19, 'Marketing', 40, 'Sala 1919'),
    (20, 'Comunicação Social', 50, 'Sala 2020');

![image](https://github.com/xArthurFerreira/BANCO-DE-DADOS-ESCOLA/assets/141787340/c655c9a8-cb43-49e6-9910-7f86bf0228ce)




# Inserção de dados na tabela Turma
    -- Inserção de dados na tabela Turma
INSERT INTO Turma (ID, AnoLetivo, Periodo, IDDisciplina, IDProfessor)
VALUES
    (1, 2022, 'Semestre 1', 1, 1),
    (2, 2022, 'Semestre 1', 2, 2),
    (3, 2022, 'Semestre 1', 3, 3),
    (4, 2022, 'Semestre 2', 4, 4),
    (5, 2022, 'Semestre 2', 5, 5),
    (6, 2022, 'Semestre 1', 6, 6),
    (7, 2022, 'Semestre 2', 7, 7),
    (8, 2022, 'Semestre 1', 8, 8),
    (9, 2022, 'Semestre 2', 9, 9),
    (10, 2022, 'Semestre 1', 10, 10),
    (11, 2022, 'Semestre 2', 11, 11),
    (12, 2022, 'Semestre 2', 12, 12),
    (13, 2022, 'Semestre 1', 13, 13),
    (14, 2022, 'Semestre 2', 14, 14),
    (15, 2022, 'Semestre 1', 15, 15),
    (16, 2022, 'Semestre 1', 16, 16),
    (17, 2022, 'Semestre 2', 17, 17),
    (18, 2022, 'Semestre 1', 18, 18),
    (19, 2022, 'Semestre 2', 19, 19),
    (20, 2022, 'Semestre 1', 20, 20);

![image](https://github.com/xArthurFerreira/BANCO-DE-DADOS-ESCOLA/assets/141787340/0663c9d7-fe6d-4d01-9761-6f6ad5719be4)





# Inserção de dados na tabela Nota

-- Inserção de dados na tabela Nota
INSERT INTO Nota (ID, IDAluno, IDDisciplina, Valor, DataLancamento)
VALUES
    (1, 1, 1, 8.5, '2022-06-01'),
    (2, 2, 1, 7.0, '2022-06-01'),
    (3, 3, 3, 9.0, '2022-06-02'),
    (4, 4, 4, 6.5, '2022-06-02'),
    (5, 5, 5, 8.0, '2022-06-03'),
    (6, 6, 6, 7.2, '2022-06-03'),
    (7, 7, 7, 9.5, '2022-06-04'),
    (8, 8, 8, 6.8, '2022-06-04'),
    (9, 9, 9, 8.3, '2022-06-05'),
    (10, 10, 10, 7.7, '2022-06-05'),
    (11, 11, 11, 8.9, '2022-06-06'),
    (12, 12, 12, 6.0, '2022-06-06'),
    (13, 13, 13, 7.5, '2022-06-07'),
    (14, 14, 14, 9.2, '2022-06-07'),
    (15, 15, 15, 6.3, '2022-06-08'),
    (16, 16, 16, 8.1, '2022-06-08'),
    (17, 17, 17, 7.0, '2022-06-09'),
    (18, 18, 18, 8.7, '2022-06-09'),
    (19, 19, 19, 6.9, '2022-06-10'),
    (20, 20, 20, 7.8, '2022-06-10');

![image](https://github.com/xArthurFerreira/BANCO-DE-DADOS-ESCOLA/assets/141787340/72cad37b-0f3b-4441-bd45-018c106dd4f9)







# Inserir dados CRUD

INSERT INTO Professor (ID, Nome, DataNascimento, Endereco, Telefone, Email, Especialidade)
VALUES (21, 'Novo Professor', '1985-03-15', 'Rua Nova, 456', '444555666', 'novo_professor@email.com', 'Nova Especialidade');

![image](https://github.com/xArthurFerreira/BANCO-DE-DADOS-ESCOLA/assets/141787340/32911eac-2f49-48ca-819d-61207f5c6cc6)


# Consultar dados CRUD

SELECT * FROM Professor WHERE ID = 21;

![image](https://github.com/xArthurFerreira/BANCO-DE-DADOS-ESCOLA/assets/141787340/9f628955-4540-4f96-99a4-71bbc7f66716)


# Atualizar dados CRUD 

UPDATE Professor SET Nome = 'Professor Atualizado' WHERE ID = 21;

![image](https://github.com/xArthurFerreira/BANCO-DE-DADOS-ESCOLA/assets/141787340/76f94a8f-8df8-4e5d-ad64-d52f6e220c08)


# Excluir dados CRUD 

DELETE FROM Professor WHERE ID = 21;

![image](https://github.com/xArthurFerreira/BANCO-DE-DADOS-ESCOLA/assets/141787340/afd7d051-dda3-457e-9b00-5ed92968e311)













    









# Banco_RPG
Banco de dados SQL - Utilizando linguagem de manipulação dos dados para inserir os dados correspondentes de um jogo de RPG online


--DDL

CREATE DATABASE BdRPG
GO

USE BdRPG
GO

CREATE TABLE Usuarios (
	IdUsuario INT PRIMARY KEY IDENTITY,
	Email VARCHAR (50) UNIQUE NOT NULL,
	Senha VARCHAR (50) NOT NULL,
)
GO

CREATE TABLE Classes (
	IdClasse INT PRIMARY KEY IDENTITY,
	Nome VARCHAR (50) UNIQUE NOT NULL,
	Descricao VARCHAR (255)
)
GO

CREATE TABLE Personagens (
	IdPersonagem INT PRIMARY KEY IDENTITY,
	Nome VARCHAR (50) UNIQUE NOT NULL,
	IdUsuario INT UNIQUE FOREIGN KEY REFERENCES Usuarios(IdUsuario),
	IdClasse INT FOREIGN KEY REFERENCES Classes(IdClasse)
)
GO

CREATE TABLE Habilidades (
	IdHabilidade INT PRIMARY KEY IDENTITY,
	Nome VARCHAR (50) UNIQUE NOT NULL,
	Descricao VARCHAR (255)
)
GO

CREATE TABLE ClasseHabilidade (
	IdClasse INT FOREIGN KEY REFERENCES Classes(IdClasse),
	IdHabilidade INT FOREIGN KEY REFERENCES Habilidades(IdHabilidade)
)
GO

--DML

INSERT INTO Usuarios (Senha, Email) VALUES (123456, 'Jullys@email.com')
INSERT INTO Classes VALUES('Bárbaro', 'Descrição da Classe Bárbaro')
INSERT INTO Habilidades VALUES ('Lança Mortal','Descrição da Lança Mortal'), ('Escudo Supremo', 'Descrição do Escudo Supremo')
INSERT INTO Personagens VALUES ('DeuBug', 1, 1)
INSERT INTO ClasseHabilidade VALUES (1, 1), (1, 2)

INSERT INTO Usuarios VALUES ('Jullys2@email.com', 123456)
INSERT INTO Classes VALUES('Monge', 'Descrição da Classe Monge')
INSERT INTO Habilidades VALUES ('Recuperar Vida', 'Descrição da Recuperar Vida')
INSERT INTO Personagens VALUES ('BitBug', 2, 2)
INSERT INTO ClasseHabilidade VALUES (2, 2), (2, 3)

UPDATE Usuarios SET Senha = 123456 WHERE IdUsuario = 1

--DQL

SELECT * FROM Usuarios
SELECT * FROM Classes 
SELECT * FROM Habilidades 
SELECT * FROM Personagens
SELECT * FROM ClasseHabilidade

--Seleciona tudo

SELECT * FROM Personagens
INNER JOIN Classes 
ON Personagens.IdClasse = Classes.IdClasse

--Especifica colunas

SELECT Personagens.Nome, Classes.Nome, Classes.Descricao FROM Personagens
INNER JOIN Classes 
ON Personagens.IdClasse = Classes.IdClasse

--Abreviando as tabelas
SELECT P.Nome, C.Nome, C.Descricao FROM Personagens P
INNER JOIN Classes C
ON P.IdClasse = C.IdClasse

--Exemplo Join

CREATE DATABASE ExemploJoin 

USE ExemploJoin

CREATE TABLE NomeA (
	Nome VARCHAR (50) NOT NULL
)

CREATE TABLE NomeB (
	Nome VARCHAR (50) NOT NULL
)
 INSERT INTO NomeA VALUES ('Caio'), ('Paula'), ('Helena'), ('Cris'), ('Ken'), ('Ryu')
 INSERT INTO NomeB VALUES ('Ken'), ('Jonas'), ('Kelly'), ('Caio'), ('Chun-li'), ('Honda')

SELECT * FROM NomeA
 JOIN NomeB
 ON NomeA.Nome = NomeB.Nome

 -- RIGHT E LEFT JOIN

SELECT * FROM NomeA
RIGHT JOIN NomeB
 ON NomeA.Nome = NomeB.Nome

 SELECT * FROM NomeA
LEFT JOIN NomeB
 ON NomeA.Nome = NomeB.Nome

SELECT * FROM NomeA
FULL OUTER JOIN NomeB
 ON NomeA.Nome = NomeB.Nome

SELECT * FROM NomeA
FULL OUTER JOIN NomeB
 ON NomeA.Nome = NomeB.Nome
 WHERE NomeA.Nome IS NULL OR NomeB.Nome IS NULL

 SELECT * FROM NomeA
FULL OUTER JOIN NomeB
 ON NomeA.Nome = NomeB.Nome

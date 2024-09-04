# Criando o Diagrama Dimensional – Star Schema – com Base no Diagrama Relacional

## Descrição do Desafio

Este desafio tem como objetivo a criação de um **Diagrama Dimensional** utilizando o **Star Schema** a partir de um diagrama relacional fornecido. O foco principal é a análise de dados relacionados aos professores, como cursos ministrados, departamentos, entre outros aspectos relevantes.

O projeto foi desenvolvido utilizando o MySQL Workbench para a modelagem e implementação das tabelas necessárias.

## Objetivos

- Criar um **Star Schema** para análise de dados dos professores.
- Definir uma **tabela fato** que centralize as informações principais dos professores.
- Criar **tabelas dimensão** para detalhar os diferentes aspectos relacionados, como cursos, departamentos e datas.
- Implementar as **relações** adequadas entre as tabelas (1:N).

## Estrutura do Star Schema

### Tabela Fato

A tabela fato **Fato_Professores** centraliza as informações principais, como o número de alunos por curso ministrado por cada professor em um departamento específico e em uma data específica.

```sql
CREATE TABLE Fato_Professores (
    Fato_ID INT PRIMARY KEY AUTO_INCREMENT,
    Professor_ID INT,
    Curso_ID INT,
    Data_ID INT,
    Departamento_ID INT,
    Numero_Alunos INT,
    FOREIGN KEY (Professor_ID) REFERENCES Dim_Professores(Professor_ID),
    FOREIGN KEY (Curso_ID) REFERENCES Dim_Cursos(Curso_ID),
    FOREIGN KEY (Data_ID) REFERENCES Dim_Datas(Data_ID),
    FOREIGN KEY (Departamento_ID) REFERENCES Dim_Departamentos(Departamento_ID)
);

```
## Tabelas Dimensão

As tabelas dimensão detalham os diferentes aspectos dos dados e são relacionadas à tabela fato através de chaves estrangeiras. Abaixo estão as definições das tabelas dimensão:

#### Dim_Professores

Armazena informações sobre os professores, como nome, email, telefone, data de contratação e departamento ao qual pertencem.

```sql
CREATE TABLE Dim_Professores (
    Professor_ID INT PRIMARY KEY AUTO_INCREMENT,
    Nome VARCHAR(100) NOT NULL,
    Email VARCHAR(100) NOT NULL UNIQUE,
    Telefone VARCHAR(20),
    Data_Contratacao DATE,
    Departamento_ID INT
);
```
#### Dim_Cursos
Contém os dados sobre os cursos oferecidos, incluindo nome, descrição, duração e o departamento responsável.

```sql
CREATE TABLE Dim_Cursos (
    Curso_ID INT PRIMARY KEY AUTO_INCREMENT,
    Nome_Curso VARCHAR(100) NOT NULL,
    Descricao_Curso TEXT,
    Duracao INT, -- Duração em horas
    Departamento_ID INT
);
```

#### Dim_Departamentos
Armazena as informações dos departamentos, como nome e descrição.

```sql
CREATE TABLE Dim_Departamentos (
    Departamento_ID INT PRIMARY KEY AUTO_INCREMENT,
    Nome_Departamento VARCHAR(100) NOT NULL,
    Descricao_Departamento TEXT
);
```

#### Dim_Datas

Inclui os detalhes relacionados às datas, como data específica, ano, mês, dia e trimestre.

```sql
CREATE TABLE Dim_Datas (
    Data_ID INT PRIMARY KEY AUTO_INCREMENT,
    Data DATE NOT NULL,
    Ano INT,
    Mes INT,
    Dia INT,
    Trimestre INT
);
```

## Relações Entre as Tabelas

No Star Schema, as relações entre as tabelas são definidas como 1
(Um-para-Muitos), onde:

- Um professor pode ministrar vários cursos (Dim_Professores → Fato_Professores).

- Um curso pode ser ministrado por vários professores ou em várias datas (Dim_Cursos → Fato_Professores).

- Um departamento pode ter vários professores e cursos (Dim_Departamentos → Dim_Professores e Dim_Departamentos → Dim_Cursos).

- Uma data pode estar associada a várias entradas na tabela fato (Dim_Datas → Fato_Professores).

## Ferramenta Utilizada

- MySQL Workbench: Ferramenta utilizada para criar e gerenciar o banco de dados, modelando as tabelas fato e dimensão conforme o Star Schema.

## Conclusão

Este desafio abordou a criação de um Star Schema, oferecendo uma visão clara e estruturada de como organizar dados para análises eficientes. As tabelas fato e dimensão foram construídas com base em um diagrama relacional, permitindo um entendimento profundo das interações entre as diferentes entidades envolvidas no contexto dos professores.

## Autor
Thiago Arantes Borges Candido

- LinkedIn: [Thiago Borges](https://www.linkedin.com/in/thiago-borges-627659223/)
- GitHub: [AllianceTechSoluções](https://github.com/AllianceTechSolutions)
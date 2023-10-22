
Para visualizar as tabelas employee e department utilizei os comandos abaixo no terminal:
show databases;
use company;
show tables;
select * from employee;
select * from departament;

Para a mescla das tabelas de employee e departamento utilizei a query abaixo:
select CONCAT (e.Fname,' ',e.Minit,' ', e.Lname) as Name, e.Salary,e.Super_ssn,e.Dno,d.Dnumber,Dname from employee  e left join departament d on e.Dno = d.Dnumber;
![image](https://github.com/ElaineCristinaG/mysql/assets/76761529/2dfea73b-55a9-4364-abe3-17343c06e9ab)

Após conexão com Power bi realizei as seguintes transformações:

trasformação de colunas: selecionei a coluna Salary , escolhi "Transform", "Data Type"e escolhi "double"

mesclar colunas de nome :
selecionei as tres colunas Fname, Minit, Lname, depois escolhi "Transform", depois "Merge Columns".escolhi o separardor de mesclagem o "espaço em branco" e "não manter as colunas anteriores" e confirmei a mesclagem

Para a junção de tabelas no power bi utilizei a seguinte query em linguagem DAX:
Tabela Resultado = 
SUMMARIZECOLUMNS (
    'employee'[Name],
    'employee'[Salary],
    'employee'[Super_ssn],
    'employee'[Dno],
    'department'[Dnumber],
    'department'[Dname]
)

Por que, neste caso supracitado, podemos apenas utilizar o mesclar e não o atribuir?
Resp: Não podemos utilizar o atribuir(Related) porque as colunas onde vamos linkar as duas tabelas possuem nomes diferentes: Dno em employee e Dnumber em Departament, portanto o mais indicado neste caso é utilizar o mesclar onde é permitido comparar a igualdade de conteudo de colunas com nomes distintos.

Quantos colaboradores existem por gerente? utilizei a seguinte query:
select d.Dname, count(e.Dno) from departament d inner join employee e on e.Dno = d.Dnumber group by d.Dname;
![image](https://github.com/ElaineCristinaG/mysql/assets/76761529/7ea35aeb-c63c-4f98-89c6-a827b21336f0)

Concatenando departamento com a  localizção pela chave Dnumber de ambas as tabelas dpt_location e departament.
select CONCAT (e.Fname,' ',e.Minit,' ', e.Lname) as Name,e.Super_ssn,e.Salary,CONCAT(d.Dname,' ','de',' ',l.Dlocation) as Depart_Location,e.Dno from employee  e left join departament d on e.Dno = d.Dnumber inner join dept_locations l on d.Dnumber = l.Dnumber;

![image](https://github.com/ElaineCristinaG/mysql/assets/76761529/801b7816-d8e0-4b93-8521-5dd02ac15b2c)


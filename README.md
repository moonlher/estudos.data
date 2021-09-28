# estudos.data
Begin SQL/mysql

-- Linguágem SQL (structed Query Language)
-- SGBD ( Sistemas Gerenciadores deBandosde Dados): MySQL
-- 2 principais tipos de banco de dados: Relacionais (sql)
     -- {1 Relacionais (SQL) Ex.: Mysql, Oracle, Sql Server
     -- {2 Não Relacionais (NoSql) Ex.: MongoDB, Cassandra, REDIS
-- A linguagem SQL NÃO É case-sensitive 


-- create database meuprimeirobd;
   -- comnado de criação de dados já foi criado não precisa cria-lo novamente. Só uma vez.

-- todo banco de dado relacional obrigatóriamente deve seguir as 3 formas normais

   -- 1ª forma norma: Chave (número identificador que não se repete que representa toda a linha de código)
       -- regra 1.: Tabela precisa ter PK (primary key)
       -- regra 2.: Todo campo deve ser atômico

   -- 2ª forma normal:
       -- regra 1.: Tabela deve estar de acordo com a 1ªFN
       -- regra 2.: Toda coluna deve ser diretamente dependente do contexto da tabela
       
   -- 3ª forma normal:
       -- regra 1.: Tabela deve estar de acordo com a 2ªFN
       -- regra 2.: Nome das colunas precisam ter um sentido independente 

-- use meuprimeirobd;

create table pessoa
(
   codpessoa         int               not null  auto_increment,
   nome              varchar(40)       not null,  
   sobrenome         varchar(30)       not null,
   idade             varchar(3)        null,
   dtnascimento      date              null,
   constraint pk_pessoa primary key (codpessoa) 

);

create table documentos 
(
   coddocumento   int                 not null auto_increment,
   codpessoa      int                 not null,
   tipodocumento  varchar(20)         not null,
   ndocumento     varchar(30)         not null,
   constraint pk_documentos primary key (coddocumento),
   constraint fk_documentos_pessoa foreign key (codpessoa) 
   references pessoa(codpessoa) 
);
-- insert into serve para adicionar informação (um dado) a algum valor (values)
insert into pessoa (nome, sobrenome, dtnascimento) values ('Paulo', 'Ponciano', '2000-01-30');
insert into pessoa (nome, sobrenome, dtnascimento) values ('Maria', 'Schuck', '1990-02-25');
insert into pessoa (nome, sobrenome, dtnascimento) values
('Izabelle', 'Lopes', '1995-12-25'),
('Aline', 'Carvalho', '1995-10-12'),
('Mirella', 'Duarte', '1995-08-01');



select * from pessoa;
-- update serve para atualizar uma informação
update pessoa set nome = 'Paulo Augusto' where codpessoa = 1;
update pessoa set sobrenome = 'Lima Duarte'   where sobrenome = 'Duarte'; 

-- para excluir (where é importante, demarcar onde) 

delete from pessoa where codpessoa = 1;

select * from documentos;

insert into documentos (codpessoa, tipodocumento, ndocumento) values
(2, 'rg', '123456'),
(2, 'cpf', '342345'),
(3, 'cnh', '453453');
 
-- para deletar de forma mais segura 
start transaction;
       
delete from documentos where codpessoa= 3;
-- se usar o commit é decisivo para exclusão. 
commit;
-- rollback serve para voltar caso excluir algo que não quis, mas tem que ter dado o comando start transaction;
rollback;





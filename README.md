# Sistema-de-Faculdade

create database db_sistema_faculdade;
use db_sistema_faculdade;

create table tbl_alunos(
id int not null primary key auto_increment,
nome varchar(45) not null,
cpf varchar(20) not null,
rg varchar(20) not null,
data_nascimento date not null,
curso_matriculado varchar(30) not null,

unique index (id)
);

create table tbl_professores(
id int not null primary key auto_increment,
nome varchar(45) not null,
cpf varchar(20) not null,
materia_lecionada varchar(35) not null,

unique index (id)
);

create table tbl_cursos(
id int not null primary key auto_increment,
nome_curso varchar(35) not null,

unique index(id)
);

create table tbl_turmas(
id int not null primary key auto_increment,
id_alunos int not null,
id_professores int not null,
id_cursos int not null,

foreign key (id_alunos) references tbl_alunos(id),
foreign key (id_professores) references tbl_professores(id),
foreign key (id_cursos) references tbl_cursos(id),

unique index (id)
);

create table tbl_notas_alunos(
id int not null primary key auto_increment,
id_alunos int not null,
id_cursos int not null,
nota float not null,

foreign key (id_alunos) references tbl_alunos(id),
foreign key (id_cursos) references tbl_cursos(id),

unique index (id)
);

create table tbl_materias(
id int not null primary key auto_increment,
id_alunos int not null,
id_professores int not null,
id_cursos int not null,
nome_materias varchar(45),

foreign key (id_alunos) references tbl_alunos(id),
foreign key (id_cursos) references tbl_cursos(id),
foreign key (id_professores) references tbl_professores(id),

unique index (id)

);

create table tbl_endereco(
  id int not null primary key auto_increment,
  logradouro varchar(100) not null,
  bairro varchar(45) not null,
  estado varchar(45) not null,
  pais varchar (45) not null,
  cidade varchar(45) not null,
  id_alunos int not null,
  
  constraint fk_cliente_endereco
  foreign key (id_alunos)
  references tbl_alunos (id),
  
  unique index (id)
  
 );

create table tbl_telefone(
 id int not null primary key auto_increment,
 numero varchar(20)not null,
 id_alunos int not null,
 
 constraint fk_alunosTelefone
 foreign key (id_alunos)
 references tbl_alunos (id),
 
 unique index (id)
 );
 
create table tbl_email (
    id int not null primary key auto_increment,
    email VARCHAR(50) not null,
    id_alunos int not null,
    constraint fk_alunos_email 
    foreign key (id_alunos) 
    references tbl_alunos(id),
   
   UNIQUE INDEX (id)
);

select *from  tbl_cursos;
alter table tbl_turmas drop column nome_alunos;
alter table tbl_materias add column carga_horaria varchar(45);
insert into tbl_alunos(nome, cpf, rg, data_nascimento, curso_matriculado)
values
('João da Silva', '123.456.789-00', '12.345.678-9', '1998-05-12', 'Recursos Humanos'),
('Fernanda Costa Santos', '789.123.456-00', '78.912.345-6', '1996-03-22', 'Medicina'),
('Ana Paula Lima', '654.987.321-00', '65.498.732-1', '1999-11-30', 'Admimistração'),
('Carlos Eduardo Souza', '321.654.987-00', '32.165.498-7', '2000-01-15', 'Engenharia Civil'),
('Maria Clara Oliveira', '987.654.321-00', '98.765.432-1', '1997-08-20', 'Direito');

insert into tbl_cursos(nome_curso, valor_mensalidade)
values
('Recursos Humanos', '550.00'),
('Medicina', '1500.00'),
('Administração', '650.00'),
('Engenharia Civil', '1350.00'),
('Direito', '1780.00');

insert into tbl_email(email, id)
value
('joao.silva@faculdade.com', 1),
('fernanda.costa@faculdade.com', 2),
('ana.lima@faculdade.com', 3),
('carlos.souza@faculdade.com', 4),
('maria.oliveira@faculdade.com', 5);

alter table tbl_email alter column id_alunos set default 1;
insert into tbl_endereco(logradouro, bairro, estado, pais, cidade, id_alunos)
values
('Rua das Flores, 123', 'Centro', 'São Paulo', 'Brasil', 'Sao Paulo', 1),
('Avenida Paulista, 987', 'Bela Vista', 'São Paulo', 'Brasil', 'Sao Paulo', 2),
('Rua Augusta, 456', 'Consolação', 'São Paulo', 'Brasil', 'Sao Paulo', 3),
('Rua da Harmonia, 789', 'Vila Madalena', 'São Paulo', 'Brasil', 'Sao Paulo', 4),
('Rua José Paulino, 876', 'Bom Retiro', 'São Paulo', 'Brasil', 'Sao Paulo', 5);

insert into tbl_materias(carga_horaria, id_alunos, id_professores, id_cursos)
values
('2.400h', 1, 1, 1),
('7.200h', 2, 2, 2),
('2.800h', 3, 3, 3),
('4.000h', 4, 4, 4),
('4.200', 5, 5, 5);

insert into tbl_professores(nome, cpf, materia_lecionada)
values
('Carlos Eduardo Souza', '123.456.789-00', 'Matemática'),
('Roberto Carlos Almeida', '258.963.147-00', 'Filosofia'),
('Gustavo Martins de Oliveira', '777.888.999-00', 'História'),
('André Carvalho de Souza', '999.000.111-22', 'Matemática'),
('Claudia Rodrigues de Almeida', '444.555.666-77', 'Matemática');

insert into tbl_telefone(numero, id_alunos)
values
(11912345678, 1),
(11987654321, 2),
(11998765432, 3),
(11934567890, 4),
(11978901234, 5);

insert into tbl_notas_alunos(nota, id_alunos, id_cursos)
values
('7.5', 1, 1),
('8.3', 2, 2),
('6.9', 3, 3),
('9.5', 4, 4),
('9.8', 5, 5);

alter table tbl_notas_alunos modify nota decimal(10,2);

select *from tbl_endereco;
update tbl_email
set id_alunos = '4'
where id = 4;

# Projeto: Atendimento a Chamados

## Breve descrição do tema
Descrição

## Imagem do MER DER Conceitual
![MER DER Conceitual](/MER%20DER%20Conceitual.png)

## Imagem do MER DER Lógico
![MER DER Lógico](/MER%20DER%20Lógico.png)

## Dicionário de dados em tabela do Git Hub (MarkDown)

| Entidade | Atributo | Tipo | Tamanho| Descrição |
|-|-|-|-|-|
|Usuário|id|int|11|Chave primária do usuário|
|Usuário|nome|varchar|100|Nome do usuário|
|Usuário|email|email|100|Email do usuário|
|Usuário|telefone|int|11|Telefone do usuário|
|Usuário|departamento|varchar|100|Departamento que o usuário trabalha|
|Usuário|cargo|varchar|100|cargo com que o usuário trabalha|
|Chamado|id|int|11|chave primaria do chamado|
|Chamado|id_usuário|int|11|chave estrangeira do usuário|
|Chamado|id_categoria|int|11|chave estrangeira da categoria|
|Chamado|id_técnico|int|11|chave estrangeira do técnico|
|Chamado|título|varchar|100|título do chamado|
|Chamado|descrição|varchar|100|descrição do chamado|
|Chamado|data de abertura|date|8|data de abertura do chamado|
|Chamado|data de fechamento|date|8|data de fechamento do chamado|
|Chamado|status|varchar|"concluido","não concluido"|status do chamado|
|Chamado|prioridade|varchar|"urgente","normal","pouca relevância"|status do chamado|
|Técnico|id|int|11|chave primaria do técnico|
|Técnico|nome|varchar|100|nome do técnico|
|Técnico|email|email|100|email do técnico|
|Técnico|especialidade|varchar|100|no que o técnico é melhor|
|Técnico|status|varchar|"ativo","inativo"|status do técnico|
|Categoria|id|int|11|chave primária da categoria|
|Categoria|nome|varchar|100|nome da categoria|
|Categoria|descrição|varchar|100|descrição da categoria|
|Histórico/Comentários|id|int|11|chave primária do histórico ou comenários da chamada|
|Histórico/Comentários|data e hora|datetime|12|data e hora do histórico ou comenários da chamada|
|Histórico/Comentários|descrição|varchar|100|descrição do histórico ou comentários da chamada|
|Histórico/Comentários|tipo|varchar|100|tipo do histórico ou comentários da chamada|

## Links para as 5 tabelas de teste
- [usuario.csv](./usuario.csv)
- [chamado.csv](./chamado.csv)
- [tecnico.csv](./tecnico.csv)
- [categoria.csv](./categoria.csv)
- [histórico/comentarios.csv](./historico.csv)

## Código DDL
```sql
DROP DATABASE IF EXISTS chamados;
CREATE DATABASE chamados;
USE chamados;

CREATE TABLE usuario(
    id int not null primary key auto_increment,
    nome varchar(100) not null,
    email varchar(100) not null,
    telefone varchar(15) not null,
    departamento varchar(100) not null,
    cargo varchar(100) not null,
    status enum('ativo', 'inativo') not null
);

CREATE TABLE chamado(
    id int not null primary key auto_increment,
    id_usuario int not null,
    id_tecnico int not null,
    id_categoria int not null,
    titulo varchar(100) not null,
    descricao varchar(500) not null,
    prioridade enum('urgente', 'normal', 'não relevante') not null,
    status enum('concluido', 'não concluido') not null,
    data_abertura datetime not null,
    data_fechamento datetime
);

CREATE TABLE tecnico(
    id int not null primary key auto_increment,
    nome varchar(100) not null,
    email varchar(100) not null,
    especialidade varchar(100) not null,
    status enum('ativo', 'inativo') not null
);

CREATE TABLE categoria(
    id int not null primary key auto_increment,
    nome varchar(100) not null,
    descricao varchar(100) not null
);

CREATE TABLE historico(
    id int not null primary key auto_increment,
    id_usuario int not null,
    id_chamado int not null,
    descricao varchar(100) not null,
    tipo varchar(100) not null,
    data_hora datetime not null
);

alter table chamado add constraint id_usuario_no_chamado foreign key (id_usuario) references usuario(id);
alter table chamado add constraint id_tecnico_no_chamado foreign key (id_tecnico) references tecnico(id);
alter table chamado add constraint id_categoria_no_chamado foreign key (id_categoria) references categoria(id);
alter table historico add constraint id_chamado_no_historico foreign key (id_chamado) references chamado(id);
alter table historico add constraint id_usuario_no_historico foreign key (id_usuario) references usuario(id);

describe usuario;
describe chamado;
describe tecnico;
describe categoria;
describe historico;
```
## Código DML
```sql
USE chamados;

INSERT INTO usuario (nome, email, telefone, departamento, cargo) VALUES
('Aura Dias', 'aura.dias@email.com', '19-99999-0001', 'Paper Company', 'Cópias'),
('Flávio', 'flavio@email.com', '19-99999-0002', 'Paper Company', 'Cópias'),
('Jacinto Pena', 'jacinto.pena@email.com', '19-99999-0003', 'Paper Company', 'Cópias');

INSERT INTO tecnico (nome, email, especialidade, status) VALUES
('Eduardo', 'eduardo@email.com', 'TI', 'ativo'),
('Heitor', 'heitor@email.com', 'Excel', 'ativo'),
('Otávio', 'otavio@email.com', 'Microsoft', 'inativo');

INSERT INTO categoria (nome, descricao) VALUES
('TI', 'Problemas de tecnologia'),
('Excel', 'Problemas com excel'),
('Microsoft', 'Problemas com microsoft');

INSERT INTO chamado (id_usuario, id_tecnico, id_categoria, titulo, descricao, prioridade, status, data_abertura, data_fechamento) VALUES
(1, 2, 2, 'Cópia Excel', 'Mensagem de erro de cópia no excel', 'urgente', 'concluido', '2009-09-19 10:00:00', '2009-09-19 11:00:00'),
(2, 3, 3, '67 Contas Microsoft', 'Como criar 67 contas na microsoft', 'normal', 'concluido', '2007-07-07 09:00:00', '2007-07-07 10:00:00'),
(3, 1, 1, 'Erro Email', 'Erro ao enviar mensagem no email', 'não relevante', 'não concluido', '2005-05-05 14:00:00', NULL);

INSERT INTO historico (id_usuario, id_chamado, descricao, tipo, data_hora) VALUES
(1, 1, 'Mensagem de erro de cópia no excel', 'texto', '2009-09-19 10:00:00'),
(2, 2, 'Como criar 67 contas na microsoft', 'texto', '2007-07-07 09:00:00'),
(3, 3, 'Erro ao enviar mensagem no email', 'texto', '2005-05-05 14:00:00');

SELECT * FROM usuario;
SELECT * FROM tecnico;
SELECT * FROM categoria;
SELECT * FROM chamado;
SELECT * FROM historico;
```

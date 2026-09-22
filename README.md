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

```

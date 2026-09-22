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

## Links para as 5 tabelas
- [usuario.csv](./usuario.csv)
- [chamado.csv](./chamado.csv)
- [tecnico.csv](./tecnico.csv)
- [categoria.csv](./categoria.csv)
- [histórico/comentarios.csv](./historico.csv)

## Código DDL
```sql
```
## Código DML
```sql
```
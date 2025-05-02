# Aprendendo SQL com Dota2

### Criando o Banco de Dados e Tabela

```sql
CREATE DATABASE dota2_heroes;

USE dota2_heroes

CREATE TABLE dota2_base(
   id                INT NOT NULL PRIMARY KEY 
  ,hero              VARCHAR(20) NOT NULL
  ,primary_attribute VARCHAR(15) NOT NULL
  ,strength          INT  NOT NULL
  ,agility           INT  NOT NULL
  ,intelligence      INT NOT NULL
  ,str_gain          NUMERIC(3,1) NOT NULL
  ,agi_gain          NUMERIC(3,1) NOT NULL
  ,int_gain          NUMERIC(3,1) NOT NULL
  ,movement_speed    INT NOT NULL
  ,sight_range_day   INT  NOT NULL
  ,sight_range_night INT NOT NULL
  ,base_attack_speed NUMERIC(3,1) NOT NULL
  ,min_base_damage   INT  NOT NULL
  ,max_base_damage   INT  NOT NULL
);

```
## Os valores da Tabela eu inseri via Importação de Arquivo .csv
### Segue abaixo um exemplo de como inserir valores via SQL

```sql
INSERT INTO dota2_base(id,hero,primary_attribute,strength,agility,intelligence,str_gain,agi_gain,int_gain,movement_speed,sight_range_day,sight_range_night,armor,base_attack_speed,min_base_damage,max_base_damage) 
VALUES 
    (1,'alchemist','strength',23,22,25,27,15,18,295,1800,800,308,17,50,56),
    (2,'axe','strength',25,20,18,28,17,16,315,1800,800,28,17,56,60),
    (3,'bristleback','strength',22,17,14,27,18,28,295,1800,800,338,18,53,59),
    .
    .
    .
    (126,'windranger','all',18,17,18,26,19,32,290,1800,800,238,15,39,51);
```
Consultado a Tabela

```sql
SELECT * FROM dota2_base
```


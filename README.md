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

Consultado a tabela

```sql
SELECT * FROM dota2_base
```

Consulta de quantos heróis existem de cada atributo

```sql
SELECT
primary_attribute,
COUNT(*) FROM dota2_base 
GROUP BY primary_attribute;
```

Categorizando os heróis por atributo

```sql
SELECT hero,
CASE 
WHEN primary_attribute = "agility" THEN "Agility Hero"
WHEN primary_attribute = "strength" THEN "Strength Hero"
WHEN primary_attribute = "intelligence" THEN "Intelligence Hero"
ELSE "Universal Hero"
END as hero_type
FROM dota2_base;
```

Consulta da Média de Atributos Geral

```sql
SELECT 
AVG(strength) as avg_str,
AVG(agility) as avg_agi,
AVG(intelligence) as avg_int 
FROM dota2_base;
```

Consulta dos heróis que estão acima da média

```sql
SELECT
hero, strength, agility, intelligence
FROM dota2_base
WHERE 
   strength > (SELECT AVG(strength) from dota2_base) AND
   agility > (SELECT AVG(agility) from dota2_base) AND
   intelligence > (SELECT AVG(intelligence) from dota2_base);
```

Consulta média da visão dos heróis

```sql
SELECT  -- consulta média da visão dos heróis
AVG(sight_range_day),
AVG(sight_range_night) FROM dota2_base;
```

Consulta dos heróis com visão acima da média 

```sql
SELECT hero, sight_range_day, sight_range_night -- consulta dos heróis com visão acima da média 
FROM dota2_base
WHERE 
    sight_range_day > (SELECT AVG(sight_range_day) FROM dota2_base)
    AND sight_range_night > (SELECT AVG(sight_range_night) FROM dota2_base);
```

Consulta dos heróis com velocidade de movimento acima da média 

```sql
SELECT hero, movement_speed
 FROM dota2_base
WHERE
	movement_speed > (SELECT AVG(movement_speed) FROM dota2_base);
```

Consulta utilizando UNION ALL para unificar o resultado de três diferentes consultas, em busca dos heróis que mais escalam no seu respectivo atributo

```sql
SELECT
hero,
str_gain,
agi_gain,
int_gain,
primary_attribute
FROM dota2_base
WHERE
	str_gain = (SELECT MAX(str_gain) from dota2_base)

UNION ALL

SELECT
hero,
str_gain,
agi_gain,
int_gain,
primary_attribute
FROM dota2_base
WHERE
	agi_gain = (SELECT MAX(agi_gain) from dota2_base)
    
UNION ALL

SELECT
hero,
str_gain,
agi_gain,
int_gain,
primary_attribute
FROM dota2_base
WHERE
	int_gain = (SELECT MAX(int_gain) from dota2_base);

```

Consulta dos heróis com diferença de dano maior do que a média geral

```sql
SELECT 
h1.hero,
(h1.max_base_damage - h1.min_base_damage) as diff_damage
FROM
dota2_base h1
WHERE (h1.max_base_damage - h1.min_base_damage) > (
	SELECT
    AVG(h2.max_base_damage - h2.min_base_damage)
    FROM
    dota2_base h2
);
```

Consulta dos heróis com dano acima da média do seu atributo primário

```sql
SELECT h1.hero, h1.max_base_damage, h1.primary_attribute
FROM dota2_base h1
WHERE h1.max_base_damage > (
    SELECT AVG(h2.max_base_damage)
    FROM dota2_base h2
    WHERE h2.primary_attribute = h1.primary_attribute  
);
```










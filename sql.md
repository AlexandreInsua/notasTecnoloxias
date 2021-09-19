# NOTAS SQL

## SENTENZA EXPLAIN

### 1. A sentenza EXPLAIN

A sentenza EXPLAIN devolve unha táboa con información sobre cada unha das táboas empregadas na consulta ordenadas na mesma orde en que van ser lidas.
A combinación con EXTENDED vai esta deprecada.
A combinación con PARTITIONS mostra información sobre as táboas particionadas na consulta. 

### 2. O resultado da exectución de EXPLAIN

O resultado da sentenza EXPLAIN mostra as seguintes columnas:

- **id**  mostra o número secuencial que identifica cada unha das táboas da sentenza.
- **select_type** mostra o tipo de select que se executo:
	- SIMPLE
	- PRIMARY
	- UNION
	- DERIVED
- **table** nome de táboa, ou resultante de unión, derivada ou subconsulta
- **partitions** mostras as particións cuxos rexistros coinciden cos da consulta.
- **type** mostra o tipo di unión que se empregou
- **possible_kqys** mostra os índices que se poden escoller 
	NULL significa que non hay índices apara usar.
- **key** mostra o índice que se usou para  consulta.
- **ref** mostra que columnas on comparados co índice.
- **rows** mostra o número de filas que vai examinar o motor da db.
- **filtered** mostra a porcentaxe de filas que se van filtrar.
- **extra** información adicional.



## OPTIMIZACIÓN DE CONSULTAS MySQL

[Artigo en _adictos al trabajo_](https://www.adictosaltrabajo.com/2016/10/24/optimizacion-de-consultas-en-mysql/)


### 1.Executar a sentenza EXPLAIN

En primeiro lugar hai que executar a sentenza `EXPLAIN`. Do resultado deste comando hai que fixarse en

- **A orde das filas** é a orde en que a base de datos consulta as táboas.
- **A columna Key** indica o índice que se está empregando para accedir a esa táboa concreta, de o houber.
- **A columna Type** indica o tipo de acceso á táboa. Os posibles valores, de mellor a peor, son:
  
	- _system_.
	- _const_.
	- _eq_ref_.
	- _ref_
	- _fulltext_
	- _ref_or_null_
	- _index_merge_
	- _unique_subquery_
	- _index_subquery_
	- _range_
	- _index_
	- _ALL_

Se algún acceso é de tipo _index_ ou _ALL_ hai que revisar esa parte da consulta porque NON está optimizada.

### 2. Optimzacións

#### 2.1. Evitar _FULL SCANS_.

Se algunha algunha táboa ten como tipo de acceso _ALL_, daquela trátase dun `FULL TABLE SCAN` que quere dicir que **se están a ler todos os rexistros da dita táboa**.  Hai que estudar a rescritura da sentenza para que se acceda por un índice ou crear un para as columnas polas que se está a buscar.

Se algunha algunha táboa ten como tipo de acceso _INDEX_, daquela trátase dun `FULL INDEX SCAN` que quere dicir que **se están a ler todos os accesos dun índice**. Non é un caso tan grave porque se fai en memoria e lese menos información por rexistro, pero está a pasar pos todos os nodos. Este tipo de acceso emprégase cando todas as columnas que queremos obter forman parte do mesmo índice e o optimizador da base de datos entende que non necesita ir ás táboas xa que poder sacala do índice.

#### 2.2. Uso correcto dos índices.

Un índice é como un dicionario `chave:valor`. O motor de base de datos buscar por chave, que é o valor do campo. No caso de índices compostos a **orde das columnas que forman o índice é fundamental** porque o índice está formado por elas secuencialmente.

#### 2.3. Sentenzas _OR_

O optimizador de MySQL non pode usar índices se se emprega a sentenza `OR` e algunha das súas restricións é unha columna non indexada. Cando se usen sentenzas `OR` hai que asegurarse que **as restricións están indexadas**.

#### 2.4. Group / order by

As sentenzas `GROUP BY` e `ORDER BY` teñen un funcionamento. Poden supor un funil cando o número de rexistros por agrupas é moi elevado (independetemente se hai un LIMIT). Hai que procurar que todas as columnas presentes nestas sentenzas **formen parte do mesmo índice que se se está consultando, na mesma orde**.

Outra técnica é definir un índice, acoutala cun WHERE e despois aplicar o GROUP/ORDER BY.

#### 2.5. Táboas derivadas vs subqueries

Unha **subconsulta** é unha consulta SELECT dentro dunha consulta maior. Unha **táboa derivada** é unha subconsulta dentro do FROM principal. Hai que ter en conta que:

- Unha subconsulta execútase por cada rexistro da consulta principal.
- Unha táboa derivada realiza unha consulta e a garda nunha táboa temporal en memoria e accede a ela por cada rexistro da consulta principal.
Normalmente a táboa derivada é máis eficiente, pero hai que ter en conta que as **táboas derivadas non están indexadas** polo que se teñen moitos rexistros va a enlentecer a consulta porque acceden unha vez por rexistro do pai. Hai que acoutar o máis posible as táboas derivadas.

#### 2.6. INNER JOIN con GROUP / ORDER

Nunha consulta con varios INNER JOIN é o optimizador que decide a orde da consulta das taboas dependendo das restricións e dos índices **agás GROUP/ORDER BY**. Para solucionar isto hai que colocar primeiro a táboa sobre a que se está facendo o GROUP/ORDER BY e usar un STRAIGHT_JOIN, que é un INNER JOIN que forza a lectura da táboa da esquerda antes que os da dereita. No caso dos LEFT JOIN, non hai problema porque a táboa da esquerda sempre se vai ler primeiro.

#### 2.7. A sentenza EXIST

As consultas con EXIST son boas alternativas para evitar crear táboas derivadas onde hai que percorrer moitos rexistros para unhas poucas agrupacións.

A técnica consiste en usar unha subconsulta no WHERE do tipo:

```sql
SELECT BIG.* FROM BIG
WHERE EXISTS ( SELECT (*) FROM HUGE WHERE HUGE.fk_big = BIG.id_big 	AND HUGE.campo_huge_1 = 'valor1')
```

## EXPORTAR BASES DE DATOS

O comando para exportar bd é `mysqldump` pide usuario e password
Admite un param `--where` para filtrar datos
A sintaxe é:

```bash
mysqldump -u -p options database tables > outfile
```

por exemplo:

```bash
mysqldump -uroot -p --where="id between 204854 and 204860" modx_apvigo ap_puerto_arribos > C:/Users/ainsua/Documents/dumps/arribos.sql

```


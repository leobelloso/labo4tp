# SQL

## DML

### Select

PERMITE EXTRAER INFO ALMACENDA EN LA BD. Es una operación de solo lectura. La sentencia SELECT consta de 2 cláusuales: SELECT  y FROM.

#### Ejercicios

1. Mostrar los datos de la tabla "Provincias".
2. Imprimir las COLUMNAS codpro y nombre de la tabla provincias.
3. Mostrar el código de artículo y el doble del precio unitario de la tabla "artículos"
4. Mostrar de la tabla lineas_fac los campos: id_factura, linea y cantidad por precio unitario.

### Select Distinct

Devuelve solo los valores no repetidos (diferentes).

**Sintaxis**

```
SELECT DISTINCT Country FROM Customers;
```

5. Mostrar los distintos IVA de la tabla facturas.

### Where (Restricción en las filas)

La cláusula **WHERE** restringe y selecciona solo algunas filas que cumplen determinada condición y se escribe siempre después del FROM. Se puede combinar con distintos campos y los operadores AND y OR.

**Sintaxis**

```
SELECT codigo, nombre
FROM ciudades
WHERE codigo < 2800
```

6. Seleccionar de la tabla CIUDADES el código y el nombre cuyo código sea mayor o igual a 2800.

7. Seleccionar las facturas del cliente nro 1 con IVA == 0.

8. Mostrar artículos cuyo stock es >= 10

9. Mostrar las facturas con fecha 1/08/2024

### EXPRESIONES Y TIPOS
SQL permite utilizar expresiones en lugares de la columna. Se pueden construir utilizando expresiones matemáticas y otras funciones.

**Operadores de Comparación** :  = , > , < > , <= , >=

## BETWEEN

The BETWEEN operator selects values within a given range. The values can be numbers, text, or dates.

**Sintaxis**

```
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

### Not Between

To display the products outside the range of the previous example, use NOT BETWEEN:

### Between con IN

The following SQL statement selects all products with a price between 10 and 20. In addition, the CategoryID must be either 1,2, or 3:

```
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20
AND CategoryID IN (1,2,3);
```

10. Escribir una expresión que devuelva el código de cliente y el nombre de la tabla de clientes de aquellos cuyo código está entre 1 y 5 inclusive.

---

## IN

The IN operator allows you to specify multiple values in a WHERE clause.

The IN operator is a shorthand for multiple OR conditions.

**Sintaxis** 
```
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2, ...);
```

### NOT IN

By using the NOT keyword in front of the IN operator, you return all records that are NOT any of the values in the list.

11. Escribir una expresión que devuelva las ciudades de CABA, BS, y Cba. en la tabla ciudades, utilizando el operador IN.

### Like

Se utiliza en una cláusula **WHERE** para buscar un patrón específico en una columna.

- The percent sign % represents zero, one, or multiple characters
- The underscore sign _ represents one, single character

**Sintaxis**

```
SELECT *
FROM clientes
WHERE apeno NOT LIKE 'P%'
```

12. Consultar todos los apellidos que empiecen con "P" en la tabla clientes.

### Case

The CASE expression goes through conditions and returns a value when the first condition is met (like an if-then-else statement). So, once a condition is true, it will stop reading and return the result. If no conditions are true, it returns the value in the ELSE clause.

**Sintaxis**

```
SELECT *,
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN conditionN THEN resultN
    ELSE result
END;
FROM table
```

13. Mostrar de la tabla FACTURAS la leyenda SIN IVA cuando el IVA sea == 0 y la leyenda PAGÓ IVA cuando el IVA sea MAYOR a 0.

---

## Datos Nulos

### IS NULL / IS NOT NULL

Un valor NULL corresponde exactamente a la ausencia de valor, el cual no puede ser comparado con ningún otro valor de ningún tipo de dato. O sea, que un vallor NULL nunca es igual a otro valor, ni tampoco diferente.

**Sintaxis**

```
SELECT *
FROM tabla
WHERE columna IS/IS NOT NULL
```

14. Mostrar FACTURAS sin código de vendedor o sin código de cliente
15. Escribir una sentencia SQL que muestre el CODIGO de los ARTICULOS con un STOCK superior a 50 y sabiendo que el campo o atributo puede ser nulo en algunas ocasiones, por lo tanto, tambien mostrar los nulos.

### Coalesce

La función retorna el primer valor "no-nulo" en una lista.
Según Ragazzo, los "convierte", en verdad, no hace eso, sino que si se encuentra con un valor nulo, lo ignora y retorna el valor que le sigue en la lista que declaramos.

**Sintaxis**

```
SELECT COALESCE(NULL, 1, 2, 'W3Schools.com');
```

16. Convertir el campo teléfono en un valor cero si el teléfono no existe

## Conversión de Datos

### to_char

Convierte una expresión de tipo fecha a un string.

Formatos: YYYY; YY; rrrr; mm; month; mi; dd; dy; hh; mm;; hh12; hh24; ss.

**Sintaxis**

```
SELECT *, TO_CHAR(columna, "formatos")
FROM tabla

SELECT EXTRACT(MONTH FROM "2017-06-15");
```

17. mostrar todos los campos de la factura y la fecha en el formato DD/MM/AA.

### Extract

Extrae parte de la fecha.

```
SELECT *
FROM tabla
WHERE EXTRACT(YEAR FROM tabla) = '2024'
```

18. Mostrar las facturas de la tabla facturas solo del año 2024.
19. Escribir una expresión que devuelva las facturas vendidas en agosto de 2024.

### Format

Format the number as "#,###,###.##" (and round with two decimal places):

```
SELECT FORMAT(250500.5634, 2);
```

20. Mostrar en la tabla linea de facturas, el importe sin decimales.

## Procesamiento de Strings

### Concat

```
SELECT concat(columna1, " leyenda  ", columna2)
FROM tabla
```

21. Concatenar el domicilio (calle nro, piso, depto) y codigo postal de la tabla clientes.

### Longitud de un String (char_length)

```
SELECT CHAR_LENGTH(col)
FROM tabla
```

### Extracción de parte de una cadena

```
select substring(col, inicio, end)
from tabla
```

22. Extraer los 5 primeros chars del nombre de la tabla clientes.

### Uso de Mayúsculas

```
select upper(col)
from tabla
```

```
select lower(col)
from tabla
```
---
## Funciones Matemáticas

```
SELECT ROUND(col, 2);
```

23. Redondear a 1 decimal el producto cantidad x precio unitario FROM lineas_fac


```
SELECT floor(col);
```

 Redondea los decimales que haya.
 
### Ejercicios varios

24. Escribir una consulta que muestre el nombre de los clientes cuyo CP comienza con 2, 11 y 28.

25. Seleccionar codcli, apeno y telefono de los clientes con codcli 1 y 10, si el telefono es null, reemplazarlo con 'Sin telefono'.

---

## Funciones de Columna

**AVG**, **COUNT**, **MAX**, **MIN**, **STDDEV**, **VARIANCE**

**NO DEBEN APARECER EN LA CLAUSULA WHERE**


**Sintaxis**

```
SELECT COUNT/MAX/AVG/etc(columna)
FROM tabla
```

26. Obtener el promedio de artículos cuyo stock sea mayor a 10 unidades en la tabla artículos.
27. Mostrar el promedio, la cantidad, la suma total, el val max y val minimo, desviación std y varianza del precio unitario en la tabla artículos.
28. Mostrar el avg del stock_min de los articulos pero, como la función avg ignora los nulos, debemos convertirlos en 0.

---

## Funciones de Agrupamiento

Conjunto de filas con una misma característica común. Dicha característica puede ser una columna, un conjunto de columnas o, incluso, una expresión de 1 o más columnas.

### Group By

The GROUP BY statement groups rows that have the same values into summary rows, like "find the number of customers in each country".

The GROUP BY statement is often used with aggregate functions (COUNT(), MAX(), MIN(), SUM(), AVG()) to group the result-set by one or more columns.

**Sintaxis**

```
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);
```

29. Contar clientes de la tabla clientes por código de ciudad.
30. Mostrar cantidad de ciudades por código de provincia.
31. Mostrar el total de cada factura de la tabla lineas_fac
32. Agrupar las facturas de la tabla "facturas" por cada año.
33. Agrupar facturas por año y mes.

### Vistas

Son tablas virtuales. Si modifico una tabla, se modifica la vista, la combinación de tablas se mantiene y la vista se actualiza. El costo es que cada vez que toco una tabla se modifica una vista, por tanto, hay que evaluar cuales conviene tener.

### Max () y LENGTH ()

En SQL, las funciones MAX() y LENGTH() se pueden usar juntas para obtener la longitud máxima de cadenas dentro de un conjunto de datos.

**LENGTH(nombre_pueblo)**: Esta función toma el valor de la columna nombre_pueblo y calcula la longitud de cada entrada en términos del número de caracteres.

**MAX(LENGTH(nombre_pueblo))**: Después de calcular la longitud de cada entrada en nombre_pueblo, la función MAX() selecciona la longitud más grande de ese grupo.

Cuando se combinan en una consulta con GROUP BY, se puede obtener la longitud máxima de los nombres de los pueblos para cada grupo especificado, en este caso, cada codigo_provincia.

34. Calcular por cada código de provincia en la tabla "Ciudades" la máxima longitud de los nombres de los pueblos.

**Sintaxis**

```
SELECT cod_prov, MAX(LENGTH(nombre)) AS max_longitud_nombre
FROM Ciudades
GROUP BY cod_prov
```

### Ejercicios varios

35. Agrupar las facturas de la tabla "facturas" por cada año.
36. Agrupar facturas por año y mes.

---

## Restricciones de Filas y de Grupo

Una consulta con agrupación admite 2 tipos de restricciones:

- Las de fila: USA la cláusula WHERE y se aplican a cada fila. Si la expresión devuelve TRUE, la fila se procesa. ES MAS EFICIENTE que el HAVING.

- Las de grupo: van en la cláusula "HAVING". Esta va siempre TRAS la cláusula **GROUP BY**.

Este tipo de restricciones tiene un funcionamiento análogo al **WHERE** pero aplicadas al **grupo**. Si la restricción es verdadera, el grupo es procesado, caso contrario, es descartado.

El having es al grupo como el where es a cada una de las filas de la tabla. Nos permite eliminar ciertos grupos. Primero agrupa y luego se fija si está dentro o fuera de lo que se pide en la instrucción.
**El WHERE es primero**.

The HAVING clause was added to SQL because the WHERE keyword cannot be used with aggregate functions.

**Sintaxis**

```
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition
ORDER BY column_name(s);
```

37. Obtener las facturas con el total de cada una por cliente pero con una suma mayor a 150.000. Tabla linea_fac
38. Calcular por código de provincia la máxima longitud del nombre en la tabla ciudades.
39. Calcular el descuento promedio aplicado a las facturas del año 2024 de cada cliente, solo si tuvieron un promedio de descuento mayor a 2000.
40. Por cada artículo en lineas_fac, mostrar el precio máximo y las unidades vendidas de las facturas de agosto del 2024 y solo artículos cuya cantidad (SUMA) sea mayor a 10.

---

## Manipulación de Datos

### Insert Into (Inserción de Datos)

The INSERT INTO statement is used to insert new records in a table.

**Sintaxis**

```
insert into nombre_table(col1,col2)
values(val1,val2)
```
SQL Respeta el orden de los campos:

```
insert into vendedores
values (13, 'faccio javier', 'soler', '1122', 2800)
```

## Update (Modificación de Datos)

Se puede modificar 1 o más columnas de la tabla y es posible definir una condición que deba cumplir la fila a modificar. Esto quiere decir que puedo modificar 1 o más columnas simultáneamente en la misma sentencia. Mediante una condición puedo determinar en qué filas de la tabla quiero hacer la modificación.


### Consideraciones

- La condición de **where** puede ser tan compleja como en un **select** .

- Si en la expresión aparecen referidas columnas de la propia tabla, en la modificación se toma el valor actual de la columna de esa fila.

- Se debe tener cuidado con la modificación de las PK.

- No se permiten violar las restricciones existentes


**Sintaxis**

```
update nombre_table
set colum1=expresion1, colum2=expres2
where condicion
```

41. Modificar el precio del stock de todos los artículos incrementándolos en 10 unidades.
42. Modificar el preu de la tabla articulos aumentandolo un 20% solo en aquellos articulos cuyo stock sea distinto de 0 y mayor a 50 000 el costo unitario.


### Delete (Borrado de datos)

La operación **DELETE** permite la eliminación de las filas de toda la tabla o aquellas que cumplan determinada condición.

**Sintaxis**

```
delete from nombre_table 
```

En este caso, sin **where**, se debe tener en cuenta que al no existir la cláusula **where** no todas las filas de la tabla podrán ser borradas, sino que **solo aquellas que cumplan con las restricciones existentes en la BD por la definición de FK** .


43. Borrar aquellos articulos cuyo stock sea igual a cero.

### Ejercicios Varios

44. Obtener el máximo descuento de la tabla facturas correspondiente a cada año.
45. Obtener una consulta de la tabla cliente que muestre el codigo postal de aquellas ciudades que tengan 2 o mas clientes.

---

## Concatenación Interna de Tablas

Se realiza a través de 2 pasos

1. Generar el producto cartesiano de ambas tablas, o sea, generar todas las combinaciones posibles de las filas de ambas.

2. Generar las filas que interesan entre todas las generadas en el paso anterior.


46. Mostrar el nombre de cada ciudad junto con el nombre de la provincia a la que pertenece.

```
select * from ciudades, provincias
where ciudades.cod_prov = provincias.codpro
```
```
select * from ciudades
inner join provincias on ciudades.cod_prov = provincias.codpro;
```

### Uso de Alias

Si los nombres de las tablas aparecen repetidamente y además son extensos, SQL proporciona un mecanismo para construir un alias de cada tabla y que se indica a continuación del nombre de la tabla y luego se puede emplear como reemplazo en cualquier sitio de la sentencia.


NOTA: en sentencias complejas, con más de 2 tablas, es recomendable utilizar el alias en todas las columnas, pues mejora las busquedas sobre las mismas por parte del DBMS.

**Sintaxis**


```
select * from ciudades C
inner join provincias P on c.cod_prov = p.codpro;
```

### Inner Join

Concatena internamente las tablas según las columnas indicadas explícitamente.

The INNER JOIN keyword selects records that have matching values in both tables.

**Sintaxis**

```
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```

47. Obtener el total de cada factura emitida, teniendo en cuenta el descuento y el IVA mostrando:
ID cliente, nro de factura, fecha e importe o monto total de cada factura.


### Using

Si las columnas que participan en la concatenación tienen el mismo nombre, se pueden utilizar en la clausula USING.

---

---

---

# DDL

## CREAR UNA BASE DE DATOS

```
create database if not exists `Atenciones`
USE Atenciones
```

## CREAR UNA TABLA


Solo son obligatorios los CAMPOS, no así las restricciones.

```
create database if not exists `Atenciones` ( 'nro_reg' int(11) NOT NULL,
'cod_os' int(11) not null, 'dni1 int(11) not null,
'fecha' date not null, primary key ('nro_reg'),
constraint `c1` check(`cod_os`>0))
```

La restricción después de check revisará que el código ingresado para la obra social sea mayor a cero.


## Restricciones (constraints)

Permiten que la BD no sea un mero almacen de información sin ningún tipo de relación entre los datos.

Su nombre debe ser único para toda la BD.

## Check

Sentencia que se utiliza para definir una restricción

## BORRADO DE TABLAS

Una tabla se puede borrar siempre y cuando no exista ninguna otra tabla en la BD que la referencie.

Ejemplo: no puedo borrar la tabla articulos si antes no borro la tabla linea de factura, porque la tiene como foreign key.

```
DROP TABLE nombre_tabla
```

## Alter Table (Modificación de Tablas)

Se realiza a través de la instrucción **ALTER TABLE**

```
alter table nombre_table
[add column def_campo restricción]
[modify column def_campo]
[drop column nombre_columna]
[constraint nombre_restriccion]
```

Para la eliminación de campos y restricciones se requiere únicamente indicar el nombre del campo. Para el resto de los campos es necesario especificar la definición completa del campo o la restricción.

La modificación de una tabla puede presentar, según el tipo de operación, restricciones debido a definiciones anteriores.

- No se puede borrar una columna que se utiliza en una restricción. Primero borrar la restriccion, luego la columna.

- No se puede eliminar una restricción que sea eliminada por otra. Por ejemplo, la PK de una tabla que sea referenciada en una FK de otra tabla.

- Si todos los valores almacenados de una columna no cumplen *a prior* con una nueva condición añadida de tipo **check** , esta no se implementará, o bien, que la tabla esté vacía.

- No se puede modificar una columna a **not null** a no ser que todos los valores de dicha columna sean **no nulos** o vacíos.

---
---
---

```
select codcli, avg(dto)
from facturas
where id_factura > 1000
group by codcli
having avg(dto) < 0
```

En este caso primero tiene en cuenta el where, los agrupa y una vez que están conformados los grupos, selecciona aquellos que cumplan con la condición.

(PREGUNTA DE PARCIAL)

En este ejemplo, el DBMS toma la tabla facturas, deja solo aquellas cuyo id es mayor a 1000, agrupa por código de cliente, y aplica restricciones de grupo y, finalmente, muestra.

---
---
---

# REGLAS NEMOTÉCNICAS PARA AGRUPAR FILAS


### Reglas de Oro

- Todo lo que aparece en el **select** o **having** deben ser funciones de grupos o estar en el **group by** .

Ejemplo INCORRECTO:

```
select codcli, avg(dto), iva
from facturas
where id_factura > 1000
group by codcli
having avg(dto) < 0
```

**IVA no va.**

### Regla de Plata

- Las funciones en columna y grupo no pueden aparecer en el **WHERE** . Porque el **WHERE** está aplicado a cada una de las filas, por lo tanto, no puede haber una función de grupo.


### Regla de Bronce

- No hace falta agrupar cuando se devuelve un solo dato.

---

## Tipos de Datos Más Comunes en María DB

### Tipos numéricos

Existen tipos de datos numéricos, que se pueden dividir en 2 grandes grupos, los que están en coma flotante (con decimales y los que no.

1. **TinyInt**:
    
    Es un número entero con o sin signo. Con signo el rango de valores válidos va desde -128 a 127. Sin signo, el rango de valores es de 0 a 255.
    
2. **Bit** o **Bool**:
    
    Un número entero que puede ser 0 ó 1.
    
3. **SmallInt**:
    
    Número entero con o sin signo.
    
    - Con signo el rango de valores va desde -32768 a 32767.
    - Sin signo, el rango de valores es de 0 a 65535.
4. **MediumInt**:
    
    Número entero con o sin signo:
    
    - Con signo: el rango de valores va desde -8.388.608 a 8.388.607.
    - Sin signo: el rango va desde 0 a 16.777.215
5. **Integer, Int**:
    
    Números entero con o sin signo:
    
    - Con signo: el rango va de valores desde -2147483648 a 2147483647.
    - Sin signo: el rango va desde 0 a 4294967295
6. **BigInt**:
    
    Número entero con o sin signo.
    
7. **Float**:
    
    Número pequeño en coma flotante de precisión simple.
    
8. **xReal, Double**:
    
    Número en coma flotante de precisión doble.
    

### Tipos DATE

Tipo fecha, almacena una fecha. El rango de valores va desde el 1 de enero del 1001 al 31 de diciembre de 9999. El formato de almacenamiento es de año-mes-día.

1. DateTime:
    
    El formato de almacenamiento es de año-mes-dia horas:minutos:segundos.
    
2. TimeStamp:
    
    El formato de almacenamiento depende del tamaño del campo.
    
3. Time:
    
    Almacena una hora. El formato de almacenamiento es de ‘HH:MM:SS’
    
4. Year:
    
    Almacena un año. El rango de valores permitidos va desde el año 1901 al año 2155. El campo puede tener tamaño 2 o 4.
    

### Tipos de cadena:

1. Char(n):
    
    Almacena una cadena de longitud fija. La cadena podrá contener desde 0 a 255 caracteres.
    
2. Varchar(n):
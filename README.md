# PL - SQL

[Curso completo de Oracle PLSQL desde cero en Español para principiantes](https://www.youtube.com/playlist?list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB)

[Video 1 - Bloques PL/SQL](https://www.youtube.com/watch?v=l6wOghW_gNI&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=1)

```sql
DECLARE --no obligatoria
-- SECCION DECLARATIVA
BEGIN
-- SECCION EJECUTABLE
EXCEPTION --no obligatoria
-- MANEJO DE EXCEPCIONES (SI HAY UN ERROR EN SECCION EJECUTABLE)
END; --FINAL DE PROGRAMA
```

**TIPOS DE BLOQUES:**

- **Bloques anonimos** = Se construyen de forma dinamica y se construyen una sola vez. No tienen nombre.
- **Bloques con nombres** = Se ejecutan de forma dinamica y se ejecutan una sola vez (Procedures, Functions, Triggers)
- **Disparadores (Triggers)** = Bloques que se almacenan en la BD, no suelen cambiar despuess de su construccion, se ejecutan seguido.

[Video 2 - Variables](https://www.youtube.com/watch?v=HfZk8Bu1Lf8&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=2)

```sql
DECLARE
		identificador  integer := 50;
		nombre         varchar2(25) := 'Raphael Nicaise';
		apodo          char(10)  := 'Rapha';
		sueldo         number(5) := 30000;
		comision       decimal(4,2) := 50.20;
		fecha_actual   date := (sysdate);
		fecha          date := to_date('2020/07/08','yyyy/mm/dd');
		saludo         varchar2(50) default 'Buen dia';
BEGIN
	dbms_output.put_line('El valor de identificador es: ' || identificador);
	dbms_output.put_line('Nombre: ' || nombre);
	dbms_output.put_line('Apodo: ' || apodo);
	dbms_output.put_line('Sueldo: ' || sueldo);
	dbms_output.put_line('Comision: ' || comision);
	dbms_output.put_line('Fecha actual: ' || fecha_actual);
	dbms_output.put_line('Fecha: ' || fecha);
	dbms_output.put_line(saludo);
END;
```

**default**, = asignamos valor a variable por defecto, osea si no se le coloca nada.

**dbms_output.put_line()** para mostrar mensajes, concatenar con | |. Despues de finalizar salta de linea.

dbms_output.put() lo mismo pero no hace el salto de linea al final.

Las variables se pueden inicializar en la seccion declarativa, como tambien en el bloque de instrucciones.

```sql
dbms_output.put_line(concatenar || 'concatenar' || variable); 
```

**DataTypes**

- integer = numero entero
- varchar2(25) = varchar2 limita caracteres, pero si sobran, borra el espacio sobrante.
- char(10) = en cambio char asigna 10 caracteres como limite aunque pongas 'a' ocupa 10.
- number(5) = permite alojar numeros con puntos, (n) caracteres de numeros.
- decimal(4,2) =  4 numeros, dos con com.
- date = para guardar fecha (:= sysdate para colocarle la fecha del sistema actual)
- clob = permite guardar grandes cadenas de texto.

[Video 3 - Constantes](https://www.youtube.com/watch?v=T1Ppp_iBa5M&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=3)

```sql
DECLARE
	mensaje constant varchar2(30) := 'Buenos dias a todos';
	numero constant number(6) := 30000;
BEGIN
	mensaje := 'Intentamos modificar variable constante';
	-- saltara un error porque a mensaje no se le puede asignar otro valor
	dbms_output.put_line(mensaje);
	dbms_output.put_line(numero);
END;
```

**Constant** se le asigna a una variable, para que esta no se pueda modificar mientras el programa se este ejecutando.

**Error : PLS-00363: expression 'variable constante' cannot be used as an assignment target**

[Video 4 - Condicionales](https://www.youtube.com/watch?v=XSJ1L41LUxI&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=4)

**IF | ELSE**

```sql
DECLARE
		a number(2) := 10;
		b number(2) := 20;
BEGIN
		IF a > b THEN
		-- bloque si condicion verdadera
		    dbms_output.put_line(a || ' es mayor que ' || b);
		ELSE
		-- bloque si condicion falsa
				dbms_output.put_line(b || ' es mayor que ' || a);
		END IF; -- FINALIZA EL BLOQUE IF
END;
```

**IF | ELSIF | ELSE**

```sql
DECLARE
		numero number(3) := 100;
BEGIN
		IF (numero=10) THEN
				dbms_output.put_line('Valor de numero es 10');
		ELSIF (numero=20) THEN
				dbms_output.put_line('Valor de numero es 20');
		ELSIF (numero=30) THEN
				dbms_output.put_line('Valor de numero es 30');
		ELSE
				-- ELSE SE EJECUTA SI NINGUNA CONDICION FUE VERDADERA
				dbms_output.put_line('Ninguna de los valores fue encontrado');
		END IF;
		dbms_output.put_line('El valor exacto de la variable es: ' || numero);
END;
```

[Video 5 - Bucles introduccion](https://www.youtube.com/watch?v=xLNXQhaqitk&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=5)

Si condicion de bucle es True, entonces se volvera a ejecutar repetidamente, hasta que esta sea falsa.

**LOOPS**

```sql
--loop basico
loop
  -- secuencia de instrucciones
  -- CONDICION DE SALIDA LA PONEMOS ADENTRO CON UN IF Y UN EXIT
end loop;

--while loop
while condicion loop
	--secuencia de instrucciones
	-- EL LOOP SE EJECUTA MIENTRAS CONDICION VERDADERA
	-- HACER ALGO 
end loop;

--for loop
for contador in valor1..valor2 loop -- RANGO DE valor1 hasta valor2
	--secuencia de instrucciones
end loop;
```

**LOOP BASICO**

```sql
DECLARE
	valor number:=10;
BEGIN
		LOOP
				dbms_output.put_line(valor); 
				valor := valor + 10; -- aumenta en 10 por cada iteracion
				IF (valor>50) THEN -- se ejecuta cuando valor sea > a 50
						EXIT;  -- CUANDO SE EJECUTA EXIT SALE DEL BUCLE
				END IF;
				-- ES LO MISMO A DECIR
		-- EXIT WHEN valor > 50;
				
		END LOOP;
		dbms_output.put_line('Valor final: ' || valor);
END
```

```sql
IF (valor>50) THEN      -- es lo mismo       
		EXIT;               <============>       EXIT WHEN valor > 50;
END IF;
```

[Video 6 - Strings](https://www.youtube.com/watch?v=f0jAj5ZEBSk&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=6)

```sql
DECLARE 
		nombre varchar2(20);
		direccion varchar2(30);
		detalles clob;
		eleccion char(1);
BEGIN
		nombre := 'Pedro Perez';
		direccion := 'Calle Mitre';
		detalles := 'Este es el detalle de la variable clob que iniciamosen la seccion declarativa, es una variable de gran almacenamiento';
		eleccion := 'y';
		IF eleccion = 'y' THEN
			dbms_output.put_line(nombre);
			dbms_output.put_line(direccion);
			dbms_output.put_line(detalles);
		END IF;
END;		
```

```sql
DECLARE
		saludo varchar2(12) := 'HOLA a todos';
BEGIN
		dbms_output.put_line(UPPER(saludo)); -- HOLA A TODOS
		dbms_output.put_line(LOWER(saludo)); -- hola a todos
		dbms_output.put_line(INITCAP(saludo)); -- Hola A Todos
		dbms_output.put_line(SUBSTR(saludo,1,4)); -- H
		--Devuelve los valores de la cadena desde posicion 1, 4 caracteres
		dbms_output.put_line(INSTR(saludo,'o')); -- 9
END;
```

UPPER(string) = Transforma a mayusculas todo el texto colocado dentro.

LOWER(string) = Transforma a minusculas todo el texto colcado dentro.

INITCAP(string) = Transforma a Mayuscula la primer letra de cada palabra despues de un espacio.

SUBSTR(string,valor,desde) = Devuelve valor de string hasta una x posicion.

INSTR(string,letra) = Devuelve la posicion de la letra en el string.

```sql
-- Comentario
/* 
Comentario
de varias
lineas
*/
```

```sql
DECLARE
		saludo varchar2(30) := '####Hola a todos####';
BEGIN
		dbms_output.put_line(RTRIM(saludo,'#')); -- ####Hola a todos
		dbms_output.put_line(LTRIM(saludo,'#')); -- Hola a todos####
		dbms_output.put_line(TRIM('#' from saludo)); -- Hola a todos
END;
```

RTRIM(string,caracter) = Corta todos los caracteres, iguales al indicado, del lado derecho

RTRIM(string,caracter) = Corta todos los caracteres, iguales al indicado, del lado izquierdo

TRIM(caracter from string) = Corta todos los caracteres, iguales al indicado, en todo el string.

[Video 7 - Bucle While](https://www.youtube.com/watch?v=3WKIgsNUBB0&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=7)

Bloque While repite una sentencia, siempre que la condicion sea verdadera, en el momento que sea falsa, el sistema ejecuta el siguiente proceso.

```sql
DECLARE
		valor number(2) := 10;
BEGIN
		WHILE (valor < 20) LOOP
				dbms_output.put_line('El valor es: ' || valor);
				valor := valor + 1;
		END LOOP;
END;
```

```sql
DECLARE
		numero number := 0;
		resultado number;
BEGIN
		WHILE (numero <= 10) LOOP
				resultado := 3*numero;
				dbms_output.put_line('3x'||numero||' = '||resultado);
				numero:=numero+1;
		END LOOP;
END;
```

[Video 8 - Bucle FOR](https://www.youtube.com/watch?v=uQr7AyxpnWc&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=8)

El bucle FOR, permite ejecutar una sentencia de instrucciones, un numero especifico de veces, controlando estas repeticiones, en un rango determinado. Por cada repeticion, la variable (definida automaticamente en el for) del contado, va a ir incrementando/decrementando.

**FOR contador IN inicio..fin LOOP = Para incrementar contador**

```sql
DECLARE
		-- no se inicializa la variable numero para el contador
BEGIN
				FOR numero IN 10..20 LOOP -- de 10 a 20.
						dbms_output.put_line('Valor de numero:'||numero); 
						-- 10
						-- 11
						-- 12..
				END LOOP;
				-- dbms_output.put_line(numero); afuera no va a funcionar porque no esta declarada
END;
```

FOR contador IN REVERSE FIN..INICIO LOOP = Para decrementar contador

```sql
-- no hace falta poner el declare ya que no tenemos que declarar ninguna variable
BEGIN
		FOR f IN REVERSE 0..5 LOOP
				dbms_output.put_line('Valor de f: '||f);
		END LOOP;
END;
```

[Video 9 - **Bucles Anidados**](https://www.youtube.com/watch?v=R2awAyXe33U&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=9)

```sql
BEGIN -- tabla del 1 al del 10, del 1 al 10
		FOR i IN 1..10 LOOP
				FOR j IN 1..10 LOOP
						dbms_output.put_line(i||' x '||j||' = '||i*j);
				END LOOP;
		END LOOP;
END;
```

```sql
DECLARE
		bucle1 number:=0;
		bucle2 number;
BEGIN
		LOOP
				dbms_output.put_line('----------------------------');
				dbms_output.put_line('Valor bucle externo = '|| bucle1);
				dbms_output.put_line('----------------------------');
				bucle2 := 0;
				LOOP
						dbms_output.put_line('Valor bucle anidado = '|| bucle2);
						bucle2 := bucle2+1;
						EXIT WHEN bucle2=5;
				END LOOP;
				bucle1 := bucle1+1;
				EXIT WHEN bucle1=3;
		END LOOP;
END;
```

[Video 10 - Matrices](https://www.youtube.com/watch?v=xUXEbL4istA&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=10)

- El Indice INICIAL de la matriz es siempre **1**
- Se pueden inicializar arrats mediante el metodo construtctor **varray.**
- Los arrays, en PL/SQL, son unidimensionales
- Los valores son null por default cuando es declarada, y deben inicializarse para poder hacer referencia a sus elementos.
- varray(N) → N cantidad de elementos

```sql
DECLARE
    type tipo_array_paises is varray(5) of varchar2(20); -- Creamos un tipo de dato que sea un array que contenga varchars
    nombre tipo_array_paises; -- matriz nombre con el tipo de dato definido en tipo_array_paises
BEGIN
    array_paises := tipo_array_paises('Argentina','Brasil','Peru','Mexico','Rep Dom'); -- creado objeto de tipo_array_paises
    FOR i IN 1..5 LOOP -- Recorre cada elemento de la matriz
        dbms_output.put_line('Nombre:' || array_paises(i)); -- array(i) para ingresar a los indices
    END LOOP;
END;
```

```sql
DECLARE
    type matriz_nombres is varray(5) of varchar2(20);
    type matriz_edades  is varray(5) of integer;
    nombres matriz_nombres;
    edades matriz_edades;
    total integer;
BEGIN
    nombres := matriz_nombres('Raphael','Hugo','Ulises','Roman','Julio');
    edades := matriz_edades(19,32,18,18,35);
    total := nombres.count; -- Devuelve la cantidad de elementos del arreglo
    FOR I IN 1..total LOOP
        dbms_output.put_line('Nombre: ' || nombres(i) || ' Edad: ' || edades(i));
    END LOOP;
END;
```

- **array.count** → devuelve la cantidad de valores existentes del array (no cuenta los null)

[Video 11 - Procedimientos Almacenados](https://www.youtube.com/watch?v=Df-QuB-LXo8&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=11)

- Un Stored Procedure es un programa de PL/SQL que puede recibir y devolver informacion, utilizando parametros de entrada y salida opcionalmente.
- Tipos:
    - A nivel de esquema.
    - Dentro de un package.
    - **Dentro de un bloque PL/SQL.**
- Partes:
    - **Parte declarativa** → para los procedimientos que tienen parametros de entrada y salida, y donde se definen las variables.
    - **Parte ejecutable** → Donde se ejecutan las sentencias
    - **Manejo de excepciones →** (Opcional)

```sql
CREATE OR REPLACE PROCEDURE saludo
AS
BEGIN
    dbms_output.put_line('Hola');
END saludo;

-- Ejecutar seleccionando cada uno
BEGIN
    saludo;
END;
-- Otra manera
EXECUTE saludo;
```

Al ejecutar este script, se compila, y por lo tanto se crea el objeto SP en la base de datos.

```sql
CREATE OR REPLACE PROCEDURE aumentar_precio
AS
BEGIN
        update libros set precio = precio + (precio*0.1);
END aumentar_precio;
```

```sql
-- Ver stored procedures creados
SELECT * FROM user_objects WHERE OBJECT_TYPE = 'PROCEDURE';
-- Ver cada procedure con otros detalles
SELECT * FROM user_procedures WHERE OBJECT_NAME LIKE '%SALUDO%'
-- Borrar un procedimiento
DROP PROCEDURE saludo;
```

[Video 12 - Procedimientos Almacenados Parte 2](https://www.youtube.com/watch?v=NzMkYNDkcEU&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=12)

**Parametros de entrada en SP**

CREATE OR REPLACE PROCEDURE name (param1 IN/OUT datatype) AS …

```sql
 -- Tabla y datos de prueba
 create table empleados(
  documento char(8),
  nombre varchar2(20),
  apellido varchar2(20),
  sueldo number(6,2),
  fechaingreso date
 );

insert into empleados values('22222222','Juan','Perez',300,to_date('10/10/1980','dd/mm/yyyy'));
insert into empleados values('22333333','Luis','Lopez',300,to_date('12/05/1998','dd/mm/yyyy'));
insert into empleados values('22444444','Marta','Perez',500,to_date('25/08/1990','dd/mm/yyyy'));
insert into empleados values('22555555','Susana','Garcia',400,to_date('05/05/2000','dd/mm/yyyy'));
insert into empleados values('22666666','Jose Maria','Morales',400,to_date('24/10/2005','dd/mm/yyyy'));
```

```sql
CREATE OR REPLACE PROCEDURE aumentarsueldo(anio IN number,porcentaje IN number)
AS                                         -- 2 parametros
BEGIN
  update empleados set sueldo = sueldo+(sueldo*porcentaje/100)
  where (EXTRACT(YEAR FROM current_date)- EXTRACT(YEAR FROM fechaingreso)) > anio;
				-- extrae el anio del current date, osea 2024 menos el year de fechaingreso
				-- y eso lo compara con anio, los que tengan mas anios, que lo indicado, se les aumennta por el porcentaje indicado
END aumentarsueldo;

BEGIN
   aumentarsueldo(10,20); -- aumenta 20% a los que tengan 10 anios o mas en la empresa
END;
```

```sql
CREATE OR REPLACE PROCEDURE ingresar_empleado 
    (doc IN char,nombre IN varchar2, apellido IN varchar2)
AS
BEGIN
    INSERT INTO empleados values(doc,nombre,apellido, NULL, current_date);
END ingresar_empleado;

BEGIN
    ingresar_empleado('50203600','Raphael','Nicaise');
END;
```

[Video 13 - Procedimientos Almacenados Parte 3](https://www.youtube.com/watch?v=NzMkYNDkcEU&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=12)

**Variables en SP**

```sql
CREATE OR REPLACE PROCEDURE autorlibro(atitulo IN varchar2)
AS
    v_autor varchar2(20); -- variable interna del procedimiento
BEGIN
    select autor into v_autor from libros where titulo = atitulo; 
    -- guarda en una variable v_autor, el autor del libro con el titulo indicado
    insert into  tabla1 select titulo,precio from libros 
    -- y eso lo inserta en la tabla uno
    where autor = v_autor;
END autorlibro;

begin
    autorlibro('El Quijote');
end
```

[Video 14 - FUNCIONES](https://www.youtube.com/watch?v=NzMkYNDkcEU&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=12)

- Al igual que los SP, son bloques de codigo que permiten agrupar y organizar sentencias PL/SQL, que se ejecutan, al llamar la funcion. Contienen la seccion declarativa y la seccion de ejecucion, pero en diferencia a los SP, las funciones tienen el return
    
    **return** → retorna el valor deseado, osea el valor que devuelve la funcion
    
    CREATE OR REPLACE FUNCTION f_prueba(valor NUMBER)
    

```sql
CREATE OR REPLACE FUNCTION f_prueba(valor NUMBER) -- SIEMPRE VA A SER IN
RETURN NUMBER -- Que tipo de dato va a retornar
IS
BEGIN
	RETURN valor*2; -- EL RETURN ES OBLIGATORIO
END;

declare
    valor1 NUMBER := 3;
    valor2 NUMBER;
begin
    valor2 := f_prueba(valor1);
    dbms_output.put_line(valor2); -- 6
end;

select f_prueba(3) as total from dual; -- DUAL ES UNA PSEUDOTABLA VACIA
																			 -- PARA PROBAR FUNCIONES ETC
```

```sql
CREATE OR REPLACE FUNCTION f_costo(valor NUMBER)
RETURN varchar2
IS
    costo varchar2(20); -- variables a usar en la funcion
BEGIN
    costo:= '';
    IF (valor <= 500) THEN
        costo := 'Economico';
    ELSE
        costo := 'Costoso';
    END IF;
    RETURN costo;
END;

select f_costo(400) from dual; 

-- TAMBIEN SE PUEDE RETORNAR DIRECTAMENTE DESDE OTROS LUGARES DEL CODIGO
CREATE OR REPLACE FUNCTION f_costo(valor NUMBER)
RETURN varchar2
IS  
BEGIN
    IF valor <= 500 THEN
        RETURN'Economico'; -- termina la funcion y devuelve 'Economico'
    else 
        RETURN 'Costoso';
    END IF;
END;
```

Ejemplo de PROC Y FUNCIONES

```sql
DECLARE
    suma NUMBER := 0;
    numero NUMBER;
    suma_total NUMBER := 0;
BEGIN
    FOR i IN 1..10 LOOP
        dbms_output.put_line('Tabla del '|| i);
        FOR j IN 1..10 LOOP
            numero := j*i;
            suma := numero + suma;
            dbms_output.put_line(i || ' x ' || j  || ' = ' || numero);
        END LOOP;
        dbms_output.put_line('Suma de todos los numeros de la tabla del ' || i || ': ' || suma);
        suma_total := suma_total + suma;
    END LOOP;
    dbms_output.put_line('Suma de la suma de todas las tablas: '||suma_total);
END;
-- EL CODIGO DE RECIEN SE TRANSFORMA EN ESTO

-- FUNCION PARA SUMAR TODOS LOS VALORES DE UNA TABLA EN CONCRETO
-- TABLA DE 3, SUMA 3 + 6 + 9 + 12, asi hasta el 3*10
CREATE OR REPLACE FUNCTION calcular_suma_tabla(atabladel IN number)
RETURN NUMBER
IS
    suma NUMBER := 0;
BEGIN
    FOR i IN 1..10 LOOP
        suma := suma + atabladel*i;
    END LOOP;
    RETURN suma;
END;
-- PROCEDIMIENTO PARA MOSTRAR UNA TABLA, QUE DENTRO CONTIENE LA FUNCION DE SUMAR
CREATE OR REPLACE PROCEDURE mostrar_tabla 
(atabladel IN number)
-- RECIBE COMO PARAMETRO LA TABLA, SI INGRESAS 1, MUESTRA LA TABLA DEL 1
AS
    multiplicacion NUMBER;
    suma_tabla NUMBER;
BEGIN
    dbms_output.put_line('Tabla del '|| atabladel);
    FOR i IN 1..10 LOOP
        
        multiplicacion := atabladel * i;
        dbms_output.put_line(atabladel ||' x '|| i ||' = '|| multiplicacion);
    END LOOP;
        suma_tabla := calcular_suma_tabla(atabladel);
        dbms_output.put_line('Suma de la tabla del '||atabladel||' = '|| suma_tabla);
        dbms_output.put_line(' ');
END mostrar_tabla;

-- CODIGO PL/SQL PARA LLAMAR AL PROCEDIMIENTO
BEGIN
    FOR i IN 1..10 LOOP
        mostrar_tabla(i);
    END LOOP;
END;
```

[Video 15 - Condicional CASE](https://www.youtube.com/watch?v=gDj5bRrpHgQ&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=15)

- Un if else anidado ↔ Case

```sql
case variable -- tiene que ser de un caracter
	when 1 then --bloque de codigo -- when variable = 1
	when 2 then -- bloque de codigo
	when 3 then -- bloque de codigo
	else -- bloque de codigo si no
end case;
```

```sql
create or replace function f_diasemana(numero int)
return varchar2
is
    dia varchar2(25);
begin
 dia := '';
    case numero
        when 1 then dia := 'Lunes';
        when 2 then dia := 'Martes';
        when 3 then dia := 'Miercoles';
        when 4 then dia := 'Jueves';
        when 5 then dia := 'Viernes';
        when 6 then dia := 'Sabado';
        when 7 then dia := 'Domingo';
        else dia := 'No es un numero correcto';
    end case;
    return dia;
end

SELECT f_diasemana(1) from dual;
```

```sql
create or replace function f_trimestre (fecha date)
return varchar2
is
    mes varchar2(20);
    trimestre number;
begin
    mes := extract(month from fecha);
    trimestre := 0;
    case mes
        when 1 then trimestre := 1;
        when 2 then trimestre := 1;
        when 3 then trimestre := 1;
        when 4 then trimestre := 2;
        when 5 then trimestre := 2;
        when 6 then trimestre := 2;
        when 7 then trimestre := 3;
        when 8 then trimestre := 3;
        when 9 then trimestre := 3;
        else trimestre :=4;
    end case;
    return trimestre;
end

select ojh.employee_id,ojh.start_date,ojh.end_date,ojh.job_id,ojh.department_id 
from oehr_job_history ojh;

select ojh.employee_id,f_trimestre(ojh.start_date) as "Entro en Trimestre",
f_trimestre(ojh.end_date) as "Se fue en Trimestre",ojh.job_id,ojh.department_id 
from oehr_job_history ojh;
-- por cada registro, le aplica la funcion a los campos seleccionados
```

[Video 16 -Triggers](https://www.youtube.com/watch?v=MfRjk5AKAiI&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=16)

- Sirven para conservar la integridad referencial y la coherencia entre los datos entre distintas tablas
- Registrar cambios que se efectuan sobre las tablas y la identidad de quien los realizo
- Realizar cualquier accion cuando una tabla es modificada
- Insertar, actualizar o eliminar datos de una tabla asociada de forma automatica

**Reglas:**

- No pueden ser invocados directamente
- Al intentar modifcar los datos de una tabla asociada, el trigger se ejecuta automaticamente
- No reciben ni retornan parametros
- No generan resultados de consultas SQL

**Clasificacion:**

- Momento en el que se dispara:
    - Before → Se ejecuta antes de la sentencia
    - After → Se ejecuta despues de la sentencia
- El evento que lo dispara: Segun se ejecute una de estas sentencias sobre la tabla
    - Insert
    - Update
    - Delete
- Nivel:
    - Depende de si se ejecuta para cada fila afectada en la sentencia (por cada fila)
    - O una unica vez por sentencia independientemente de las filas afectadas

```sql
-- DDL para las tablas control y libros
 create table libros(codigo number(6),titulo varchar2(40),autor varchar2(30),editorial varchar2(20),precio number(6,2));
 create table control(usuario varchar2(30),fecha date);
```

```sql
create or replace trigger tr_ingresolibros
before insert -- Esto se ejecuta cuando se detecte una insercion en libros, antes 
on libros -- tabla en la que se detectera la insercion
begin
    insert into control values (user, sysdate); -- accion
    -- user devuelve el usuario de la sesion, y sysdate la fecha actual
end tr_ingresolibros;

insert into libros (CODIGO,TITULO,AUTOR,EDITORIAL,PRECIO) 
values (3231,'Aprendiendo Triggers','Yo','PL/SQL Editorial',3);
-- Cuando insertemos los datos, se va a ejecutar el trigger
-- Se ejecuta una vez por cada vez que hagamos la sentencia insert, aunque se inserteb varios registros
select * from libros;
select * from control;
```

```sql
SELECT * FROM USER_TRIGGERS WHERE TRIGGER_NAME = 'TR_INGRESOLIBROS';
-- Para ver la informacion del trigger
```

[Video 17 -  Triggers FOR EACH ROW](https://www.youtube.com/watch?v=xkhGEFEH_Ec&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=17) 

- Se va a activar el trigger por cada registro que se ingresa en una tabla, y no por sentencia

```sql
-- DDL para tabla de ejemplo
CREATE TABLE empleados (documento char(8),apellido varchar2(30),nombre varchar2(30),seccion varchar2(20));
-- Truncate vacia toda la tabla, pero no la borra
TRUNCATE TABLE control;
-- Dropear Trigger
DROP TRIGGER tr_ingresaempleado;

```

```sql
create or replace trigger ingresaempleados
before insert -- para cada REGISTRO ingresado en empleados, antes ejecutar el begin end
on empleados -- si no pusiesemos for each row, seria por cada insercion, que pueden ser varias filas
for each row -- para cada registro ingresado

begin
    insert into control values (user,sysdate); -- ingresamos esto a la tabla por cada registro ingresado en empleados
end ingresaempleados;
```

```sql
INSERT ALL
     into empleados values('22333444','ACOSTA','Ana','Secretaria')
     into empleados values('22777888','DOMINGUEZ','Daniel','Secretaria')
     into empleados values('22999000','FUENTES','Federico','Sistemas')
     into empleados values('22555666','CASEROS','Carlos','Contaduria')
     into empleados values('23444555','GOMEZ','Gabriela','Sistemas')
     into empleados values('23666777','JUAREZ','Juan','Contaduria')
SELECT * FROM dual; -- MANERA EN PL/SQL de hacer inserts en conjunto

-- por cada insercion, se inserto un registro en control
```

[Video 18 -  Triggers BEFORE DELETE](https://www.youtube.com/watch?v=cxxxXU3gkDE&list=PL2Z95CSZ1N4EO3wqFmTBNZXCovLpxkEqB&index=18) 

- Una accion después de detectar un delete en una tabla

```sql
-- DDL y DML para ejemplos
create table alumnos(
legajo varchar2(4) not null,
documento varchar2(8) not null,
nombre varchar2(30) not null,
curso number(1) not null,
materia varchar2(15) not null,
nota_final number(3,2) not null);

INSERT ALL
 into alumnos values('A234','23333333','LOPEZ ANA',5,'MATEMATICA',9)
 into alumnos values('A345','24444444','GARCIA CARLOS',6,'MATEMATICA',8.5)
 into alumnos values('A457','26666666','PEREZ FABIAN',6,'LENGUA',3.2)
 into alumnos values('A348','25555555','PEREZ PATRICIA',6,'LENGUA',7.85)
 into alumnos values('A123','22222222','PEREZ PATRICIA',5,'MATEMATICAS',9)
 into alumnos values('A124','32222222','GONZALES JOSE',5,'BIOLOGIA',9)
 into alumnos values('A124','32222222','GONZALES JOSE',5,'MATEMATICAS',8)
SELECT * FROM DUAL;
```

```sql
create or replace trigger tr_borradoalumnos
before delete
on alumnos
for each row
	-- Por cada registro eliminado, se registrara en la tabla control
begin
    insert into control values (user, sysdate);
end tr_borradoalumnos;

select * from alumnos;
delete from alumnos where nota_final < 8; -- se borran 2 registros
-- por cada registro eliminado, el trigger tr_borradoalumnos
-- registra una fila en control con datos
```

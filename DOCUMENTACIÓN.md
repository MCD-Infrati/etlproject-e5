# Documentación proceso ETL

## Integrantes

- Arlex Pino
- Andrés Ocampo

## Pasos a ejecutar

Antes de iniciar con la documentación, es importante hacer una anotación importante. Los pasos 1 y 2 se ejecutaron con el propósito de generar al final un listado códigos únicos de la variable PID (llave). Esto lo hicimos con el propósito de asegurarnos que todos los cruces posteriores con las distintas bases de datos (pasos 3 a 6) resulten correctos. Habiendo dicho esto, a continuación se describen los pasos que se llevaron a cabo:

**1. Cargue de bases de datos BSMNT (Mongo) y la base amesdbtemp (Elephant) elección únicamente de codigos PID:** Este paso consistió en el cargue de dos bases, bsmnt de Mongo y amesdbtemp (Elephant). Es importante anotar que aunque en este paso se cargaron todas las variables de la base, en los nodos posteriores (en la imagen, "Valores_BSMNT" y "Valores Elephane") se eligieron solamente las que referenciaban al código PID, pues recordemos que, como se decía anteriormente, estos primeros dos pasos se ejecutan con el único propósito de dejar al final un listado de códigos únicos. Se realiza entonces el join entre estas dos bases, mientras que los nodos que siguen después de este nodo: "Null_J(B_E)2, "Concatena_J(B-E)", y así hasta llegar al nodo "Ordena_F-J(B-E)" comprende una serie de operaciones de transformación sobre el campo PID, que al final del flujo nos permite tener los valores únicos requeridos.

![1](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/7e28dd82-015f-4f5b-b8d2-1fa5064ba158)

**2: Cargue de archivo CSV AmesProperty y generación de listado de códigos únicos:** Se realizó inicialmente el cargue del archivo CSV AmesProperty. Seguidamente, se realiza el join entre este archivo y el archivo generado en el paso anterior que resultó de la unión de las bases bsmnt (Mongo) y amesdbtemp (Elephant). Seguidamente, se realizan los mismos pasos de depuración del campo del código para poder tener al final el listado de códigos únicos requeridos. 

![2](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/21c6590e-4711-4428-8203-fe3d88eee395)

**3. Cargue de base de datos completa BSMNT (Mongo) y unión:** En este paso se cargó la base bsmnt de Mongo. Recordemos que aunque esta base ya se cargó en el paso 1, en ese paso no se seleccionaron todas las variables, puesto que los pasos 1 y 2 se ejecutaron con el propósito de dejar un listado único de PID, por lo que esa era la única variable de interés en esos pasos. Ahora, entonces, se carga la base completa bsmnt y se aplica la primera transformación que consistió en el reemplazo de valores nulos (NA para variables cualitativas y 0 para cuantitativas). Seguidamente, se hace el join con la base de listados únicos resultante de la aplicación de los pasos 1 y 2.

![3](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/7f57c6d8-7f71-48f9-82e1-66244ffd6d01)

**4. Cargue de bases de datos completas de Elephant, transformaciones y unión:** En este paso se cargaron de forma completa todas las tablas que están en Elephant. En la imagen abajo se deja la consulta SQL que permitió el cargue de estas tablas en solo una. En esta consulta se puede apreciar que se realiza la transformación del cálculo del total de baños. Seguidamente se realiza la otra transformación requerida, que es la extracción del mes y del año del campo Sale Date. Seguidamente, se aplica otra transformación requerida que es la creación del nuevo campo "Gr Live Area" que se creó a partir de la suma de los tres campos 1st Flr SF, 2dn Flr SF y Low Qual Fin SF. Luego entonces se hace el join entre la base resultante de este paso, y la anterior que se había generado ya en el paso 3. 

![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/08ea202e-aa42-4db9-8542-23d94d15d2ff)

![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/a48e6198-afb8-4e42-8cb2-509159673147)

**5. Cargue de archivo CSV AmesProperty, transformación y unión:** En este paso se carga el archivo CSV AmesProperty. Seguidamente, se realiza la otra transformación requerida que consistió en la imputación de los valores de la variable "Year Built" a los valores nulos de la variable "Year Remod/Add". Se realizó posteriormente el join entre la base resultante de este paso y la que se había generado ya en el paso 4. 

![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/578b4ba1-4aa1-4b40-9138-77a5313f29b1)

**6. Cargue de bases restantes, transformación y unión para generación de archivo final:** En este paso final, se cargan el resto de bases que son garage, misc y pool, todas provenientes de Mongo. En el caso de garage, se evidencia que tiene algunos valores nulos, por lo que se realiza la transformación requerida que consistió en el reemplazo de nulos (NA para variables cualitativas y 0 para cuantitativas). Seguidamente, se hace un join entre la base resultante de esta transformación y la que ya se había generado en el paso 5. Se hace lo mismo para base misc, a la cual no se le aplica transformación alguna de nulos pues no tiene; se hace una unión entre esta base y la resultante hasta el momento. Luego, se hace exactamente lo mismo para la base pool. En el nodo final "Select values 2" se depuran algunas variables y se renombran otras, esto con el fin de guardar completa coherencia con el orden y nombramiento de las variables. Al final, se genera entonces el archivo requerido.

![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/af7d1273-d034-4c9d-b40b-faa1d689bbcc)

**OUTPUS RESULTANTES DEL PROCESO:**

- ARCHIVO_FINAL (csv): contiene el archivo de salida en formato .csv con todas las variables requeridas.
- ETL_FINAL (ktr): archivo de Pentaho que contiene todo el pipeline con los pasos anteriores ejecutados.
- DOCUMENTACIÓN (.md): archivo actual el cual contiene toda la documentación de los pasos ejecutados.





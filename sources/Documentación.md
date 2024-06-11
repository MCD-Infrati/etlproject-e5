# Documentación proceso ETL

## Integrantes

- Arlex Pino
- Andrés Ocampo

## Pasos a ejecutar

**1. Cargue de bases de datos de MongoDB:** Este paso consistió en el cargue en pentaho de las cuatro colecciones de MongoDB: BSMT, garage, misc y pool. Esto se hizo a través de los nodos de carga de Mongo que tiene pentaho como se puede apreciar en la siguiente imagen:

![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/55f1f9a2-1b9d-477b-85ea-86305284a467)

**2: Reorganización de campos en las bases de datos de MongoDB:** Se realizó una reorganización de las variables en cada una de las cuatro colecciones de MongoDB tal como lo pedía el enunciado.

![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/6c9347aa-374d-4493-ab15-c184994f1616)

![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/a3e84c0b-6e72-48b0-a871-dc0e47dd70a5)

![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/7ab3368c-f2db-450a-9efc-c469ef8d1569)

![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/bc92b89c-ad50-4934-8965-e21a83c11db8)

**3. Realización de joins entre las bases de datos de MongoDb:** Este paso consistió en el uso de un nodo multiway merge de pentaho, a través del cual se realizaron los joins entre bsmnt y garage. Posteriormente, esta base resultante se unió con la base misc. Finalmente, la base resultante de estas uniones se unió
con la última base pool. Esto se muestra en la siguiente imagen.

 ![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/a6ccfc40-c725-4f23-b1ce-586a9d5b55a9)

 **4. Selección de variables:** De la base resultante del punto 3. se realiza una selección de variables tal como se muestra en la siguiente imagen:

 ![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/aa67295e-2d03-4060-9e3a-e349959a3d9e)

 **5. Aplicación de filtro:** Se aplica un filtro a través del cual se desea sacar de la base de datos todos aquellos registros que tengan el valor de PID null. Se genera entonces una base sin estos nulos (text file output).

![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/ef2463bc-0462-4e8b-be77-64e481ab8990)

**6: Cargue de bases de datos de Elephant:** Se ingresa a la aplicación web de ElephantSQL y allí se crea la instancia "Proyecto_ETL_E5". Luego, se ejecuta el script "scriptAmesDB.sql", para entonces subir los datos de la carpeta scriptDatos. En la siguiente imagen se presenta el script SQL de la consulta a Elephant:

![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/6bab16c5-af2b-4972-bd7c-5b8fea052308)






# Documentación proceso ETL

## Integrantes

- Arlex Pino
- Andrés Ocampo

## Pasos a ejecutar

**1. Cargue de bases de datos de MongoDB:** Este paso consistió en el cargue en pentaho de las cuatro bases de datos de MongoDB: BSMT, garage, misc y pool. Esto se hizo a través de los nodos de carga de bases de datos de Mongo que tiene pentaho como se puede apreciar en la siguiente imagen:

![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/6aa1c0d7-c24d-4b64-ab3c-a988d3d95da5)

**2. Realización de joins entre las bases de datos de MongoDb:** Este paso consistió en el uso de un nodo multiway merge de pentaho, a través del cual se realizaron los joins entre bsmnt y garage. Posteriormente, esta base resultante se unió con la base misc. Finalmente, la base resultante de estas uniones se unió
con la última base pool. Esto se muestra en la siguiente imagen.

 ![image](https://github.com/MCD-Infrati/etlproject-e5/assets/126924740/a6ccfc40-c725-4f23-b1ce-586a9d5b55a9)




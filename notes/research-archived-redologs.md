# Archived Redo Logs    

## Entrevista

* __Entrevistado__: Francisco Cabral DBA BDI

* __Preguntas__:
  __Que son los Archive de Oracle?__
  __R.__ *son archivos que contiene todas la informacion en tiempo real de las bases de datos y es el primer paso antes de la escritura en los redologs, tablespace y datafiles*

  __Cual es la relacion entre Redologs y Archived?__
  __R.__ *La relacion es que los Archived son el paso previo a la escritura de los redologs; cuando un archived se concluye estos se convierten en redologs*

  __Que beneficios o con que fin se utilizan los archived?__
  __R.__ *Se utilizan con el fin de poder contar con un punto de retorno de la base de datos con todas las transacciones al momento; se utiliza para poder salvar la base de datos completa en caso de caida de lo servidores, hader espejos de base de datos, replica. Su mayor  beneficio es la posibilidad de una restauracion lo mas real posible*

  __Que prerequisito se necesitan para utilizarlos?__
  __R.__ *el principal prerequisito es que se necesita activar la base de datos en ARCHIVEDLOGS mode on, el cual viene por defecto desactivado; esto es recomendable para base de datos de produccion no laboratorio porque el consumo de recursos es significativo*

## Investigacion

  __¿Qué son?__
  __R.__ Son los archivos que se graban antes que los redologs y estos archivos son resultados del proceso de archiving de la base de datos. Hay que hacer la salvedad de que esto solo es posible si la base de datos se cuenta en "ARCHIVELOG mode".EJemplo:
  ```
  LOG_ARCHIVE_DEST = '/disk1/arc'
  LOG_ARCHIVE_DUPLEX_DEST = '/disk2/arc'
  ```
  __¿Dónde se ubican ?__
  __R.__ esto se ubican donde describamos en la propiedad del init de la base de datos LOG_ARCHIVE_DEST y LOG_ARCHIVE_DUPLEX_DEST

  __¿Cómo se utilizan (ejemplo práctico)?__
  __R.__ Este se pueden activar al momento de la creacion de la base de datos con el comando dbca como se muestra en la imagen [active-archived.JPG](resources\images\active-archived.JPG) o con el siguientes proceso:

  ```SQL
  --1. primero debemos bajar la base de datos, con el fin de realizar un backup pues vamos a realizar una cambios significativo en la base de datos.
  SHUTDOWN
  --2. Luego modificamos el init file con los parametros necesario e iniciamos la base de datos pero sin abrir las conexiones.
  STARTUP MOUNT

  --3. Activamos el archive mode y abrimos las conexiones
  ALTER DATABASE ARCHIVELOG;
  ALTER DATABASE OPEN;

  --4. Bajamos nuevamente la base de datos y realizamos un backup nuevamente con el fin de restaurarla hasta ese punto pues ninguno de los backup anteriores nos servira leugo de activo el archive mode
  SHUTDOWN IMMEDIATE;
  ```

  __¿Por que utilizar?__
  __R.__ Una razon por la cual utilizar el "ARCHIVEDLOG mode" cuando no se puede permitir perder ninguna transaccion realizada en la base de datos por cuestion de fallos en el disco. Uno de las razones por el cual utilizar es que si no estan activo el archive mode no se podra recuperar la base de datos no mas del ultimo backup realizado, con archivelogs mode se puede restablecer todas las transaccion subsecuentes.

  Se puede utilizar con el fin de hacer un recover de la base de datos, actulizar una base datos de stantby y obtener informacion historica de la base de datos utilizando el LogMiner.

  __¿Cuando se graban?__
  __R.__ Esto se graban por el LogWriter de forma inmediata cuando la transaccion es envianda a la base de datos. Como lo podemos ver en la imagen del [spotlight.jpg](..\resources\images\spotligth.jpeg)
  __Beneficios__
  __R.__
  * Backup con la base de datos abierta y usuarios trabajando
  * Respaldo de todas las transaccion realizadas hasta la fecha
  * Facilitar la posiblidad de un ambiente de espejo.

## Fuentes
* What Is the Archived Redo Log? - https://docs.oracle.com/cd/B28359_01/server.111/b28310/archredo001.htm#ADMIN11329
* Managing Archived Redo Logs - https://docs.oracle.com/cd/B19306_01/server.102/b14231/archredo.htm

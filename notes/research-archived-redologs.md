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

* __Conclusiones__:

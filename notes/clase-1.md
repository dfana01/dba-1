# Clase 1 - DBA I

## Notas

* __Nota Importante__: mayoria de problema de instalacion es por cuestion de que el SID no ha sido exportado en la session del usuario debe verificar el .bashrc y/o exportarla manual
* Storage de la instalacion:
..* Avanzado: se utiliza cuando se tiene un arreglo de disco o un meto de almacenamiento diferente a un solo disco
..* Basico: Se utiliza cuando se tiene un solo disco y se utilizara el OS stanalone
* Oracle Linux 6.8: es el OS que estaremos utilizando en la clase

* Enlace por defecto de entreprise manager: https://ora6.fcld.acl:1158/em

* lsnrctl: comando para el manejo de listener

* Informacion para la instalacion:
  * Nombre maquina: ora5.fcld.acl
  * [Particiones](../resources/images/particiones.jpg):
    * desc  | espacio | tipo
    * /swap | 8gb     | vg
    * /boot | 500mb   | vg
    * /     | 25gb    | vl
    * /opt  | resto   | vl
  * root/codigolibre

* Orden de lectura:
  1. Básico
  2. Fundamentos
  3. Administración
  4. Lectura del manual del hipopótamo
  5. Comandos DBA
  6. Práctica DBA1

## Procesos

### Instalacion de Oracle

* Imagen de Instalacion: V138414-01 - Oracle Linux 6 Update 8 for x86 64 bit, 3.7 GB.iso

* Pasos abstractos para instalar ORACLE
  1. Edit hostname con el fin de que el nombre de la maquina sea resuelto, es necesario para utilizara el asistente de instalacion de oracle
  2. Instalar los paquetes necesario para el software (DBMS) de oracle. ref: utilizar recursos install-oracle.txt
  3. Agregar usuario y grupos necesarios par el correcto funcionamiento de Oracle
  4. Agregar directorios necesarios y asignar los dueños y grupos correctos
  5. Modificar el .bashrc del Oracle para que tenga las variables necesarias
  6. Modificar los parametros de kernel y otros necesarios
  7. Adquirir archivos de instalacion del software (DBMS)
  8. Instalar software (clase servidor para un servidor de base de datos). Nota: si se instala remoto utilizar el parametro -X con el fin de que el asistente suba en la maquina remota
  9. Ejecutar comandos especificados por el asistente de oracle
  10. Instalar y verificar entreprise manager. Usar url del final del curso.


## Recursos

### Archivos:
* [oracle_ofa_whitepapaer.pdf](../resources/others/oracle_ofa_whitepapaer.pdf): descripcion de las buenas practicas para la instalacion de oracle database and software
* [install-oracle.txt](../resources/others/install-oracle.txt): proceso resumido de la instalacion de oracle en Oracle Linux
* [comandos-gnu-dba.pdf](../resources/books/comandos-gnu-dba.pdf): comandos para un dba
* [gnu-certifice-oracle-administrator.pdf](../resources/books/gnu-certifice-oracle-administrator.pdf): practica para admnistra base de datos oracle
* [gnu-oracle-administrator.pdf](../resources/books/gnu-oracle-administrator.pdf): libro de administracion para base de datos oracle

## Comandos:

* __du__: espacio en un directorio
* __rpm -e__: desistalar un paquete
* __kill__: enviar señales a un procesos
* __‎hostname -I__: ip máquina
* __dbca__: crear instancia y base de datos (debe ejecutarse con usuario oracle y con el software instalado)

## Paquetes
* rwwrap: paquete para mejorar el sqlplus con historia

## Libros:

* Oracle RMAN

## Tarea
  * Traer descrito el uso de cada uno de los usuario principales de la instalacion en oracle
    * Usuario
      * __SYS__: es el dueno de la base de datos que contiene los diccionario de datos.Es un usuario el cual tiene los dictionarios de datos del sistema y se utiliza con fines administrativos
      * __SYSTEM__: es el administrador de la base de datos desde su creacion tiene permisos de dba. Igual que SYS se utiliza con fines administrativos
      * __DBSNMP__: Este usuario se utiliza con el fin de manejar componentes de el enterprise manager
      * __SYSMAN__: Se utiliza para realizar tareas administrativas en el EM. se puede utilzia sys o system para estos fines tambien
    * Fuentes:
      * Administering Roles: https://docs.oracle.com/cd/B16351_01/doc/server.102/b14196/users_secure002.htm#CFHBHBAH
      * Overview of Users and Security: https://docs.oracle.com/cd/B16351_01/doc/server.102/b14196/users_secure001.htm
      * Administering User Accounts and Security: https://docs.oracle.com/cd/E11882_01/server.112/e10897/users_secure.htm#ADMQS007

  * Traer investigacion de los "Archieved Oracle" de oracle: [research-archived-redologs.md](notes\research-archived-redologs.md)

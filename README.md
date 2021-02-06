# CURSO DE INTRODUCCION A LA TERMINAL Y LINEA DE COMANDOS

## Windows Subsystem for Linux (WSL): Cómo acceder a la terminal en Windows

- Distribución de Linux recomendada: Ubuntu.
- Requisitos:
	1. Tener acceso como administrador de la computadora para hacer la instalacion.

1. Comencemos abriendo una terminal Window PowerShell (como administrador)
2. escribe el siguiente comando: Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
3. Reinicia tu computadora
4. Al reiniciar estará todo listo para instalar tu distribución favorita
5. Ingresa a la tienda de Windows:
6.  Buscar Linux
7. Escoger distribucion favorita: Ubuntu es de las mas famosas.
8. Instalar y lanzar.

### COMANDOS PARA MOVERSE EN LA TERMINAL

`ls`
-Permite ver todos los archivos en un directorio

`ls -a`
-Para ver todos los archivos listados incluso los ocultos

`pwd `
-para identificar el directorio (Print Working Directory) 

`cd`
-para cambiar de directorio

`cd ~`
-atajo para volver al home (con la virgulilla-el sombrerito de la ñ-)

`cd -`
-atajo para regresar al ultimo directorio visitado


### COMANDOS PARA ORGANIZAR ARCHIVOS

`mkdir [nombre del directorio]`
-para crear un directorio o carpeta (make directory)

`cp [nombre de archivo a copiar] [directorio al cual copiar/]`
-copiar un archivo

`rm [nombre de archivo a borrar]`
-borrar un archivo

`mv [nombre del archivo a mover]`
-mover un archivo

`rmdir`
-eliminar directorio (remove directory). Primero borrar los archivos del directorio para poder borrar el directorio

## Manejo de archivos de texto y utilidades interactivas

### TIPOS DE ARCHIVOS
- Binarios
	- Programas ejecutables
	- Archivos de datos
- Texto
	- Contenido legible por humanos	

### Utilidades interactivas
- VIM
	- Para salir con :q 
	- Para guardar con :w
- NANO
	- Contiene ayudas
- EMACS
	- Flexible
	- Customizable

## Utilidades Batch
Programas que procesan texto y emiten un resultado

**cat**: Nos muestra el contenido completo de un archivo
ejemplo: cat tables.txt

**head:** Nos muestra las primeras lineas (También podemos escoger cuantas lineas queremos utilizando el modificador [-n #]).
Ejemplos:

1. head tables.txt
2. head -n 5 tables.txt

**tail**: Muestras las ultimas lineas del final (Inverso a head, tambien le funciona modificadores)
Ejemplos:

1. tailtables.txt
2. tail -n 5 tables.txt

### Utilidades Batch Avanzadas:

**grep:** Permite trabajar con expresiones regulares, funciona como un buscador dentro del archivo.
Ejemplos:

1. **grep hanks dump1.sql** = [comando][expresión regular][archivo]

2. Para buscar sin importar si esta en mayuscula o miniscula:
 **grep -i hanks dump1.sql**
 
3. Tambien podemos buscar una expresión de una frase que termine con la misma palabra que estemos buscando:
**grep -i “hanks’),$” .**

#### **SED**
Screem Editor, tratamiento de flujos de caracteres. Este comando nos permite reemplazar una expresión por otra.

Ejemplos:

1. **sed ‘s/hanks/selleck/g’ dump1.sql **= [comando][subcomando- sustitución][expresión original][nueva expresión][modificador-(/g de global, indica que tiene que hacerse a lo largo de todo el flujo)][Indicar cual es el flujo a utilizar (Archivo de texto)]

*SED no modifica el archivo, lo que hace es crear un nuevo flujo con la modificación*

Para eliminar la ultima linea podemos utilizar:

**sed ‘$d’ nuevasPelis.csv = [Comando][’$sub-comando’][archivo]**

#### AWK
Trataminento de texto delimitado, este comando sirve para trabajar con archivos de textos delimitados por comas.
Ejemplos:

1. awk -F ‘;’ ‘{ print $1}’ nuevasPelis.csv


## Trabajo fundamental con archivos de texto

touch: nos permite crear archivos.
> touch archivo.txt

cat: nos permite visualizar todo el contenido de nuestros archivos.
> cat archivo.txt

head: es muy parecido al comando cat. También nos permite visualizar el contenido de nuestros archivos, pero debemos indicarle cuántas líneas nos debe mostrar. Por defecto nos mostrará las primeras 10.

**primeras 10 líneas**
> head archivo.txt

**primeras 20 líneas**
> head -n 20 archivo.txt

tail: funciona igual que el comando head, pero al revés. También debemos indicarle cuántas líneas nos debe mostrar, la diferencia es que no las mostrará de abajo hacia arriba. Por defecto nos mostrará las últimas 10.

**últimas 10 líneas**
> tail archivo.txt

**últimas 5 líneas**
> tail -n 5 archivo.txt

### Búsqueda y tratamiento de texto

Imagina que tenemos un archivo gigante, con cientos o incluso miles de líneas.

Se vuelve más complicado si necesitamos que las palabras que buscamos cumplan ciertas condiciones, como solo mayúsculas o minúsculas, que la siguiente o anterior palabra cumpla ciertas condiciones, etc.

En estos casos podemos utilizar el comando **grep **para filtrar las líneas que queremos visualizar utilizando (o no) expresiones regulares:

>grep “palabra-clave” archivo_gigante.txt

Si nos da igual si la palabra clave incluye mayúsculas o minúsculas podemos utilizar el flag -i:
>grep -i “pAlaBra-cLAvE” archivo_gigante.txt

También podemos verificar si la línea incluye esta palabra clave al final:

>grep “palabra-clave$” archivo_gigante.txt

O si la incluye al principio:
>grep “^palabra-clave” archivo_gigante.txt

También hay situaciones donde necesitamos modificar un poco la información que obtenemos de un archivo de texto.

Por ejemplo, imagina que nuestro archivo contiene un poema, frase o saludo para responderle a los usuarios de nuestra aplicación. El problema es que cada usuario tiene un nombre diferente.

>¡Hola, NOMBRE_USUARIO! Felicitaciones por completar tu desafío con PUNTOS_USUARIO puntos.

No queremos editar este archivo. Solo necesitamos cambiar los caracteres NOMBRE_USUARIO por el verdadero nombre del usuario.

Para esto podemos utilizar el comando **sed**. Solo debemos indicarle que queremos realizar una sustitución (s/), la palabra que vamos a cambiar (NOMBRE_USUARIO), la nueva palabra que vamos a incluir (Ana) y cerrar con el símbolo /.

> sed ‘s/NOMBRE_USUARIO/Ana/’ archivo-saludo.txt

Ahora imagina que, además del nombre, debemos cambiar también la puntuación que obtuvo el usuario:

> sed ‘s/NOMBRE_USUARIO/Ana/; s/PUNTOS_USUARIO/35/’ archivo-saludo.txt

Puedes ver muchos más usos del comando sed en este [tutorial](https://likegeeks.com/es/sed-de-linux/. "tutorial")


## Comunicación entre procesos: Qué son y cómo se utilizan los flujos estándar

### Flujos estandar
- Entrada

- Salida 

- Error
Aveces queremos diferenciar la salida de errores que no queremos que salga por el canal convencional

### Procesamiento de datos
Conectados a los puertos comunes
comando < archivo :ejecutar archivo descrito
comando > archivo :la salida se guarde en un archivo
comando >> archivo :agregar el resultado al archivo existente
ls -l >> archivo.txt
ls -l | more :el pipe encadena el resultado al siguiente comando
wc :Cuenta cuantas lineas tiene el archivo

>cat archivo.txt | wc -l

Cuenta cuantas lineas tiene el archivo + cuantas palabras hay + cuantos caracteres.
>wc -c bytes

>wc -m caracteres

>wc -l lineas

>wc -L maximo display

>wc -w palabras


## Administración de procesos en background y foreground


[![Administracion](administracion "Administracion")](https://imgur.com/ylDUsUm "Administracion")

## Permisos sobre archivos: El sistema de permisos octal

Todos los archivos de linux tienen:

- Dueno
- Grupo 
- Otros 


Permisos y operaciones
- Lectura 
- Escritura
- Ejecucion 

Alterar permisos asociados
- chmod (cambia individualmente los permisos)
- chown (cambia el propietario del archivo)
- chgrp (cambia grupo de usuarios que pueden acceder)

> $chmod -o-w nombre_archivo.txt 



| chmod-o-w nombre_archivo.txt  |  Modifica los permisos de un archivo o directorio para los usuarios. o Para otros usuarios. -w (write) quitar elpermiso de escritura al archivo  |
| ------------ | ------------ |
|  chmod+x nombre_archivo.txt |   Modifica los permisos de un archivo nombre_archivo.txt o directorio para los usuarios.  +x(Execute) agrega el permiso de ejecutar a todos los usuarios|
| chmod 760 nombre_archivo.txt  |  7 todos los permisos lectura (r) escritura (w) y ejecucion(x) para el usuario propietario. 6 permisos de lectura (r) y escritura (w) para el grupo.  0 denegado todos los permisos para otros usuarios|
|  sudo nombre_comando | permite ejecutar comandos nombre_comando con permisos especiales (comandos que no se dejan ejecutar por cualquier usuario) como si fuera el root (administrador)  |
|   sudo chown nombre_usuario nombre_archivo.txt|  cambia el propietario de un archivo nombre_archivo.txt por otro usuario del sistema nombre_usuario |
| sudo chgrp nombre_grupo nombre_archivo.txt  |  cambia el grupo de un archivo nombre_archivo.txt por otro grupo del sistema nombre_grupo |




## Sistemas de manejo de paquetes
### Paquetes de Software:

Existen programas que se descargan e instalan sus archivos de programa en lugares ya indicados y se configuran para que dicho programa pueda correr en la computadora. Los paquetes de software se encargan de realizar todo lo anterior dicho.
.
### Administradores de Paquetes:

Estos son los que conocen de donde realizar las descargas, que otros paquetes ya están instalados en nuestro sistema y como configurar todo, a medida que no haya conflicto.

### Paquetes binarios
- apt
- zypper
- rpm

1. > sudo apt-get update

2. > sudo apt install lynx

lynx es un navegador de linea de comandos. 

### Paquetes de lenguajes

- pip 
	Es para Python
	ejemplo: [sudo][pip][install][pandas] = pandas es el nombre de la librería.

- composer
	PHP
	
- npm
	NODE.JS

### Otros:

Existen unos nuevos manjadores de paquetes que pretenden ser mas genéricos instalando tanto paquetes binarios como de lenguajes.
- conda
- homebrew

------------

## Herramientas de compresión y combinación de archivos

### Archivos .gz:
Comprimir: gzip archivo.txt
Descomprimir: gzip -d archivo.txt.gz
 


### Archivos .tar:
Empaquetar: tar cf paquete.tar /carpeta/a/empaquetar/
Ver contenido del paquete: tar tf paquete.tar
Empaquetar y ver contenido empaquetado: tar -cvf paquete.tar /carpeta/a/empaquetar/
Desempaquetar: tar xf paquete.tar
 

### Archivos .tar.gz:
Empaquetar y Comprimir: tar czf empaquetado.tar.gz /carpeta/a/empaquetar/y/comprimir
Descomprimir: tar xzf archivo.tar.gz



------------


## Herramientas de búsqueda de archivos

### Busqueda de archivos
#### locate
Funciona mediante una base de datos que debe ser explicitamente actualizada periodicamente
#### whereis
Para ubicar archivos binarios. Especialmente interesante cuando tenemos varias versiones de un mismo ejecutable
#### find

>find [ruta] [expresión_de_búsqueda] [acción]
 
##### Ruta
Si no se indica una ruta se toma en cuenta entonces el directorio donde se este actualmente, es decir el directorio de trabajo actual, que es lo mismo que indicar con un punto “.”.
 
Es posible asignar mas de una ruta de búsqueda también como por ejemplo

> find /etc /usr /var -group admin
 

##### Búsquedas básicas 👍
Algunas banderas que podemos utilizar para buscar:

- name = Busca nombre de un archivo

	*iname = Igual que name pero este no toma en consideración si tiene alguna mayúscula*

- user = El usuario propietario

- group = El grupo propietario

- type = tipo de archivo, f para directorios

 
##### Búsquedas a través del tiempo ⏰

- mmin = Tiempo en minutos

- mtime = Periodos de 24 horas
 
- exec; El poder aumenta 👊
 
- exec Permite ejecutar acciones sobre el resultado de cada línea o archivo devuelto por find, ejemplo:

> find . -type f -mtime +7 -exec cp {} ./backup/ \;

type = tipo de archivo, f para directorios

f es para files, no directorios. 



------------


Editor.md
Open source online Markdown editor.

​
**export: **Este comando se utiliza para asignar a toda la sesión
Ejemplo: export MI_VAR = mauro, si luego escribimos echo $MI_VAR se mostrará mauro en la terminal. (Este permanecerá miestras dure mi sesión)
.
**var:** Este comando solo asigna el valor para el proximo proceso que se va a ejecutar. este no es muy usual.
Ejemplo: MI_VAR=/home php env.php
​
​
<br>
------------
​
​
## Cómo y para qué escribir scripts en Bash
### Dejar tareas programadas
​
|  Comandos |  Descripcion |
| ------------ | ------------ |
|  service-status-all | Muestra el estado de todos los servicios actualmente   |
| sudo service atd start  |  Inicia el servicio de atd |
|  sudo service cron start |   Inicia el servicio de cron|
| at now + numero_tiempo tiempo_ingles  |  Se ejecuta una tarea despues de un determinado numero_tiempo en unidades tiempo_ingles. Ejemplo: at now +2 minutes  at >echo "mensaje" > ~/archivo/txt. Se sale con Ctrl + D |
|  contab -e | Muestra las tareas que estan programadas de forma periodicas  |
​
[Enlaces Interesantes](https://crontab.guru/ "Enlaces Interesantes")
​
​
​
​
​

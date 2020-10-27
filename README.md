# Git Knowledge

## Básicos de configuración
* COMPROBAR VERSIÓN: ```git --version```
* OBTENER AYUDA: ```git help [comando]```
* SETEAR EMAIL Y NOMBRE: ```git config --global user.name ("nombre")```, ```git config --global user.email ("email")```
* EDITAR FICHERO DE CONFIGURACIÓN GLOBAL: ```git config --global -e```
* LEER FICHER DE CONFIGURACIÓN GLOBAL: ```git config --global -l```
* SI HAY PROBLEMAS CON EL CRLF (caracter de fin de línea): ```git config core.autocrlf true```
* SI HAY PROBLEMAS CON EL CERTIFICADO SSL: ```git config [--global] http.sslVerify false```
* CREAR ALIAS: ```git config --global alias.(alias) "(todo el comando excluyendo 'git')"```. Ejemplo: ```git config --global alias.lg "log --oneline --decorate --all --graph"```. Ahora podemos escribir ```git lg```

## Básicos del repositorio
* CREAR REPO: ```git init```
* COMPROBAR STATUS: ```git status```
* COMPROBAR STATUS PERO MÁS SIMPLE: ```git status -s```
* COMPROBAR STATUS SIMPLE PERO MOSTRANDO LA RAMA: ```git status -s -b```
* AGREGAR TODOS LOS ARCHIVOS CAMBIADOS: ```git add .```
* AGREGAR FOLDER: ```git add (nombre del folder)```
* AGREGAR ARCHIVO: ```git add (nombre del archivo)```
* AGREGAR ARCHIVOS POR EXTENSIÓN DEL DIRECTORIO ACTUAL: ```git add *.(extensión)```
* AGREGAR ARCHIVOS POR EXTENSIÓN DE TODO EL PROYECTO: ```git add "*.(extensión)"```
* COMMITEAR CAMBIOS: ```git commit -m ("texto-del-commit")```
* REVERTIR CAMBIOS (situándonos en el último commit): ```git checkout -- .```
* EXCLUIR UN ARCHIVO AGREGADO: ```git reset (nombre del archivo)```
* RENOMBRAR ARCHIVO: ```git mv (nombre antiguo) (nuevo nombre)```
* ELIMINAR ARCHIVO: ```git rm (nombre del archivo)```
* ELIMINAR Y RENOMBRAR FUERA DE GIT: ```git add -u```, después de eliminar o renombrar en local.

## Básicos de comprobación
* COMPROBAR LOG DEL REPOSITORIO: ```git log```
* COMPROBAR LOG EN UNA LÍNEA: ```git log --oneline```
* MOSTRAR LOG DE TODAS LAS RAMAS EN UNA LÍNEA Y TODO BONITO: ```git log --oneline --decorate --all --graph```

## Viajes en el tiempo
* COMPROBAR CAMBIOS EN LOS ARCHIVOS QUE NO HAN SIDO AÑADIDOS: ```git diff [nombre del archivo/folder]```
* COMPROBAR CAMBIOS EN ARCHIVOS QUE YA FUERON AÑADIDOS: ```git diff --staged [nombre del archivo/folder]```
* SACAR ARCHIVO DEL STAGE: ```git reset HEAD [nombre del archivo/folder]```
* BORRAR CAMBIOS DEL STAGE DEFINITIVAMENTE (usar con precaución): ```git checkout -- [nombre del archivo/folder]```
* GIT ADD + GIT COMMIT A LA VEZ: ```git commit -am ("mensaje")```
* AÑADIR ALGO AL ÚLTIMO COMMIT: ```git commit --amend -m ("nuevo mensaje")```. Útil para modificar el mensaje, pero también para cambios de última hora.
* DESHACER EL ÚLTIMO COMMIT (PARA AÑADIR ALGO MÁS): ```git reset --soft HEAD^```. Después hacemos otro commit y listo, ya hemos rehecho el commit. El --soft hace que deshagamos el commit sin perder los cambios que hicimos. Podemos escribir --hard para deshacer el último commit pero perdiendo los cambios de este. Esto último deberá usarse con precaución.
* VIAJAR A UN COMMIT ANTERIOR, SEA CUAL SEA: ```git reset --soft (commit hash)```
* VER HISTORIAL DE OPERACIONES CON COMMITS QUE HEMOS HECHO: ```git reflog```
* REGRESAR A UN PUNTO FUTURO (INCLUSO SI NOS HEMOS CARGADO COMMITS CON --hard): ```git reset --hard (commit hash deseado)```

## Ramas, merges, conflictos y tags
* CREAR NUEVA RAMA: ```git branch (nombre nueva rama)```
* VER TODAS LAS RAMAS: ```git branch```
* MOVERNOS ENTRE RAMAS: ```git checkout (nombre de la rama)```
* DIFERENCIAS ENTRE RAMAS: ```git diff (rama 1) (rama 2)```

### Fast Forward
* UNIR RAMAS: (Unir cambios de otra rama a la nuestra) ```git merge (nombre de la rama)```. Esto funcionará sin problemas cuando no haya conflictos.
* BORRAR RAMA: ```git branch -d (nombre de la rama)```

### Unión automática
* CREAR NUEVA RAMA Y MOVERNOS A ELLA: ```git checkout -b (nombre nueva rama)```
* UNIR RAMAS: (Unir cambios de otra rama a la nuestra) ```git merge (nombre de la rama)```. Esto funcionará sin problemas cuando no haya conflictos.

### Merge con conflictos
* Unimos ramas de la misma manera que antes, pero en este caso nos dará un mensaje por pantalla con la lista de archivos donde hay problemas.
* Los conflictos se resuelven bien con el plugin de Git para VSCode por ejemplo.
* Los conflictos van a aparecer igualmente si no usamos plugins, y más o menos se ven y se solucionan bien.
* Guardamos los cambios, hacemos el nuevo commit y listo.

### Tags
* Son referencias a commits, para no usar siempre los hashes, que son mucho menos legibles. Cuando creamos un tag, este referencia a nuestro commit actual por defecto.
* CREAR TAG BÁSICO: ```git tag (nombre tag)```
* VER TODOS LOS TAGS DEL REPO: ```git tag```
* BORRAR TAG: ```git tag -d (nombre tag)```
* CREAR TAG DE FORMA COMPLETA: ```git tag -a (version (ej: v1.0.0)) -v ("texto (ej: nombre de la versión)")```
* CREAR TAG A UN COMMIT QUE NO ES EL ACTUAL: ```git tag -a (version) (commit hash) -m ("mensaje")```
* VER TAGS DE FORMA DETALLADA: ```git show (tag version)```

## Git stash y git rebase
### Stash
* GUARDAR CAMBIOS ACTUALES: ```git stash```
* LISTAR LOS STASH: ```git stash list```. Se pueden tener varios, pero no es recomendable, se puede hacer todo un lío.
* RECUPERAR CAMBIOS DEL ÚLTIMO STASH SIN BORRARLO: ```git stash apply```
* RECUPERAR CAMBIOS DEL ÚLTIMO STASH BORRANDO EL STASH: ```git stash pop```. Esto extrae los cambios y elimina el stash. Esto es recomendable si vamos a tener varios stashes.
* RECUPERAR CAMBIOS DE OTRO STASH PASADO: ```git stash apply stash@{(numero del stash)}```
* Si hay conflictos con el stash, deberemos resolverlo después de hacer el pop, y posteriormente comitear los cambios. En este punto, el stash no va a ser borrado y hay que borrarlo a mano.
* BORRAR ÚLTIMO STASH: ```git stash drop```
* BORRAR CUALQUIER STASH: ```git stash drop stash@{(numero del stash)}```
* METER EN EL STASH TODOS LOS ARCHIVOS MENOS LOS QUE YA ESTÁN EN EL STAGE, O AÑADIDOS: ```git stash save --keep-index```
* METER EN EL STASH TODOS LOS ARCHIVOS, INCLUSO LOS QUE NO ESTÁN RECIBIENDO SEGUIMIENTO: ```git stash save --include-untracked```
* MOSTRAR STASH DETALLADAMENTE: ```git show stash [stash@{(numero del stash)}]```
* BORRAR DEFINITIVAMENTE TODOS LOS STASH: ```git stash clear```

### Rebase
* Se utiliza para incluir ciertos commits en mi rama, que en origen no estaban, porque se crearon después de abrirme el nuevo camino.
* HACER UN REBASE: ```git rebase (nombre de la rama a la que quiero rebasar (generalmente master))```. Después de hacer esto satisfactoriamente (si no existen conflictos), podríamos hacer un merge de la rama rebasada sin problemas.
* Podemos hacer otro tipo de rebase, el rebase interactivo, para dar tratamiento a varios commits de nuestra propia rama (ya vemos que el rebase no sólo se utiliza para rebasar ramas ajenas). Esto significa que podemos coger los últimos cuatro commits, por ejemplo, y hacer un squash (juntarlos) de todos ellos.
* REBASE INTERACTIVO: ```git rebase -i HEAD~4```.
* TAMBIÉN PODEMOS HACER UN REBASE INTERACTIVO DE ALGÚN COMMIT EN PARTICULAR (para editar el mensaje, o el commit mismo): ```git rebase -i (commit hash)```

## Git remote, push y pull
* DATO IMPORTANTE: La palabra origin es el nombre que nosotros le damos al repositorio remoto. Es origin por estándar, pero podría ser otro.
* REVISTAR REPOSITORIOS REMOTOS: ```git remote -v```.
* DATO IMPORTANTE: El -u cuando hacemos un push o un pull, se usa para recordar la rama a la que pusheamos, para no tenerla que escribir de nuevo.
* HACER UN PUSH A NUESTRO REPO REMOTO: ```git push origin (nombre de la rama a la que pushear)```
* HACER PUSH DE LOS TAGS CREADOS: ```git push --tags```
* TRAER LOS ÚLTIMOS CAMBIOS DE UNA RAMA REMOTA: ```git pull origin (nombre de la rama remota)```
* CLONAR UN REPOSITORIO: ```git clone (dirección del repositorio remoto)```
* DIFERENCIA ENTRE UN FETCH Y UN PULL: Básicamente, el fetch te dice que han habido cambios, pero no los trae. El pull trae dichos cambios a tu local.
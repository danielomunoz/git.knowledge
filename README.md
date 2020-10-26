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

## Básicos de comprobación
* COMPROBAR LOG DEL REPOSITORIO: ```git log```
* COMPROBAR LOG EN UNA LÍNEA: ```git log --oneline```
* MOSTRAR LOG DE TODAS LAS RAMAS EN UNA LÍNEA Y TODO BONITO: ```git log --oneline --decorate --all --graph```


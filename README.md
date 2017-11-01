# Fundamentos de Git

## Datos Básicos

* Proyecto equivale a Repositorio
* Respositorio central [Método clásico]
* Repositorio Distribuido [Método Git]
* Una Rama es una línea del tiempo de commits
* Un Merge es la unión de una rama con otra
    * Fast-forward -> Merge sin cambios detectados
    * Unión automática -> Merge con cambios detectados pero sin conflictos
    * Union manual -> Merge con conflictos encontrados [Es necesario corregirlos]
* Un Stash es una caja de seguridad donde puedes guardar todos los cambios, y volver a la rama anterior
sin perder ningun cambio

## Comandos

### Comandos Básicos de Configuración

* git --version                           //Permite saber la versión del git instalado
* git help                                //Permite obtener ayuda de git
* git config --global user.name "Name"    //Permite configurar el nombre de la persona que está trabajando con git ahora
* git config --global user.email "Email"  //Permite configurar el email de la persona que está trabajando con git ahora
* git config --global -e                  //Permite editar los elementos que se han añadido a la configuracion global
* git config --global -l                  //Permite listar los elementos que se han añadido a la configuracion global

### Comandos Inicialización Proyecto

* git init                                //Permite inicializar un Proyecto

* git status                              //Permite ver en el estado en que se encuentran los cambios
    * git status -s                       //Permite mostar el estado de los cambios más simplificado (silent)
    * git status -s -b                    //Permite mostar el estado de los cambios más simplificado, pero indicando la rama actual

* git add .                               //Permite añadir todos los archivos al stage
    * git add -- .                            //Permite añadir todos los archivos al stage
    * git add -A                              //Permite añadir todos los archivos al stage
    * git add --all                           //Permite añadir todos los archivos al stage
    * git add *.extensión                     //Permite añadir todos los archivos del directorio actual con .extensión al stage
    * git add "*.extensión"                   //Permite añadir todos los archivos del proyecto con .extension al stage
    * git add carpeta/                        //Permite añadir todos los archivos de la carpeta al stage
    * git add carpeta/*.extension             //Permite añadir todos los archivos de la carpeta con .extensión al stage

* git reset *.extensión                   //Permite excluir del stage los archivos .extension
* git checkout -- .                       //Deshace todos los cambios que no han sido commiteados aún [No queda registro en el log]

* git commit -m "Mensaje"                 //Crea un commit
    * git commit -am "Mensaje"                //Comando que engloba añadir y hacer commit
    * git commit --ammend -m "Mensaje"        //Permite corregir el mensaje del commit HEAD

* git diff                                //Lista los cambios que hay en los archivos
* git diff --staged                       //Lista todos los cambios de los archivos del stage

* git reset HEAD README.md                //Quita el README.md del stage [Queda registro en el log]
    * git reset --soft HEAD^                  //Deshace todos los cambios, pero sin modificar los archivos
    * git reset --mixed id_commit             //Reset commit normal
    * git reset --hard id_commit              //Reset commit + archivos

* git mv "FileOld.txt" "FileNew.txt"      //Permite modificar el nombre de un archivo del repositorio [Commmit needed]
* git rm "File.txt"                       //Permite eliminar un archivo del repositorio [Commit needed]

* git branch ramaX                        //Permite crear una rama
    * git branch                              //Permite ver las ramas que hay actualmente creadas
    * git checkout ramaX                      //Permite cambiarte a una rama determinada
    * git checkout -b ramaX                   //Permite crear y moverse a la rama creada a la vez
    * git branch -d ramaX                     //Permite borrar una rama

* git diff ramaX master                   //Permite ver las diferencias entre dos ramas    
* git merge ramaX                         //Permite hacer un merge [metera la rama ramaX a la rama seleccionada]

### Comandos log

* git log                                 //Permite mostrar un listado de los commits, merges, etc, del proyecto
    * git log --oneline                           //Permite mostrar los logs más simplificados
    * git log --oneline --decorate --all --graph  //Permite mostrar todos los logs más simplificados y con personalizaciones
* git reflog                              //Muestra todos los logs que existen

### Comandos Tags

* git tag Etiqueta                        //Permite crear una etiqueta/tag
    * git tag                                 //Permite ver los tags creados
    * git tag -a v1.0.0 -m "Version 1.0.0"    //Permite crear una etiqueta con versionado
    * git tag -d Etiqueta                     //Permite borrar una etiqueta
    * git tag -a v1.0.0 id_commit -m "M"      //Permite crear una etiqueta para una rama determinada

* git show v1.0.0                         //Permite ver toda la información relativa a una etiqueta


## Stash

* git stash                               //Crea un stash con los cambios actuales y carga el anterior commit
    * git stash save                          //Equivalente a 'git stash'
    * git stash save "Mensaje"                //Permite guardar un stash con un mensaje    
    * git stash save --keep-index             //Guarda todo menos los archivos en el stage (que tiene seguimiento)
    * git stash save --include-untrack        //Incluye todos los archivos, junto a los que no les da seguimiento
    * git stash list                          //Muestra los stash disponibles actualmente
    * git stash list --stat                   //Muestra más información acerca de la entrada
    * git stash apply stash@{i}               //Permite cargar un stash determinado
    * git stash pop                           //Saca los cambios guardados del stash y elimina el stash
    * git stash drop                          //Permite eliminar un stash junto con los cambios almacenados
    * git stash drop stash@{i}                //Permite eliminar un stash junto con los cambios almacenados
    * git stash clear                         //Borra todoas las entradas en el stash

* git show stash                          //Muestra información acerca de el último stash
* git show stash stash@{i}                //Muestra información acerca de un determinado stash

## Rebase

Permite:
    * Ordenar commits
    * Corregir mensajes de los commits
    * Unir commits
    * separar commits

* git rebase master                       //Mueve las ramas al inicio de la rama master
* git rebase -i HEAD~4                    //Muestra los últimos 4 cambios, y permite editar los commits
    * [a] -> Permite editar el archivo
    * [ESC :wq] -> Permite guardar los cambios
* git reset HEAD^
* git rebase --continue

## Remote

* git remote add <remote> <url>           //Te permite añadir un nuevo origen remoto
* git remote -v                           //Te permite ver los origenes que hay agregados a la máquina

### Pull

* git pull <remote> <branch>              //Te permite traer los últimos cambios del repositorio de una rama determinada
* git fetch                                  //Permite realizar un merge no automático
   * git pull
### Push

* git push -f <remote> <branch>              //Te permite subir los últimos cambios a una determinada rama de manera forzada
* git push -u <remote> <branch>              //Te permite subir los últimos cambios a una determinada rama y especificar como predeterminada la rama <branch>
   * git push --tags                         //Te permite añadir todos los tags creados localmente
   
### Clonar repositorio

* git clone <url>
   
## Comandos alias

* git config --global alias.lg "log --oneline --decorate --all --graph"   //Ejemplo de alias para log [git lg]
* git config --global alias.s "status -s -b"                              //Ejemplo de alias para status [git s]

## Ignorar archivos

Crear .gitignore

Añadir linea por línea los archivos que se van a ignorar, y hacer commit de .gitignore para que se guarde en el repositorio. 
Ejemplo:

    1. *.log
    2. data.log
    3. data/
    
 # For more help with markdown
 
 [Markdown](https://guides.github.com/features/mastering-markdown/)

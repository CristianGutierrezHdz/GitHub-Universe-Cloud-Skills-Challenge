
# Procedimientos para crear y modificar un poryecto de Git
___
## Introducción

A medida que las organizaciones crecen, los proyectos que llevan a cabo crecen con ellas. A modo de ejemplo, trabaja en una empresa de software de aviónica que se está embarcando en un proyecto nuevo. El equipo de la empresa quiere que sea el responsable de crear el proyecto.

Decide compilar un sitio web que le permita compartir fotografías de sus gatos con sus amigos y, así, continuar aprendiendo a usar Git en un entorno divertido antes de aplicar esos conocimientos a su trabajo. Se ha propuesto compilar el sitio mediante Git para realizar un seguimiento de los cambios.

En este módulo, podrá iniciar su propio proyecto en Git y adquirir práctica editando algunos errores que pueden existir en el código. Sin duda, Git puede parecer confuso cuando lo utiliza por primera vez, pero a medida que adquiera más práctica en su funcionamiento podrá navegar por él sin problemas.

## Objetivos de aprendizaje
Al final de este módulo, podrá hacer lo siguiente:

  * Descubrir cómo crear un proyecto de Git
  * Entender cómo realizar un seguimiento de los cambios en Git
  * Saber cómo corregir errores sencillos en Git
  * Recuperar archivos eliminados en Git
  
__
## Ejercicio: Inicia de un proyecto

Ahora que ha dedicado tiempo a descubrir los comandos de Git fundamentales, pasaremos a crear un proyecto en Git.

En los ejercicios que siguen, va a agregar un sencillo archivo HTML al árbol de trabajo para empezar a usar Git. Luego va a realizar algunos cambios en el directorio y a aprender a confirmar los cambios.


#### Creación y adición (almacenamiento provisional) de un archivo
Git no hace mucho con los directorios vacíos, así que vamos a agregar un archivo al árbol de trabajo para que actúe como página principal del sitio web de fotos de gatos.

1. Asegúrese de que la sesión de Cloud Shell sigue activa y de que se encuentra en la carpeta del repositorio de nombre Cats.

2. Use un comando `touch` para crear un archivo denominado *index.html*:
``` bash
touch index.html
```

`touch` actualiza la hora de la última modificación de un archivo, si este existe. Si el archivo no existe, Git crea un archivo vacío con ese nombre de archivo.

3. Ahora, use `git status` para obtener el estado del árbol de trabajo:

``` bash 
git status
```

Git responde informándole de que no se ha confirmado nada, pero el directorio contiene un nuevo archivo:

``` bash
No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

    index.html

nothing added to commit but untracked files present (use "git add" to track)
```

Observe que `git status` ofrece sugerencias sobre lo que puede hacer a continuación. Git puede configurarse para que sea menos detallado, pero en esta fase, cuanto más, mejor.

4. Use `git add` para agregar el nuevo archivo al índice de Git, seguido de `git status` para comprobar el estado. *No olvide el punto al final del comando*. Este indica a Git que indexe todos los archivos del directorio actual que se han agregado o modificado.

``` bash
git add .
```

Ahora se ha almacenado provisionalmente una confirmación. El índice de Git es un área de almacenamiento provisional para las confirmaciones. Se trata de una lista de todas las versiones de archivo que van a formar parte de la siguiente confirmación que se haga.

En lugar de `git add .`, podría haber usado `git add index.html`, porque *index.html* era el único archivo nuevo del directorio. Pero si se hubieran agregado varios archivos, `git add .` los habría incluido todos.

5. Por último, vuelva a usar `git status` para asegurarse de que los cambios se han almacenado provisionalmente de forma correcta:

``` bash 
git status
```

6. Debería ver una salida como la de este ejemplo:

``` bash
On branch main

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

    new file:   index.html
```
#### Realización de la primera confirmación
Ahora que index.html se ha agregado al índice, el paso siguiente consiste en confirmarlo.

1. Utilice el comando siguiente para crear otra confirmación:
``` bash
git commit index.html -m "Create an empty index.html file"
```

La *marca* `-m` en este comando indica a Git que está proporcionando un mensaje de confirmación.

Hay muchas maneras de formular mensajes de confirmación, pero una buena pauta consiste en escribir la primera línea de modo que indique lo que la confirmación hace en el árbol. También es habitual poner en mayúsculas la primera letra y dejar fuera el punto final para ahorrar espacio. Imagine que la primera línea del mensaje completa la oración que empieza por "Cuando se inserte, esta confirmación...".

Un mensaje de confirmación puede tener varias líneas. La primera línea no debe tener más de 50 caracteres y debe ir seguida de una línea en blanco. Las líneas siguientes no deben tener más de 72 caracteres. No se trata de requisitos estrictos, y se remontan a los días de las tarjetas perforadas y los terminales "tontos", pero mejoran el aspecto de la salida de `git log`.

2. Git responde con una confirmación de lo que ha hecho:
``` bash
[main (root-commit) 87e874c] Create an empty index.html file
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 index.html
```

3. Realice un seguimiento con un comando `git status` y confirme que el árbol de trabajo está limpio, es decir, que no contiene cambios sin confirmar.

4. Ahora, use un comando `git log` para mostrar información sobre la confirmación:
``` bash 
git log
```

5. La respuesta de Git debería ser similar a este ejemplo:
``` bash
commit 87e874c4aeeb3f9692ae5d9875235353708d7dd5
Author: User Name <user-name@contoso.com>
Date:   Fri Nov 15 20:47:05 2019 +0000

Create an empty index.html file
```

#### Modifique index.html y confirme el cambio.
*index.html* se ha creado para servir como página principal del sitio web, pero actualmente está vacío. El siguiente paso es agregarle algún código HTML. Para hacerlo sencillo, vamos a usar el editor integrado de Cloud Shell para agregar una sola línea de HTML.

1. Abra *index.html* en el editor en línea escribiendo code index.html en el símbolo del sistema de Terminal:

``` bash
code index.html
```

2. Escriba o pegue las instrucciones siguientes en el editor:

``` html
<h1>Our Feline Friends</h1>
```

3. Guarde el archivo y cierre el editor en línea. Puede seleccionar los puntos suspensivos "..." de la esquina derecha del editor de Cloud Shell o usar la tecla de aceleración (Ctrl+S en Windows y Linux, Cmd+S en macOS).

4. Use un comando `git status` para comprobar el estado del árbol de trabajo:
``` bash 
git status
```

5. Puede ver que Git es consciente de los cambios realizados:
``` bash 
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
```

6. Ahora, confirme los cambios:
``` bash 
git commit -a -m "Add a heading to index.html"
```

Observe que esta vez no se ha ejecutado el comando `git add` para almacenar provisionalmente los cambios. En su lugar, usamos la marca `-a` en el comando `git commit`. La opción `-a` agrega todos los archivos que se han modificado desde la última confirmación. No agregará archivos nuevos. Para agregar nuevos archivos, se sigue necesitando `git add`.


7. Compruebe los resultados. Deberían parecerse a los de este ejemplo:
``` bash 
[main 8c9143a] Add a heading to index.html
 1 file changed, 1 insertion(+)
```

Se ha confirmado el cambio en *index.html*. Ahora hay dos versiones del archivo en el repositorio, aunque solo se ve una de ellas (la actual). Una de las ventajas de usar Git es que se pueden revertir los cambios realizados o retroceder en el tiempo y ver las versiones anteriores. Veremos más cosas sobre este tema tan importante más adelante.

___

## Ejercicio: Realización de cambios y seguimiento de estos con Git

La mayoría de los proyectos de desarrollo son iterativos. Se escribe algún código y luego se prueba para asegurarse de que funciona. Luego se escribe más código y se invita a otras personas a contribuir. La iteración significa que hay muchos cambios: adiciones de código, correcciones de errores, eliminaciones y sustituciones.

A medida que trabaje en el proyecto, Git le ayudará a realizar un seguimiento de los cambios que realice. También permite deshacer errores. En los ejercicios siguientes va a continuar compilando el sitio web en el que está trabajando y a aprender algunos nuevos comandos importantes, como `git diff`.

#### Modificación de index.html

La página principal del sitio web, index.html, de momento contiene una sola línea de HTML. Vamos a actualizarla para hacer más cosas y luego a confirmar el cambio en Git.

1. Vuelva a abrir el archivo index.html en el editor en línea de Cloud Shell (`code index.html`) y reemplace el contenido del archivo por el siguiente código HTML:

``` bash
<!DOCTYPE html>
<html>
  <head>
    <meta charset='UTF-8'>
    <title>Our Feline Friends</title>
  </head>
  <body>
    <h1>Our Feline Friends</h1>
    <p>Eventually we will put cat pictures here.</p>
    <hr>
  </body>
</html>
```

2. Guarde el archivo y cierre el editor en línea.

3. Use un comando `git diff` para ver lo que ha cambiado:
``` bash
git diff
```
El formato de salida es el mismo que el del comando `diff` de Unix, y el comando de Git tiene muchas de las mismas opciones. Aparece un signo "más" delante de las líneas que se han agregado, y un signo "menos" indica las líneas que se han eliminado.

El valor predeterminado para comparar el árbol de trabajo con el índice es `git diff`. Es decir, muestra todos los cambios que aún no se han almacenado provisionalmente (agregado al índice de Git). Para comparar el árbol de trabajo con la última confirmación, puede usar `git diff HEAD`.

Si el comando no vuelve al símbolo del sistema después de ejecutarse, escriba `q` para salir de la vista de diferencias.

4. Ahora confirme el cambio. En lugar de usar la marca `-a`, puede asignar explícitamente un nombre a un archivo para que se almacene provisionalmente y se confirme si Git ya lo tiene en el índice (el comando `commit` solo comprueba la existencia de un archivo).
``` bash
git commit -m "Add HTML boilerplate to index.html" index.html
```

5. Use `git diff` de nuevo para comparar el árbol de trabajo con el índice:
``` bash
git diff
```
Esta vez `git diff` no genera ninguna salida porque el árbol de trabajo, el índice y `HEAD` concuerdan.

6. Digamos que decide que "peludo" suena más amigable que "felino". Sustituya las dos apariciones de "Felino" en *index.html* por "Peludo". A continuación, guarde el archivo.

Si ha usado el editor de código integrado con el comando `code`, no verá nada inusual. Pero si ha usado otro editor, como uno llamado sed, es probable que haya creado un archivo index.html.bak que no quiere confirmar. Editores como Vim y Emacs crean archivos de copia de seguridad con nombres como *index.html~* y *index.html.~1\~*, en función de cómo estén configurados.

7. Use el comando siguiente para crear y abrir un archivo denominado *.gitgnore* en el editor de código integrado:
``` bash 
code .gitignore
```

8. Agregue las líneas siguientes al archivo:
``` bash 
*.bak
*~
```
Esta línea indica a Git que omita los archivos cuyos nombres de archivo terminan en *.bak* o ~.

*.gitignore* es un archivo muy importante en el mundo de Git porque impide que los archivos extraños se envíen al control de versiones. Hay archivos *.gitignore* reutilizables disponibles para lenguajes y entornos de programación populares.

9. Guarde y cierre el editor y luego use estos comandos para confirmar los cambios:
``` bash
git add -A
git commit -m "Make small wording change; ignore editor backups"
```

En este ejemplo se usa la opción `-A` con `git add` para agregar todos los archivos sin seguimiento (y no omitidos), así como los que han cambiado, a los archivos que ya están bajo control de Git.

Si en este momento usa `git diff`, la salida estará vacía porque los cambios se han confirmado. Sin embargo, siempre puede usar un comando `git diff HEAD^` para comparar las diferencias entre la confirmación más reciente y la anterior. Pruébelo y vea. No olvide incluir el carácter `^` de cursor de inserción al final del comando.

##### Adición de un subdirectorio
La mayoría de los sitios web usan hojas de estilo CSS y HTML, y el sitio que está compilando no es una excepción. Normalmente, las hojas de estilo se almacenan en un subdirectorio, así que vamos a crear uno llamado CSS y a agregarlo al repositorio.

1. Empiece por crear un subdirectorio llamado CSS en el directorio del proyecto:
``` bash
mkdir CSS
```

2. Luego ejecute `git status`:
``` bash 
git status
```

¿Por qué indica Git que no hay nada que confirmar?

Los usuarios a menudo se sorprenden al saber que Git no considera que agregar un directorio vacío sea un cambio. Esto se debe a que Git solo realiza el seguimiento de los cambios en los *archivos*, no en los directorios.

En ocasiones, especialmente en las fases iniciales de desarrollo, quiere tener directorios vacíos como marcadores de posición. Una convención común es crear un archivo vacío, a menudo llamado *.git-keep*, en un directorio de marcador de posición.

3. Use los comandos siguientes para crear un archivo vacío con ese nombre en el subdirectorio *CSS* y agregue el contenido del subdirectorio al índice:
``` bash
touch CSS/.git-keep
git add CSS
```

4. Vuelva a realizar un seguimiento mediante `git status` para comprobar el estado del repositorio. Confirme que informa de un nuevo archivo.

#### Reemplazo de un archivo
Ahora vamos a reemplazar *.git-keep* por un archivo CSS y a actualizar *index.html* para hacer referencia a él.
1. Elimine .git-keep del subdirectorio CSS:
``` bash 
rm CSS/.git-keep
```

2. Use el editor integrado para crear un archivo denominado *site.css* en el subdirectorio CSS:
``` bash 
cd CSS
code site.css
```

3. Agregue el siguiente CSS al archivo. Después, guarda y cierra el archivo.
``` css 
h1, h2, h3, h4, h5, h6 { font-family: sans-serif; }
body { font-family: serif; }
```

4. Ahora agregue la siguiente línea a *index.html* (no olvide volver al directorio Cats) después de la línea `<title>` y guarde el archivo modificado:
``` html 
<link rel="stylesheet" href="CSS/site.css">
```

5. Use `git status` para ver un resumen de los archivos que han cambiado. Luego, use los siguientes comandos para almacenar provisionalmente los archivos sin seguimiento en el control de versiones y confirmar los cambios en *site.css* e *index.html*:
``` bash 
git add .
git commit -m "Add a simple stylesheet"
```

A diferencia de la mayoría de los VCS, Git registra el contenido de los archivos en lugar de las diferencias (cambios) entre ellos. Esto es en gran medida lo que hace que la confirmación, la bifurcación y el cambio entre ramas sean tan rápidos en Git. Otros VCS tienen que aplicar una lista de cambios que se quieren obtener entre una versión de un archivo y otra. Git solo descomprime la otra versión.

#### Enumeración de las confirmaciones
Ahora que tiene un número razonable de cambios registrados, puede usar `git log` para verlos. Al igual que con la mayoría de los comandos de Git, hay muchas opciones entre las que elegir. Uno de los ejemplos más útiles es `--oneline`.

1. Use el comando siguiente para revisar todas las confirmaciones:
```bash
git log
```

2. Compruebe los resultados. Deben tener un aspecto similar a este ejemplo:
``` bash
commit ae3f99c45db2547e59d8fcd8a6723e81bbc03b70
Author: User Name <user-name@contoso.com>
Date:   Fri Nov 15 22:04:05 2019 +0000

    Add a simple stylesheet

commit 4d07803d7c706bb48c52fcf006ad50946a2a9503
Author: User Name <user-name@contoso.com>
Date:   Fri Nov 15 21:59:10 2019 +0000

    Make small wording change; ignore editor backups
  ...
```

3. Ahora, use este comando para obtener una lista más concisa:
``` bash
git log --oneline
```

4. Vuelva a comprobar la salida. Esta vez debe parecerse a este ejemplo:
``` bash 
ae3f99c Add a simple stylesheet
4d07803 Make small wording change; ignore editor backups
f827c71 Add HTML boilerplate to index.html
45535f0 Add a heading to index.html
a69fe78 Create an empty index.html file
```
Puede ver por qué cuando hay cientos (o miles) de confirmaciones en un proyecto la opción `--oneline` puede ser su mejor aliada. Otra opción útil es `-nX`, donde `X` es un número de confirmación: 1 para la última confirmación, 2 para la anterior, y así sucesivamente. Para verlo, pruebe un comando `git log -n2`.

Hemos avanzado mucho en cuanto al uso de la funcionalidad básica de Git. A continuación, suba de nivel y aprenda a usar Git para recuperarse de errores comunes.

___

## Corrección de errores simples

En ocasiones, algo no sale según lo previsto. Es posible que se olvide de agregar un archivo nuevo o que agregue uno por error. Quizás haya cometido un error ortográfico en la confirmación más reciente o haya confirmado algo que no quería confirmar. Quizás haya eliminado accidentalmente un archivo.

Git le permite realizar cambios sin miedo, porque `siempre` ofrece una manera de volver atrás. Puede incluso cambiar el historial de confirmaciones de Git siempre y cuando cambie solo las confirmaciones que no se hayan compartido.

#### Rectificación de una confirmación: marca --amend

En el ejercicio anterior ha actualizado el archivo `index.html` para modificar la ruta de acceso a la hoja de estilos. Debería haber agregado la siguiente instrucción:
``` html
<link rel="stylesheet" href="CSS/site.css">
```

Imagine que descubre que ha cometido un error al escribir la instrucción. En lugar de especificar la ruta de acceso de la carpeta como `CSS`, ha escrito `CS`:
``` html
<link rel="stylesheet" href="CS/site.css">
```

Al actualizar la página en el explorador, observará que no se aplica la hoja de estilos CSS. Después de investigar, se da cuenta de que ha especificado los valores de la ruta de acceso de forma incorrecta.

Por lo tanto, actualice *index.html* con la ruta de acceso correcta a la hoja de estilos. En este punto bastaría con confirmar la versión corregida de index.html, pero, en lugar de ello, prefiere colocarla en la misma confirmación que la original. La opción `--amend` para `git commit` permite cambiar el historial (¿y con qué frecuencia se tiene la oportunidad de cambiar el historial?).
``` bash
git commit --amend --no-edit
```
La opción `--no-edit` indica a Git que realice el cambio sin cambiar el mensaje de confirmación. También puede usar `--amend` para editar un mensaje de confirmación, para agregar archivos dejados accidentalmente fuera de la confirmación o para quitar archivos agregados por equivocación.

    Nota:
    La capacidad de cambiar el historial es una de las características más útiles de Git. Al igual que la mayoría de las herramientas avanzadas, debe usarse con cuidado. En concreto, es mala idea cambiar las confirmaciones que se han compartido con otro desarrollador, o que se han publicado en un repositorio compartido, como GitHub.

#### Recuperación de un archivo eliminado: git checkout

Imagine que ha realizado un cambio en un archivo de código fuente que ha interrumpido todo el proyecto, por lo que quiere revertir a la versión anterior de ese archivo. Quizás haya eliminado un archivo por completo accidentalmente. Git facilita la recuperación de una versión anterior, incluso aunque la versión actual ya no exista. El mejor aliado en esta situación es el comando *[git checkout][5]*.

[5]: https://git-scm.com/docs/git-checkout

`git checkout` tiene varias utilidades, pero en el siguiente ejercicio se va a usar para recuperar un archivo eliminado. `git checkout` actualiza los archivos del árbol de trabajo para que coincidan con la versión del índice o la del árbol especificado.

Si ha eliminado un archivo por accidente, puede recuperarlo si devuelve la versión del índice al árbol de trabajo con este comando:
``` bash
git checkout -- <file_name>
```

También puede extraer del repositorio un archivo de una confirmación anterior (normalmente, el nivel superior de otra rama), pero el valor predeterminado es obtener el archivo del índice. El objeto `--` de la lista de argumentos sirve para diferenciar la confirmación de la lista de rutas de archivo. No es estrictamente necesario en este caso, pero si tuviera una rama llamada <nombre_archivo> (quizás porque ese es el nombre del archivo en el que se está trabajando en esa rama), `--` evitaría que Git se confundiera.

Más adelante va a aprenderá que `checkout` también se usa para cambiar de rama.

#### Recuperación de archivos: git reset
También puede eliminar un archivo con `git rm`. Este comando elimina el archivo en el disco, pero también hace que Git registre su eliminación en el índice.

Por lo tanto, si ha ejecutado este comando:
``` bash
git rm index.html
git checkout -- index.html
```

Git *no* restauraría *index.html* fácilmente. Por el contrario, se obtendría un error como este ejemplo:
``` bash
error: pathspec 'index.html' did not match any file(s) known to git.
```

Para recuperar *index.html*, habría que usar otra técnica: `git reset`. Puede usar `git reset` para anular el almacenamiento provisional de los cambios.

*index.html* se puede recuperar con estos dos comandos:
``` bash
git reset HEAD index.html
git checkout -- index.html
```
Aquí, `git reset` revierte la eliminación del archivo del almacenamiento provisional de Git. Este comando devuelve el archivo al índice, aunque sigue eliminado del disco. Luego se puede restaurar en el disco desde el índice con `git checkout`.

He aquí otro momento "¡Ahá!" para los nuevos usuarios de Git. Muchos VCS hacen que los archivos sean de solo lectura para asegurarse de que solo una persona pueda efectuar cambios cada vez; los usuarios usan un comando `checkout` no relacionado para obtener una versión grabable del archivo. También usan `checkin` para una operación similar a la que realiza Git con una combinación de `add`, `commit` y `push`. A veces este hecho origina confusión cuando los usuarios empiezan a usar Git.

#### Reversión de una confirmación: git revert
El último comando importante que se debe conocer para corregir errores con Git es `git revert`. `git checkout` solo funciona en situaciones en las que los cambios que se van a deshacer están en el índice. Después de confirmar los cambios, debe emplear otra estrategia para deshacerlos. En este caso se puede usar `git revert` para revertir la confirmación anterior. Crea *otra* confirmación que cancela la primera.

Se puede usar `git revert` HEAD para realizar una confirmación exactamente *opuesta* a la última, con lo que esta se deshace y deja todo el historial intacto. La parte `HEAD` del comando simplemente indica a Git que se quiere "deshacer" solo la última confirmación.

Por otro lado, también se puede quitar la confirmación más reciente con el comando git reset:
``` bash
git reset --hard HEAD^
```
Git ofrece varios tipos de restablecimientos. El valor predeterminado es `--mixed`, que restablece el índice, pero no el árbol de trabajo; también mueve `HEAD` si se especifica otra confirmación. La opción -`-soft` solo mueve HEAD y deja el índice y el árbol de trabajo sin cambios. Esta opción deja todos los cambios como "pendientes de confirmar", como indicaría `git status`. Un restablecimiento `--hard` cambia el índice y el árbol de trabajo para que coincidan con la confirmación especificada; los cambios realizados en los archivos seguidos se descartan.

___

## Ejercicio: Uso de Git para corregir errores

#### Práctica de recuperación de un archivo eliminado

1. En primer lugar, intente eliminar index.html:
``` bash
rm index.html
```
Puede parecer una mala idea, pero recuerde: Git le cubre las espaldas.

2. Use un comando `ls` para comprobar que *index.html* se haya eliminado:
``` bash
ls
```

3. Debería ver la siguiente salida. Observe que ahora no hay ningún archivo index.html.
``` bash
CSS
```

4. Vamos a recuperar *index.html*. Use `git checkout` para recuperar index.html:
``` bash 
git checkout -- index.html
```

5. Vuelva a utilizar `ls` para comprobar el contenido del directorio actual. ¿Se ha restaurado *index.html*?
Sí. Ahora la salida debe tener un archivo *index.html* y un directorio CSS:
``` bash
CSS  index.html
```

#### Práctica de la recuperación de un archivo eliminado: git rm
Si quiere recuperar archivos eliminados, las cosas son un poco más complicadas si los elimina mediante `git rm `en lugar de `rm`.

1. Para ver lo que sucede, pruebe este comando:
``` bash 
git rm index.html
```

2. De nuevo, busque *index.html* al ejecutar `ls`. No debería ver *index.html*.

3. Intente recuperar *index.html* lo mismo que la última vez:
``` bash 
git checkout -- index.html
```

4. Esta vez, Git indica que no sabe nada de *index.html*. Esto se debe a que Git no solo ha eliminado el archivo, sino que ha registrado la eliminación en el índice:
``` bash 
error: pathspec 'index.html' did not match any file(s) known to git.
```

5. Revierta la eliminación de *index.html* del almacenamiento provisional con el comando `git reset`:
``` bash 
git reset HEAD index.html
```

6. Busque esta salida, que lo confirma:
``` bash 
Unstaged changes after reset:
D       index.html
```

7. Ahora puede recuperar el archivo del índice con el comando que ha usado antes:
``` bash
git checkout -- index.html
```
`git reset` deshizo el cambio, pero el archivo seguía borrado, así que tuvo que usar `checkout` para recuperarlo.

8. Vuelva a comprobar que ha funcionado al ejecutar `ls`.

#### Reversión de una confirmación
Ahora vamos a complicar las cosas un poco más. Imagine que por accidente sobrescribe un archivo con otro, o que hace un cambio en un archivo que resulta ser un gran error. Quiere revertir el archivo a la versión anterior, pero ya ha confirmado los cambios. En este caso, un sencillo `git checkout` no va a funcionar.

Una solución a este problema consiste en revertir la confirmación anterior.

1. Abra *index.html* con `code`:
``` bash
code index.html
```

2. Reemplace el contenido de *index.html* por este código:
``` html
<h1>That was a mistake!</h1>
```

3. Guarde y cierre el archivo.

4. Use estos comandos para confirmar los cambios y mostrar la confirmación más reciente:
``` bash
git commit -m "Purposely overwrite the contents of index.html" index.html
git log -n1
```
La marca `-n1` aquí indica a Git que solo se quiere la entrada de confirmación más reciente.


5. Use los comandos siguientes para intentar restaurar *index.html*:
``` bash
git checkout -- index.html
```


6. Abra *index.html* en el editor:
``` bash
code index.html
```
¿Qué versión de *index.html* verá? ¿La versión anterior o la nueva?

En esta situación, la mejor opción es *revertir* el cambio realizando otra confirmación que cancele la primera. Este es un trabajo para `git revert`.

7. Cierre el archivo y use `git revert` para deshacer los cambios confirmados:
``` bash 
git revert --no-edit HEAD
```
La marca `--no-edit` aquí indica a Git que no se quiere agregar un mensaje de confirmación para esta acción.


8. Compruebe los resultados. Deben tener un aspecto similar a este ejemplo:
``` bash 
[main 6a27310] Revert "Purposely overwrite the contents of index.html"
1 file changed, 13 insertions(+), 1 deletion(-)
```

9. Realice un seguimiento con un comando `git log` para mostrar la confirmación más reciente:
``` bash 
git log -n1
```

10. Vuelva a comprobar la salida. Deberían parecerse a los de este ejemplo
``` bash 
Author: User Name <user-name@contoso.com>
Date:   Tue Nov 19 23:42:26 2019 +0000

Revert "Purposely overwrite the contents of index.html"

This reverts commit 15d3bded388470c98881a632025bc15190fe9d17.
```

11. Por último, abra el archivo *index.html* para asegurarse de que el contenido es la versión correcta.

La reversión no es la única manera de solucionar esta situación; bastaría con editar *index.html* y confirmar el archivo corregido. Esa opción es más difícil si los cambios confirmados fueran muchos. En cualquier caso, `git revert` es una clara señal de intenciones.

___

## Prueba de conocimientos
1. ¿Cómo se incluye un archivo nuevo en el índice de Git? 
  - [ ] Con el comando "git include"
  - [ ] Con el comando "git add"
  - [ ] Con el comando "git commit"
<!-- Correcto. git add agregará cualquier archivo que indique al índice de Git. -->

2. ¿Qué hace la etiqueta -m a la confirmación? 
  - [ ] La etiqueta -m no es una etiqueta válida en Git.
  - [ ] La etiqueta modifica la confirmación si olvidó agregar algo.
  - [ ] Esta etiqueta permite agregar un mensaje a la confirmación.
<!-- Correcto. Asegúrese de que los mensajes de confirmación sean cortos y legibles. -->

3. ¿Cuál de los siguientes es un buen ejemplo de mensaje de confirmación? 
  - [ ] Agregar una característica al administrador de alertas para el nuevo registro de usuarios...
  - [ ] Se ha agregado una característica nueva
  - [ ] Agregar etiquetas de nombre, edad, altura, peso y salario con los cuadros de texto correspondientes y mucho más a través de un botón Enviar en la página web para asegurarse de que el usuario tiene claro lo que se agrega...
<!-- Correcto. Una buena regla general es que los mensajes de confirmación de Git tengan menos de 50 palabras y asegurarse de que son descriptivos para otros desarrolladores. -->

4. ¿Cuál de las siguientes es una manera de corregir una de las confirmaciones anteriores sin necesidad de realizar una nueva confirmación? 
  - [ ] Eliminar el archivo y crear uno en su lugar con los cambios correctos.
  - [ ] Usar la etiqueta "modificar" de Git.
  - [ ] Revertir la confirmación y realizar una nueva
<!-- Correcto. Usar la modificación significa que está cambiando lo que se ha puesto en la confirmación inicial. -->

5. ¿Cómo puede elegir entre el restablecimiento y la restauración de Git para recuperar un archivo perdido? 
  - [ ] La restauración de Git puede recuperar un archivo que podría haber eliminado por accidente. El restablecimiento de Git recuperará un archivo que eliminó mediante el comando "git rm".
  - [ ] Use siempre la restauración de Git porque es la opción más segura.
  - [ ] Cree un archivo con el mismo nombre y use el restablecimiento de Git.
<!-- Correcto. La restauración de Git actualiza el archivo con el que aparece en el índice de Git, mientras que el restablecimiento de Git revierte la eliminación de los archivos eliminados. -->

6. ¿Cuándo debe evitar cambiar una confirmación anterior? 
  - [ ] Evite modificar confirmaciones en las que otros desarrolladores hayan basado su trabajo.
  - [ ] Cuando quiere agregar un archivo nuevo a la confirmación.
  - [ ] Cuando quiere cambiar una confirmación que no sea la más reciente.
<!-- Correcto. Al modificar una confirmación, la anterior a esta desaparece y la reemplaza la confirmación modificada. -->

___

## Resumen
¡Enhorabuena! En este módulo, ha descubierto cómo crear un proyecto de Git y editar los errores que existían en él.

Ha aprendido:

- Procedimientos para crear un proyecto en Git
- Procedimientos para realizar confirmaciones en el área de trabajo de Git
- Procedimientos para realizar un seguimiento de los cambios y modificar archivos en el área de trabajo de Git
- Procedimientos para editar confirmaciones anteriores en el área de trabajo de Git
- Procedimientos para recuperar archivos eliminados en el área de trabajo de Git
- Procedimientos para deshacer una confirmación en Git

En este momento, ya sabe lo suficiente sobre Git para crear y modificar un proyecto. La colaboración con otros desarrolladores es donde el control de versiones destaca. Vea los demás módulos de esta ruta de aprendizaje para obtener más información sobre el empleo de Git con otros usuarios.

Recursos
Si quiere profundizar más, aquí tiene más recursos:

- Ejecute los comandos `git help tutorial` y `git help tutorial-2`.
- Visite el sitio *[Everyday Git][20]* o use el comando `git help everyday`.
- Revise los *[recursos de aprendizaje de Git y GitHub][21]*.
- Vea el vídeo de *[introducción al resumen de Git][22]*.
- Vea la *[sección de documentación][23]* del *[sitio web oficial de Git][24]*.

[20]: https://git-scm.com/docs/everyday
[21]: https://help.github.com/en/articles/git-and-github-learning-resources
[22]: https://www.youtube.com/watch?v=9uGS1ak_FGg%3Fazure-portal%3Dtrue
[23]: https://git-scm.com/doc
[24]: https://git-scm.com/docs/everyday
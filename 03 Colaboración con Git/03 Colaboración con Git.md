
# Colaboración de Git
___
## Introducción

Imagine que es un nuevo desarrollador de software en una empresa que escribe software de aviónica para líneas aéreas comerciales. El control de calidad es crítico y los desarrolladores trabajan en equipos pequeños y usan Git para el control de versiones. Ya sabe algo sobre Git y lo ha usado localmente por su cuenta para realizar el seguimiento de los cambios y corregir errores. Pero sabe que el control de versiones resulta más útil para trabajar en el código con un equipo y quiere practicar un poco.

Ya ha creado un pequeño sitio web que usted y sus amigos pueden usar para practicar con Git compartiendo fotografías de sus gatos. Ha reclutado a un par de amigos que son desarrolladores de software para que le ayuden.

Va a usar Git para colaborar y hacer un seguimiento de los cambios (y de quién los hace), asegurarse de que no haya ningún error cuando dos usuarios modifiquen el mismo archivo y realizar copias de seguridad de todos los archivos de código fuente.

#### Objetivos de aprendizaje
Objetivos de este módulo:

  * Clonación de un repositorio
  * Insertar cambios en un repositorio remoto
  * Guardado provisional de cambios
  * Incorporar los cambios de otros usuarios para actualizar un repositorio

___

## Colaboración mediante un comando de incorporación de cambios

En su tiempo de ocio ha estado trabajando en un sitio web que hospeda fotos de gatos. Ha estado usando Git para el control de versiones, y es hora de invitar a colaboradores al proyecto. Durante una cena en su casa, su amiga y también amante de los gatos, Alice, se ofrece a ayudarle a materializar su proyecto, y usted acepta encantado.

Alice primero debe hacer una copia del proyecto de Git. Luego es recomendable que Alice le envíe sus cambios a medida que los realiza. En esta situación es donde destaca la naturaleza *distribuida* de Git. Con Git, dos o más usuarios pueden trabajar juntos en un proyecto sin miedo a sobrescribir el trabajo de los otros. Además, puede comprobar el trabajo de Alice antes de combinarlo con el suyo. (Alice tiene talento, pero ningún desarrollador es perfecto. Confíe, pero compruebe)

En esta lección va a aprender a clonar un repositorio (también denominado repo) para ponerlo a disposición de otros usuarios. También aprenderá a usar una de las características más importantes de Git: las solicitudes de incorporación de cambios.

#### Clonación de un repositorio (git clone)

En Git, un repositorio se copia al *clonarlo* mediante el comando `git clone`. Puede clonar un repositorio independientemente de dónde esté almacenado, siempre que tenga una dirección URL o una ruta de acceso a la que apuntar.

`git clone` acepta rutas de acceso del sistema de archivos, rutas de acceso SSH (por ejemplo, `git@example.com:alice/Cats`; estará familiarizado con este formato si ha usado Rsync o SCP) o direcciones URL, normalmente una que empiece por `file:`, `git:` o `ssh`. Los distintos formatos se describen en la documentación de `git clone`. En Unix y Linux, la operación de clonación usa vínculos físicos, así que es rápida y usa un espacio mínimo, ya que solo hay que copiar las entradas de directorio, no los archivos.

#### Repositorios remotos (git pull)

Cuando Git clona un repositorio, crea una referencia al repositorio original, al que se llama *remoto*, mediante el nombre `origin`. Configura el repositorio clonado de modo que *incorpore* o recupere datos del repositorio remoto. (Git también puede *enviar* cambios. Va a obtener información sobre el envío de cambios en Git más adelante en este módulo). `origin` es la ubicación predeterminada desde la que Git incorpora los cambios y a la que los envía. `git pull` copia los cambios del repositorio remoto en el local. El comando `git pull` es muy eficaz, porque solo copia las confirmaciones y los objetos nuevos y luego los inserta en el árbol de trabajo.

Puede incorporar cambios de `origin` mediante el comando `git pull`. Resulta útil comparar `git pull` con otros métodos de copia de archivos. El comando `scp` copia todo. (`scp` es similar al comando `cp` de Unix, salvo que los archivos que se copian no tienen que estar en el mismo equipo). Si hay 10 000 archivos en el directorio remoto, `scp` los copia todos. Un programa más eficaz llamado Rsync examina todos los archivos de los directorios local y remoto y solo copia los que son diferentes. Rsync se suele usar para realizar copias de seguridad, pero tiene que aplicar hash a todos los archivos, a menos que tengan diferentes tamaños o fechas de creación.

Git solo examina las confirmaciones. Ya sabe cuál es la última confirmación que ha obtenido del repositorio remoto porque ha guardado la lista de confirmaciones. Luego, Git indica al equipo desde el que está copiando que envíe todo lo que ha cambiado, incluidas las nuevas confirmaciones y los objetos a los que apuntan. Esos objetos y confirmaciones se agrupan en un archivo denominado *paquete* que se envía en un lote. Por último, Git actualiza el árbol de trabajo al desempaquetar todos los objetos que han cambiado y combinarlos (si fuera necesario) con las confirmaciones y los objetos del árbol de trabajo.

Git solo incorpora o envía cambios si el usuario se lo indica. En eso difiere de, por ejemplo, Dropbox, que tiene que pedir al sistema operativo que le notifique los cambios realizados en su carpeta y, a veces, preguntar al servidor si alguna otra persona ha realizado cambios.

#### Creación de solicitudes de incorporación de cambios (git request-pull)

Una vez que otro desarrollador, como Alice, ha clonado el repositorio y realizado algunos cambios en local, es recomendable que incorpore esos cambios al repositorio original. Podría parecer que lo adecuado sería enviar los cambios al repositorio original, pero se produciría un error al hacerlo, ya que otros usuarios no tienen permiso para realizar cambios en él. Y así debe ser. Por ahora, quiere revisar los cambios entrantes antes de combinarlos con la base de código principal.

Por ahora, Alice tendrá que enviar una *solicitud de incorporación de cambios* para pedirle que incorpore sus cambios a la base de código principal. Alice puede hacerlo mediante `git request-pull`, que podría tener el aspecto de este ejemplo:
``` bash
git request-pull -p origin/main .
```
Alice hace referencia a la rama `main` del remoto `origin` como `origin/main`.

Esta solicitud de incorporación de cambios es básicamente lo mismo que una de GitHub, que es un lugar para almacenar código del que no se habla en este módulo. Una solicitud de incorporación de cambios le ofrece la posibilidad de revisar los cambios de otros colaboradores antes de incorporar su trabajo al que está realizando en el sitio web. Las revisiones de código son una parte importante (algunos dirían que la más importante) de la programación colaborativa.

#### Creación de un remoto (git remote) y finalización de la solicitud de incorporación de cambios (git pull)

Como propietario del proyecto, debe saber cómo combinar las solicitudes de incorporación de cambios. En primer lugar, use el comando `git remote` para configurar el repositorio de otro desarrollador como *remoto*. Luego use ese remoto para las incorporaciones y las solicitudes de incorporación de cambios mediante el comando `git pull`.

En segundo plano, `git pull` es una combinación de dos operaciones más sencillas: `git fetch`, que obtiene los cambios, y git merge, que combina esos cambios en el repositorio. En este caso, la combinación era de *avance rápido*, lo que significa que Alice tenía la confirmación más reciente en su repositorio, por lo que esta confirmación podría agregarse al principio del historial sin ninguna modificación.

___

## Ejercicio: Clonación de un repositorio

Para que Alice practique cómo clonar un repositorio y realizar una solicitud de incorporación de cambios, primero se debe configurar un repositorio para que Alice lo clone.

#### Configuración

Git ya se ha instalado automáticamente en Azure Cloud Shell, por lo que podemos usar Git en Cloud Shell, a la derecha.

1. Use el comando `mkdir` para crear una carpeta denominada *Cats*:
``` bash
mkdir Cats
```

2. Use el comando `cd` para ir a la carpeta del proyecto:
``` bash
cd Cats
```

3. Ahora, inicialice el nuevo repositorio y establezca el nombre de la rama predeterminada en `main`.

Si está ejecutando la versión 2.28.0 o una posterior de Git, use los comandos siguientes: 
``` bash
git init --initial-branch=main
git init -b main
```
En versiones anteriores de Git, use estos comandos:
``` bash
git init
git checkout -b main
```

4. Configure Git mediante la incorporación de sus credenciales. Reemplace `<USER_NAME>` y `<USER_EMAIL>` por su propia información (por ejemplo, "Nombre de usuario" y "user-name@contoso.com"). 
``` bash
git config user.name "<USER_NAME>"
git config user.email "<USER_EMAIL>"
```

5. Cree algunos archivos con el comando `touch` y almacénelos provisionalmente y confírmelos mediante Git: 
``` bash
touch index.html
mkdir CSS
touch CSS/site.css
git add .
git commit -m "Create empty index.html, site.css files"
```

6. Agregue algún código HTML al archivo index.html mediante el editor de código de Cloud Shell, que puede abrir con el comando `code` en el símbolo del sistema del terminal: 
``` bash
code index.html
```

7. Pegue este código HTML: 
``` html
<!DOCTYPE html>
<html>
  <head>
    <meta charset='UTF-8'>
    <title>Our Feline Friends</title>
    <link rel="stylesheet" href="CSS/site.css">
  </head>
  <body>
    <h1>Our Feline Friends</h1>
    <p>Eventually we will put cat pictures here.</p>
    <hr>
  </body>
</html>
```

8. Guarde el archivo y cierre el editor. Puede seleccionar los puntos suspensivos "..." de la esquina derecha del editor o usar el método abreviado de teclado (Ctrl+S en Windows y Linux, Cmd+S en macOS). 

9. Vaya al directorio CSS y abra *site.css* en el editor: 
``` bash
cd CSS
code site.css
```

10. Agregue el siguiente CSS a *site.css*: 
``` bash
h1, h2, h3, h4, h5, h6 { font-family: sans-serif; }
body { font-family: serif; }
```

11. Vuelva al directorio *Cats*.
``` bash
cd ..
```

12. Por último, confirme los cambios de nuevo:
``` bash
git add .
git commit -m "Add simple HTML and stylesheet"
```

13. Compruebe rápidamente el registro de Git para asegurarse de que todo parezca correcto:
``` bash
git log --oneline
```

14. Compruebe los resultados. Debería ver una salida como la de este ejemplo:
``` bash
2bf69ab Add simple HTML and stylesheet
bb371c8 Create empty index.html, site.css files
```

#### Clonación de un repositorio

Ahora vamos a asumir el papel de Alice y a practicar la clonación de un repositorio para colaborar en él.

Para simular la clonación del repositorio por parte de Alice en el equipo de ella, cree un directorio denominado *Alice* en su equipo y clone en él el directorio del proyecto. En la vida real, esta colaboración se lograría mediante la configuración de un recurso compartido de red o un remoto accesible por medio de una dirección URL.

1. Cree un directorio denominado *Alice* en el que clonar el repositorio. *No* debe ser un subdirectorio del directorio del proyecto (*Cats*), así que use `cd` de nuevo para ir al directorio principal desde el directorio del proyecto a fin de convertir Alice en un elemento del mismo nivel que el directorio del proyecto. Luego, use `cd` para ir al directorio Alice.
``` bash
cd ..
mkdir Alice
cd Alice
```

2. Ahora use `git clone` para clonar el repositorio que se encuentra en el directorio del proyecto en el directorio *Alice*. Asegúrese de incluir el punto al final del comando:
``` bash
git clone ../Cats .
```
`../Cats` indica a Git desde dónde debe realizar la clonación, mientras que `.` le indica la ubicación de destino de esta. En Unix, `.` hace referencia al directorio actual

3. Compruebe los resultados. Git debe mostrar este texto para indicarle que ha funcionado:
``` bash
Cloning into '.'...
done.
```

___

## Ejercicio: Creación de una solicitud de incorporación de cambios

En el espacio aislado, asegúrese de que sigue en el directorio *Alice*, que es la carpeta superior del clon de Alice del repositorio Cats. Puede usar el comando `pwd` para comprobar la ubicación de la carpeta.
``` bash
pwd
```

En este momento no hay nada que Alice pueda incorporar, porque no se ha realizado ningún cambio desde que ella clonó el repositorio. Puede probarlo con el siguiente comando, que muestra la salida `Already up-to-date`:
``` bash
git pull
```

#### Realización de un cambio y envío de una solicitud de incorporación de cambios
Alice comienza a trabajar en el sitio web. Su primera decisión es cambiar el color de fondo del sitio. Alice experimenta en local y, finalmente, elige su tono favorito de azul claro.

1. Configure una identidad para Alice mediante la ejecución de los siguientes comandos:
``` bash
git config user.name "Alice"
git config user.email "alice@contoso.com"
```
Estos valores de configuración `config` se almacenan en el repositorio en el archivo *.git/config*, así que no tendrá que volver a escribirlos. Cada vez que vaya al directorio *Alice*, asumirá la identidad de Alice.

2. Abra el archivo site.css del directorio *Alice*/CSS:
``` bash
code CSS/site.css
```

3. Para cambiar el color de fondo de la página a azul claro, reemplace la segunda línea del archivo por la siguiente instrucción: 
``` css
body { font-family: serif; background-color: #F0FFF8; }
```
Luego guarde el archivo y cierre el editor.

4. Ahora confirme el cambio:
``` bash
git commit -a -m "Change background color to light blue"
```

5. Luego realice una solicitud de incorporación de cambios al repositorio original: 
``` bash
git request-pull -p origin/main .
```

6. Compruebe los resultados. Debería ver una salida similar al ejemplo siguiente: 
``` bash
The following changes since commit 2bf69ab0226d8d35efd1e92c83cd92c5cc09a7ae:

  Add simple HTML and stylesheet (2019-11-21 01:57:24 +0000)

are available in the git repository at:

  .

for you to fetch changes up to 95bbc3b6929953e9b04353920e97230b463022f0:

  Change background color to light blue (2019-11-21 02:33:48 +0000)

----------------------------------------------------------------
Alice (1):
      Change background color to light blue

 CSS/site.css | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

diff --git a/CSS/site.css b/CSS/site.css
index caefc86..86d41e8 100644
--- a/CSS/site.css
+++ b/CSS/site.css
@@ -1,2 +1,2 @@
 h1, h2, h3, h4, h5, h6 { font-family: sans-serif; }
-body { font-family: serif; }
\ No newline at end of file
+body { font-family: serif; background-color: #F0FFF8; }
\ No newline at end of file
```

#### Creación de un remoto y finalización de la solicitud de incorporación de cambios

Dado que el directorio del proyecto y el directorio *Alice* están en el mismo equipo, puede incorporar los cambios directamente desde el directorio *Alice*. En la vida real, el directorio *Alice* estaría en el equipo de ella. Esta circunstancia se soluciona mediante la configuración de un *remoto* con el comando `git remote`. Luego se usa ese remoto para las solicitudes de incorporación y envío de cambios. En este ejercicio no resulta práctico configurar dos máquinas para realizar estos pasos, así que se va a configurar un remoto que use un nombre de ruta de acceso local. En realidad, se usaría una ruta de acceso de red o una URL.

1. Vuelva al directorio del proyecto y use el comando `git remote` para crear un remoto de nombre `remote-alice` que tenga como destino el directorio del proyecto de Alice:
``` bash
cd ../Cats
git remote add remote-alice ../Alice
```

2. Ahora ejecute una incorporación de cambios:
``` bash
git pull remote-alice main
```
Observe que tiene que especificar una rama, `main`, en el comando de incorporación de cambios. En la siguiente lección va a aprender a configurar una dirección URL ascendente para la rama.


3. Compruebe los resultados. Debería ver una salida como la de este ejemplo, que muestra que la solicitud de incorporación de cambios se ha realizado correctamente:
``` bash
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 1), reused 0 (delta 0)
Unpacking objects: 100% (4/4), done.
From ../Alice
 * branch            main     -> FETCH_HEAD
 * [new branch]      main     -> remote-alice/main
Updating 2bf69ab..95bbc3b
Fast-forward
 CSS/site.css | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```
La diversión acaba de empezar. En la siguiente lección, aprenderá a configurar y utilizar un repositorio compartido, lo que hace que la colaboración resulte más sencilla y cómoda.

___

## Ejercicio: Colaboración mediante un repositorio compartido

La incorporación de cambios directa desde el repositorio de otro usuario funciona, siempre que ambos estén en la misma red. Pero es un proceso burdo, y la mayoría de los colaboradores no están en la misma red. Es mejor configurar un repositorio central en el que todos los colaboradores pueden insertar y enviar.

Cuando le habla a su amigo desarrollador Bob sobre su proyecto y este le pide participar, eso es exactamente lo que decide hacer: configurar un repositorio central, que también se conoce como *repositorio vacío*.

#### Creación de un repositorio vacío

Lo que necesita es un repositorio que no tenga árbol de trabajo. Un repositorio vacío tiene varias ventajas con respecto a un árbol de trabajo:

  * Sin un árbol de trabajo, todo el mundo puede enviar cambios sin tener que preocuparse de qué rama se extrae del repositorio.

  * Para Git es fácil detectar si otro usuario ha enviado cambios que podrían entrar en conflicto con los suyos.

  * Un repositorio compartido se escala a cualquier número de desarrolladores. Con un repositorio vacío solo tiene que saber sobre el repositorio compartido y no sobre los demás colaboradores de los que puede que tenga que incorporar.

  * Al colocar el repositorio compartido en un servidor al que todos pueden acceder, no tiene que preocuparse por los firewalls ni los permisos.

  * No necesita cuentas independientes en el servidor, ya que Git realiza un seguimiento de quién ha realizado cada confirmación. (GitHub tiene millones de usuarios que comparten la cuenta git. Todos usan el protocolo de red criptográfico de Secure Shell (SSH) y los usuarios se distinguen por sus claves públicas).

Crear un repositorio vacío para compartir es sencillo:

1. Cree un nuevo directorio denominado Shared.git en el mismo nivel que los directorios *Alice* y *Cats* para que contenga el repositorio vacío:
``` bash
cd ..
mkdir Shared.git
cd Shared.git
```
El nombre del directorio no tiene importancia, pero en estos ejercicios nos referiremos a él como el directorio *Shared.git* o simplemente como el directorio *compartido*.

Al asignar al directorio el nombre *Shared.git* se sigue la larga tradición de asignar a los repositorios vacíos un nombre que finaliza en `.git` para distinguirlos de los árboles de trabajo. Se trata de una convención, no de un requisito.


2. Ahora use el siguiente comando para crear un repositorio vacío en el directorio compartido:
``` bash
git init --bare
```

3. Cuando un repositorio todavía está vacío, no se puede usar el comando `git checkout` para establecer el nombre de la rama predeterminada. Para realizar esta tarea, puede cambiar la rama `HEAD` para que apunte a otra rama; en este caso es la rama `main`: 
``` bash
git symbolic-ref HEAD refs/heads/main
```

4. El siguiente paso consiste en obtener el contenido de su repositorio en el repositorio compartido. Use estos comandos para volver al directorio del proyecto donde está almacenado el repositorio, configure un remoto `origin` y realice un envío de cambios inicial:
``` bash
cd ../Cats
git remote add origin ../Shared.git
git push origin main
```

5. Compruebe los resultados. La salida debería indicar que la operación se ha realizado correctamente:
``` bash
Counting objects: 12, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (8/8), done.
Writing objects: 100% (12/12), 1.07 KiB | 0 bytes/s, done.
Total 12 (delta 1), reused 0 (delta 0)
To ../Shared.git
 * [new branch]      main -> main
```

6. Quiere que `push` y `pull` usen de manera predeterminada la rama `main` de `origin`, como si se hubiera creado el repositorio clonándolo. Pero primero debe indicar a Git la rama cuyo seguimiento se va a efectuar. 
``` bash
git branch --set-upstream-to origin/main
```

7. Busque esta salida: 
``` bash
Branch main set up to track remote branch main from origin.
```
Git se quejaría si se intentara ejecutar este comando antes del envío de cambios inicial, ya que el nuevo repositorio no tendría ramas. Git no puede realizar el seguimiento de una rama que no existe. Lo único que Git hace por debajo es buscar en `.git/refs/remotes/origin` un archivo denominado *trunk*.


#### Configuración para colaboradores

El siguiente paso es que Bob clone el repositorio vacío y que Alice defina el origen en su repositorio para establecer como destino de las incorporaciones y los envíos de cambios el repositorio compartido.

1. Cree un directorio denominado *Bob* que sea un elemento del mismo nivel que el directorio del proyecto y luego vaya al directorio *Bob*:
``` bash
cd ..
mkdir Bob
cd Bob
```

2. Ahora, clone el repositorio compartido (asegúrese de incluir el punto al final del comando): 
``` bash
git clone ../Shared.git .
```

3. Actualmente, el repositorio de Alice está configurado para enviar e incorporar cambios desde su propio repositorio. Use los siguientes comandos para ir al directorio *Alice* y cambie `origin` para que apunte al repositorio compartido:
``` bash
cd ../Alice
git remote set-url origin ../Shared.git
```


#### Inicio de la colaboración

Ahora que Bob lo tiene todo a punto para trabajar en el sitio web, decide agregar un pie de página en la parte inferior. Vamos a asumir el rol de Bob y Alice durante unos minutos para aprender los aspectos básicos de la colaboración.

1. Comience por ir al directorio Bob y trabaje como Bob:
``` bash
cd ../Bob
git config user.name Bob
git config user.email bob@contoso.com
```

2. Abra *index.html* y reemplace el elemento `<hr>` por esta línea (se encuentra al final del elemento `<body>`):
``` html
<footer><hr>Copyright (c) 2021 Contoso Cats</footer>
```
Luego guarde el archivo y cierre el editor.

3. Confirme los cambios e insértelos en el origen remoto:
``` bash
git commit -a -m "Put a footer at the bottom of the page"
git push
```

4. Compruebe los resultados. Si ve una advertencia similar a la del ejemplo siguiente, no se preocupe. Simplemente comunica a los usuarios un cambio en los comportamientos predeterminados de Git. Si quiere asegurarse de no volver a ver esta advertencia, puede ejecutar `git config --global push.default simple`.
``` bash
warning: push.default is unset; its implicit value has changed in
Git 2.0 from 'matching' to 'simple'. To squelch this message
and maintain the traditional behavior, use:

  git config --global push.default matching

To squelch this message and adopt the new behavior now, use:

  git config --global push.default simple

When push.default is set to 'matching', git will push local branches
to the remote branches that already exist with the same name.

Since Git 2.0, Git defaults to the more conservative 'simple'
behavior, which only pushes the current branch to the corresponding
remote branch that 'git pull' uses to update the current branch.

See 'git help config' and search for 'push.default' for further information.
(the 'simple' mode was introduced in Git 1.7.11. Use the similar mode
'current' instead of 'simple' if you sometimes use older versions of Git)
```

5. Mientras Bob edita el sitio, Alicia también lo hace. Ella decide agregar una barra de navegación a la página. Esta incorporación obliga a Alice a modificar dos archivos: *index.html* y *site.css*. Empiece por volver al directorio *Alice*:
``` bash
cd ../Alice
```

6. Ahora, abra *index.html* e inserte la línea siguiente inmediatamente después de la etiqueta `<body>`, en la línea 8:
``` html
<nav><a href="./index.html">home</a></nav>
```
Luego guarde el archivo y cierre el editor.


7. Abra `site.css` en la carpeta CSS y agregue la línea siguiente en la parte inferior:
``` css
nav { background-color: #C0D8DF; }
```
Guarde el archivo y cierre el editor.


8.  Ahora imagine que Alice recibe un correo electrónico de Bob en el que le dice que ha hecho cambios en el sitio. Alice decide extraer los cambios de Bob antes de confirmarlos. (Si Alice ya hubiera confirmado los cambios, tendrían otro problema que trataremos en otro módulo). Alice ejecuta este comando:
``` bash
git pull
```

9. Compruebe los resultados. Por la salida, parece que Git ha evitado un problema:
``` bash
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 2), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From ../Shared
   843d142..2cf6cbf  main     -> origin/main
Updating 843d142..2cf6cbf
error: Your local changes to the following files would be overwritten by merge:
        index.html
Please commit your changes or stash them before you can merge.
Aborting
```
Git advierte que la incorporación de cambios sobrescribiría la versión de Alice de *index.html* y se perderían sus cambios. Esto se debe a que Bob también ha modificado *index.html*. Si Alice no hubiera cambiado *index.html*, Git habría confirmado la combinación.


10. Use un comando `git diff` para ver qué cambios ha realizado Bob en *index.html*:
``` bash
git diff origin -- index.html
```

11. Compruebe los resultados. Por la salida, es evidente que los cambios de Alice y los de Bob no se superponen. Ahora Alice puede guardar *provisionalmente* sus cambios.

`git stash` guarda el estado del árbol de trabajo y el índice mediante un par de confirmaciones temporales. Piense en el almacenamiento provisional como una manera de guardar el trabajo actual mientras hace otra cosa, sin tener que realizar una confirmación "real" ni afectar al historial del repositorio.

En realidad, Alice debería haber confirmado o guardado provisionalmente sus cambios antes de intentar incorporar cambios. La incorporación de cambios a un árbol de trabajo "sucio" es algo arriesgado, ya que puede provocar incidencias más complejas de subsanar.

Use el siguiente comando para guardar provisionalmente los cambios de Alice:
``` bash
git stash
```

12. Compruebe los resultados. Deberían parecerse a los de este ejemplo:
``` bash
Saved working directory and index state WIP on main: 95bbc3b Change background color to light blue
HEAD is now at 95bbc3b Change background color to light blue
```

13. Ahora Alice puede incorporar los cambios con seguridad, después de lo cual puede "sacar" los cambios guardados provisionalmente, que están organizados como una pila. (De hecho, `git stash` es una forma abreviada de `git stash push`. Es muy similar a la pila donde se colocan las facturas que aún no se han podido pagar). Ejecute estos comandos:
``` bash
git pull
git stash pop
```
Los cambios guardados provisionalmente se combinan al extraerlos. Si los cambios se superponen, podría haber un conflicto. Puede obtener información sobre cómo resolver esas situaciones en un módulo de Git más avanzado de Microsoft Learn.


14. Compruebe los resultados. Alice debería ver esta salida, que le permite saber que la combinación se ha realizado correctamente y que los cambios están de vuelta, aunque aún no se hayan almacenado provisionalmente para su confirmación:
``` bash
Auto-merging index.html
On branch main
Your branch is up-to-date with 'origin/main'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   CSS/site.css
        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (0cfb7b75d56611d9fc6a6ab660a51f5582b8d9c5)
```
En este punto Alice puede seguir trabajando o simplemente confirmar y enviar los cambios. Vamos a hacer otro cambio como Alice: asignar a los pies de página el mismo estilo que a las barras de navegación.


15. Abra site.css en la carpeta CSS y reemplace la tercera línea (la que aplica estilo a los elementos `<nav>`) por esta regla CSS compartida. Luego, como de costumbre, guarde los cambios y cierre el editor.
``` css
nav, footer { background-color: #C0D8DF; }
```

16. Ahora confirme los cambios y envíelos al repositorio compartido:
``` bash
git commit -a -m "Stylize the nav bar"
git push
```
El sitio actualizado está ahora en el repositorio compartido.

17. El sitio actualizado está ahora en el repositorio compartido. 
``` bash
cd ../Cats
git pull
```

18. Abra *index.html* (el que se encuentra en el directorio del proyecto) para confirmar que los cambios realizados por Bob y Alice están presentes en el repositorio local. Compruebe que *index.html* tiene el código más actualizado:
``` bash
<!DOCTYPE html>
<html>
  <head>
    <meta charset='UTF-8'>
    <title>Our Feline Friends</title>
    <link rel="stylesheet" href="CSS/site.css">
  </head>
  <body>
    <nav><a href="./index.html">home</a></nav>
    <h1>Our Feline Friends</h1>
    <p>Eventually we will put cat pictures here.</p>
    <footer><hr>Copyright (c) 2021 Contoso Cats</footer>
  </body>
</html>
```

16. En este momento, su repositorio y el de Alice están sincronizados, pero el de Bob no lo está. Para finalizar, actualice también el de Bob:
``` bash
cd ../Bob
git pull
```
Los tres repositorios ya están alineados. El repositorio compartido es el único origen de confianza para todos los usuarios, y todos los envíos de cambios e incorporaciones se dirigen a él.

Si tiene curiosidad por el aspecto del sitio web, aquí se muestra una vista previa:

![drawing](./cats-home-page.png)

Si quiere, puede descargar los archivos para obtener una versión preliminar local de ellos:

1. Comprima la carpeta *Cats*:
``` bash
cd ..
zip -r Cats.zip Cats
```

2. Descargue el archivo ZIP:
``` bash
download Cats.zip
```

3. Ahora, descomprima el archivo en la máquina local y abra *index.html* para verlo por sí mismo.

___

## Prueba de conocimientos

1. ¿Cuál es la principal ventaja de la naturaleza distribuida de Git? 
   - [ ] Git combina automáticamente los cambios guardados de varios autores remotos en un único repositorio de proyecto.
   - [ ] Varios colaboradores remotos pueden trabajar juntos en un proyecto sin miedo a sobrescribir el trabajo de los demás. Los colaboradores pueden comprobar los cambios de otro colaborador antes de combinarlos con los suyos.
   - [ ] Git distribuye archivos y una estructura de carpetas a la máquina de cada colaborador por medio de una red de área extensa para mantener la seguridad. Esta arquitectura proporciona un almacenamiento de datos muy seguro y garantiza que los datos del repositorio del proyecto no se puedan dañar.
<!-- Correcto. La naturaleza distribuida de Git ayuda a todos los colaboradores a garantizar y mantener la validez del contenido del proyecto. -->

2. Cuando un usuario de Git copia un repositorio, ¿qué término describe la referencia que Git configura para el repositorio original? 
   - [ ] origen
   - [ ] repo
   - [ ] Conexión remota
<!-- Correcto. Al clonar (copiar) un repositorio, Git crea una referencia al repositorio original denominada "remoto". Git usa el nombre "origen" para referirse al repositorio remoto. -->

3. ¿Qué comando de Git hace una copia de un repositorio existente? 
   - [ ] `git clone <repo-name>`
   - [ ] `git clone <repo-path>`
   - [ ] `git copy <repo-name>`
<!-- Correcto. El comando git clone toma una dirección URL o una ruta de acceso a un repositorio existente como parámetro. -->

4. ¿Qué comando de Git se puede usar para guardar los cambios actuales sin usar una solicitud de incorporación de cambios?
   - [ ] git stash
   - [ ] git save
   - [ ] git store
<!-- Correcto. El comando git stash guarda el estado del árbol de trabajo y el índice mediante la realización de un par de confirmaciones temporales. Este tipo de proceso de guardar no afecta al historial del repositorio. -->

5. Imagine que tiene un proyecto con diez archivos en la rama de trabajo local del repositorio. Recientemente ha actualizado tres de los archivos: `toc.yml`, `intro.txt` y `exercise.json`. Ahora quiere crear una solicitud de incorporación de cambios solo para los cambios del archivo JSON. ¿Qué conjunto de comandos de Git debe usar para crear la solicitud de incorporación de cambios solo de esos cambios? 
   - [ ] 
   ``` bash
        git add .
        git commit -m "my changes for the exercise"
        git push origin <working-branch>
   ```

   - [ ] 
   ``` bash
      git add exercise.json
      git commit -m "my changes for the exercise"
      git push origin <working-branch>
   ```


   - [ ] 
   ``` bash
      git add exercise
      git commit -m "my changes for the exercise"
      git push remote <working-branch>
   ```  
<!-- Correcto. Para enviar todos los cambios actuales, especifique . después de git add. Para enviar los cambios de un solo archivo, escriba el nombre de archivo específico. --> 

___

## Resumen
Enhorabuena. En este módulo ha aprendido a usar Git para colaborar con otros desarrolladores.

En este módulo ha aprendido:

- Cómo clonar un repositorio
- Cómo guardar cambios provisionalmente
- Cómo enviar cambios a un repositorio
- Qué son las solicitudes de incorporación de cambios y cómo se inician

En este momento ya sabe lo suficiente sobre Git para colaborar de algunas maneras básicas, pero todavía queda mucho más por aprender.

Si quiere profundizar más en el tema, aquí tiene algunos recursos que le resultarán útiles:

- Ejecute los comandos `git help tutorial` y `git help tutorial-2`.
- *[Everyday Git][20]* (también disponible desde la línea de comandos, como `git help everyday`).
-  *[Recursos de aprendizaje de Git y GitHub][21]* de GitHub.

También puede obtener más información en la *[sección de documentación][22]* del *[sitio web oficial de Git][23]*.


[20]: https://git-scm.com/docs/everyday
[21]: https://help.github.com/en/articles/git-and-github-learning-resources
[22]: https://git-scm.com/doc
[23]: https://git-scm.com/
___
## Introducción

Imagine que es un nuevo desarrollador de software en una empresa que escribe software de aviónica para líneas aéreas comerciales. El control de calidad es crítico y los desarrolladores trabajan en equipos pequeños que usan Git para el control de versiones. Ha oído hablar del control de versiones, pero nunca ha usado Git, por lo que tiene muchas ganas de ponerse al día.

Decide compilar un sitio web que le permita compartir fotografías de sus gatos con sus amigos y, así, aprender a usar Git en un entorno divertido antes de aplicar esos conocimientos a su trabajo. Se propone compilar el sitio con Git para efectuar el seguimiento de los cambios y mantener copias de seguridad de todos los archivos de código fuente en caso de que el servidor deje de funcionar. Pero antes de entrar primero en Git, debe cubrir los conceptos básicos.

En este módulo, se ofrece una introducción al control de versiones y a Git. Git puede parecer un poco críptico al principio, incluso a veces frustrante, pero si lo conoce paso a paso, verá que hay una razón por la que se está convirtiendo rápidamente en el sistema de control de versiones más popular del mundo, no solo entre los desarrolladores de software, sino también entre los equipos que escriben documentación y colaboran en otras tareas.


### Ver un vídeo
Para obtener información general sobre los ejercicios de este módulo, vea el vídeo de *[introducción al resumen de Git][1]*

[1]: https://www.youtube.com/watch?v=9uGS1ak_FGg%3Fazure-portal%3Dtrue

### Objetivos de aprendizaje
Objetivos de este módulo:

  * Más información sobre el control de versiones
  * Descripción de los sistemas de control de versiones distribuidos, como Git
  * Comprensión de las diferencias entre Git y GitHub y los roles que desempeñan en el ciclo de vida de desarrollo de software
___

## ¿Qué es el control de versiones?

Un sistema de control de versiones (VCS) es un programa o conjunto de programas que realiza un seguimiento de los cambios en una colección de archivos. Uno de los objetivos de un VCS es recuperar fácilmente versiones anteriores de archivos individuales o de todo el proyecto. Otro objetivo es permitir que varios miembros de un equipo trabajen en un proyecto, incluso en los mismos archivos, al mismo tiempo sin que eso afecte al trabajo de los demás.

Otro nombre para un VCS es un sistema de administración de configuración de software (SCM). Los dos términos suelen usarse indistintamente; de hecho, la documentación oficial de Git se encuentra en *[git-scm.com.][1]* Técnicamente, el control de versiones es solo uno de los procedimientos que implica el SCM. Un VCS se puede usar para otros proyectos además de los de software, incluidos libros y tutoriales en línea.

[1]: https://git-scm.com/

Con un VCS, puede:
  * Ver todos los cambios realizados en el proyecto, cuándo se hicieron los cambios y quién los efectuó.
  * Incluir un mensaje con cada cambio para explicar los motivos.
  * Recuperar versiones anteriores del proyecto completo o de archivos individuales.
  * Crear ramas, donde los cambios se pueden hacer experimentalmente. Esta característica permite que se trabaje en varios conjuntos de cambios diferentes (por ejemplo, características o correcciones de errores) al mismo tiempo, posiblemente personas distintas, sin que ello afecte a la rama principal. Más adelante se pueden combinar los cambios que se quieren mantener en la rama principal.
  * Adjuntar una etiqueta a una versión, por ejemplo, para marcar una nueva versión.

Git es un VCS de código abierto rápido, versátil, muy escalable y gratuito. Su autor principal es Linux Torvalds, creador de Linux.

### Control de versiones distribuido
Las instancias anteriores de los VCS, como CVS, Subversion (SVN) y Perforce, usaban un servidor centralizado para almacenar el historial de un proyecto. Esta centralización significaba que un solo servidor también era un único punto de error en potencia.

Git es un sistema distribuido, lo que significa que el historial completo de un proyecto se almacena en el cliente y en el servidor. Se pueden editar archivos sin conexión de red, protegerlos localmente y sincronizarlos con el servidor cuando una conexión esté disponible. Si un servidor deja de funcionar, todavía tendrá una copia local del proyecto. Técnicamente, ni siquiera es necesario tener un servidor. Los cambios pueden pasarse por correo electrónico o compartirse mediante medios extraíbles, pero, en la práctica, nadie usa Git así.

### Terminología de Git
Para entender Git, debe comprender la terminología. Esta es una breve lista de los términos que los usuarios de Git emplean con frecuencia. De momento no se preocupe por los detalles; todos estos términos le irán resultando familiares a medida que avanza por los ejercicios de este módulo.

  * Árbol de trabajo: conjunto de directorios y archivos anidados que contienen el proyecto en el que se trabaja.

  * Repositorio (repo): directorio, situado en el nivel superior de un árbol de trabajo, donde Git mantiene todo el historial y los metadatos de un proyecto. A veces se hace referencia a los repositorios como repos. Un repositorio vacío es aquel que no forma parte de un árbol de trabajo; se usa para compartir o realizar copias de seguridad. Un repositorio vacío suele ser un directorio con un nombre que acaba en `.git`, por ejemplo, `project.git`.

  * Hash: número generado por una función hash que representa el contenido de un archivo u otro objeto como un número de dígitos fijo. Git usa hashes de 160 bits de longitud. Una ventaja de usar códigos hash es que Git puede indicar si un archivo ha cambiado aplicando un algoritmo hash a su contenido y comparando el resultado con el hash anterior. Si se cambia la marca de fecha y hora del archivo, pero el hash del archivo no, Git sabe que el contenido del archivo no se ha modificado.

  * Objeto: un repositorio de Git contiene cuatro tipos de objetos, cada uno identificado de forma única por un hash SHA-1. Un objeto blob contiene un archivo normal. Un objeto árbol representa un directorio, y contiene nombres, valores hash y permisos. Un objeto de confirmación representa una versión específica del árbol de trabajo. Una etiqueta es un nombre asociado a una confirmación.

  * Confirmación: cuando se usa como verbo, confirmar significa crear un objeto de confirmación. Esta acción toma su nombre de las confirmaciones en una base de datos. Significa que se confirman los cambios realizados para que otros usuarios también puedan verlos.

  * Rama: serie con nombre de confirmaciones vinculadas. La confirmación más reciente en una rama se denomina nivel superior. La rama predeterminada, que se crea al inicializar un repositorio, se denomina `main`, y suele tener el nombre `master` en Git. El nivel superior de la rama actual se denomina `HEAD`. Las ramas son una característica increíblemente útil de Git porque permiten a los desarrolladores trabajar de forma independiente (o conjunta) en ramas y luego combinar los cambios en la rama predeterminada.

  * Remoto: referencia con nombre a otro repositorio de Git. Cuando se crea un repositorio, Git crea un remoto denominado `origin`, que es el remoto predeterminado para las operaciones de envío e incorporación de cambios.

  * Comandos, subcomandos y opciones: las operaciones de Git se realizan mediante comandos como `git push` y `git pull`. git es el comando, mientras que `push` o `pull` es el subcomando. El subcomando especifica la operación que quiere que Git realice. Los comandos suelen ir acompañados de opciones, que usan guiones (-) o guiones dobles (--). Por ejemplo, `git reset --hard`.

Estos términos y otros, como `push` e `pull`, tendrán más sentido en breve. Pero tiene que empezar por algún lado, y puede que le resulte útil volver y revisar este glosario de términos después de terminar este módulo.


### Herramientas de línea de comandos de Git
Hay varias GUI diferentes disponibles para Git, incluido GitHub Desktop. Muchos editores de programación, como Visual Studio Code de Microsoft, también tienen una interfaz para Git. Todos funcionan de manera diferente y tienen distintas limitaciones. Ninguno de ellos implementa toda la funcionalidad de Git.

En los ejercicios de este módulo se usa la línea de comandos de Git, en concreto los comandos de Git que se ejecutan en Azure Cloud Shell. Pero la interfaz de la línea de comandos de Git funciona lo mismo independientemente del sistema operativo que se use. Además, la línea de comandos le permite aprovechar toda la capacidad de Git. Los desarrolladores que ven Git solo por medio de una GUI a veces reciben mensajes de error que no pueden resolver, por lo que tienen que recurrir a la línea de comandos para empezar de nuevo.

### Git y GitHub
Cuando trabaje con Git se preguntará sobre las diferencias entre las características que ofrece y las incluidas en GitHub.

Como se ha mencionado anteriormente, Git es un sistema de control de versiones distribuido (DVCS) que varios desarrolladores y otros colaboradores pueden usar para trabajar en un proyecto. Proporciona una manera de trabajar con una o varias ramas locales y luego insertarlas en un repositorio remoto.

GitHub es una plataforma en la nube que usa Git como tecnología principal. Simplifica el proceso de colaboración en proyectos y proporciona un sitio web, más herramientas de línea de comandos y un flujo integral que los desarrolladores y usuarios pueden usar para trabajar juntos. GitHub actúa como el repositorio remoto mencionado anteriormente.

Entre las características clave que ofrece GitHub se incluyen las siguientes:

Incidencias
Debates
Solicitudes de incorporación de cambios
Notificaciones
Etiquetas
Acciones
Bifurcaciones
Proyectos

Para obtener más información sobre GitHub, vea el módulo *[Introducción a GitHub][1]*  de Microsoft Learn o la documentación de ayuda *[Comenzar con GitHub][3]*.



[2]: https://learn.microsoft.com/es-es/training/modules/introduction-to-github
[3]: https://docs.github.com/free-pro-team@latest/github/getting-started-with-github

___

## Ejercicio: Prueba de Git

Para poder crear el primer repositorio, debe asegurarse de que Git está instalado y configurado. Git está preinstalado en Azure Cloud Shell, por lo que podemos usar Git en Cloud Shell, a la derecha.

### Configuración de Git

1. En Cloud Shell, para comprobar que Git está instalado, escriba `git --version`:
``` bash
git --version
```

2. Debería ver una salida similar a la de este ejemplo:
``` bash
git version 2.7.4
```

3. Para configurar Git, debe definir algunas variables globales: `user.name` y `user.email`. Ambas son necesarias para realizar confirmaciones.

4. Establezca su nombre en Cloud Shell con el siguiente comando. Reemplace `<USER_NAME>` por el nombre de usuario que quiere usar.
``` bash
git config --global user.name "<USER_NAME>"
```

5. Ahora, use este comando para crear una variable de configuración user.email; para ello, reemplace `<USER_EMAIL>` por su dirección de correo electrónico:
``` bash
git config --global user.email "<USER_EMAIL>"
```

6. Ejecute el siguiente comando para comprobar que los cambios han funcionado:
``` bash
git config --list
```

7. Confirme que la salida incluye dos líneas similares al siguiente ejemplo. El nombre y la dirección de correo electrónico serán distintos a los que se muestran en el ejemplo.
``` bash
user.name=User Name
user.email=user-name@contoso.com
```

### Configuración del repositorio de Git
Git funciona buscando cambios en los archivos dentro de una determinada carpeta. Vamos a crear una carpeta que actúe como árbol de trabajo (directorio del proyecto) y a permitir que Git sepa sobre ella para que pueda comenzar a seguir los cambios. Se indica a Git que empiece a realizar el seguimiento de los cambios mediante la inicialización de un repositorio de Git en esa carpeta.

Empiece por crear una carpeta vacía para el proyecto y luego inicialice un repositorio de Git dentro de ella.

1. Cree una carpeta con el nombre Cats. Esta carpeta va a ser el directorio del proyecto, también denominado árbol de trabajo. El directorio del proyecto es donde se almacenan todos los archivos relacionados con el proyecto. En este ejercicio, es donde se almacenan el sitio web y los archivos que crean el sitio web y su contenido.
``` bash
mkdir Cats
```

2. Vaya al directorio del proyecto mediante el comando `cd`:
``` bash
cd Cats
```

3. Ahora, inicialice el nuevo repositorio y establezca el nombre de la rama predeterminada en `main`:
Si está ejecutando la versión 2.28.0 o una posterior de Git, use el comando siguiente:
``` bash
git init --initial-branch=main
```
O bien, use el siguiente comando:
``` bash
git init -b main
```
En versiones anteriores de Git, use estos comandos:
``` bash
git init
git checkout -b main
```

Después de ejecutar el comando de inicialización, debería ver una salida similar a la de este ejemplo:
``` bash
Initialized empty Git repository in /home/<user>/Cats/.git/

Switched to a new branch 'main'
```

4. Ahora, use un comando `git status` para mostrar el estado del árbol de trabajo:
``` bash
git status
```
Git responde con esta salida, que indica que `master` es la rama actual. (De hecho, también es la única rama). Por ahora todo está claro.
``` bash
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

5. Use un comando `ls` para mostrar el estado del árbol de trabajo:
``` bash
ls -a
```

Confirme que el directorio contiene un subdirectorio denominado *.git*. (El uso de la opción `-a` con `ls` es importante, ya que Linux normalmente oculta los nombres de archivos y directorios que comienzan con un punto). Esta carpeta es el repositorio de Git: el directorio en el que Git almacena los metadatos y el historial del árbol de trabajo.

Normalmente no se hace nada directamente con el directorio .git. Git actualiza los metadatos a medida que el estado del árbol de trabajo cambia para mantener un seguimiento de lo que ha cambiado en sus archivos. Este directorio es práctico para usted, pero es increíblemente importante para Git.


### Ayuda desde Git
Git, al igual que la mayoría de las herramientas de línea de comandos, tiene una función de ayuda integrada que se puede usar para buscar comandos y palabras clave.

1. Escriba el comando siguiente para obtener ayuda sobre lo que puede hacer con Git:
``` bash
git --help
```

2. El comando muestra la salida siguiente:
``` bash 
usage: git [--version] [--help] [-C <path>] [-c name=value]
       [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
       [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
       [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
       <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   branch     List, create, or delete branches
   checkout   Switch branches or restore working tree files
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   merge      Join two or more development histories together
   rebase     Forward-port local commits to the updated upstream head
   tag        Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
```

Lea las distintas opciones disponibles con Git y observe que cada comando incluye su propia página de ayuda, para cuando empiece a profundizar más. No todos estos comandos tendrán sentido todavía, pero es posible que algunos le resulten familiares si tiene experiencia con un VCS.

En la lección siguiente va a obtener más información sobre los comandos que acaba de probar y los aspectos básicos de Git.

___

## Comandos básicos de Git

Git recuerda los cambios efectuados en los archivos como si tomara instantáneas del sistema de archivos.

Vamos a hablar de algunos comandos básicos para iniciar el seguimiento de los archivos del repositorio. Luego va a guardar la primera "instantánea" con la que Git va a comparar.

#### git status
El primer comando de Git, y el que se usa con más frecuencia, es `git status`. Ya lo ha usado una vez en el ejercicio anterior para ver que había inicializado correctamente el repositorio de Git.

`git status` muestra el estado del árbol de trabajo (y del área de almacenamiento provisional, de la que pronto hablaremos más). Permite ver los cambios que Git está siguiendo en ese momento para poder decidir si quiere pedir a Git que tome otra instantánea.

#### git add 
`git add` es el comando que se usa para indicar a Git que empiece a realizar un seguimiento de los cambios en determinados archivos.

El término técnico *es almacenamiento provisional* de estos cambios. Va a usar `git add` para almacenar provisionalmente los cambios a fin de prepararse para una confirmación. Todos los cambios en los archivos que se han agregado pero que aún no se han confirmado se almacenan en el *área de almacenamiento provisional*.

#### git commit
Después de haber almacenado provisionalmente algunos cambios para su confirmación, puede guardar el trabajo en una instantánea si invoca al comando `git commit`.

Confirmar (o "commit") es un verbo y un sustantivo. Básicamente tiene el mismo significado que cuando se confirma en un plan o se confirma un cambio en una base de datos. Como verbo, la confirmación de cambios significa que se coloca una copia (del archivo, el directorio u otra "cosa") en el repositorio como una nueva versión. Como sustantivo, una confirmación es el pequeño fragmento de datos que asigna una identidad única a los cambios que se confirman. Los datos que se guardan en una confirmación incluyen el nombre del autor y la dirección de correo electrónico, la fecha, los comentarios sobre lo que se ha hecho (y por qué), una firma digital opcional y el identificador único de la confirmación anterior.

#### git log
El comando `git log` permite ver información sobre las confirmaciones anteriores. Cada confirmación tiene un mensaje adjunto (un mensaje de confirmación), y el comando `git log` permite imprimir información sobre las confirmaciones más recientes, como su marca de tiempo, el autor y un mensaje de confirmación. Este comando ayuda a realizar un seguimiento de lo que ha estado haciendo y de los cambios que se han guardado.

#### git help
Ya ha probado el comando `git help`, pero vale la pena recordar ciertas cosas. Use este comando para obtener información fácilmente sobre todos los comandos que conoce hasta ahora y más.

Recuerde que cada comando incluye también su propia página de ayuda. Para encontrar estas páginas de ayuda, escriba `git <command> --help`. Por ejemplo, `git commit --help` muestra una página que proporciona más información sobre el comando git commit y cómo usarlo.



___

## Prueba de conocimientos

1. ¿Cuál de los siguientes escenarios es un caso de uso habitual de un sistema de control de versiones? 
   - [ ] Eliminación de versiones anteriores de un proyecto o archivo para saber que se está trabajando solo con el archivo o los datos más recientes.
   - [ ] Realización de cambios experimentales en el proyecto en una rama aislada.
   - [ ] Recopilación de requisitos de características de un proyecto grande y su comunicación a las partes interesadas.
<!-- Correcto. El uso de ramas para crear diferentes conjuntos de cambios en un proyecto es un caso de uso clave del control de versiones. -->

2. ¿Cuál es otro nombre para un sistema de control de versiones? 
   - [ ] Software de administración de versiones (VMS)
   - [ ] Sistema de administración de control de software (SCM)
   - [ ] Sistema de administración de configuración de software (SCM)
<!-- Correcto. Sistema de administración de configuración de software (SCM). -->

3. ¿Cuál es la diferencia entre Git y GitHub? 
   - [ ] Git permite trabajar con una o más ramas locales y enviar los cambios a un repositorio remoto. GitHub actúa como el repositorio remoto al que se accede por medio de un sitio web o herramientas de línea de comandos.
   - [ ] Git es un sistema de control de versiones distribuido (DVCS) que se ejecuta en la nube. GitHub es una capa de interfaz que proporciona acceso a la tecnología de Git.
   - [ ] Git se usa por parte de un colaborador individual. GitHub se usa por parte de varios colaboradores para simplificar el trabajo de desarrollo en grupo.
<!-- Correcto. Git es la herramienta que se puede usar para trabajar con una rama local y enviar los cambios a un repositorio remoto. GitHub actúa como el repositorio remoto. -->

4. ¿Qué comando de Git ofrece información sobre cómo usar Git? 
   - [ ] git init
   - [ ] git status
   - [ ] git help
<!-- Correcto. Use git help para ver información sobre cómo usar Git. -->
___

## Resumen
Enhorabuena. En este módulo, ha aprendido los aspectos básicos del uso de Git.

Ha aprendido:

- Introducción a los Sistemas de control de versiones (VCS)
- Terminología importante de Git.
- Las diferencias entre Git y GitHub.
- Cómo configurar Git.
- Algunos comandos básicos de Git.

En este punto ya sabe lo suficiente sobre Git para usar el control de versiones por sí mismo en un proyecto básico. La colaboración con otros desarrolladores es donde el control de versiones destaca. Vea los demás módulos de esta ruta de aprendizaje para obtener más información sobre el empleo de Git con otros usuarios.

#### Recursos
Si quiere profundizar más, aquí tiene más recursos:

- Ejecute los comandos `git help tutorial` y `git help tutorial-2`.
- Visite el sitio *[Everyday Git][4]* o use el comando `git help everyday`.
- Revise los *[recursos de aprendizaje de Git y GitHub][5]*.
- Vea el vídeo de *[introducción al resumen de Git][6]*.
- Vea la *[sección de documentación][7]* del *[sitio web oficial de Git][8]*.


[4]: https://git-scm.com/docs/everyday
[5]: https://help.github.com/en/articles/git-and-github-learning-resources
[6]: https://www.youtube.com/watch?v=9uGS1ak_FGg%3Fazure-portal%3Dtrue
[7]: https://git-scm.com/doc
[8]: https://git-scm.com/
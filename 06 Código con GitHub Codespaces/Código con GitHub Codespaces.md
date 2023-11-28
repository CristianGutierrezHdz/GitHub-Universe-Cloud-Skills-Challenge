
## Código con GitHub Codespaces

GitHub Codespaces es un entorno de desarrollo totalmente configurado que se hospeda en la nube. Con GitHub Codespaces, el área de trabajo está disponible desde cualquier equipo con acceso a Internet, junto con todos los entornos de desarrollo configurados.

Objetivos de aprendizaje
Al término de este módulo, sabrá hacer lo siguiente:
- Describir GitHub Codespaces.
- Explicar el ciclo de vida de GitHub Codespace y cómo realizar cada paso.
- Definir las distintas personalizaciones que puede aplicar con GitHub Codespaces.
- Distinguir las diferencias entre GitHub.dev y GitHub Codespaces.
___

## Introducción
GitHub Codespaces es un entorno de desarrollo instantáneo basado en la nube que usa un contenedor para proporcionar lenguajes, herramientas y utilidades comunes para el desarrollo.

En este módulo:, haremos lo siguiente:
- Explorar el ciclo de vida y los procesos de los codespaces.
- Revisar las formas en las que puede personalizar la configuración del codespace.
- Comparar las diferencias entre GitHub Codespaces y GitHub.dev.
- Completar un ejercicio para practicar la codificación en Codespaces.

___ 

## Ciclo de vida de un codespace

Ciclo de vida de un codespace

GitHub Codespaces se puede configurar, lo que le permite crear un entorno de desarrollo personalizado para el proyecto. Al configurar un entorno de desarrollo personalizado para su proyecto, puede tener una configuración de codespace repetible para todos los usuarios del proyecto.

El ciclo de vida de un codespace comienza cuando se crea y termina cuando se elimina. Puede desconectarse y reconectarse a un codespace activo sin que esto afecte a sus procesos en ejecución. También puede detener y reiniciar un codespace sin perder los cambios que haya realizado en su proyecto.

![drawing](./img/codespace-circular-lifecycle.png)

Crear un codespace
Puede crear un codespace en GitHub.com, en Visual Studio Code o en la CLI de GitHub. Existen cuatro formas de crear un codespace:

- Desde una plantilla de GitHub o desde cualquier repositorio de plantillas de GitHub.com para iniciar un nuevo proyecto.
- Desde una rama del repositorio para el trabajo de nuevas características.
- Desde una solicitud de cambios abierta para explorar el trabajo en curso.
- Desde una confirmación en el historial de un repositorio para investigar un error en un punto específico del tiempo.


Puede usar un codespace temporalmente para probar código o volver al mismo codespace para realizar trabajo de características de larga duración.

Puede crear más de un codespace por repositorio o incluso por rama. Sin embargo, hay límites respecto al número de codespaces que puede crear y ejecutar al mismo tiempo. Si alcanza el número máximo de codespaces e intenta crear otro, aparece un mensaje que indica que se debe quitar o eliminar un codespace existente para poder crear uno nuevo.

Puede crear un nuevo codespace cada vez que desarrolle en GitHub Codespaces o mantener un codespace de larga duración para una característica. Si va a iniciar un proyecto nuevo, cree un codespace a partir de una plantilla y publíquelo en un repositorio de GitHub más adelante.

Al crear un codespace cada vez que se trabaja en un proyecto, debe enviar los cambios periódicamente para asegurarse de que todas las confirmaciones nuevas estén en GitHub. Al usar un codespace de larga duración para un proyecto nuevo, incorpore los cambios desde la rama predeterminada del repositorio cada vez que empiece a trabajar en el codespace. Esto permite al entorno obtener las últimas confirmaciones. El flujo de trabajo es similar a trabajar con un proyecto en una máquina local.

Los administradores de repositorios pueden habilitar las precompilaciones de GitHub Codespaces para que un repositorio acelere la creación de un codespace.

Para ver un tutorial y una guía detallados, consulte los recursos Guía para principiantes para aprender a codificar con GitHub Codespaces y Desarrollar en un codespace que se encuentran en la unidad Resumen al final de este módulo.

#### Proceso de creación de un codespace

![drawing](./img/codespace-connection-editor.png)

Al crear un codespace de GitHub tienen lugar cuatro procesos:

1. Se asignan al codespace una máquina virtual y almacenamiento.
2. Se crea un contenedor.
3. Se establece una conexión con el codespace.
4. Se realiza una configuración posterior a la creación.

#### Guardar cambios en un codespace
Cuando se conecta a un codespace a través de la web, se habilita de forma automática la opción de autoguardado para guardar los cambios cuando haya transcurrido una cantidad de tiempo específica. Al conectarse a un codespace a través de Visual Studio Code en ejecución en el escritorio, debe habilitar Autoguardado.

El trabajo se guarda en una máquina virtual en la nube. Puede cerrar y detener un codespace y volver al trabajo guardado más adelante. Si tiene cambios sin guardar, recibirá un mensaje para guardarlos antes de salir. Sin embargo, si el codespace se elimina, se pierde el trabajo. Para guardar el trabajo, debe confirmar los cambios y enviarlos al repositorio remoto o publicar el trabajo en uno nuevo si ha creado el codespace a partir de una plantilla.

#### Apertura de un codespace existente
Puede volver a abrir cualquiera de los codespaces activos o detenidos en GitHub.com, en un IDE de JetBrains, en Visual Studio Code o mediante la CLI de GitHub.

Para reanudar un codespace existente, puede ir al repositorio donde existe el codespace, presionar la tecla "," en el teclado y seleccionar Reanudar este codespace o bien abrir https://github.com/codespaces en el explorador, seleccionar el repositorio y, a continuación, seleccionar el codespace existente.

#### Tiempos de espera de un codespace
Si un codespace está inactivo o si sale del codespace sin detenerlo de forma explícita, la aplicación agota el tiempo de espera después de un período de inactividad y deja de ejecutarse. El tiempo de espera predeterminado es después de 30 minutos de inactividad. No se puede personalizar la duración del período de tiempo de espera para los nuevos codespaces. Cuando se agota el tiempo de espera de un codespace, se preservan los datos de la última vez que haya guardado los cambios.

#### Conexión a Internet al usar GitHub Codespaces
Un codespace requiere conexión a Internet. Si la conexión a Internet se pierde mientras trabaja en un codespace, no podrá acceder a este. Sin embargo, cualquier cambio pendiente de confirmación se guarda. Al restablecer la conexión a Internet, puede acceder al codespace en el mismo estado que se dejó cuando se perdió la conexión.

Si tiene una conexión de internet inestable, debe confirmar e insertar los cambios frecuentemente.

#### Cerrar o detener un codespace
Si sale del codespace sin ejecutar el comando para detenerlo (por ejemplo, cierra la pestaña del explorador) o si deja el codespace en ejecución sin interacción, el codespace y sus procesos en ejecución continuarán durante el período de tiempo de espera de inactividad. El período de tiempo de espera de inactividad predeterminado es de 30 minutos. Puede definir su configuración de tiempo de espera personal para los codespaces que cree, pero una directiva de tiempo de espera de la organización puede invalidarla.

Solo los codespaces en ejecución conllevan cargos de CPU. Un codespace detenido solo conlleva costos de almacenamiento.

Puede detener y reiniciar un codespace para aplicar cambios. Por ejemplo, si cambia el tipo de máquina que se usa para el codespace, debe detenerlo y reiniciarlo para que el cambio surta efecto. Al cerrar o detener su codespace, todos los cambios pendientes de confirmación se preservan hasta que vuelva a conectarse al codespace.

También puede detener el codespace y elegir restablecerlo o eliminarlo si encuentra un error o algo inesperado.

#### Recompilación de un codespace
Puede recompilar el codespace para implementar cambios en la configuración de contenedor de desarrollo. Para la mayoría de los usos, puede crear un codespace como alternativa a recompilar uno. Al recompilar su codespace, las imágenes de la memoria caché aceleran el proceso de recompilación. También puede realizar una recompilación completa para borrar la memoria caché y recompilar el contenedor con imágenes nuevas.

Al recompilar el contenedor en un codespace, los cambios realizados fuera del directorio /workspaces se borran. Los cambios realizados dentro del directorio /workspaces, incluido el clon del repositorio o la plantilla desde la que ha creado el codespace, se conservan al recompilar.

#### Eliminar un codespace
Puede crear un codespace para una tarea determinada. Después de enviar los cambios a una rama remota, puede eliminar ese codespace de forma segura.

Si intenta eliminar un codespace con confirmaciones de GIT sin enviar, el editor le notifica que tiene cambios que no se han enviado a una rama remota. Puede enviar cualquier cambio deseado y, después, eliminar su codespace. También puede continuar con la eliminación del codespace y los cambios pendientes de confirmación o exportar el código a una rama nueva sin crear un codespace.

Los codespaces detenidos que permanecen inactivos durante un período de tiempo especificado se eliminan automáticamente. Los codespaces inactivos se eliminan después de 30 días, pero puede personalizar los intervalos de retención de codespaces.

___

## Personalizar su codespace

GitHub Codespaces es un entorno dedicado. Puede configurar los repositorios con un contenedor de desarrollo para definir su entorno predeterminado de GitHub Codespaces y personalizar la experiencia de desarrollo en todos los codespaces con dotfiles y Sincronización de configuración.

#### Qué se puede personalizar

Existen muchas formas de personalizar su codespace. Se revisarán a continuación.

- Sincronización de configuración: puede sincronizar la configuración de Visual Studio Code (VS Code) entre la aplicación de escritorio y el cliente web de VS Code.
- Dotfiles: puede usar un repositorio dotfiles para especificar scripts, preferencias del shell y otras configuraciones.
- Cambiar un codespace de nombre: al crear un codespace, se le asigna un nombre para mostrar generado automáticamente. Si tiene varios codespaces, el nombre para mostrar le ayuda a diferenciar entre ellos. Puede cambiar el nombre para mostrar del codespace.
- Cambiar el shell: puede cambiar el shell en un codespace para mantener su configuración habitual. Al trabajar en un codespace, puede abrir una nueva ventana de terminal con un shell de su elección, cambiar el shell predeterminado para las nuevas ventanas de terminal o instalar un nuevo shell. También puedes usar dotfiles para configurar el shell.
- Cambiar el tipo de máquina: puede cambiar el tipo de máquina que ejecuta el codespace para usar los recursos adecuados para el trabajo que lleva a cabo.
- Establecer el editor predeterminado: puede establecer el editor predeterminado para codespaces en su página de configuración personal. Establezca el editor de su preferencia para que, al crear un codespace o abrir un codespace existente, se abra en el editor predeterminado.
    - Visual Studio Code (aplicación de escritorio)
    - Visual Studio Code (aplicación cliente web)
    - JetBrains Gateway: para abrir codespaces en un IDE de JetBrains
    - JupyterLab (interfaz web para Project Jupyter)
- Establecer la región predeterminada: puede configurar la región predeterminada en la página de configuración de perfil de GitHub Codespaces para personalizar el lugar donde se conservan sus datos.
Establecer el tiempo de espera: un codespace dejará de ejecutarse después de un período de inactividad. De manera predeterminada, este período es de 30 minutos, pero puede especificar un período de tiempo de espera predeterminado más largo o más corto en su configuración personal en GitHub. La configuración actualizada se aplica a - los codespaces que cree o a los ya existentes la próxima vez que los inicie.
- Configuración de eliminación automática: los codespaces inactivos se eliminan de forma automática. Puede elegir cuánto tiempo se conservan los codespaces detenidos, hasta un máximo de 30 días.

En la unidad Resumen, al final de este módulo, existe información adicional e instrucciones detalladas relativas a la personalización.

#### Agregar al codespace con extensiones o complementos
Puede agregar complementos y extensiones en un codespace para personalizar su experiencia en JetBrains y VS Code.

#### Extensiones de VS Code

Si trabaja en sus codespaces en el cliente web o la aplicación de escritorio de VS Code, puede agregar cualquier extensión que necesite desde Visual Studio Code Marketplace. Consulte el artículo sobre *[compatibilidad con el desarrollo remoto y GitHub Codespaces][1]* en la documentación de VS Code para obtener información sobre cómo se ejecutan las extensiones en GitHub Codespaces.

[1]: https://code.visualstudio.com/api/advanced-topics/remote-extensions

Si ya utiliza VS Code, puede usar Sincronización de configuración para sincronizar automáticamente las extensiones, configuraciones, temas y métodos abreviados de teclado entre la instancia local y cualquier codespace que cree.

#### Complementos de JetBrains
Si trabaja con los codespaces en un IDE de JetBrains, puede agregar complementos desde el Marketplace de JetBrains.

___ 

## Codespaces versus GitHub.dev editor
Probablemente se pregunte cuándo debe usar GitHub Codespaces y cuándo GitHub.dev.

Puede usar GitHub.dev para navegar por archivos y repositorios de código fuente desde GitHub, así como hacer cambios de código y confirmarlos. Puede abrir cualquier repositorio, bifurcación o solicitud de incorporación de cambios en el editor GitHub.dev.

Si quiere realizar tareas más complicadas, como probar el código, use GitHub Codespaces. Se asocia con un proceso, por lo que puede compilar el código, ejecutarlo y tener acceso de terminal. GitHub.dev no incluye ningún proceso. Con GitHub Codespaces se obtiene la potencia de una máquina virtual (VM) personal con acceso de terminal, de la misma forma que puede usar el entorno local, solo en la nube.

#### Comparison of Codespaces and GitHub.dev
En la tabla siguiente se enumeran las diferencias principales entre Codespaces y GitHub.dev:

|   | GitHub.dev | GitHub Codespaces |
|:------------:|:------------:|:------------:|
| Costee |	Gratuito |	Cuota mensual gratuita de uso para cuentas personales |
| Disponibilidad |	Disponible para todos en GitHub.com |	Disponible para todos en GitHub.com |
| Startup |	GitHub.dev se abre instantáneamente al presionar una tecla y puede comenzar a usarlo de inmediato sin tener que esperar a su configuración o instalación. | Al crear o reanudar un codespace, a este se le asigna una máquina virtual y el contenedor se configura en función del contenido de un archivo devcontainer.json. Esta configuración tarda unos minutos en crear el entorno de desarrollo. | 
| Proceso |	No hay cálculos asociados, así que no podrá compilar y ejecutar su código ni utilizar el terminal integrado. | Con GitHub Codespaces se obtiene la eficacia de una máquina virtual dedicada para ejecutar y depurar la aplicación. |
| Acceso al terminal | Ninguno |	GitHub Codespaces proporciona un conjunto común de herramientas de manera predeterminada, lo que significa que puede utilizar el terminal exactamente como lo haría en su entorno local. |
| Extensiones |	En la vista de extensiones solo aparece un subconjunto de las extensiones que pueden ejecutarse en la web y que se pueden instalar. | Con GitHub Codespaces se pueden usar la mayoría de las extensiones de Visual Studio Code Marketplace. |

#### Continuación del trabajo en Codespaces
Puede iniciar el flujo de trabajo en Github.dev y seguir trabajando en un codespace. Si intenta acceder a la vista de ejecución y depuración o al terminal, se le notifica que no están disponibles en GitHub.dev.

Para continuar el trabajo en un codespace, seleccione **Continuar trabajando en**.... Seleccione **Crear un codespace** para crear un codespace en la rama actual. Antes de que elijas esta opción, debes confirmar cualquier cambio.

___

## Ejercicio: Código con Codespaces y Visual Studio Code

Ahora que comprende el ciclo de vida y los procesos de Codespaces, es el momento de practicar la codificación en Codespaces y Visual Studio Code (VS Code). Siga las instrucciones a continuación para completar este ejercicio.

#### Instrucciones
1. Haga clic con el botón derecho en el vínculo del *[ejercicio de GitHub][2]* para abrirlo en una pestaña nueva.
2. En la página principal del ejercicio de GitHub, haga clic con el botón derecho en el botón Iniciar curso para abrirlo en una pestaña nueva.
    - En dicha pestaña, la mayoría de los mensajes se rellenan automáticamente.
    - Para el propietario, elija su cuenta personal o una organización para hospedar el repositorio.
    - Se recomienda crear un repositorio público, ya que los repositorios privados usarán minutos de Acciones.
3. Desplácese hacia abajo y seleccione el botón Crear repositorio en la parte inferior del formulario.
4. Una vez creado el nuevo repositorio, espere unos 20 segundos y actualice la página. Siga las instrucciones detalladas del archivo LÉAME del nuevo repositorio.

[2]: https://github.com/skills/code-with-codespaces

Cuando finalice el ejercicio en GitHub, vuelva aquí para:
- Completar una prueba de conocimientos.
- Revisar un resumen de lo que ha aprendido en este módulo.
- Obtener un distintivo por completar este módulo.

___


## Prueba de conocimientos

#### Comprobación de conocimientos

1. ¿En qué directorio se coloca el clon después de crear un codespace? 
- [ ] `/workspaces directory`
- [ ] `Directorio /temp`
- [ ] `Directorio ~/.bashrc`
<!-- Correcto. Después de crear un codespace, el clon se coloca en el directorio /workspace. -->

Directorio Linux
2. ¿Cuál es el número máximo de codespaces que puede crear por repositorio o rama? 
- [ ] Solo puede crear dos codespaces.
- [ ] Puede crear un total de diez codespaces.
- [ ] Puede crear un total de treinta codespaces.
- [ ] Puede crear un número ilimitado de codespaces por repositorio o rama, en función del espacio disponible. Cuando se alcanza una cantidad máxima de recursos, aparece un mensaje que indica que un codespace existente debe quitarse o eliminarse para poder crear uno nuevo.
<!-- Correcto. Puede tener un número ilimitado de codespaces por repositorio o incluso por rama. Sin embargo, hay límites respecto al número de codespaces que puede crear y ejecutar al mismo tiempo. -->


3. ¿Qué ocurre cuando un codespace pierde la conectividad a Internet? 
- [ ] Si la conexión a Internet se pierde mientras trabaja en un codespace, no podrá acceder a este.
- [ ] Un codespace no requiere conexión a Internet. Puedo acceder a mi codespace con independencia de que se pierda la conectividad.
- [ ] Si pierde la conexión a Internet mientras trabaja en su codespace, los cambios no se guardan.
<!-- Correcto. Un codespace requiere conexión a Internet. Si la conexión a Internet se pierde mientras trabaja en un codespace, no podrá acceder a este. -->

4. ¿Qué define el principio del ciclo de vida de un codespace? 
- [ ] El ciclo de vida de un codespace comienza cuando se crea y termina cuando se elimina.
- [ ] El ciclo de vida de un codespace comienza inmediatamente cuando GitHub se abre y termina cuando se cierra el software.
- [ ] El ciclo de vida de un codespace comienza cuando se crea un repositorio y termina cuando se elimina.
<!-- Correcto. El ciclo de vida de un codespace comienza cuando se crea y termina cuando se elimina. -->

___

## Resumen

En este módulo ha obtenido información sobre GitHub Codespaces, un entorno de desarrollo totalmente configurado que se hospeda en la nube.

Ahora debería poder hacer lo siguiente:

- Describir GitHub Codespaces.
- Explicar el ciclo de vida de GitHub Codespaces y cómo realizar cada paso.
- Definir las distintas personalizaciones que puede aplicar con GitHub Codespaces.
- Distinguir las diferencias entre GitHub.dev y GitHub Codespaces.

#### Recursos
Aquí tiene algunos vínculos para obtener más información sobre los temas analizados en este módulo:

- *[Guía para principiantes para aprender a codificar con GitHub Codespaces][5]*
- *[Desarrollar en un codespace][6]* 
- *[Personalizar tu codespace][7]* 

#### Envío de comentarios
Use este *[formulario de incidencia][8]* para proporcionar comentarios relacionados con el contenido o sugerir cambios para este módulo de Microsoft Learn. GitHub mantiene este contenido y un miembro del equipo evaluará las prioridades de la solicitud. Gracias por darse el tiempo de mejorar nuestro contenido.

[5]: https://github.blog/2023-02-22-a-beginners-guide-to-learning-to-code-with-github-codespaces/
[6]: https://docs.github.com/en/codespaces/developing-in-codespaces/developing-in-a-codespace
[7]: https://docs.github.com/en/codespaces/customizing-your-codespace
[8]: https://github.com/githubpartners/microsoft-learn/issues/new/choose

___
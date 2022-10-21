Configuración de un repositorio
git init git clone git config
Este tutorial ofrece una visión general sobre cómo configurar un repositorio con el sistema de control de versiones Git. Se explicará cómo iniciar un repositorio de Git para un proyecto nuevo o existente. A continuación, se ofrecen ejemplos de workflows de repositorios creados localmente o clonados de repositorios remotos. La guía supone que estás mínimamente familiarizado con la interfaz de línea de comandos.

video thumbnail
Los puntos de mayor nivel que cubrirá esta guía son:

Inicio de un nuevo repositorio de Git
Clonación de un repositorio de Git existente
Confirmación de la versión modificada de un archivo al repositorio
Configuración de un repositorio de Git para la colaboración remota
Comandos comunes de control de versiones de Git
Al final de este módulo, deberías poder crear un repositorio de Git, usar comandos comunes de Git, confirmar un archivo modificado, ver el historial de tu proyecto y configurar una conexión a un servicio de almacenamiento de Git (Bitbucket).

¿Qué es un repositorio de Git?
Un repositorio de Git es un almacenamiento virtual de tu proyecto. Te permite guardar versiones del código a las que puedes acceder cuando lo necesites.

Inicio de un nuevo repositorio: git init
Para crear un nuevo repositorio, usa el comando git init. git init es un comando que se utiliza una sola vez durante la configuración inicial de un repositorio nuevo. Al ejecutar este comando, se creará un nuevo subdirectorio .git en tu directorio de trabajo actual. También se creará una nueva rama principal.

Versión de un proyecto existente con un repositorio de Git nuevo
En este ejemplo, suponemos que ya cuentas con una carpeta de proyecto en la que quieres crear un repositorio. Primero deberás establecer el directorio de la carpeta raíz del proyecto con el comando cd y luego ejecutar git init.

cd /path/to/your/existing/code 
git init
Apuntar git init a un directorio de proyecto existente hará que se ejecute la misma configuración de inicio mencionada arriba, pero en el ámbito de ese directorio.

git init <project directory>
Visita la página sobre git init para obtener información más detallada sobre el comando git init.

Clonación de un repositorio existente: git clone
Si un repositorio ya se ha configurado en un repositorio central, el comando de clonación es la manera más común de obtener una copia de desarrollo local. Igual que git init, la clonación suele ser una operación única. Una vez que un desarrollador ha obtenido una copia de trabajo, todas las operaciones de control de versiones se administran por medio de su repositorio local.

git clone <repo url>
El comando git clone se usa para crear una copia o clonar un repositorio remoto. Se utiliza git clone con la URL de un repositorio. Git es compatible con varios protocolos de red y sus formatos de URL correspondientes. En este ejemplo, usaremos el protocolo Git SSH. Las URL Git SSH siguen la siguiente estructura: git@HOSTNAME:USERNAME/REPONAME.git.

Un ejemplo de una URL Git SSH sería el siguiente: git@bitbucket.org:rhyolight/javascript-data-store.git, donde los valores de la plantilla equivalen a:

HOSTNAME: bitbucket.org
USERNAME: rhyolight
REPONAME: javascript-data-store
Al ejecutarlo, se extraerá la última versión de los archivos del repositorio remoto en la rama principal y se añadirá a una nueva carpeta. Esta carpeta nueva tendrá el mismo nombre que el repositorio (REPONAME), en este caso, javascript-data-store. La carpeta contendrá el historial completo del repositorio remoto y una rama principal recién creada.

Para obtener más información sobre el uso de git clone y los formatos de URL compatibles con Git, visita la página sobre git clone.

Guardar cambios en el repositorio: git add y git commit
Ahora que has iniciado o clonado un repositorio, puedes realizar commits en la versión del archivo. Para el siguiente ejemplo asumiremos que has configurado un proyecto en /path/to/project. Los pasos son los siguientes:

Cambia el directorio a /path/to/project
Crea un archivo nuevo CommitTest.txt con el contenido "test content for git tutorial"
Ejecuta el comando git add para añadir CommitTest.txt al área de preparación del repositorio
Crea un commit nuevo con un mensaje que describa qué trabajo se ha hecho en el commit
cd /path/to/project 
echo "test content for git tutorial" >> CommitTest.txt 
git add CommitTest.txt 
git commit -m "added CommitTest.txt to the repo"
Después de llevar este ejemplo, en el historial de tu repositorio se mostrará CommitTest.txt y se realizará el seguimiento de las actualizaciones futuras a este archivo.

En este ejemplo se han introducido dos comandos git adicionales: add y commit. Ha sido un ejemplo muy limitado, pero ambos comandos se tratan más en profundidad en las páginas sobre git add y git commit. El comando git add se suele usar con la opción --all. Al ejecutar git add --all, se añadirán todos los archivos con cambios y sin seguimiento al repositorio y se actualizará el árbol de trabajo.

Colaboración entre repositorios: git push
Es importante comprender que la idea de "copia de trabajo" de Git es muy distinta a la copia de trabajo que se obtiene al extraer código fuente de un repositorio SVN. A diferencia de SVN, Git no distingue entre las copias de trabajo y el repositorio central: todos son repositorios Git completos.

Por tanto, colaborar con Git es intrínsecamente distinto que con SVN. Mientras que SVN depende de la relación entre el repositorio central y la copia de trabajo, el modelo de colaboración de Git se basa en la interacción entre repositorios. En lugar de insertar una copia de trabajo en el repositorio central de SVN, se extraen o envían commits de un repositorio a otro.

Por supuesto, nada te impide dar un significado especial a ciertos repositorios Git. Por ejemplo, con solo definir un repositorio de Git como el "central", es posible replicar un workflow centralizado usando Git. Esto se consigue por medio de convenciones, no porque esté integrado en el propio VCS.

Repositorios bare (vacíos) frente a repositorios clonados
Si en la sección anterior, "Inicio de un nuevo repositorio", has usado git clone para configurar tu repositorio local, entonces ya está listo para la colaboración remota. El comando git clone configura automáticamente el repositorio con un remote que apunta a la URL Git de donde lo has clonado. Esto significa que, una vez hagas cambios en un archivo y lo confirmes, puedes enviar los cambios al repositorio remoto con git push.

Si has usado el comando git init para crear un repositorio nuevo, entonces no tendrás ningún repositorio remoto al cual enviar cambios. Un patrón común a la hora de iniciar un nuevo repositorio es ir a un servicio Git alojado, como Bitbucket, y crear un repositorio ahí. El servicio te proporcionará una URL Git que podrás añadir a tu repositorio de Git local y enviar con git push al repositorio alojado. Una vez que hayas creado un repositorio remoto con el servicio de tu elección, deberás actualizar tu repositorio local con una asignación. Comentaremos este proceso en la guía de ajustes y configuración que hay más adelante.

Si prefieres alojar tu propio repositorio remoto, deberás configurar un "repositorio bare". Tanto git init como git clone aceptan el argumento --bare. Un repositorio bare se suele usar para crear un repositorio central de Git remoto.

Ajustes y configuración: git config
Una vez configurado el repositorio remoto, deberás añadir una URL de repositorio remoto a tu git config local y configurar una rama de nivel superior para tus ramas locales. El comando git remote te ofrece tal utilidad.

git remote add <remote_name> <remote_repo_url>
Este comando asignará el repositorio remoto en  a una referencia en tu repositorio local bajo . Una vez asignado el repositorio remoto, puedes enviar ramas locales ahí.

git push -u <remote_name> <local_branch_name>
Este comando enviará la rama del repositorio local < local_branch_name > al repositorio remoto < remote_name >.

Para profundizar más en el comando git remote, consulta la página sobre git remote.

Además de configurar una URL de repositorio remoto, puede que también necesites configurar ajustes globales de Git como el username (nombre de usuario) o el email. El comando git config te permite configurar la instalación de Git (o un repositorio individual) desde la línea de comandos. Este comando puede definir cualquier cosa: desde la información de usuario, hasta las preferencias o el comportamiento del repositorio. A continuación, se listan varias opciones de configuración.

Git almacena las opciones de configuración en tres archivos distintos, lo que te permite ajustar opciones para repositorios individuales (local), usuarios (global) o todo el sistema (sistema):

Local: /.git/config —ajustes específicos del repositorio.
Global: ~/.gitconfig —ajustes específicos del usuario. Aquí es donde se almacenan las opciones configuradas con la marca --global.
Sistema: $(prefix)/etc/gitconfig —ajustes de todo el sistema.
Define el nombre del autor que se va a usar en todas las confirmaciones del repositorio actual. Normalmente, será preferible utilizar el indicador --global para establecer las opciones de configuración del usuario actual.

git config --global user.name <name>
Define el nombre del autor que se va a usar en todas las confirmaciones del usuario actual.

Añadir la opción --local o, sencillamente, no pasar una opción de configuración, establecerá el user.name para el repositorio local actual.

git config --local user.email <email>
Define el correo electrónico del autor que se va a usar en todas las confirmaciones del usuario actual.

git config --global alias.<alias-name> <git-command>
Crea un atajo de teclado para un comando Git. Es una utilidad muy potente para crear atajos personalizados para comandos que uses con frecuencia. Veamos este ejemplo:

git config --global alias.ci commit
De este modo se crea el comando ci, que puedes ejecutar como atajo para git commit. Para obtener más información sobre los alias git, visita la página sobre git config.

git config --system core.editor <editor>
Define el editor de texto que se utilizará con comandos como git commit para todos los usuarios en la máquina actual. El argumento  debería ser el comando que abra el editor deseado (por ejemplo, vi). En este ejemplo introducimos la opción --system. La opción --system configurará todo el sistema, lo que significa todos los usuarios y repositorios de una máquina. Para información más detallada sobre los niveles de configuración visita la página sobre git config.

git config --global --edit
Abre el archivo de configuración global en un editor de texto para editarlo de forma manual. Puedes encontrar una detallada guía acerca de cómo configurar un editor de texto para usarlo con Git en la página de configuración de Git.

Análisis
Todas las opciones de configuración se almacenan en archivos de texto sin formato, así que el comando git config en realidad no es más que una interfaz práctica de la línea de comandos. Generalmente, solo tendrás que configurar la instalación de Git la primera vez que empieces a trabajar con una máquina de desarrollo nueva y, en prácticamente todos los casos, querrás usar la marca --global. Una excepción importante es cuando quieras invalidar la dirección de correo electrónico del autor. Es posible que desees usar tu dirección personal para repositorios personales y de código abierto y tu dirección de correo profesional para los repositorios relacionados con el trabajo.

Git almacena las opciones de configuración en tres archivos distintos, lo que te permite ajustar opciones para repositorios individuales, usuarios o todo el sistema.

/.git/config – Configuración específica del repositorio.
~/.gitconfig —ajustes específicos del usuario. Aquí es donde se almacenan las opciones configuradas con la marca --global.
$(prefix)/etc/gitconfig – Configuración de todo el sistema.
Cuando se producen conflictos entre las opciones de estos archivos, la configuración local sobrescribe la configuración del usuario que, a su vez, sobrescribe todo el sistema. Si abres alguno de estos archivos, podrás ver ejemplos como este:

[user] name = John Smith email = john@example.com [alias] st = status co = checkout br = branch up = rebase ci = commit [core] editor = vim
Puedes editar estos valores de forma manual para que tengan el mismo efecto que git config.

Ejemplo
Lo primero que debes hacer después de instalar Git es introducir tu nombre y tu correo electrónico y personalizar la configuración predeterminada. Una configuración predeterminada habitual puede tener un aspecto similar a este:

Indícale a Git quién eres git config

git --global user.name "John Smith" git config --global user.email john@example.com
Selecciona tu editor de texto favorito.

git config --global core.editor vim
Añade algunos alias de tipo SVN.

git config --global alias.st status 
git config --global alias.co checkout 
git config --global alias.br branch 
git config --global alias.up rebase 
git config --global alias.ci commit
De este modo obtendrás el archivo ~ /.gitconfig de la sección anterior. Echa un vistazo más a fondo a la configuración de Git en la página de configuración de Git.
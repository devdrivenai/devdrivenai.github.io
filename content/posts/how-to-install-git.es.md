---
title: "Cómo instalar Git"
date: 2023-05-30
draft: false
author: devdrivenai
description: De cómo instalar y conectar Git y GitHub en Windows y Ubuntu
categorías: ['cómo', 'instalación']
etiquetas: ['git', 'github', 'windows', 'ubuntu', 'gh-cli']
---

## Por qué instalar Git (y ¿por qué no?)

¡Hola! 

Tal vez vos ya viniste a este post con la intención de instalar Git. Si tal es el caso, podés ir directamente a la siguiente sección (si querés, podés ayudarte con los enlaces en el índice o "Tabla de Contenidos", más arriba).
Sin embargo, si te estás preguntando por qué deberías instalarlo, te comento algunos aspectos interesantes:
- Es como un `CTRL + Z` que nos permite volver unos pasos atrás sin tener que acordarnos de memoria de qué líneas cambiamos. Por esto se le llama sistema de *control de versiones*.
- Nos permite trabajar en equipo de manera tal que varias personas van registrando cambios en su máquina y luego todo se sincroniza en un "cajón" central (llamado repositorio, o *repo* para los amigos). Por esto se le llama sistema *distribuido* de control de versiones.
- Nos permite recuperar un archivo que borramos (o que alguien borró) por accidente o error.
- Nos permite ver cómo se resolvió un problema similar sin estar buscando archivo por archivo, línea por línea (buscando por *commit*, es decir cuándo se hizo ese cambio en específico).
- Nos permite llevar un control increíble sobre qué se cambia y cuándo en nuestro código.
- Y muchas más ventajas.

Ahora que estás al tanto de todo eso, me gustaría preguntarte, ¿por qué no? ¿Tal vez porque te parece muy complejo? Si tal es el caso, a decir verdad, es cierto que *todo* es un poco más pesado y complicado al principio, pero si lo integrás en tu flujo de trabajo en cada proyecto que hacés, de a poquito se va a ir ganando un lugar en tu corazón, tomame la palabra.

*Premisas asumidas en este artículo*: asumo que estás trabajando en una máquina con Windows, con WSL (Ubuntu) instalado. No obstante, si estás trabajando en uno solo de ellos (Windows o Ubuntu), las instrucciones pertinentes en este artículo deberían funcionar para vos.

## Instalación de Git en Windows

Si queremos instalar Git en Windows, vamos a tener que visitar primero [esta URL](https://git-scm.com/download/win). Una vez allí, hacemos click on `Click here to download` en la parte superior de la página.

Una vez descargado el instalador, podemos hacer clic y seguir las indicaciones. No obstante, al menos en mi caso, prefiero personalizar algunas cositas. Por ejemplo:
- Me encanta agregar un perfil del Git Bash al Windows Terminal (esta es una opción que me encanta, ya que desde el Terminal, podemos gestionar varias pestañas con diversos shells, como por ejemplo Git Bash, WSL, etc., simultáneamente, lo cual no es posible -o al menos, no tan fácilmente- hacer en Git Bash).
- En el paso del editor predeterminado, suelo elegir VSC (Visual Studio Code), dado que de todos modos podría, si llegara a desearlo o necesitarlo, abrir los archivos con Vim desde el Git Bash.
- También, prefiero modificar el nombre predeterminado de la rama principal (para nuevos repos) para que sea `main` (va a aparecer una opción para hacerlo).

Vas a ver que hay muchas más posibilidades de personalización que se nos ofrecen durante el proceso de instalación. En mi caso, estos son mis 'overrides' y, por ahora, me quedo con los valores predeterminados para el resto. Pero en tu caso, obviamente, no tenés por qué escoger igual. Podés elegir los valores que mejor se adecúen a tu forma de trabajar. Además, tengamos en cuenta que igualmente es posible [cambiar cualquier valor](https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Configurando-Git-por-primera-vez) de nuestra configuración de Git más tarde, desde el archivo `.gitconfig` que debería estar ubicado en el directorio `Git/etc/`, dentro de nuestra ruta de instalación (la predeterminada es `C:/Program Files/`, así que, por ejemplo: `C:/Program Files/Git/etc/.gitconfig`) o el archivo `config` dentro de la carpeta `.git` de un repo en particular (si queremos que esa config sea especifica para este repo).

## Instalación de Git en Linux (Ubuntu)

Si estás en Ubuntu, es muy probable que ya tengas Git instalado. No obstante, no estaría mal asegurarse de ello.

Así que, primero vamos a comprobar si Git ya está instalado. Bueno, en realidad, comprobemos si nuestras fuentes* (["¡Pará! ¿Y eso de 'las fuentes' de qué va?"](https://www.cyberciti.biz/faq/what-does-sudo-apt-get-update-command-do-on-ubuntu-debian/). Artículo previo en inglés: [este es en español](https://keepcoding.io/blog/como-configurar-un-repositorio-en-linux/).) estén actualizadas:

> *NOTA TLDR: asegurarnos de que los repos remotos que nos brindan nuestro software, tengan la última versión de manera local. 

```shell
sudo apt update
```
(vamos a tener que escribir la contraseña de nuestro usuario en Ubuntu, ya que `sudo` exige permisos de administrador)

... y, si algo requiere de actualización, actualicemos:

```shell
sudo apt upgrade
```

Vamos a tener que escibir `y` para aceptar las modificaciones, y luego nuestros paquetes se actualizarán. (O simplemente `sudo apt upgrade -y` en un solo paso.)

Ahora, comprobemos si ya tenemos `git`:

```shell
git --version
```

Por lo general, ya va a estar instalado, en cuyo caso simplemente mostrará la versión de git, pero si la respuesta consiste en un mensaje del estilo de 'git: command not found', tendremos que instalarlo.

No hay problema, hacerlo es muy sencillo:

```shell
sudo apt install git
```

> *NOTA: también podríamos usar `apt-get` en vez de `apt`, [pero este último elimina versiones anteriores y es más moderno](https://aws.amazon.com/compare/the-difference-between-apt-and-apt-get/), entre otras cosas.

En mi caso, recibo un mensaje que dice: `git is already the newest version`, pero a vos ahora debería permitirte instalarlo, pidiéndote tu confirmación.

Una vez terminada la instalación, a fin de comprobar que todo haya salido bien, ingresamos:

```shell
git --version
```

Esto debería mostrarnos la versión instalada de Git.

Y ya está. Ya tenemos Git instalado. Lo que sí que ahora va a haber que configurarlo.

## Creación de una cuenta de GitHub (Windows y Ubuntu)

La creación de una cuenta en [GitHub](https://github.com) debería ser algo muy sencillo de realizar, en gran parte gracias a la magnífica experiencia que GitHub ofrece al registrar una cuenta. No quiero hacer mucho spoiler acá, prefiero que vos lo experimentes de primera mano. Lo que te puedo decir es que es una de las mejores experiencias de registro que he visto en mi vida.

No obstante, una cosa que puede que queramos tener en cuenta es que, más tarde, cuando *pusheemos* (o "publiquemos") nuestros commits a GitHub, nuestra dirección de correo (¡electrónico, no te asustes!)  quede expuesta al público. Si no queremos que esto ocurra, algo que podemos configurar es una dirección *"noreply"* de correo. El proceso necesario es muy sencillo, e incluso puede que esta funcionalidad esté habilitada de manera predeterminada en tu caso, pero si te interesa esto y te gustaría asegurarte, mirá cómo podemos hacerlo:

Una vez iniciada nuestra sesión en GitHub en nuestro browser, vamos hacia la pequeña flecha ubicada al costado de la foto de usuario de nuestro perfil, en la esquina superior derecha. La desplegamos y seleccionamos `Settings`. Ahora, sobre el lado izquierdo de la pantalla, deberíamos ver varias secciones de ajustes, busquemos la sección `Access` y, dentro de esta, el elemento `Emails`. Entonces, aquí es donde podemos decidir si queremos marcar la casilla `Keep my email addresses private` ("Preservar mis direcciones de correo electrónico en privado"). De marcarla, esto será efectivo de inmediato para todas las operaciones web (es decir: cualquier operación que hagamos en el browser). Eso sí, tengamos en cuenta que, bajo esta casilla, GitHub nos advierte que aún tendremos que asociar esta dirección *noreply* de correo en nuestra app *local* de Git, para que este ajuste también funcione con operaciones locales de Git (commits, pushes, etc.). Para poder hacerlo, hallaremos la dirección *noreply* en la nota que aparece bajo la casilla, así como también en la nota bajo "Primary email address".

También es posible marcar la casilla siguiente, `Block command line pushes that expose my email`, para evitar que cualquier comando, por accidente o lo que sea, pueda revelar nuestro(s) correo(s).

Así que, bueno, ahora ya tenemos Git y GitHub, pero ¿cómo saben el uno del otro? Mediante el archivo `gitconfig/config` que mencionábamos anteriormente. Vamos a charlar un poco de esto.

## Conexión del Git local con la cuenta de GitHub (Windows)

A decir verdad, existen varias maneras de hacerlo. La que nosotros vamos a usar es mediante HTTPS, pero tengamos en cuenta que también podríamos hacerlo por medio de [SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh), si esto se adapta mejor a nuestro caso.

Lo primero que hacemos es agregar nuestra dirección de correo electrónico (ya sea nuestra dirección real de correo o la *noreply*, ver más arriba) a la configuración de git. Esto podríamos hacerlo simplemente abriendo el archivo en cuestión con Vim, Nano o incluso VSC, y editándolo a mano con los cambios a continuación, pero existe una manera algo más práctica y cómoda, mediante la CLI de Git:

```shell
git config --global user.email <nuestro_correo_aquí>
```

El *setter* está implícito al añadir nuestro correo, por lo que el *getter* es el mismo comando, pero sin agregar ningún correo. Es decir, si queremos comprobar que se haya configurado bien nuestro correo, podemos consultar u *obtener* (*get*) el valor configurado, escribiendo de nuevo prácticamente lo mismo, pero sin ningún correo:

```shell
git config --global user.email
```

Y la respuesta recibida debería ser el correo configurado.

> Aviso: *Si, por algún motivo, queremos utilizar un correo específico para este repo (por ejemplo: un GitHub más personal vs uno para el trabajo), no usamos la opción (o flag) `--global`. Al hacerlo así, el correo ingresado se almacenará dentro de la carpeta `.git/` del repo, no en el archivo de configuración global de Git. Tengamos en cuenta que, de hacerlo así, con cada nuevo repo local, cuando intentemos hacer nuestro primer commit, se nos pedirá que ingresemos la configuración de usuario `user.email`*.

Bueno, ahora ya podemos empezar a versionar nuestro trabajo con `git add`, `git commit`, `git push`, etc. ¡Pará! ¡Yo ya creé un repo local y metí algunos commits, pero ahora `git push` se está quejando! Sí, y eso pasa porque solamente creamos un repo local. Si realmente queremos conectarlo con GitHub, vamos a necesitar un repo en Github, también.

Llegados a este punto, una vez más, tenemos varias maneras distintas de proceder, podríamos crear el repo en GitHub y luego seguir las instrucciones que se nos den allí, podríamos seguir las indicaciones de `git` tras ingresar `git push` en nuestra CLI, o también podríamos usar `gh`, la CLI de GitHub. ¿Cuál preferís vos? Por si acaso no te inclinás por una en particular, veámoslas todas acá. (Aviso: en realidad no *todas*, porque existen muchas maneras distintas de hacer las cosas. Otra que no vamos a mencionar acá, por ejemplo, consiste en crear el repo primero en GitHub y luego clonarlo en local.)

### 1) Crear el repo en GitHub (y las instrucciones subsiguientes)

En la página de GitHub, en la esquina superior derecha, deberíamos ver un signo de `+`. Si lo presionamos, nos presentará algunas opciones; la que más nos atañe es `New Repository`, así que le hacemos clic. En la siguiente pantalla, solamente es necesario escribir el nombre del repo bajo `Repository name` y decidir si este proyecto va a ser público o privado. De las otras opciones, por ahora no hay por qué preocuparse. 

Luego, presionamos `Create repository`. A esta altura, se nos mostrarán algunas alternativas. 

- Podríamos decidirnos por `Set up in Desktop` (sí, ¡hasta ofrecen una GUI! Se la puede descargar desde [aquí](https://desktop.github.com/)) e instalarla en nuestro sistema.
- Podríamos decidirnos por hacerlo mediante HTTPS o SSH (como mencionamos anteriormente, aquí vamos a decantarnos por el primero de ellos).
- También nos ofrecen instrucciones por si queremos crerar un repo local de cero desde nuestra CLI y pushearlo a este repo que acabamos de crear en GitHub (`…or create a new repository on the command line`).
- Por último, el que nos concierne en este caso está bajo: `...or push an existing repository from the command line`.

Este método nos muestra en pantalla los tres comandos de CLI que tenemos que ingresar en nuestra CLI local (Git/Bash/Terminal), los cuales, en esencia, hacen esto, línea por línea:
1. Paso previo: puede que sea obvio o no tan obvio, pero lo primero de lo que tenemos que asegurarnos es de estar posicionados en el directorio raíz (*root directory*) de nuestro repo local, mediante `cd`:
```shell
cd <dir_raíz_del_repo>
```
2. añadir el `remote` (este repo en GitHub) a nuestro repo local (la carpeta en nuestro sistema):
```shell
git add remote origin <url_del_repo>.git
```
3. cambiar el nombre de la rama principal a `main` (esto no debería ser necesario si ya lo seleccionamos cuando instalamos Git, ver más arriba):
```shell
git branch -M main
```
4. pushear nuestro código al repo (y [definir el upstream](https://git-scm.com/docs/git-branch/2.13.7#Documentation/git-branch.txt--ultupstreamgt) con `-u`, para que así, la próxima vez, podamos simplemente escribir `git push`):
```shell
git push -u origin main
```

A continuación, se nos va a pedir nuestra contraseña de GitHub y, si tenemos instalado Git for Windows 2.29 o superior (viene con el "nuevo" Git Credential Manager y admite OAuth), esta ya va a quedar guardada en nuestro sistema. Ya no debería ser necesario tener que ingresarla de nuevo. ¡Y listo! ¡Ya quedaron conectados!

> NOTA: si estás en Windows y tus credenciales no funcionan, pegale una ojeada a [esta página](https://docs.github.com/en/get-started/getting-started-with-git/caching-your-github-credentials-in-git) y, específicamente, buscá los cuadros color durazno, cerca del pie de la página, para recibir orientación acerca de cómo resolverlo.

De aquí en adelante, podremos simplemente hacer `git push` después de nuestros commits y todo debería funcionar sin problemas. 

### 2) Hacer `git push` y seguir las indicaciones

Bueno, en realidad, este método no va a funcionar, dado que para cuando hacemos `git push`, nos dirá que no se halla el repositorio (remoto). No obstante, si seguimos las indicaciones previas de Git en la CLI, ya habremos creado el `remote` (si probamos con `git remote -v` lo veremos), así que una vez creemos el repo con la URL correspondiente, solamente alcanzará con hacer el push.

Pero y entonces ¿para qué incluimos este método acá en esta lista? Bueno, porque si estamos haciendo `git-push` por primera vez y tenemos que ingresar nuestras credenciales, pero, asimismo, el repo todavía no existe, etc., si se da cierta combinación de circunstancias, puede que nos sintamos algo perdidos.

Por lo cual es bueno saber que Git nos está guiando mediante el prompt mencionado anteriormente, que nos dice:

```shell
$ git push
fatal: No configured push destination.
Either specify the URL from the command-line or configure a remote repository using

    git remote add <name> <url>

and then push using the remote name

    git push <name>
```

Es muy posible que aquí, se nos pida la contraseña, pero cuando hagamos clic para ingresarla, se abra el browser en blanco o ni nos abra nada, dado que la URL del repo aún no existe.

El mensaje debería lucir algo así como:
```shell
$ git push -u origin main
info: please complete authentication in your browser...
remote: Repository not found.
fatal: repository '<repo_URL_here>' not found
```

Así que, si pasa esto, como mencionamos más arriba, una vez hayamos efectivamente creado el repo, si volvemos a intentar el `git push`, se nos pida de nuevo la contraseña y, esta vez, sí funcione, porque la URL ahora sí "sabe adónde apunta".

### 3) Instalar la CLI de GitHub y usarla para esto

Si nos interesa este método, vamos a tener que dirigirnos [acá](https://cli.github.com/) para descargar la CLI de GitHub.

Tendremos que seguir las indicaciones y, una vez finalizado, abrir una ventana del Git Bash (o la shell que utilicemos) e ingresar `gh` (si teníamos alguna ventana del Git Bash o el Windows Terminal abierta, tendremos que cerrarlas primero y volver a abrirlas, de lo contrario, `gh` todavía no funcionará). Este comando debería devolvernos como respuesta un vistazo de los comandos disponibles. Si no lo hace, puede que algo no haya salido bien en la instalación, por lo que deberemos realizarla de nuevo.

Como se puede apreciar en la respuesta, todo el abanico de operaciones relacionadas con el repo quedan a cargo del comando `gh repo`, así que veamos qué nos ofrece:

```shell
gh repo --help
```

Aunque acá veremos un montón de posibilidades, centrémonos en lo que nos ocupa por ahora, que era crear el repo, ¿cierto?

```shell
gh repo create --help
```

Y lo que nos aparece ahora es de mucha, mucha ayuda. A nivel... ¡GitHub! Acá te recomiendo que leas y escojas el método que mejor funcione en tu caso. Mi favorito es el interactivo.

Así que hacemos:

```shell
gh repo create
```

...y luego elegimos las opciones en cada paso. 

> NOTA: tengamos en cuenta que puede que necesitemos abrir el Git Bash del Windows Terminal (o reinstalar Git for Windows y activar la casilla "Enable experimental support for pseudo consoles" en el proceso de instalación, aunque creo que la primera opción es un poco menos dramática, ¿no?) para poder disfrutar de los beneficios de la CLI de gh.

Así que, tendremos que elegir el nombre del repo, su visibilidad y otras características, así como también si queremos clonarlo de forma local (en nuestra máquina). Al final de este proceso de unos pocos segundos, tendremos una nueva carpeta creada para nuestro repo con git inicializado en ella, el `remote` ya configurado adecuadamente y demás. Ahora, solamente nos faltará añadir nuestro email a la config (si no lo hicimos ya de manera global) y autenticarnos, tal como hicimos en los métodos previos.

¿Decime si no está buenísimo?

## Conexión del Git local con la cuenta de GitHub (Ubuntu)

Una vez más, existen diversas maneras de hacerlo. Y yo he hecho elecciones y asumido premisas que podrían ser o no adecuadas en tu caso. He asumido que trabajamos en el combo Windows/WSL. He elegido usar HTTPS, no SSH. He elegido no usar el token de GitHub, sino más bien la combinación CLI de `gh` + `google-chrome`. Tené en cuenta que algunas otras elecciones podrían adaptarse más a tu caso en particular. En cualquier caso, familiarizarse con este método podría venir bien.

### Instalar la CLI de `gh`

Las instrucciones de instalación de la CLI de `gh` están [acá](https://github.com/cli/cli/blob/trunk/docs/install_linux.md). No obstante, si sos un poco curioso o curiosa (¡como yo!), es probable que quieras saber qué es lo que estamos haciendo acá, ¿verdad?

Así que, vamos paso a paso:

1.
```shell
type -p curl >/dev/null || (sudo apt update && sudo apt install curl -y)
```
*TLDR: La línea anterior comprueba si ya tenemos `curl` instalado y, de no ser así, lo instala.*
> [*--verbose-reading mode alert*:
>
>`type <app>` nos dice la ruta en la que una app está instalada. Por ejemplo: `type curl` nos diría `curl is /usr/bin/curl`.
> 
>La flag (opción) `-p` determina que la respuesta solamente contenga la ruta (es decir: `/usr/bin/curl`).
> 
>El operador de salida `>` envía la salida a algún lado (por ejemplo, a un archivo). 
>
>Y el destino `/dev/null` es una especie de tarro de basura, en el sentido de que todo lo que va a él, simplemente desaparece; es como un agujero negro digital. {{% spanclass emoji %}} :smiling_face: {{% /spanclass %}}
>
>Así que, si juntamos todo: averiguá la ruta de curl, pero yo no la necesito ahora, no me la des...
>
>Entonces, acá consultamos por una ruta, pero ¿y si lo hacemos con una app que no está instalada?
>```shell
>type microsoft-edge
>-bash: type: microsoft-edge: not found
>```
>No la encuentra (*not found*) o, en otras palabras, esa ruta *no existe*.
>
>Luego, tenemos ||, que básicamente significa que si el resultado del comando previo no existe (es decir: si `curl` no está instalada)... entonces `sudo apt install curl -y`, la flag -y es para asegurarnos de no tener que confirmar todos los prompts con `y`.
>
>Para ser honesto, igual, podríamos simplemente haber hecho `curl` aquí y, si no la hallaba, instalarla. Sin embargo, este bloque de código está pensado para ser ejecutado todo de una vez (por eso los `\` al final de cada línea) y, por tanto, no debería ser interrumpido. Por eso las instrucciones son de esta manera.
>
> *end --verbose-reading mode*]

2.
```shell
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
```
Básicamente, lo que hacemos acá es descargar el archivo desde la URL suministrada (por eso `curl` -> Client URL) y duplicarlo (o copiarlo) en la ruta indicada tras el comando `sudo` (sudo por los permisos, obviamente).

3.
```shell
sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg
```
Le damos permisos de lectura (*'reading'*) para ese archivo al 'grupo' (*'group'*) y 'otros' (*'others'*). Así que es, `chmod` por 'cambiar modo' (*'change mode'*, es decir: cambiar los permisos de un archivo) y luego 'go' (*'group'* y *'others'*), '+' (añadir) y 'r' (*read* o lectura).

4.
```shell
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
```
En este pasan más cosas, pero el resumen sería: ¿te acordás cuando hacemos `sudo apt update` y `upgrade`? Bueno, el sistema sabe qué comprobar gracias a la lista del sistema de repos disponibles. Lo que hacemos con este comando es añadir el que especificamos, para luego poder instalar (y, eventualmente, actualizar) la CLI de `gh`. Si te interesa, después de ejecutar este comando, abrí los archivos `sources.list.d` y `github-cli.list` (en la ruta especificada en el comando) con vim o nano y vas a ver qué cambió. Dado que usamos `echo`, que tiende a mostrar la salida o respuesta, finalizamos el comando con el operador de salida (`>`) y `/dev/null`, lo cual ya debería sonarnos conocido (ver más arriba).

5.
Luego,
```shell
sudo apt update
```
para actualizar las fuentes, y:
```shell
sudo apt install gh -y
```
... para instalar CLI de `gh` y confirmar automáticamente todos los prompts con `y`.

A estas alturas, si ingresamos `gh`, deberíamos recibir un mensaje muy completo de bienvenida con un montón de opciones de lo que podemos hacer (es decir: comandos, flags, etc.).

### Instalar Chrome

Sí, aun cuando estemos usando WSL, podemos instalar Chrome en Ubuntu. "Pero... ¿con GUI y todo?" ¡Por cierto!

Las instrucciones para hacerlo están por [acá](https://learn.microsoft.com/en-us/windows/wsl/tutorials/gui-apps#install-google-chrome-for-linux). Así que, vamos a repasarlas:

1.
```shell
cd /tmp
```
Simplemente vamos a la carpeta `tmp`, el lugar para almacenar archivos que serán necesarios de manera *temporal*.

2.
```shell
sudo wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```
En este caso, en vez de usar `curl` (perfectamente podríamos haberlo hecho así), las instrucciones nos indican una manera para descargar el archivo en la ruta especificada mediante `wget` (normalmente preinstalado con Ubuntu).

3.
```shell
sudo dpkg -i google-chrome-stable_current_amd64.deb
```
Tengamos en cuenta que no fue necesario actualizar nuestras fuentes ni nada por el estilo. Eso es así porque vamos a utilizar este comando en vez del `sudo apt install`. Además, el comando `dpkg` solamente instala el paquete que especificamos, mientras que `apt install` también instala las dependencias. Así que, esencialmente, lo que hacemos con este comando  es instalar el paquete mediante el archivo que acabamos de descargar. ¿Por qué? Porque no se nos brinda un repo de Ubuntu para descargarlo, sino solamente un archivo .deb. No obstante, de todos modos recibiremos el siguiente mensaje como parte de la salida del comando:
```shell
dpkg: dependency problems prevent configuration of google-chrome-stable:
```
... seguido de una larga lista de dependencias ausentes.

4.
```shell
sudo apt install --fix-broken -y
```
Por eso, ahora vamos a asegurarnos de que se resuelvan todos los problemas de dependencias (puede que esto lleve un ratito, dado que hay varias deps).

5.
```shell
sudo dpkg -i google-chrome-stable_current_amd64.deb
```
Al volver a ejecutar este comando, deberíamos salir de todo problema, y tener el paquete `google-chrome` instalado.

Si estás listo o lista para recibir una sorpresa sumamente grata, ingresá `google-chrome` y observá cómo se abre una ventana de Chrome con la GUI de Ubuntu frente a tus ojos. ¿Decime si no está impresionante?

### Autenticarnos en GitHub mediante la CLI de `gh` y Chrome

Es increíble lo que han simplificado este paso. Simplemente tenemos que ingresar:
```shell
gh auth login
```
...y recibiremos un prompt interactivo que nos pregunta si queremos iniciar sesión en GitHub.com o Enterprise, si queremos usar HTTPS o SSH, si queremos usar un token de acceso de GitHub o simplemente usar el browser, y luego, si escogimos el método HTTPS -> browser, recibiremos un código en la CLI y se nos pedirá que presionemos `Enter` para abrir el browser.

Una vez hecho esto, el browser que hayamos instalado (Chrome, en nuestro caso) abrirá una ventana de GitHub pidiendo que iniciemos sesión y peguemos (o ingresemos) el código recibido, y luego presionemos 'Authorize GitHub'.

Una vez hecho esto, nuestra `gh` CLI estará autenticada. Así que ahora podremos clonar o crear un repo valiéndonos de ella. Ya mencionamos cómo crear un repo en la sección "[3) Instalar la CLI de GitHub y usarla para esto](#3-instalar-la-cli-de-github-y-usarla-para-esto)", así que ahora vamos a ver cómo clonar un repo ya existente.

Bueno, esto es muy sencillo, y de hecho está indicado en la página del repo en GitHub. Si vamos a la página de nuestro repo en GitHub, vamos a ver un botón verde que dice 'Code' con una flecha en la esquina superior derecha. Si hacemos clic en él, nos ofrecerá diversas maneras en las que podemos clonar el repo, ya sea de manera local o con 'Codespaces'. La primera es la que nos ocupa. Vamos a ver que acá se nos indican tres métodos: HTTPS, SSH y (nuestra selección) GitHub CLI. Esta última indica el comando necesario (y podemos incluso copiarlo de ahí mismo): 
```shell
gh repo clone <usuario_gh/nombre_del_repo>
```
Tengamos en cuenta que, en este caso, no necesitamos el sufijo `.git`, como en el método por HTTPS.

No obstante, vas a ver que ahí se muestran todas las opciones, incluso la de [GitHub Desktop](https://desktop.github.com/), si sos más visual y te entendés mejor con las GUI.

Bueno, a decir verdad, hay mucho más que se puede hablar sobre cómo usarlos el uno junto al otro (Win-WSL) y este artículo ya se está alargando mucho, pero si te interesa más el tema, pegale una ojeada a [esta página](https://code.visualstudio.com/docs/remote/troubleshooting#_resolving-git-line-ending-issues-in-wsl-resulting-in-many-modified-files) (y más recursos similares, si querés, por supuesto) si querés configurarlos de una manera que se adecue más a tu manera de trabajar.

## Conclusión

En fin, este proceso posiblemente parecerá un poco complicado la primera vez, pero después que lo hayamos hecho unas cuantas veces, se volverá completamente natural. Y, a cambio, ¡nos ofrecerá tantos beneficios! Como, por ejemplo, poder volver unos pasos atrás cuando nos dimos cuenta que cometimos un error, respaldar nuestros repos en línea para que, así sea que nuestra compu colapse, no perdamos nada, colaborar con otros en el mismo proyecto, ¡y mucho más! Y esto solo a modo de ejemplo.

Al fin y al cabo, usar Git y GitHub es una decisión de la que no nos vamos a arrepentir.


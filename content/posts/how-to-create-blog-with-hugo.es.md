---
title: "Cómo hice mi blog con Hugo"
date: 2023-05-12
draft: false
author: devdrivenai
description: Cómo hice mi blog con Hugo (¡y cómo vos también podés hacerlo!)
categorías: ['cómo', 'creación']
etiquetas: ["hugo", "blog"]
---

## El porqué de un blog (¿y por qué no?)

¡Hola! Para empezar, quiero que hagamos un ejercicio juntos. Consiste en una pregunta para vos. Si sos un desarrollador o desarrolladora (o incluso aspirás a serlo, como yo) y todavía no tenés tu propio blog, ¿por qué no lo has hecho? Es muy probable que te ayude a solidificar lo que ya sabés y distinguir lo que entendés de lo que asumís o suponés. Además, siempre puede haber alguien a quien le sea de ayuda. 

¿Puede que no lo estés haciendo en parte por miedo? ¡Estamos en la misma! Y pienso escribir al respecto, así que no te vayas muy lejos, y volvé cada tanto, a ver si ya lo publiqué.

Si solamente lo estás posponiendo, ¿qué estás esperando?

No obstante, si tenés algún otro motivo, te invito a analizar si es válido y también a pensar en los pros de hacerlo, algunos de los cuales mencioné más arriba. 

Sin embargo, si tus motivos son válidos, disculpá la pregunta. La verdad es que yo necesitaba hacérmela y pensé que quizás vos también. {{% spanclass emoji %}} :smiling_face: {{% /spanclass %}}

Ahora, entonces hablemos del cómo. Del cómo yo hice mi blog con Hugo. Y también, en un futuro post, una "secuela" de este, charlemos acerca de una de las maneras más simples (¡y gratuita!) de desplegar este blog en línea y poder mostrárselo a la familia, los amigos y, tan importante como ello, si no más, a posibles reclutadores y empleadores.

Pero, primero lo primero. Hablemos de requisitos:

## Requisitos

Si querés hacer esto junto conmigo, vas a necesitar:
- tener Hugo instalado en tu equipo 
- tener Git instalado en tu equipo
- tener tu propia cuenta de GitHub (para el despliegue, pero también para respaldar tu control de versiones)
- un terminal y un editor de código

En relación con el último elemento de esta lista, podrías inclinarte por diversas alternativas, ya sea hacer todo desde el terminal, utilizar el terminal que viene integrado dentro del editor de código o cualquier combinación entre ellos. Yo suelo preferir usar Git Bash (viene con Git for Windows) y WSL. Y, como editor, uso Visual Studio Code (configurando Git Bash como el terminal integrado predeterminado). Pero vos podés elegir según te convenga. 

NOTA: Además, si usás Windows, puede que utilizar el [Windows Terminal](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=es-es) te ahorre varios dolores de cabeza cuando necesites varias ventanas del terminal. Y, obviamente, podés personalizarlo con cualquier terminal disponible en tu sistema (e incluso tu WSL).

## Elección de un theme

Tomame la palabra, esto se puede complicar, pero por un buen motivo. Es que hay tanta variedad y tan buenos themes entre los cuáles elegir que se te puede poner difícil quedarte con uno. {{% spanclass emoji %}} :smiling_face: {{% /spanclass %}}

Lo bueno es que el sitio web de Hugo nos [guía bastante](https://themes.gohugo.io/), con vistas previas, descripciones y filtros.

No obstante, si ahí no encontrás lo que vos estás buscando, siempre está la posibilidad de crear tu propio theme. Pero, eso sí, tenés que estar seguro o segura de que esa sea una inversión de tiempo que te valga la pena.

En mi caso, en este momento, mi prioridad es arrancar cuanto antes, sin preocuparme en exceso por cosas que podremos mejorar más tarde, dado que me quiero presionar a publicar contenido, para así ignorar al miedo que me ha estado sujetando por bastante tiempo. 

Teniendo eso en cuenta, el theme [PaperMod](https://adityatelange.github.io/hugo-PaperMod/) me pareció muy apropiado para mi caso específico, puesto que trae (integradas) las funcionalidades más prioritarias para mí, a saber: light and dark mode (modo claro y modo oscuro/nocturno), sitios multilingües y, muy importante, una interfaz moderna y a la vez despejada, que invita al lector o lectora a centrarse en el contenido, por no mencionar otras joyitas que también ofrece.

## Primeros comandos de Hugo

Si sos como yo, no te gusta simplemente seguir instrucciones (o copiarlas y pegarlas) sin primero averiguar qué estás haciendo y que más podrías hacer.

Por fortuna, Hugo te hace la vida más fácil de dos maneras: 1) su exhaustiva [documentación](https://gohugo.io/documentation/) y 2) el comando `help` y la opción (o *flag*) `--help` de su CLI. Y, por cierto, la documentación del enlace anterior también incluye una interfaz visual que explica los comandos y opciones de la CLI.

Así que entonces, comencemos a abrirnos paso con el comando `help`:
```shell
hugo help
```

Una de las líneas de la respuesta dice:
```
Available commands:
...
...
...
  new       Create new content for your site
```

Aunque pueda parecer que esto implique que ya necesitás tener un sitio, en realidad también podés crear uno con el comando: `hugo new site` *más* la ruta o nombre de tu proyecto.

Entonces, exploremos la opción `--help` para ese comando:
```shell
hugo new --help
```
...nos devuelve:
```shell
Available Commands:
  site        Create a new site (skeleton)
  theme       Create a new theme
```

NOTA: *Por lo general, suele ser muy buena idea perderse un rato con la opción `--help` de una CLI hasta familiarizarse con ella. Si aún no lo has probado, esta sería una oportunidad perfecta para que pares la lectura y te pierdas un rato con ella.* {{% spanclass emoji %}} :smiling_face: {{% /spanclass %}}

Sin embargo, si les pegás una ojeada a las opciones que aparecen, se están enumerando todas las opciones disponibles para ambos comandos (`site` y `theme`).
Ahora mismo, el que nos concierne es únicamente el primero de ellos (`site`):
```shell
$ hugo new site --help
Create a new site in the provided directory.
The new site will have the correct structure, but no content or theme yet.
Use `hugo new [contentPath]` to create new content.

Usage:
  hugo new site [path] [flags]

Flags:
      --clock string               set the clock used by Hugo, e.g. --clock 2021
-11-06T22:30:00.00+09:00
  -e, --environment string         build environment
      --force                      init inside non-empty directory
  -f, --format string              config file format (default "toml")
  -h, --help                       help for site
      --ignoreVendorPaths string   ignores any _vendor for module paths matching
 the given Glob pattern
  -s, --source string              filesystem path to read files relative from
      --themesDir string           filesystem path to themes directory

Global Flags:
      --config string      config file (default is hugo.yaml|json|toml)
      --configDir string   config dir (default "config")
      --debug              debug output
      --log                enable Logging
      --logFile string     log File path (if set, logging enabled automatically)
      --quiet              build in quiet mode
  -v, --verbose            verbose output
      --verboseLog         verbose logging
```

Bueno, acá aparecen menos opciones, aunque siguen siendo un montón.

## Creación de nuestro sitio

En esencia, la respuesta de más arriba nos dice que tenemos que ingresar `hugo new site` y luego el `[path]` (o *ruta*, el directorio actual, de manera predeterminada, por lo cual alcanza con ingresar el nombre de tu proyecto) y las `[flags]` (*opciones*), de haber alguna.

El argumento `path` es obligatorio. Lo que Hugo hace con él es crear dicha carpeta (o ruta) *dentro* de la carpeta en que te encontrás actualmente. Y dentro de esta nueva carpeta, añadir ciertos directorios y archivos que conformarán la estructura básica de tu blog.

Las opciones te permiten personalizar una cantidad de cosas según tus gustos y tu caso en particular. La que utilizaremos en este caso es `-f` (o `--format`, si así lo preferís), que tiene que ir seguida de una cadena de texto o *string* (`-f, --format string`). Esta cadena informa a Hugo cuál de los tres formatos posibles preferís utilizar para tu archivo config*: `.toml` (predeterminado), `.yaml` o `.json`. Dado que (al día que escribo esto) estoy más familiarizado con json, vamos a especificarlo de esa manera.

```shell
hugo new site misitio -f json
```

*TLDR NOTA (POR LAS RAMAS): *aunque en los docs y la respuesta de la CLI, se menciona en la opción `--config` que el nombre predeterminado del archivo de configuración es `hugo.yaml|json|toml` (fijate en la respuesta a `hugo new site --help` más arriba), al día que escribo esto (versión 0.111.3 de Hugo) el archivo config creado todavía se llama `config.<tu_extensión_aquí>`. No obstante, tienen planes de cambiarlo por `hugo.<tu_extensión_aquí>`, como nombre predeterminado, tal como se menciona [acá](https://gohugo.io/getting-started/configuration/#hugotoml-vs-configtoml) en la documentación y también en un comentario que han dejado en su código fuente, diciendo que "eventualmente" habrá que cambiar "config" por "hugo". Así y todo, si cambiás -a mano- el nombre del archivo `config` a `hugo`, va a funcionar bien. Algo a tener en cuenta.*

Bueno, volviendo a lo nuestro:

Ahora sí, ¡felicitémonos! ¡Nuestro nuevo sitio ya tiene vida! !Qué grande, Huguito! Y, ya de paso, si ojeamos el mensaje emitido por la CLI, Hugo nos da varias pistas acerca de qué nos queda por hacer:

```shell
Congratulations! Your new Hugo site is created in D:\\gh_clones\\misitio.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>\<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
```

## Un primer vistazo a la estructura de nuestro sitio

Con esto, ahora tendremos, dentro de la carpeta actual, una nueva carpeta con el nombre `misitio/`, con un archivo `config.json`, que lucirá así:

```json
{
   "baseURL": "http://example.org/",
   "languageCode": "en-us",
   "title": "My New Hugo Site"
}
```

...y las siguientes carpetas:

`- archetypes/`

`- assets/`

`- content/`

`- data/`

`- layouts/`

`- public/`

`- static/`

`- themes/`

Excepto en el caso de `archetypes/`, estarán todas vacías. Charlaremos más acerca de ellas (¿probablemente?) en el futuro, pero por ahora eso no será necesario, ya que apenas nos estamos acostumbrando a lo más básico de Hugo. Lo que importa por ahora es que ese primer sitio salga adelante.

## Levantemos el servidor

Y, hablando de eso, ¿ya podremos intentar levantar el servidor? ¿Funcionará?

```shell
hugo help
```

```
Available commands:
...
...
...
  server      A high performance webserver
```

Vale la pena comentar que, tal como se analiza [acá](https://discourse.gohugo.io/t/hugo-serve-vs-hugo-server/24872) y se menciona en su opción `--help`, `hugo serve` y `hugo server` hacen exactamente lo mismo, dado que el primero es simplemente un alias del segundo.

Así que, ¡adiviná qué vamos a hacer ahora!

Exacto:

```shell
hugo serve --help
```

Como podés ver en la respuesta (si lo estás haciendo conmigo), acá hay numerosas opciones disponibles, aunque aún no necesitamos ninguna. Vamos a levantarlo con los valores predeterminados, sin modificar nada.

```shell
hugo serve
```

Respuesta:
```shell
WARN <fecha_acá><hora_acá> found no layout file for "HTML" for kind "home": You should create a template file w
hich matches Hugo Layouts Lookup Rules for this combination.
WARN <fecha_acá><hora_acá> found no layout file for "HTML" for kind "taxonomy": You should create a template fi
le which matches Hugo Layouts Lookup Rules for this combination.
```

Esa sección de la respuesta parece indicar que algo salió mal, sobre todo si seguimos la indicación en esta línea:

```shell
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
```

Si abrís el navegador con esa URL, recibirás un 404 bien vacío y aburrido. ¿Qué pasó?

Recordemos esta línea de la respuesta a `hugo new site --help`: 
```shell
The new site will have the correct structure, but no content or theme yet.
```

Bueno, Hugo está buscando los archivos de layout (es decir, los archivos dentro de la carpeta `layouts/` que expliquen a Hugo como "organizar" el contenido de nuestro sitio). Podríamos crearlos nosotros, por supuesto, pero aquí es cuando los *themes* pueden ayudarnos a dar ese arranque más rápido.

Esta es la razón por la que escogimos uno más arriba. Yo seleccioné el [PaperMod](https://adityatelange.github.io/hugo-PaperMod/), ¿te acordás? ¿Y vos cuál elegiste?

Bueno, incorporemos nuestro theme. Aunque, un segundo... ¿cómo lo hacemos?

## Incorporación del theme seleccionado

Por lo general, los creadores de themes te dan un poco de guía en este sentido, y nuestro seleccionado, PaperMod, [no es una excepción](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-installation/). Hugo también da alguna guía básica [acá](https://gohugo.io/getting-started/quick-start/).

Como podrás apreciar, hay muy diversos métodos en que se puede hacer esto, pero por ahora vamos a decantarnos por uno de los más simples:
```shell
cd misitio # movernos al directorio raíz del proyecto
git init # inicializar un repo desde el mismo
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
# obviamente, la URL tras 'add' deberá apuntar al repo del theme que hayas elegido vos
``` 

Lo que hacemos aquí es, primero, inicializar un repo con `git`, y luego emplear la funcionalidad [`submodule`](https://git-scm.com/book/en/v2/Git-Tools-Submodules) de git para incorporar el repo del theme como submódulo dentro de la carpeta `themes/` de nuestro proyecto, con el nombre que especifiquemos (en mi caso, PaperMod, pero la tuya debería llevar el nombre del theme que corresponda).

Todavía queda un paso importante: tenemos que decirle a Hugo que busque este theme, mediante el archivo de configuración del proyecto (el archivo config/hugo antes mencionado). Dado que yo estoy usando un archivo `.json`, así es como lo hago:

*config.json*
```diff
...
+   "title": "misupernombre",
-   "title": "My New Hugo Site",
+   "theme":"PaperMod"
...
```

Ahora, peguemos una ojeada a cómo luce el sitio, yendo para ello a `http://localhost:1313/`.

Bueno, dependiendo de qué theme hayas elegido, puede que luzca algo... vacío. Y el motivo de ello es que aún no hemos añadido ningún contenido.  

## Añadimos primer contenido

Recordemos la respuesta a `hugo new --help`. En, parte, decía:
```shell
Create a new content file and automatically set the date and title.
It will guess which kind of file to create based on the path provided.
```

El contenido, y esto era de esperar, irá dentro de la carpeta `content/`. Pero lo que nosotros podemos decidir es qué tipo de contenido queremos añadir. Por ejemplo, si queremos un post para el blog, haremos:

```shell
hugo new posts/hello-hugo.md
```

Esto creará una carpeta `posts/` (si aún no existe) dentro de `content/`, y un archivo `hello-hugo.md` dentro de la primera, con el siguiente contenido:

```
---
title: "Hello Hugo"
date: <fecha del post acá>
draft: true
---
```

Esto se llama ["front matter"](https://gohugo.io/content-management/front-matter/). Ya hablaremos más de eso en el futuro. Por ahora, lo que importa es que si cambiamos `draft` (borrador) a `false` (es decir, ya no es un borrador, ¡ahora está publicado!) o añadimos la opción `-D`* al comando `hugo serve` (permanece como borrador, pero de todos modos es accesible), ahora veremos nuestro post en el navegador.

*Línea a tener en cuenta:
```shell
-D, --buildDrafts                include content marked as draft
```
\
Del mismo modo, si quisiéramos, por ejemplo, una página "sobre mí", podríamos hacer:

```shell
hugo new about.md
```

Si querés, proba y fijate. (Tené en cuenta que ahora la URL no va a quedar dentro de `posts/`.)

La manera en que se les muestre dependerá del contenido de nuestra carpeta `layouts/` (en nuestro caso, sin embargo, está vacía, y esto es gestionado por la carpeta `layouts/` de nuestro theme: `themes/PaperMod/layouts/`).

## ¿Y qué del despliegue?

Lo único que nos faltaría ahora sería escribir un poco de markdown, para contar con varias páginas y posts. Bueno, y probablemente vamos a querer desplegar esto en línea, para poder darle vida, más allá de nuestro equipo, pero de eso charlaremos en el próximo post.

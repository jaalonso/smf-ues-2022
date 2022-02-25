# Demostración de teoremas interactiva asistida usando Lean

En este pequeño curso vamos a introducir los conceptos básicos del
lenguaje y software Lean, desarrollado por Microsoft Research.  El
Software Lean nos permite usar la teoría de tipos para describir y
demostrar virtualmente cualquier proposición matemática. Por ejemplo, en
2020, [Kevin Buzzard, Johan Commelin y Patrick Massot definieron
espacios
perfectoides](https://leanprover-community.github.io/lean-perfectoid-spaces/).
Estos son conceptos de la investigación actual en geometría algebráica,
que entre otros le valió una medalla de Fields a Peter Scholze en 2018.
En otras palabras, Lean puede manejar conceptos y teoremas matemáticos
en los que se está investigando, ayudando a comprobar que el
razonamiento es correcto y automatizando parte del proceso.

En el curso aprenderemos las bases de Lean, cubriendo simples conceptos
de lógica. Luego, pasaremos a definir los números naturales usando los
axiomas de Peano y demostraremos propiedades básicas de ellos.
Finalmente pasaremos a construcciones más complejas. El objetivo de este
curso es aprender cómo este software nos puede ayudar a razonar
matemáticamente, siéndole útil tanto a principiantes como a
investigadores avanzados.

# Instalar Lean

Este mini-curso requiere el uso del sistema Lean, para la demostración
de teoremas interactiva. En este curso usaremos la versión 3 de Lean,
la versión comunitaria, pues esta es la verisión más estable y
compatible con la biblioteca matemática Mathlib. Estas indicaciones
servirán para instalar Lean en su computadora antes del curso. Estas
instrucciones (en inglés) y más detalles los puede encontrar también en
línea: <https://leanprover-community.github.io/>

## GNU/Linux

Si dispone de una distribución de GNU/Linux basada en Debian
(p.e. Ubuntu), la forma más fácil de instalar es abriendo una terminal y
corriendo el siguiente comando, que instalará todo directamente:

    wget -q https://raw.githubusercontent.com/leanprover-community/mathlib-tools/master/scripts/install_debian.sh && bash install_debian.sh ; rm -f install_debian.sh && source ~/.profile

El siguiente video (en inglés) muestra cómo hacerlo:
<https://www.youtube.com/watch?v=02ff4WrW0FU> Esto deberá instalar todo,
incluyendo VS Code y leanproject. ¡Su computadora está lista para el
minicurso!

Si prefiere instarlo manualmente, o tiene otra discribución de
GNU/Linux, asegúrese de tener los paquetes: git, curl, y python3,
instalándolos con el gestor de paquetes de su distribución (como yum,
pacman, portage, etc.) Luego, ejecute el siguiente comando:

    curl https://raw.githubusercontent.com/leanprover/elan/master/elan-init.sh -sSf | sh

Luego necesitará un editor como Visual Studio Code o Emacs que son los
que tienen mejor soporte para Lean. Para descargar Visual Studio Code,
siga las instrucciones en <https://code.visualstudio.com/>. Acceda por el
menú a la seleción de extensiones (también puede hacerlo pulsando
Shift + Control + X). Instale la extensión "Lean", la cual puede
encontrar buscando "leanprover". Nota: **No** descargue la extensión
"Lean4", esta no es compatible con Mathlib y no la usaremos en este
minicurso.

Finalmente, instalaremos una herramienta llamada leanproject para
manejar proyectos. La instalamos corriendo los sugientes comandos.

    python3 -m pip install --user pipx
    python3 -m pipx ensurepath
    source ~/.profile
    pipx install mathlibtools

## Microsoft Windows

El siguiente video (en inglés) muestra el proceso de instalación
<https://www.youtube.com/watch?v=y3GsHIe4wZ4>

A continuación detallamos del proceso de instalación paso a paso: Para
instalar Lean en Microsoft Windows primero descargamos e instalamos Git
para Windows:

<https://gitforwindows.org/>

Luego de instalada, en la barra de búsqueda (del menú de inicio) escriba
"git bash". Le aparecerá una terminal. Copie y pegue este comando en la
terminal que aparece:

    curl https://raw.githubusercontent.com/leanprover/elan/master/elan-init.sh -sSf | sh

Cuando le aparezca una pregunta en la ventana, presione "enter". Para
asegurarse que la terminal encuentre los archivos, copie y pegue esto en
la terminal:

    echo 'PATH="$HOME/.elan/bin:$PATH"' >> "$HOME/.profile"

Luego de esto puede cerrar esta terminal. El siguiente paso es descargar
Python, si no lo tiene todavía: <https://www.python.org/downloads/>
Descargue la versión más nueva.

Durante la instalación de Python, eliga la opción de agregar python al
entorno PATH cuando el instalador le de la opción. Eliga la instalación
estándar.

Para comprobar su instalación de Python, abra nuevamente la terminal
(buscando "git bash" en el menú de inicio) y escriba lo siguiente:

    which python

Debería ver algo como lo siguiente:

    /c/Users/<user>/AppData/Local/Programs/Python/Pythonxx-xx/python

Si, en vez, ve algo como:

    /c/Users/<user>/AppData/Local/Microsoft/WindowsApps/python

entonces ha sucedido algo mal. ¿Tal vez olvidó agregar python al entorno
PATH durante la instalación? En ese caso reinstale, seleccionando esta
opción.  Si no olvidó seleccionar esta opción, entonces ha ocurrido otro
problema. Para solucionarlo, en el menú de inicio escriba: "manage app
execution aliases" y abra la sección correspondiente en la configuración
del sistema. Debería haber dos entradas de Python: "App Installer
python.exe" y "App Installer python3.exe", asegúrese que ambas estén
apagadas. Cierre y vuelva a abrir la terminal (git bash) y repita este
paso de comprobación.

En la terminal, ejecute el siguiente comando para asegurarse que pueda
llamar al programa Python usando también el nombre "python3":

    cp "$(which python)" "$(which python)"3

Luego de hacer esto, compruebe que haya funcionado ejecutando lo siguiente:

    python3 --version
    pip3 --version

Ambos comandos deberían reportarle un número de la versión que tiene
instalada. Si el segundo, pip3, no funciona, entonces puede instalarlo
ejecutando:

    python3 -m pip install --upgrade pip

Finalmente, instale las herramientas de mathlib ejecutando lo siguiente:

    pip3 install mathlibtools

Ya con todo esto instalado, sólo necesitamos un editor. En esta guía
usaremos Visual Studio Code. Descarguélo e instálelo de la siguiente
página: <https://code.visualstudio.com/>

Acceda por el menú a la seleción de extensiones (también puede hacerlo
pulsando Shift + Control + X). Instale la extensión "Lean", la cual
puede encontrar buscando "leanprover". Nota: **No** descargue la
extensión "Lean4", esta no es compatible con Mathlib y no la usaremos en
este minicurso.

## Mac

Si ud tiene una Mac con chip de Intel (la mayoría, excepto ciertos
modelos 2020-2021), entonces la forma más fácil es abrir una terminal
(presione Command + Espacio, escriba "terminal" y presione enter). En la
terminal copie y pegue lo siguiente:

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/leanprover-community/mathlib-tools/master/scripts/install_macos.sh)" && source ~/.profile

Esto instalará todo en su computadora, sin pedirle permisos de
administrador. Si ud. prefiere más control sobre la instalación, la
siguiente página (en inglés) muestra más detalles:

<https://leanprover-community.github.io/install/macos_details.html>

Si ud. tiene una nueva Macbook con un chip M1 (de Apple), le sugerimos
seguir las instrucciones siguientes (en inglés):
<https://leanprover-community.github.io/install/macos.html>

# No pude/no quise instalar Lean

Si intentó instalar Lean y de verdad no pudo, puede usar Lean en el
navegador. Sin embargo, *no* se recomienda esta alternativa, porque no
podrá usar toda la funcionalidad ni guardar su progreso, etc.

A continuación, se muestran los enlaces para abrir Lean en la Red con
los distintos módulos:
 - [Lógica](https://leanprover-community.github.io/lean-web-editor/#url=https%3A%2F%2Fraw.githubusercontent.com%2Fgoens%2Fsmf-ues-2022%2Fmaster%2Fsrc%2Flogica.lean)
 - [Numeros naturales](https://leanprover-community.github.io/lean-web-editor/#url=https%3A%2F%2Fraw.githubusercontent.com%2Fgoens%2Fsmf-ues-2022%2Fmaster%2Fsrc%2Fnumeros_naturales.lean)
 - [Grupos](https://leanprover-community.github.io/lean-web-editor/#url=https%3A%2F%2Fraw.githubusercontent.com%2Fgoens%2Fsmf-ues-2022%2Fmaster%2Fsrc%2Fgrupos.lean)

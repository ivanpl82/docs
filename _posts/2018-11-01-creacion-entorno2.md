---
layout: post
title: Creación entorno de desarrollo parte 2
tags:
  - entorno desarrollo
  - mac
  - bash
excerpt_separator:  <!--more-->
---

## Consola

Como consola a mi me gusta usar [Hyper](https://hyper.is/) desarrollada por el MIT y tiene un monton de addons que puede ayudarnos en nuestras tareas diarias.

Podremos descargar la aplicación del siguiente enlace para mac: [download](https://releases.hyper.is/download/mac)

La personalización es muy importante ya que nos permite trabajar de una manera cómoda, a mi me gusta usar un juego de colores que sea "solorizado" para ello basta con ejecutar en la consola hyper:

```
hyper i hyper-whimsy
```

## Pipenv

Cuando estoy desarrollando procesos en python me gusta tener el entorno limpio, para que en caso de querer probar una librería diferente no tenga que estar modificando el sistema y haciéndolo inestable.

Para ello utilizo [pipenv](https://pipenv.readthedocs.io/en/latest/) que nos permite la creación de instancias virtuales en las que instalaremos las librerías y probaremos nuestros códigos.

Lo instalaremos de la siguiente manera:

```
pip3 install pipenv
```

### Uso

Accedemos a la carpeta del proyecto que queremos explotar, para instalar en el directorio el pipfile y el pipfile.lock.

```
pipenv install
```

Una vez que ya tenemos el directorio del proyecto preparado para instalar librerías bastará con ejecutar:

```
pipenv install <librería>
```

Si deseamos realizar la instalación del paquete pero solo para el entorno de desarrollo:

```
pipenv install <librería> --dev
```

Actualizará los ficheros pipfile añadiendo el entorno de desarrollo.

**NOTA** es muy recomendable anclar las versiones de las librerías de producción, pues en el pipfile vendrán como asterisco, e intentará automáticamente actualizar el paquete siempre a la última versión.

Para entrar en la shell con todas nuestras librerías del entorno virtual disponibles para ser cargadas:

```
pipenv shell
```

### Desinstalación de paquetes

```
pipenv uninstall <librería> --dev
```

Fácil, actualizará los pipfile, pero no eliminará las dependencias, para eliminar las dependencias que sobren:

```
pipenv clean
```

### Verificar bugs en nuestras dependencias.

```
pipenv check
```

Nos mostrará un listado de los paquetes que deberíamos actualizar y en que versión se solventa el problema mencionado.

### Carga de variables de entorno

Cargará las variables de entorno que se encuentre en el fichero `.env` del directorio.

Y desde python podremos hacer referencias a estas de la siguiente manera:

```
import os
os.environ.get['nombre_de_la_variable']
```

La documentación lo recoge de la siguiente forma:

```
$ cat .env
HELLO=WORLD

$ pipenv run python
Loading .env environment variables…
Python 2.7.13 (default, Jul 18 2017, 09:17:00)
[GCC 4.2.1 Compatible Apple LLVM 8.1.0 (clang-802.0.42)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import os
>>> os.environ['HELLO']
'WORLD'
```

### Gráfico de dependencias

```
pipenv graph
```

### Verificar las dependencias que no se están usando

```
pipenv check --unused
```

Nos mostrará las dependencias que se han quedado huérfanas o que no se están usando.

Para más información aquí el [enlace de la documentación](https://pipenv.readthedocs.io/en/latest/)


## Jupyter

Jupyter es un interprete web de python, en el que nos permite de una manera cómodo estructurar el código ejecutarlo por bloques, muestra gráficos de forma nativa, y los notebook o cuadernos que se generan son sencillos de compartir, de hecho en muchas universidades piden los ejercicios en este tipo de cuadernos.

Para instalarlo:

```
pip3 install jupyter
```

Para ejecutarlo:

```
jupyter notebook
``` 

Nos abrirá un servicio web publicado en un puerto, por defecto es el 8888, seguramente nos abra también automáticamente un navegador para acceder al servicio, y ahí ya podremos empezar a trabajar.

Pero... si tengo un entorno virtual, como le digo a Jupyter que acceda a ese entorno?

En el directorio de nuestro proyecto ejecutaremos lo siguiente:

```
pipenv install ipykernel
pipenv shell
```

En la shell nueva ejecutaremos la siguiente sentencia para crear un kernel con las librerias que tenemos de ese entorno.

```
python -m ipykernel install --user --name=[nombre del entorno]
```

Cuando volvamos a abrir el jupyter podremos elegir entre los kernels que tengamos disponibles, entre ellos estará el que acabamos de crear.

## Visual Studio Code

Supongo que no necesita presentación, es un IDE de programación, entre tantos como hay, seguramente de los mejores programas que ha hecho Microsoft.

La versión de MAC podremos descargar en sl siguiente [enlace](https://code.visualstudio.com/docs/?dv=osx)

Y yo suelo utilizar los siguientes plugins.

### plugins

- [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
- [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)
- [Spanish - Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker-spanish)
- [Visual Studio IntelliCode - Preview](https://marketplace.visualstudio.com/items?itemName=VisualStudioExptTeam.vscodeintellicode)


## Agradecimientos

La idea de crear este tipo de post se la debo a [nicolashery](https://github.com/nicolashery/mac-dev-setup) que leyendo su post me proporciono las ideas para construir el entorno como realmente necesito.

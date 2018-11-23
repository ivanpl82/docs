---
layout: post
title: Creación entorno de desarrollo parte 1
tags:
  - entorno desarrollo
  - mac
  - bash
excerpt_separator:  <!--more-->
---

## Variables de entorno

Ejecutamos en consola para descargar los siguientes ficheros:

```
cd ~
curl -O https://raw.githubusercontent.com/ivanpl82/docs/master/files/profile/.bash_profile
curl -O https://raw.githubusercontent.com/ivanpl82/docs/master/files/profile/.bash_prompt
curl -O https://raw.githubusercontent.com/ivanpl82/docs/master/files/profile/.aliases
```


## Homebrew

[Homebrew](http://brew.sh/) es un administrador de paquetes, el más popular en MacOS.

### Instalación

Ejecutaremos en consola:

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Verificamos que funciona ejecutando:

```
brew doctor
```  

### Uso

Para instalar software en homebrew se llaman **formulas** utilizaremos

```
brew install <formula>
```

Para actualizar la cache de la lista de las formulas a su última versión:

```
brew update
```

**Nota**: Si algún comando falla puede ser debido a un bug, para solucionarlo deberíamos ejecutar las siguientes sentencias:

```
cd /usr/local
git fetch origin
git reset --hard origin/master
```

Para ver que paquetes necesitan ser actualizados:

```
brew outdated
```

Para actualizar un paquete:

```
brew upgrade <formula>
```

Para limpiar la cache:

```
brew cleanup
```

Para listar los paquetes que tienes instalados con su numero de versión:

```
brew list --versions
```


## Git

Para instalar git, ya que tenemos homebrew ejecutaremos:

```
brew install git
```

Para verificar que esté bien instalado:

```
git --version
```

Descargaremos el fichero .gitconfig a nuestro home:

```
cd ~
curl -O https://raw.githubusercontent.com/ivanpl82/docs/master/files/profile/.gitconfig
```

### gitignore    

Para los proyectos que podamos utilizar igual nos vendría bien un fichero gitignore como el siguiente:

```
cd [directorio del proyecto]
curl -O https://raw.githubusercontent.com/ivanpl82/docs/master/files/git/.gitignore
```


### huella ssh

Yo prefiero usar el ssh al https ya que con vs code va así por defecto, y añadiendo las credenciales 

Para crear las credenciales o incluso añadirlas podemos seguir las siguientes [instrucciones](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)

Una vez tengamos la huella creada e importada a github podemos utilizarla sin más, yo además he guardado esta semilla en una bóveda encriptada por si en el periodo inferior a su caducidad tuviera que restaurarla.

Para ello descargaríamos los dos archivos, la parte privada y publica en ˜/.ssh y ejecutaremos:

```
eval "$(ssh-agent -s)"
ssh-add -K ~/.ssh/github
```

Para indicar a git que los eventos de push y fetch se harán por ssh lo haremos con el siguiente comando:

```
git remote set-url origin git@github.com:[usuario]/[repositorio].git

Ejemplo:
git remote set-url origin git@github.com:ivanpl82/torpezanatural.github.io.git
```

**Nota** para distinguirla de otras huellas yo suelo generarlas con el nombre de la aplicación en la que se va a utilizar.


## Agradecimientos

La idea de crear este tipo de post se la debo a [nicolashery](https://github.com/nicolashery/mac-dev-setup) que leyendo su post me proporciono las ideas para construir el entorno como realmente necesito.

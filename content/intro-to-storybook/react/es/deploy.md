---
title: 'Desplegar Storybook'
tocTitle: 'Desplegar'
description: 'Desplegar Storybook online con GitHub y Netlify'
---

Durante este tutorial, construimos componentes en nuestra máquina de desarrollo local. En algún momento, vamos a necesitar compartir nuestro trabajo para obtener feedback del equipo. Vamos a desplegar Storybook para ayudar a nuestros compañeros a revisar la implementación de la interfaz de usuario.


## Exportando como una app estática

Para desplegar Storybook primero necesitamos exportarlo como una aplicación web estática. Esta funcionalidad ya está incorporada en Storybook y preconfigurada.

Running `yarn build-storybook` will output a static Storybook in the `storybook-static` directory, which can then be deployed to any static site hosting service.

Ejecutando `yarn build-storybook` generará un Storybook estático en el directorio `storybook-static`, que luego se puede desplegar en cualquier servicio de hosting de sitios estáticos.

## Publicar Storybook

This tutorial uses <a href="https://www.chromatic.com/?utm_source=storybook_website&utm_medium=link&utm_campaign=storybook">Chromatic</a>, a free publishing service made by the Storybook maintainers. It allows us to deploy and host our Storybook safely and securely in the cloud.

Este tutorial usa <a href="https://www.chromatic.com/?utm_source=storybook_website&utm_medium=link&utm_campaign=storybook">Chromatic</a>, un servicio de publicación gratuito hecho por los mantenedores de Storybook. Nos permite desplegar y alojar nuestro Storybook de forma segura en la nube.

___


## Despliegue continuo

Queremos compartir la última versión de los componentes cada vez que hagamos push del código. Para ello necesitamos desplegar de forma continua Storybook. Confiaremos en GitHub y Netlify para desplegar nuestro sitio estático. Estaremos usando el plan gratuito de Netlify.

### GitHub

Primero debes configurar Git para tu proyecto en el directorio local. Si estás siguiendo el capítulo anterior sobre testing, salta a la creación de un repositorio en GitHub.

```shell
git init
```

Agrega archivos al primer commit.

```shell
git add .
```

Ahora haz commit de los archivos.

```shell
git commit -m "taskbox UI"
```

Ve a Github y configura un repositorio [aquí](https://github.com/new). Nombra tu repo “taskbox”.

![GitHub setup](/intro-to-storybook/github-create-taskbox.png)

En la nueva configuración del repositorio copia la URL de origen del repositorio y añádelo a tu proyecto git con este comando:

```shell
git remote add origin https://github.com/<your username>/taskbox.git
```

Finalmente haz push al repo en GitHub.

```shell
git push -u origin main
```

### Netlify

Netlify tiene incorporado un servicio de despliegue continuo que nos permitirá desplegar Storybook sin necesidad de configurar nuestro propio CI.

<div class="aside">
Si usas CI en tu empresa, añade un script de implementación a tu configuración que suba <code>storybook-static</code> a un servicio de alojamiento de estáticos como S3.
</div>

[Crea una cuenta en Netlify](https://app.netlify.com/start) y da click en “crear sitio”.

![Crear sitio en Netlify](/intro-to-storybook/netlify-create-site.png)

A continuación, haz clic en el botón de GitHub para conectar Netlify a GitHub. Esto le permite acceder a nuestro repositorio remoto Taskbox.

Ahora selecciona el repo de taskbox de GitHub de la lista de opciones.

![Conectar un repositorio en Netlify](/intro-to-storybook/netlify-account-picker.png)

Configura Netlify resaltando el comando build que se ejecutará en tu CI y el directorio en el que se enviará el sitio estático. Para la rama elegir `main`. El directorio es `storybook-static`. Ejecuta el comando `yarn build-storybook`.

![Ajustes Netlify](/intro-to-storybook/netlify-settings.png)

Ahora envía el formulario para construir e implementar el código en la rama `main` del taskbox.

Cuando esto termine veremos un mensaje de confirmación en Netlify con un enlace al Storybook de Taskbox online. Si lo estás siguiendo, tu Storybook desplegado debería estar en línea [como este](https://clever-banach-415c03.netlify.com/).

![Despliegue de Netlify Storybook](/intro-to-storybook/netlify-storybook-deploy.png)

Terminamos de configurar el despliegue continuo de tu Storybook! Ahora podemos compartir nuestras historias con nuestros compañeros de equipo a través de un enlace.

Esto es útil para la revisión visual como parte del proceso de desarrollo de aplicaciones estándar o simplemente para mostrar nuestro trabajo💅.

# Arquitecturas Web

Las arquitecturas web definen la forma en que las páginas de un sitio web están estructuradas y enlazadas entre sí. Las aplicaciones web se basan en en modelo cliente-servidor.

## Cliente / Servidor

<figure>
  <img src="https://github.com/aitor-medrano/dwes2122/blob/master/docs/imagenes/01/clienteservidor.png" />
  <figcaption>Arquitectura Cliente Servidor</figcaption>
</figure>

Uno o varios cliente acceden a un servidor. La nuevas arquitecturas sustituyen el servidor por un balanceador de carga de manera que N servidores dan respuesta a M clientes.

En las aplicaciones web, el cliente es el navegador web.

El cliente hace la petición (*request* normalmente mediante el protocolo GET mediante el puerto 80/443) y el servidor responde (*response*).

### Página web dinámica

Si la página web únicamente contiene HTML + CSS se considera una página estática. Para generar una página dinámica, donde el contenido cambia, a día de hoy tenemos dos alternativas:

* Utilizar un lenguaje de servidor que genere el contenido, ya sea mediante el acceso a una BD o servicios externos.
* Utilizar servicios REST de terceros invocados desde JS.

<figure>
  <img src="https://github.com/aitor-medrano/dwes2122/blob/master/docs/imagenes/01/paginadinamica.png" />
  <figcaption>Página web dinámica</figcaption>
</figure>

Las tecnologías empleadadas (y los perfiles de desarrollo asociados) para la generación de páginas dinámicas son:

| Perfil                    | Herramienta           | Tecnología
| ---                       | ---                   | ---
| *Front-end* / cliente     | Navegador Web         | HTML + CSS + JavaScript
| *Back-end* / servidor     | Servidor Web + BBDD   | PHP, Python, Ruby, Java / JSP, .Net / .asp

!!! tip "Perfil *Full-stack*"
    En las ofertas de trabajo cuando hacen referencia a un *Full-stack developer*, están buscando un perfil que domina tanto el *front-end* como el *back-end*.

### *Single Page Application*

A día de hoy, gran parte del desarrollo web está transicionando de una arquitectura web cliente-servidor clásica donde el cliente realiza una llamada al backend, por una arquitectura SPA donde el cliente gana mucho mayor peso y sigue una programación reactiva que accede a servicios remotos REST que realizan las operaciones (comunicandose mediante JSON).

<figure>
  <img src="https://github.com/aitor-medrano/dwes2122/blob/master/docs/imagenes/01/01spa.png" />
  <figcaption>Arquitectura tradicional vs SPA</figcaption>
</figure>

## Arquitectura de 3 capas

Hay que distinguir entre capas **físicas** (*tier*) y capas **lógicas** (*layer*).

### Tier

Capa física de una arquitectura. Supone un nuevo elemento hardware separado físicamente. Las capas físicas más alejadas del cliente están más protegidas, tanto por firewalls como por VPN.

Ejemplo de arquitectura en tres capas físicas (*3 tier*):

* Servidor Web
* Servidor de Aplicaciones
* Servidor de base de datos

<figure>
  <img src="https://github.com/aitor-medrano/dwes2122/blob/master/docs/imagenes/01/tier3.png" />
  <figcaption>Arquitectura de tres capas físicas</figcaption>
</figure>

!!! warning "Cluster en tiers"
    No confundir las capas con la cantidad de servidores. Actualmente se trabaja con arquitecturas con múltiples servidores en una misma capa física mediante un cluster, para ofrecer tolerancia a errores y escalabilidad horizontal.

### Layer

![Arquitectura de tres capas físicas](https://github.com/aitor-medrano/dwes2122/blob/master/docs/imagenes/01/layer3.png){ align=right }

En cambio, las capas lógicas (*layers*) organizan el código respecto a su funcionalidad:

* Presentación
* Negocio / Aplicación / Proceso
* Datos / Persistencia

Como se observa, cada una de las capas se puede implementar con diferentes lenguajes de programación y/o herramientas.

<figure>
  <img src="https://github.com/aitor-medrano/dwes2122/blob/master/docs/imagenes/01/tierlayer.png" />
  <figcaption>Arquitectura de tres capas físicas en tres lógicas</figcaption>
</figure>

## MVC

![MVC](https://github.com/aitor-medrano/dwes2122/blob/master/docs/imagenes/01/mvc.png){align=right & width=500}

*Model-View-Controller* o Modelo-Vista-Controlador es un modelo de arquitectura que separa los datos y la lógica de negocio respecto a la interfaz de usuario y el componente encargado de gestionar los eventos y las comunicaciones.

Al separar los componentes en elementos conceptuales permite reutilizar el código y mejorar su organización y mantenimiento. Sus elementos son:

* Modelo: representa la información y gestiona todos los accesos a ésta, tanto consultas como actualizaciones provenientes, normalmente, de una base de datos. Se accede via el controlador.
* Controlador: Responde a las acciones del usuario, y realiza peticiones al modelo para solicitar información. Tras recibir la respuesta del modelo, le envía los datos a la vista.
* Vista: Presenta al usuario de forma visual el modelo y los datos preparados por el controlador. El usuario interactura con la vista y realiza nuevas peticiones al controlador.

Lo estudiaremos en más detalle al profundizar en el uso de los frameworks PHP.

## Decisiones de diseño

* ¿Qué tamaño tiene el proyecto?
* ¿Qué lenguajes de programación conozco? ¿Vale la pena el esfuerzo de aprender uno nuevo?
* ¿Voy a usar herramientas de código abierto o herramientas propietarias? ¿Cuál es el coste de utilizar soluciones comerciales?
* ¿Voy a programar la aplicación yo solo o formaré parte de un grupo de programadores?
* ¿Cuento con algún servidor web o gestor de base de datos disponible o puedo decidir libremente utilizar el que crea necesario?
* ¿Qué tipo de licencia voy a aplicar a la aplicación que desarrolle?

## Herramientas

### Servidor Web

Software que recibe peticiones HTTP (GET, POST, DELETE, ...). Devuelve el recurso solicitado (HTML, CSS, JS, JSON, imágenes, etc...)

El producto más implantando es Apache Web Server (<https://httpd.apache.org/>), creado en 1995.

* Software libre y multiplataforma
* Sistema de módulos dinámicos → PHP, Python, Perl
* Utiliza el archivo `.htaccess` para su configuración

En la actualidad, *Apache* está perdiendo mercado respecto a Nginx (<https://www.nginx.com>). Se trata de un producto más moderno (2004) y que en determinados escenarios tiene mejor rendimiento que Apache.

* Comparativa servidores web: <https://w3techs.com/technologies/history_overview/web_server/ms/q>

### Servidor de Aplicaciones

* Software que ofrece servicios adicionales a los de un servidor web:
    * Clustering
    * Balanceo de carga
    * Tolerancia a fallos
* *Tomcat* (<http://tomcat.apache.org/>) es el servidor de aplicaciones *open source* y multiplataforma de referencia para una arquitectura Java.
    * Contiende un contenedor Web Java que interpreta *Servlets* y JSP.

!!! info
    Tanto los servidores web como los servidores de aplicaciones los estudiaremos en profundidad en el módulo de *"Despliegue de Aplicaciones Web"*.

### Lenguajes en el servidor

Las aplicaciones que generan las páginas web se programan en alguno de los siguientes lenguajes:

* PHP
* JavaEE: Servlets / JSP
* Python
* ASP.NET → Visual Basic .NET / C#
* Ruby
* ...

#### JavaEE

*Java Enterprise Edition* es la solución Java para el desarrollo de aplicaciones *enterprise*. Ofrece una arquitectura muy completa y compleja, escalable y tolerante a fallos. Planteada para aplicaciones para grandes sistemas.

![JavaEE](https://github.com/aitor-medrano/dwes2122/blob/master/docs/imagenes/01/javaee.png)

#### PHP

* Lenguaje de propósito general diseñado para el desarrollo de páginas web dinámicas
* En un principio, lenguaje no tipado.
* Actualmente en la versión 8. Se recomienda al menos utilizar una versión superior a la 7.0.
* Código embebido en el HTML
* Instrucciones entre etiquetas `<?php` y `?>`
    * Para generar codigo dentro de PHP, podemos usar la instrucción `echo`
* Multitud de librerías y frameworks:
    * Laravel, Symfony, Codeigniter, CakePHP, Zend

Su documentación es bastante completa: <https://www.php.net/manual/es/index.php>

El siguiente mapa mental muestra un resumen de sus elementos:

<figure>
  <img src="https://github.com/aitor-medrano/dwes2122/blob/master/docs/imagenes/01/php.jpg" />
  <figcaption>Elementos del lenguaje PHP</figcaption>
</figure>

Durante las siguientes unidades vamos a estudiar PHP en profundidad.

## Puesta en marcha

Para poder trabajar con un entorno de desarrollo local, hemos de preparar nuestro entorno de desarrollo con las herramientas comentadas. A lo largo del curso vamos a utilizar la versión 8 de PHP.

### XAMPP

XAMPP (https://www.apachefriends.org/es/index.html) es una distribución compuesta con el software necesario para desarrollar en entorno servidor. Se compone de las siguientes herramientas en base a sus siglas:

* X para el sistema operativo (de ahí que se conozca tamnbién como LAMP o WAMP).
* A para Apache.
* M para MySQL / MariaDB. También incluye phpMyAdmin para la administración de la base de datos desde un interfaz web.
* P para PHP.
* la última P para Perl.

Desde la propia página se puede descargar el archivo ejecutable para el sistema operativo de nuestro ordenador. Se recomienda leer la FAQ de cada sistema operativo con instrucciones para su puesta en marcha.

!!! note "XAMPP en Windows"
    Si vas a trabajar con tu propio ordenador, XAMPP o MAMPP es una solución más sencilla que Docker, sobre todo si trabajar con Windows como sistema operativo.


### Entorno de desarrollo

En este curso vamos a emplear *Visual Studio Code* (<https://code.visualstudio.com>) o [PhpStorm](https://www.jetbrains.com/es-es/phpstorm/) la más conocida pero siendo de pago pero tenemos licencia.

*VSCode* es un editor de código fuente que se complementa mediante extensiones. Para facilitar el trabajo a lo largo del curso vamos a utilizar las siguientes extensiones:

* [PHP Intelephense](https://marketplace.visualstudio.com/items?itemName=bmewburn.vscode-intelephense-client)
* [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)

En la siguiente sesión comenzaremos a utilizar *Intelephense* pero en esta sesión nos vamos a centrar en *Docker* (más adelante instalaremos nuevas extensiones).

Por ejemplo, si abrimos la extensión de *Docker*, podréis visualizar tanto los contenedores como las imágenes de vuestro sistema. Desde cada contenedor, mediante clic derecho, podemos iniciar/detener/reiniciar cada contenedor, así como ver su contenido o abrir un terminal dentro del mismo.

<figure>
  <img src="https://github.com/aitor-medrano/dwes2122/blob/master/docs/imagenes/01/vscodedocker.png" width="300"/>
  <figcaption>Opciones mediante extensión Docker en VSCode</figcaption>
</figure>

### Hola Mundo

Y como no, nuestro primer ejemplo será un *Hola Mundo* en PHP.

Si nombramos el archivo como `index.php`, al acceder a `http://localhost` automáticamente cargará el resultado:

``` html+php hl_lines="9-11"
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hola Mundo</title>
</head>
<body>
    <?php
        echo "Hola Mundo";
    ?>
</body>
</html>
```

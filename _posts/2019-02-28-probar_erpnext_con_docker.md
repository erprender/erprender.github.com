---
layout: article
title: Instalar ERPNext con Docker
published: true
---
Una de las formas más fáciles de instalar ERPNext para poder explorarlo es mediante Docker.

Si bien existen múltimples imágenes de Docker publicadas que permiten ejecutar ERPNext en este artículo usaremos la imagen de [Docker Compose que proporciona Frappe.](https://github.com/frappe/frappe_docker)

Veamos cómo hacerlo.

Necesitaremos tener instalado Docker y Docker Compose en nuestro ordenador. En el caso de Ubuntu (y probablemente otras distribuciones basadas en Debian) se puede ejecutar:

{% highlight bash %}
sudo apt install docker-compose docker.io
sudo usermod -aG docker ${USER}
{% endhighlight %}

Debemos salir y entrar de la cuenta para que se aplique el grupo a nuestro usuario. Otra opción en lugar de entrar y salir de la sesión es ejecutar:

{% highlight bash %}
su - ${USER}
{% endhighlight %}


Nos descargaremos el repositorio con la imagen Docker desde GitHub:
{% highlight bash %}
git clone https://github.com/frappe/frappe_docker.git
cd frappe_docker
{% endhighlight %}

Inicializaremos las instancias de Docker:

{% highlight bash %}
./dbench setup docker
{% endhighlight %}

Este comando utilizará Docker Compose (`docker-compose up -d`) para crear cinco instancias de Docker garantizando que se arrancan en el orden adecuado:

* mariadb
* redis-queue
* redis-cache
* redis-socketio
* frappe


Inicializaremos bench para que disponga del framework Frappe:
{% highlight bash %}
./dbench init
{% endhighlight %}

Con esto tenemos Bench y Frappe instalados en la imagen Docker _frappe_. Sin embargo para que podamos acceder mediante el navegador todavía necesitamos añadir un sitio. 

{% highlight bash %}
./dbench new-site site1.local 
./dbench start
{% endhighlight %}

Ahora ya podemos ver algo en el navegador. Abrimos [http://localhost:8000](http://localhost:8000) y nos encontraremos con la aplicación básica de Frappe.

Frappe es el framework en el que se basa ERPNext y ofrece de base un buen puñado de características:
* Lista de tareas
* Tableros Kanban
* Calendario
* Notas y recordatorios
* Gestión de sitio web
  - Creación de páginas
  - Formularios web
  - Blogs

Podremos fisgar utilizando el usuario _Administrator_ y la clave _admin_.

![Cuadro de mandos básico de Frappe]({{site.baseurl}}/images/Screenshot_20190228_215231.png)

Sin embargo lo nos interesa ver es un instalación de ERPNext. Pararemos el servidor pulsando `Ctrl + C`. Reinstalaremos el sitio y le añadiremos ERPNext.


{% highlight bash %}
./dbench --site site1.local reinstall
./dbench get-app erpnext https://github.com/frappe/erpnext
./dbench --site site1.local install-app erpnext
./dbench start
{% endhighlight %}

Ahora sí abrimos [http://localhost:8000](http://localhost:8000) y podremos configurar nuestra instalación de ERPNext tras lo que nos encontraremos con la versión en desarrollo actual.

En nuestro caso nos hemos encontrado con un problema en la instalación. Tras la parametrización del asistente inicial nos muestra el mensaje:
	
    Setup failed
	Could not start up: Error in setup

![Setup failed Could not start up: Error in setup]({{site.baseurl}}/images/setup_failed.png)

Tras unos pocos reintentos la aplicación finalmente está disponible.

![Dashboard ERPNext]({{site.baseurl}}/images/cuadro_de_mando_dashboard_erpnext_12.png)

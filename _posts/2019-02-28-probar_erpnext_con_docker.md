---
layout: article
title: Instalar ERPNext con Docker
published: true
---
Una de las formas más fáciles de instalar ERPNext para poder explorarlo es mediandte Docker.

Si bien existen múltimples imágenes de Docker publicadas que permiten ejecutar ERPNext en este artículo usaremos la imagen de [Docker Compose que proporciona Frappe.](https://github.com/frappe/frappe_docker)

Veamos cómo hacerlo.

Necesitaremos tener instalado Docker y Docker Compose en nuestro ordenador. En el caso de Ubuntu (t probablemente otras distribuciones basadas en Debian) se puede ejecutar:

{% highlight bash %}
sudo apt install docker-compose docker.io
sudo usermod -aG docker ${USER}
{% endhighlight %}

Debemos salir y entrar de la cuenta para que se aplique el grupo a nuestro usuario. Otra opción en lugar de entrar y salir de la sesión es ejecutar:

{% highlight bash %}
su - ${USER}
{% highlight bash %}

{% highlight bash %}
git clone https://github.com/frappe/frappe_docker.git
cd frappe_docker
{% highlight bash %}

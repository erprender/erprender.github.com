---
layout: article
title: Instalar ERPNext con Docker
published: true
---
Una de las formas más fáciles de instalar ERPNext para poder explorarlo es mediandte Docker.

Si bien existen múltimples imágenes de Docker publicadas que permiten ejecutar ERPNext en este artículo usaremos la imagen de [Docker Compose que proporciona Frappe.](https://github.com/frappe/frappe_docker)

Veamos cómo hacerlo.

Necesitaremos tener instalado Docker y Docker Compose en nuestro ordenador. En el caso de Ubuntu (y probablemente otras distribuciones basadas en Debian) se puede ejecutar:

{% highlight bash %}
sudo apt install docker-compose docker.io
sudo usermod -aG docker \$\{USER\}
{% endhighlight %}



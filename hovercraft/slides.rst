:title: docker-compose
:author: Fernando Espíndola
:description: docker-compose
:css: stylesheet.css

----

.. image:: images/docker-logo.png
    :height: 600px

Docker Compose

----

.. code:: yaml

  mysql:
    image: mysql:5.6.24
  environment:
    - MYSQL_DATABASE=exemplo
    - MYSQL_ROOT_PASSWORD=password

  app:
    build: .
  links:
    - mysql

----

* Compose is a tool for defining and running complex applications with Docker

----

* define your containers in simples yaml file.
* Compose container together.
* Manage group of containers with single tool.

----

.. code:: yaml

  mysql:
    image: mysql:5.6.24
  environment:
    - MYSQL_DATABASE=exemplo
    - MYSQL_ROOT_PASSWORD=password

----

.. code:: yaml

  app:
    build: .
  links:
    - mysql


----

.. code:: shell

  $ docker-compose build
  $ docker-compose up
  $ docker-compose ps

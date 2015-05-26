:title: docker-compose
:author: Fernando Espíndola
:description: docker-compose
:css: stylesheet.css

----

Docker Compose
==============

.. image:: images/docker-logo.png
    :height: 600px

----

Docker Compose
==============

* Compose is a tool for defining and running complex applications with Docker.
* define your containers in simples YAML file.
* Originated from Fig

----

Example
=======
  * Application ABC

  * Dependencies

      * MySQL
      * Redis
      * MongoDB

----

Docker Hub Registry
===================

.. image:: images/docker-hub-registry.png
    :height: 600px

https://registry.hub.docker.com/

----

:data-x: r+1500
:data-y: r+0
:data-scale: 1

----

:data-x: r+0
:data-y: r-200
:data-scale: .5
:id: docker-compose

docker-compose.yml
==================


.. code:: yaml

  mysql:
    image: mysql:5.6.24
    volumes:
      - ~/.docker/boletos/mysql:/var/lib/mysql
    environment:
      - MYSQL_DATABASE=boletos
      - MYSQL_ROOT_PASSWORD=password

----

:data-x: r+0
:data-y: r+110

.. code:: yaml

  mongo:
    image: mongo:3.0.2
    volumes:
      - ~/.docker/boletos/mongo:/data/db

----

:data-y: r+70

.. code:: yaml

  redis:
    image: redis:2.8.19
    volumes:
      - ~/.docker/boletos/redis:/data

----

:data-y: r+80

.. code:: yaml

  boletos:
    build: .
    command: uwsgi --ini uwsgi.ini
    links:
      - mysql
      - redis
      - mongo

----

:data-y: r+100

.. code:: yaml

  celery:
    build: .
    command: celery -A boletos worker -l info -B
    links:
      - mysql
      - redis
      - mongo

----

:data-scale: 1
:data-x: r+1500
:data-y: r-200

Dockerfile
==========

.. code:: docker

  FROM ubuntu:14.04.2
  MAINTAINER  fer.esp@gmail.com

  RUN apt-get update

  RUN apt-get -y install build-essential
  RUN apt-get -y install make
  RUN apt-get -y install gcc
  RUN apt-get -y install git
  RUN apt-get -y install libmysqlclient-dev
  RUN apt-get -y install python
  RUN apt-get -y install python-dev
  RUN apt-get -y install python-pip
  RUN apt-get -y install python-setuptools
  RUN apt-get -y install python-virtualenv
  RUN apt-get -y install vim

  RUN apt-get -y autoremove
  RUN apt-get -y autoclean
  RUN apt-get -y clean

  WORKDIR /app

----

:data-y: r+0
:data-x: r+1500

Putting It All Together
=======================

Build
-----

.. code:: shell

  $ docker-compose build

Running
-------

.. code:: shell

  $ docker-compose up

----

:id: questions

Questions?
==========

.. image:: images/img-04.jpg
    :width: 400px

Thank you! Fernando Espíndola
------------------------------

+------------------------------------+-----------------------------------------+
| .. image:: images/gmail-logo.jpg   |  fer.esp@gmail.com                      |
|         :height: 20px              |                                         |
+------------------------------------+-----------------------------------------+
| .. image:: images/twitter-logo.jpg | `@feresp <https://twitter.com/feresp>`_ |
|         :height: 35px              |                                         |
+------------------------------------+-----------------------------------------+

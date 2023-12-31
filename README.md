# Docker - PHP

[Github][1] [Docker][2] is a **Docker and PHP** repository


Setup
------------
* ``composer install --ignore-platform-reqs --working-dir=./app``


* For a standard build / setup
  
  ``docker compose up -d ``

* For a development build / setup

  ``bash ./bin/dev-mode.sh -d``

* For a development build / setup with XDEBUG
  
  ``XDEBUG_MODE=debug bash ./bin/dev-mode.sh -d``

> [!IMPORTANT] PHP Storm -> Settings -> Languages & Frameworks -> PHP -> Set "CLI Interpreter"
> 
> Pick "Docker" 
> 
> Image name: "kmtsvetanov/php-composer:1.2"
> 
>  This will use php 8.2.11

> [!IMPORTANT] DB init is in ./docker/db/dump.sql

Useful Info
------------
* For installing Docker Desktop on Windows if you wish to use another directory (C: is full) in cmd:
  
  *
    ``start /w "" "Docker Desktop Installer.exe" install -accept-license --installation-dir="D:\WORK\DOCKER-VIRTUAL\Docker" --wsl-default-data-root="D:\WORK\DOCKER-VIRTUAL\wsl" --windows-containers-default-data-root="D:\WORK\DOCKER-VIRTUAL"``


* Create Images for Prod and store them in DockerHub:
  
  * ``docker login -u <<username>>`` 
  * ``docker build --target app -t <<username>>/symfony-php-composer:1.0 -f ./docker/php/Dockerfile .``
  * ``docker build -t <<username>>/symfony-nginx-php:1.0 -f ./docker/nginx/Dockerfile .`` 
  * ``docker push <<username>>/symfony-php-composer:1.0`` 
  * ``docker push <<username>>/symfony-nginx-php:1.0`` 
  
  * ``docker login -u kmtsvetanov`` 
  * ``docker build --target app -t kmtsvetanov/symfony-php-composer:1.0 -f ./docker/php/Dockerfile .``
  * ``docker build -t kmtsvetanov/symfony-nginx-php:1.0 -f ./docker/nginx/Dockerfile .`` 
  * ``docker push kmtsvetanov/symfony-php-composer:1.0`` 
  * ``docker push kmtsvetanov/symfony-nginx-php:1.0`` 


* We checked if our [environment can run symfony][3] (run inside `setup-app`)
  * ``symfony check:requirements``


* [Install Symfony][4]
  * ``composer create-project symfony/skeleton:"6.3.*" my_project_directory``

On merge into main we want to:
------------
* Run the tests
* Build our two images
* Login to the registry (DockerHub)
* Push our built images to the registry


* Irl we would then deploy our code to whatever cloud service we use


[1]: https://github.com/KMTsvetanov/Setup
[2]: https://hub.docker.com/search?q=kmtsvetanov%2F
[3]: https://symfony.com/doc/current/setup.html#technical-requirements
[4]: https://symfony.com/doc/current/setup.html#creating-symfony-applications



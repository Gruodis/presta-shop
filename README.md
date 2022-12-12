<p align="center"><img width="150" alt="Shows an illustrated sun in light mode and a moon with stars in dark mode." src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Prestashop.svg/1194px-Prestashop.svg.png"></p>

<h1 align="center"> PrestaPro Projektų paleidimas </h1>


<br/>
<br/>


<p align="center"><img width="150" alt="Shows an illustrated sun in light mode and a moon with stars in dark mode." src="https://user-images.githubusercontent.com/43164261/207134539-134dfea4-35c3-47f4-a1f4-2977e4631e3e.svg"></p>

## Naujam projekto paleidimui

Check if docker/compose installed:

- ```bash
  docker -v docker-composer -v
  ```

- ```bash
  sudo apt-get install docker-compose
  ```
<br/>

- #### Docker FYI:

  Configure Docker to start on boot with systemd
  ```bash
  sudo systemctl enable docker.service
  sudo systemctl enable containerd.service
  ```
  To stop this behavior, use disable instead.
  ```bash
  sudo systemctl disable docker.service
  sudo systemctl disable containerd.service
  ```


<br/>

* Run:

- ```bash 
  cp app/config/parameters.php.dist app/config/parameters.php
  ```

- ```bash
  sudo docker-compose up --build --force-recreate
  ```
- :interrobang: Jeigu bandant paleist dockeri meta:
    ```bash
    https://packages.sury.org/php/apt.gpg | apt-key add - && apt-get update -qq' returned a non-zero code: 100ERROR: Service 'prestashop' failed to build : Build failed
    ```
-  :heavy_check_mark: iš **docker/Dockerfile.prestashop** ištrinam:
    ```bash
    RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee -a /etc/apt/sources.list.d/php.list \
        && curl https://packages.sury.org/php/apt.gpg | apt-key add - \
        && apt-get update -qq
    ```
    
-  Failas turėtų atrodyt taip (galima tiesiog copy paste):
     
    ```bash
    FROM prestashop/prestashop:1.7-7.2-apache // šitos eilutės nenaudojame nebent būtina

    RUN apt-get update -qq \
        && DEBIAN_FRONTEND=noninteractive apt-get install -y git \
        mariadb-client wget curl \
        ca-certificates lsb-release apt-transport-https gnupg bsdmainutils

    #Adding package
    RUN pecl install zip

    RUN a2enmod ssl

    ADD ./docker/ssl /etc/apache2/ssl
    ADD ./docker/php/php.ini /usr/local/etc/php/php.ini

    ADD ./docker/site.conf /etc/apache2/sites-available/000-default.conf


    EXPOSE 443
    EXPOSE 80

    ```
  
- :interrobang: Jeigu bandant paleist docker meta:
  - ```bash
    PHP Fatal error:  Uncaught  --> Smarty: unable to write file /var/www/html/cache/smarty/compile/37/65/91/wrt636e46e56f3193_90422010 <-- \n  thrown in /var/www/html/tools/smarty/sysplugins/smarty_internal_write_file.php on line 46
    ```
  -  :heavy_check_mark: einame į projekto dir **"../cache/"** ir patikriname folderio **"../smarty"** permission:
    
<br>
<br>

## Pakartotiniam projekto paleidimui:

- ```bash
  sudo docker-compose up
  ```
  
<br>
<br>

# :red_circle: Jau startuoto projekto atnaujinimui as folows:

:interrobang: Naujai ir pakartotinai paleidus projektą ištrinti <b>admin</b> ir <b>install</b>

```bash
sudo docker-compose down
```
- Atsinaujiname branch'ą, tuomet:

```bash
sudo docker-compose up --build -d --force-recreate
```
  
<br>
<br>


# :interrobang: Error'ai ir sprendimai:

- Jeigu bandant paleist dockeri gauname ***permission*** error'ą:

- First try this command and reboot system:
  ```bash
  sudo gpasswd -a $USER docker
  newgrp docker
  ```
- Or You can run docker with ``sudo docker-compose up`` or run this command:
  ```bash
  sudo chmod 666 /var/run/docker.sock
  ```
  and then ``docker-compose up``

<br>
<br>

#### Jiegu neatidaro nuoroų:
<ol>
 <li>Einame į PrestaShop admin,</li>
 <li>Konfiguruoti -> Parduotuves nustatymai -> Duomenu srautas ir SEO, (Shop Parameters -> Traffic & SEO -> SEO & URLs)</li>
 <li>Pasirenkame nustatymą: URL/Draugiškas URL == TAIP (Choose Set up URLs: Friendly URL == YES)</li>
 <li>Išsaugome pakeitimus.</li>
</ol>


Links:  https://marabika-fe.5z.lt/category.html https://marabika-fe.5z.lt/blog.html


### Danija
SEO  -> disable friendly url

```bash
Press shift two times in Phpstorm define:/* Debug only */
if (!defined('_PS_MODE_DEV_')) {
 define('_PS_MODE_DEV_', false);/* Compatibility warning */
define('_PS_DISPLAY_COMPATIBILITY_WARNING_', false);
if (_PS_MODE_DEV_ === false) {
```
<br>

### Fix missing images, open phpMyAdmin -> prestashop table -> sql:
```bash
TRUNCATE prestashop.ps_image;
TRUNCATE prestashop.ps_image_lang;
TRUNCATE prestashop.ps_image_shop;
```
<hr/>

https://codepen.io/devam-soni/pen/PoqaKWm


### APPLE KEYBOARD ON LINUX
Probably because you accidentally press F6, which is labeled Num Lock. When Num Lock is on, the only keys active are the numeric keypad keys marked by numbers on the lower right corners.

Docker compose in phpterminal:https://docs.docker.com/desktop/install/ubuntu/


## To Do
- [ ] - https://www.freecodecamp.org/news/create-a-portfolio-website-using-html-css-javascript/

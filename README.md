<p align="center"><img width="150" alt="Shows an illustrated sun in light mode and a moon with stars in dark mode." src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Prestashop.svg/1194px-Prestashop.svg.png"></p>

# PrestaPro Projektų paleidimas

## Naujam projekto paleidimui

-  jeigu nėra instaliuota docker-composer, patikrinimui ```docker -v docker-composer -v```

- ```bash
  sudo apt-get install docker-compose
  ```
 
* Run:

- ```bash 
  cp app/config/parameters.php.dist app/config/parameters.php
  ```

- ```bash
  sudo docker-compose up --build --force-recreate
  ```
- :interrobang: Jeigu bandant paleist dockeri meta:
  - ```bash
    https://packages.sury.org/php/apt.gpg | apt-key add - && apt-get update -qq' returned a non-zero code: 100ERROR: Service 'prestashop' failed to build : Build failed
    ```
  -  :heavy_check_mark: iš **docker/Dockerfile.prestashop** ištrinam:
  - ```bash
    RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee -a /etc/apt/sources.list.d/php.list \
        && curl https://packages.sury.org/php/apt.gpg | apt-key add - \
        && apt-get update -qq
    ```
- :interrobang: Jeigu bandant paleist dockeri meta:
  - ```bash
    PHP Fatal error:  Uncaught  --> Smarty: unable to write file /var/www/html/cache/smarty/compile/37/65/91/wrt636e46e56f3193_90422010 <-- \n  thrown in /var/www/html/tools/smarty/sysplugins/smarty_internal_write_file.php on line 46
    ```
  -  :heavy_check_mark: einame į projekto dir **"../cache/"** ir patikriname folderio **"../smarty"** permission:
    




## Pakartotiniam projekto paleidimui:

- ```bash
  sudo docker-compose up
  ```
## Jau startuoto projekto atnaujinimui as folows:

- ```bash
  sudo docker-compose down
  ```
- Atsinaujiname branch'ą, tuomet:

- ```bash
  sudo docker-compose up --build -d --force-recreate
  ```



### Naujai ir pakartotinai paleidus projektą ištrinti <b>admin</b> ir <b>install</b>

# :interrobang: Error'ai ir sprendimai:

- :red_circle: Jeigu bandant paleist dockeri gauname ***permission*** error'ą:
- ```bash
  sudo chmod 666 /var/run/docker.sock
  ```

-  Failas turėtų atrodyt taip (galima tiesiog copy paste):
- ```bash
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
### Fix missing images, open phpMyAdmin -> prestashop table -> sql:
```bash
TRUNCATE prestashop.ps_image;
TRUNCATE prestashop.ps_image_lang;
TRUNCATE prestashop.ps_image_shop;
```
<hr/>


https://codepen.io/devam-soni/pen/PoqaKWm

### AlpineJS lessons: 
https://laracasts.com/series/alpine-essentials/episodes/1

### APPLE KEYBOARD ON LINUX
Probably because you accidentally press F6, which is labeled Num Lock. When Num Lock is on, the only keys active are the numeric keypad keys marked by numbers on the lower right corners.

Docker compose in phpterminal:https://docs.docker.com/desktop/install/ubuntu/

## PhpStorm
### PhpStorm & Tailwind autocomplete & Commands available in PhpStorm terminal
Download and unpack PhpStorm v2022.2.1 package to /opt location and running this installation should make commands available in the terminal.

#### Create PhpStorm shortcut in OS Applications
<ol>
 <li>Create file in: /usr/share/applications/phpstorm.desktop</li>
 <li>Inside phpstorm.desktop file:</li>
</ol>
 
```bash
[Desktop Entry]
Version=2022.2.1
Name=PhpStorm-Tailwind
Comment=Phpstorm
Exec=/opt/PhpStorm-222.3739.61/bin/phpstorm.sh
Icon=/opt/PhpStorm-222.3739.61/bin/phpstorm.svg
Terminal=false
Type=Application
Categories=Utility;Application;
```

### PhpStorm terminal change:
Settings > Tools > Terminal > Shell path: /bin/bash -i

## Active Collab Timer linux
```bash
sudo apt-get install libgconf-2-4
```
#### Then install: 
```bash
sudo dpkg -i activecollab-timer.deb
```
#### After app launches:
<ol>
 <li>Set to: self hosted</li>
 <li>tasks.onesoft.io</li>
 <li>enter credentials</li>
<ol>

## To Do
- [ ] - https://www.freecodecamp.org/news/create-a-portfolio-website-using-html-css-javascript/

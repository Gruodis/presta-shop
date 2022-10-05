# Good to know

## How to commit:
Commit local project to github repo:
```bash
git initgit add .    (add all files to stage for later commit)git commit -m "Message to describe commit."
```
pull requestupdate project (patikkrinam ar nera pasikeitimu brance)jeigu commit metu failas neisikelia i serveri ir raudonuoja, reikia Git -> Add (įkeliam failą į stage).

# PrestaPro Projektų paleidimas
## Marabika:
### Jeigu bandant paleist dockeri meta:
```bash
https://packages.sury.org/php/apt.gpg | apt-key add - && apt-get update -qq' returned a non-zero code: 100ERROR: Service 'prestashop' failed to build : Build failed
```
#### Vaistai: iš docker/Dockerfile.prestashop ištrinam:
```bash
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee -a /etc/apt/sources.list.d/php.list \
    && curl https://packages.sury.org/php/apt.gpg | apt-key add - \
    && apt-get update -qq
```

#### Failas turėtų atrodyt taip (galima tiesiog copy paste):
```bash
FROM prestashop/prestashop:1.7-7.2-apache

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

### Jiegu neatidaro nuoroų:
Einame į PrestaShop admin >
Konfiguruoti > Parduotuves nustatymai > Duomenu srautas ir SEO > 
Pasirinkti nustatymą: URL/Draugiškas URL == ON > Save


## Marabika:
--naujam projekto paleidimui
```bash
sudo apt-get install docker-compose
```
--naujam/pakartotiniam projekto paleidimui:
```bash
sudo chmod 666 /var/run/docker.sockdocker-compose up
```
--naujai ir pakartotinai paleidus projektą ištrinti admin install 

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

https://codepen.io/devam-soni/pen/PoqaKWm

### AlpineJS lessons: 
https://laracasts.com/series/alpine-essentials/episodes/1

## APPLE KEYBOARD ON LINUX
Probably because you accidentally press F6, which is labeled Num Lock. When Num Lock is on, the only keys active are the numeric keypad keys marked by numbers on the lower right corners.

Docker compose in phpterminal:https://docs.docker.com/desktop/install/ubuntu/

### PhpStorm & Tailwind autocomplete & Commands available in PhpStorm terminal
Download and unpack PhpStorm v2022.2.1 package to /opt location and running this installation should make commands available in the terminal.

-- Create file in: /usr/share/applications/phpstorm.desktop <br />
-- inside phpstorm.desktop file: <br />
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
### PppStorm terminal change:
Settings > Tools > Terminal > Shell path: /bin/bash -i

### Active Collab Timer linux
```bash
sudo apt-get install libgconf-2-4
```
#### Then install: 
```bash
sudo dpkg -i activecollab-timer.deb
```
#### After app launches:

--set to self hosted  <br />
--tasks.onesoft.io & credentials

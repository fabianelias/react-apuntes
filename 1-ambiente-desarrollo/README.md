### Instalación ambiente desarrollo Linux

#### Requisitos previos.

Para la realización de esta guía usted está trabajando en Linux Ubuntu >14...

Para poder seguir deberá tener instalado el SDK de Android, puede seguir la siguientes instrucciones para su instalación   
[link](http://facebook.github.io/react-native/docs/getting-started.html#android-development-environment) .
#### 1- Instalación de Node.js

Para comenzar se debe instalar NodeJS, desde una terminal ejecutar los siguientes comandos:

`
sudo apt-get install -y build-essential
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo ln -s /usr/bin/nodejs /usr/bin/node
`

**NOTA** : Las instrucciones anteriores son para Ubuntu. Si estás en una distribución diferente, por [NodeJs](https://nodejs.org/en/download/)

-----------------------------

#### 2- Instalación de watchman

Watchman es una herramienta de Facebook para la observación de los cambios en el sistema de archivos. Es necesario que lo instale para un mejor rendimiento y evitar un archivo de observación de nodo de errores.

Pegue lo siguiente en su terminal para compilar vigilante de la fuente e instalarlo:
`
git clone https://github.com/facebook/watchman.git
cd watchman
git checkout v4.1.0  # the latest stable release
./autogen.sh
./configure
make
sudo make install
`

#### 3- Instalación de Flow

El flujo es un corrector de tipo estático JavaScript. Para instalarlo, pegue el siguiente en la terminal:
`sudo npm install -g flow-bin`

-----------------------------

#### Configuración de un dispositivo Android
Vamos a crear un dispositivo Android para ejecutar nuestro proyecto inicial.

Lo primero es que conectar el dispositivo y comprobar el código del fabricante usando lsusb, que si algo salida como esta:

`
$ lsusb
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 003: ID 22b8:2e76 Motorola PCS
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
`

Estas líneas representan los dispositivos USB conectados actualmente a su máquina.

Desea que la línea que representa su teléfono. Si usted está en duda, intente desconectar el teléfono y ejecutar el comando de nuevo:
`
$ lsusb
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
`
Usted verá que después de quitar el teléfono, la línea que tiene el modelo de teléfono ( "Motorola PCS" en este caso) desapareció de la lista. Esta es la línea que nos importa.
`Bus 001 Device 003: ID 22b8:2e76 Motorola PCS`
Desde la línea de arriba, quieres coger los cuatro primeros dígitos de la ID del dispositivo:

22b8:2e76

En este caso, es 22b8. Ese es el identificador para Motorola.

Tendrá que éste sea incorporado sus reglas udev con el fin de poner en marcha:

`
eco SUBSISTEMA == "usb" , ATTR { idVendor } == "22b8" , MODO = "0666" , GRUPO = "plugdev"  | sudo tee / etc / udev / reglas . d / 51 - androide - USB . reglas
`
Asegúrese de que reemplaza 22b8con el identificador se obtiene en el comando anterior.

Ahora compruebe que el dispositivo se conecta correctamente con el BAD, el puente de depuración de Android, utilizando adb devices.

`Lista de los dispositivos conectados dispositivo TA9300GLMK`

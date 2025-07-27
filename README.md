# Shelly Victron Multiplus 2

¡Bienvenido al proyecto **Shelly Victron Multiplus 2**

Este proyecto te proporciona los archivos necesarios y las instrucciones para integrar tu dispositivo **Shelly PM 1 Plus** con el ecosistema **Victron Energy**. Su función principal es emular el comportamiento de un inversor **Victron Multiplus 2**, permitiéndote monitorizar y visualizar los datos de potencia y energía de tu Shelly directamente en tu sistema Victron (por ejemplo, a través de un dispositivo GX como el Cerbo GX).

---

## ¿Para qué sirve este script?

El Shelly PM 1 Plus es un medidor de energía muy versátil. Sin embargo, los sistemas Victron no lo reconocen de forma nativa como una fuente de energía o consumo compatible. Esta solución actúa como un "traductor" inteligente:

* Toma las lecturas en tiempo real de tu Shelly PM 1 Plus.
* Las convierte a un formato que un equipo Victron (como un Multiplus 2) puede entender.
* Presenta esta información en el sistema Victron como si fuera un Multiplus 2 real.

Esto es extremadamente útil para:

* **Si tienes un inversor que no tiene comunicacion y quieres integrarlo en el ecositema victron**
* **Monitorizar consumos o producción fotovoltaica** medida por tu Shelly directamente en tu entorno Victron.
* **Centralizar toda tu información energética** en tu GX Device (Cerbo GX, Color Control GX, etc.) para una visión completa.
* **Integrar equipos no Victron** en tu sistema Victron de forma sencilla y eficiente.

---

## Origen de los Proyectos Base y Agradecimientos

Esta solución se basa en la modificación de dos excelentes proyectos de código abierto ya existentes en GitHub. Un enorme agradecimiento a sus autores originales:

* **Dbus Shelly PVInverter:** [https://github.com/Halmand/dbus-shelly-1pm-and-pm1-Plus-pvinverter-multi-instance](https://github.com/Halmand/dbus-shelly-1pm-and-pm1-Plus-pvinverter-multi-instance)
* **Dbus Multiplus Emulator:** [https://github.com/mr-manuel/venus-os_dbus-multiplus-emulator](https://github.com/mr-manuel/venus-os_dbus-multiplus-emulator)

---

## Requisitos Previos

Para que esta solución funcione correctamente en tu sistema, necesitarás lo siguiente:

* El dispositivo **Shelly PM 1 Plus** configurado y accesible en tu red local, instalado en la salida de red de tu inversor NO victron.
* Un **dispositivo Victron GX** (como un Cerbo GX o Color Control GX) para visualizar los datos.

---

## Instalación y Uso

Sigue estos pasos detallados para poner en marcha el Shelly Victron Bridge en tu sistema. Este proceso implica descargar los proyectos base, y luego **reemplazar el código de los archivos originales** con tus versiones modificadas.

### 1. Clonar los Proyectos Originales

Copia y pega en tu SSH.

wget https://github.com/Halmand/dbus-shelly-1pm-and-pm1-Plus-pvinverter-multi-instance/archive/refs/heads/main.zip
unzip main.zip "dbus-shelly-1pm-and-pm1-Plus-pvinverter-multi-instance-main/*" -d /data
mv /data/dbus-shelly-1pm-and-pm1-Plus-pvinverter-multi-instance-main /data/dbus-shelly-1pm-pvinverter01
chmod a+x /data/dbus-shelly-1pm-pvinverter01/install.sh
/data/dbus-shelly-1pm-pvinverter01/install.sh
rm main.zip

y despues:

wget -O /tmp/download_dbus-multiplus-emulator.sh https://raw.githubusercontent.com/mr-manuel/venus-os_dbus-multiplus-emulator/master/download.sh

bash /tmp/download_dbus-multiplus-emulator.sh


#Seleccione la versión que desea instalar.#

(el primero)

y

Instalar el controlador como servicio:

bash /data/etc/dbus-multiplus-emulator/install.sh

REINICIAR.

### 2. Cambia archivo config.ini.

[DEFAULT]
AccessType     = OnPremise
SignOfLifeLog  = 5
Deviceinstance = 44
CustomName     = (nombre de tu inversor)
Phase          = L1
Position       = 1
PlusPmSupport  = True
LogLevel       = CRITICAL

[ONPREMISE]
Host           = (LA IP DE TU SHELLY)
Username       =
Password       =

### 3. Remplazar codigo pyton con winSCP.

Acceder a carpeta de carpeta /data/dbus-shelly-1pm-pvinverter01  y remplazar archivo (dbus-shelly-1pm-pvinverter.py) por el que os dejo.
Acceder a carpeta de carpeta  venus-os_dbus-multiplus-emulador/ emulador dbus-multiplus
/ y remplazar archivo (dbus-multiplus-emulator.py) por el que os dejo.

Reiniciar.

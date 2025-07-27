Instrucciones para Miguel Covatel:
Abre tu navegador web y ve a tu repositorio:
https://github.com/MiguelCovatel/shelly-victron-bridge

Haz clic en el archivo README.md en la lista de archivos.

Haz clic en el icono de lápiz (editar) en la esquina superior derecha del área de contenido del archivo.

Borra todo el contenido actual del README.md.

Copia el texto completo que aparece debajo de esta sección (desde --- hasta ---) y pégalo en el editor de GitHub.

Desplázate hacia abajo y haz clic en el botón verde "Commit changes". Puedes dejar el mensaje de commit por defecto o poner algo como "Finalized README.md with detailed instructions".

Shelly Victron Bridge
¡Bienvenido al proyecto Shelly Victron Bridge!

Este proyecto contiene un conjunto de scripts de Python modificados diseñados para integrar tu dispositivo Shelly PM 1 Plus con el ecosistema Victron Energy. Su función principal es emular el comportamiento de un inversor Victron Multiplus 2, permitiéndote monitorizar y visualizar los datos de potencia y energía de tu Shelly directamente en tu sistema Victron (por ejemplo, a través de un dispositivo GX como el Cerbo GX).

¿Para qué sirve este script?
El Shelly PM 1 Plus es un medidor de energía muy versátil. Sin embargo, los sistemas Victron no lo reconocen de forma nativa como una fuente de energía o consumo compatible. Este conjunto de scripts actúa como un "traductor" inteligente:

Toma las lecturas en tiempo real de tu Shelly PM 1 Plus.

Las convierte a un formato que un equipo Victron (como un Multiplus 2) puede entender.

Presenta esta información en el sistema Victron como si fuera un Multiplus 2 real.

Esto es increíblemente útil para:

Monitorizar consumos o producción fotovoltaica medida por tu Shelly directamente en tu entorno Victron.

Centralizar toda tu información energética en tu GX Device (Cerbo GX, Color Control GX, etc.) para una visión completa.

Integrar equipos no Victron en tu sistema Victron de forma sencilla y eficiente.

Origen de los Scripts y Agradecimientos
Este proyecto es una modificación y adaptación de dos excelentes proyectos de código abierto ya existentes en GitHub. Se han unido y ajustado para funcionar específicamente con el Shelly PM 1 Plus y emular un Multiplus 2 en el entorno Victron.

Dbus Shelly PVInverter: https://github.com/Halmand/dbus-shelly-1pm-and-pm1-Plus-pvinverter-multi-instance

Dbus Multiplus Emulator: https://github.com/mr-manuel/venus-os_dbus-multiplus-emulator

Un enorme agradecimiento a Halmand y a mr-manuel por sus contribuciones originales. Su trabajo ha sido fundamental para hacer posible esta integración.

Requisitos Previos
Para que este conjunto de scripts funcione correctamente en tu sistema, necesitarás lo siguiente:

Python 3.x instalado en tu sistema (se recomienda Python 3.8 o superior).

Un dispositivo Shelly PM 1 Plus configurado y accesible en tu red local.

Un dispositivo Victron GX (como un Cerbo GX o Color Control GX) para visualizar los datos, o un sistema Victron compatible con la emulación de servicios DBus.

Instalación y Uso
Sigue estos pasos detallados para poner en marcha el Shelly Victron Bridge en tu sistema. Hemos empaquetado todas las modificaciones necesarias para que solo tengas que clonar este repositorio.

1. Clonar el Repositorio
Abre tu terminal (Git Bash en Windows, o la aplicación Terminal en macOS/Linux) y ejecuta el siguiente comando para descargar todos los archivos necesarios:

Bash

git clone https://github.com/MiguelCovatel/shelly-victron-bridge.git
2. Navegar al Directorio del Proyecto
Una vez que el repositorio se haya descargado, entra en la carpeta del proyecto usando la terminal:

Bash

cd shelly-victron-bridge
3. Instalar Dependencias de Python
Es crucial instalar todas las librerías de Python adicionales que los scripts puedan necesitar. Este repositorio incluye un archivo requirements.txt con todas ellas. Instálalas ejecutando:

Bash

pip install -r requirements.txt
4. Configuración de los Scripts
Ambos scripts necesitan una configuración mínima para funcionar correctamente con tu Shelly y tu sistema Victron.

Abre el archivo dbus-shelly-1pm-and-pm1-Plus-pvinverter.py (o el nombre que le hayas dado a tu script Shelly modificado) con un editor de texto (como Notepad++, VS Code, Sublime Text, etc.).

Localiza la variable de configuración para la dirección IP de tu Shelly PM 1 Plus y cámbiala por la IP real de tu dispositivo en tu red local.

Verifica cualquier otro parámetro que hayas modificado o que necesite ajustarse a tu configuración específica del Shelly.

Abre el archivo dbus-multiplus-emulator.py (o el nombre que le hayas dado a tu script emulador de Multiplus modificado).

Revisa la configuración de los puertos de comunicación entre este script y el script del Shelly. Normalmente, ambos se comunicarán usando localhost y un puerto específico. Asegúrate de que los puertos configurados en ambos scripts coincidan si has realizado cambios.

Confirma que el puerto en el que el emulador escucha para el Victron GX no entre en conflicto con otros servicios en tu sistema (el puerto 502 es común para Modbus/TCP, pero verifica tu configuración).

5. Ejecutar los Scripts
Para que la emulación funcione y los datos de tu Shelly lleguen al sistema Victron, ambos scripts deben estar ejecutándose de forma simultánea. Se recomienda iniciarlos en el orden indicado.

5.1. Iniciar el Script del Shelly (Traductor de Datos)
Este script es el que se encarga de comunicarse directamente con tu Shelly PM 1 Plus y procesar sus datos. Ejecútalo en tu terminal:

Bash

python dbus-shelly-1pm-and-pm1-Plus-pvinverter.py
(Si le has cambiado el nombre a este archivo, usa el nombre correcto en el comando.)

Asegúrate de que este script se inicie sin errores y esté mostrando que lee datos de tu Shelly. Puedes dejar esta ventana de la terminal abierta o ejecutarlo en segundo plano si sabes cómo (por ejemplo, con nohup o screen en Linux).

5.2. Iniciar el Script Emulador del Multiplus (Victron Bridge)
Una vez que el script del Shelly esté funcionando y enviando datos, inicia el emulador del Multiplus. Este script se conectará al script del Shelly y empezará a emular el dispositivo en tu sistema Victron.

Bash

python dbus-multiplus-emulator.py
(Si le has cambiado el nombre a este archivo, usa el nombre correcto en el comando.)

De forma similar, puedes dejar esta ventana de la terminal abierta.

6. Verificar la Emulación en Victron OS
Una vez que ambos scripts estén ejecutándose, deberías poder ver el dispositivo emulado en tu sistema Victron:

En tu GX Device (Cerbo GX, Color Control GX, etc.), accede a la interfaz de usuario.

Navega a la sección de dispositivos o servicios.

Deberías ver un nuevo dispositivo aparecer, identificado como un Multiplus 2 (o similar, dependiendo de la configuración del emulador), reportando los datos de tu Shelly PM 1 Plus en tiempo real.

Contribución y Soporte
Si encuentras algún problema, tienes ideas para mejoras o quieres contribuir con código (¡tus propias modificaciones!), no dudes en abrir un "issue" (un informe de problema) o enviar un "pull request" (una propuesta de cambio de código) en este repositorio. ¡Toda ayuda es bienvenida!

Una vez que hayas pegado esto y guardado los cambios en GitHub, tu README.md estará listo.

¡El último paso crucial y manual para ti: Asegúrate de que tus versiones modificadas de los archivos dbus-shelly-1pm-and-pm1-Plus-pvinverter.py y dbus-multiplus-emulator.py (y cualquier otro archivo necesario como requirements.txt) estén subidos a tu repositorio de GitHub. Si aún no los has subido, házmelo saber y te guío para hacerlo directamente desde la interfaz web, es muy sencillo.

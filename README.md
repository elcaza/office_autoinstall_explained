# Office Autoinstall & Hack Explained

Este repositorio pretende mostrar la forma en que funciona la instalación automática de office y su posterior activación. 

+ Este script permite instalar de forma automática:
	+ `Office 2016 Pro Plus x64`
	+ `Office 2016 Pro Plus x32`
	+ `Office 365 Pro Plus x64`
	+ `Office 365 Pro Plus x32`
	+ Otras versiones de office (P. Ej. Enterprise)
	+ Todo en cualquier lenguaje
+ Un script con el que podemos observar que es posible realizar una activación del producto.
	+ **ADVERTENCIA**
		+ Este material es meramente educativo y no se incentiva de ninguna manera a el uso de la pirateria.
		+ Como alternativa recomendamos:
			+ La compra de licencias originales
			+ Obtener licencias gratuitas para estudiantes
			+ Usar software libre

# Instalación Automatizada de Office
La mayor parte de las aplicaciones instalables en windows se pueden configurar a través de archivos `.xml`. Por lo anterior, es posible correr el archivo de instalación de office `setup.exe` y darle como parámetro el `archivo_de_configuracion.xml` para lograr una instalación automatizada.

## Contenido de la carpeta deploy_office

Todo lo necesario para lanzar la instalación de office de una manera automatizada, se encuentra dentro de la carpeta `deploy_office`. 

Dentro de ella los siguientes archivos:
+ `config_sample.xml` (Archivo ejemplo de configuración)
+ `EULA`  (Los términos de licencia)
+ `setup.exe` Exe que se encarga de realizar la instalación. (Office Deployment Tool)
+ `configuration_*.xml` (Archivos de configuracion de cada version en especifico)
	+ Office365_x64
	+ Office365_x86
	+ Office Enterprise
	+ Office 2016 Pro Plus
+ `install_config.cmd` (Archivo que lanza la instalación)
	+ Office365_x64
	+ Office365_x86
	+ Office Enterprise
	+ Office 2016 Pro Plus

## ¿Cómo se configura el archivo .xml?

## ¿Cómo se configura el archivo .cmd?

# ¿Validación de licencia? ¿Crack Office?

Es posible validar la licencia mediante un simple script. 

## Password
`activate`

# Referencias / Agradecimientos
+ http://MSGuides.com
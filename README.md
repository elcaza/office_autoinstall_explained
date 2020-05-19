# Office Autoinstall & Hack Explained

Este repositorio pretende mostrar la forma en que funciona la instalación automática de office y su posterior activación. 

+ Este script permite instalar de forma automática:
	+ `Office 2016 Pro Plus x64`
	+ `Office 2016 Pro Plus x32`
	+ `Office 365 Pro Plus x64`
	+ `Office 365 Pro Plus x32`
	+ Otras versiones de office (P. Ej. Enterprise)
	+ Todo en cualquier lenguaje
+ Se adjunta un script con el que podemos observar que es posible realizar una activación del producto.

## ADVERTENCIA
+ Este material es meramente educativo y no se incentiva de ninguna manera a el uso de la pirateria.
+ Como alternativa recomendamos:
	+ La compra de licencias originales
	+ Obtener licencias gratuitas para estudiantes
	+ Usar software libre


## Este contenido también se encuentra disponible en:
+ [Medium: Instalación automática de Office con Office Deployment Tool](https://medium.com/@elcaza/instalaci%C3%B3n-autom%C3%A1tica-de-office-con-office-deployment-tool-36d352dcd2d0)


# Instalación Automatizada de Office

##### * (Si usted únicamente quiere realizar la instalación salte hasta el punto *"3) ¿Cómo comenzar la instalación automatizada?"*)

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

## 1) ¿Cómo se configura el archivo .xml?
Nosotros ya contamos diversos archivos de configuración `.xml` por defecto. Sin embargo, estos pueden ser modificados para que se acoplen completamente a nuestras necesidades. Para ello a continuación explicaremos las partes del archivo `config_sample.xml`

```xml
<Configuration>

  <Add OfficeClientEdition="64" Channel="Monthly">
    <Product ID="O365ProPlusRetail">
      <Language ID="es-es" />
      <ExcludeApp ID="Access" />
      <ExcludeApp ID="InfoPath" />
      <ExcludeApp ID="Lync" />
      <ExcludeApp ID="SharePointDesigner" />
      <ExcludeApp ID="Visio" />
      <ExcludeApp ID="Skype" />
      <ExcludeApp ID="Skypeforbusiness" />
      <ExcludeApp ID="Groove" />
    </Product>
    <Product ID="VisioProRetail">
      <Language ID="es-es" />
    </Product>
  </Add>
</Configuration>
```

Como podemos observar el archivo de configuración únicamente consta de un par de etiquetas en las que destacan:
+ Add OfficeClientEdition
	+ Aquí podemos elegir los valores `32` o `64` dependiendo si queremos hacer la instalación de 32bits o 64bits
+ Product ID
	+ Aquí podemos seleccionar el producto a instalar
		+ `O365ProPlusRetail` (Office 365 ProPlus)
		+ `ProPlusRetail` (Office 2016 ProPlus)
	+ Language ID
		+ `en-us`
		+ `es-es`
		+ <a href="https://docs.microsoft.com/en-us/deployoffice/overview-deploying-languages-microsoft-365-apps" target=_blank>Puede ver todos los códigos de lenguajes aquí</a>
	+ ExcludeApp ID
		+ Aplicaciones a excluir. No serán instaladas
	+ Product ID
		+ Aplicaciones extras que se incluirán

## 2) ¿Cómo se configura el archivo .cmd?
Ya que nuestro `setup.exe` depende de un archivo de configuración, este debe correrse a través de la consola, ya sea mediante `cmd` ó `powershell`.
Para facilitar esto nosotros podemos crear un archivo `install_config.cmd`.
* Nuevamente, nosotros ya tenemos un par de archivos preconfigurados
	+ 

¿Qué hay dentro de este archivo?

```bat
@echo off
cd /d %~dp0
setup.exe /configure config_sample.xml
pause
```

Básicamente este pequeño script lo que realiza es: 
1. Llamar a `setup.exe` 
2. Dar la bandera `/configure` que indica que le darás un archivo de configuración 
3. Indicar el nombre del archivo de configuración `install_config.cmd`

Si lo queremos modificar solamente cambiamos el punto *"número 3"* especificando el nombre del archivo de configuración que se tendrá.
* Si creamos un archivo desde cero, hay que recordar guardarlo con extensión *.bat* o *.cmd*

## 3) ¿Cómo comenzar la instalación automatizada?

Para comenzar una instalación automatizada únicamente debemos dirigirnos hacia la carpeta `deploy_office` y hacer doble click en el `install_config.cmd` deseado.
+ Como vimos anteriormente contamos con distintas configuraciones dependiendo de nuestras necesidades
	+ Office365_x64
	+ Office365_x64
	+ Una customizada, en caso de que la haya creado
+ Si tiene algún problema durante este proceso consulte la sección de "Problemas / Soluciones"

Una vez ejecutado nuestro `install` aparecerá la tipica pantalla de instalación de Office y tras varios minutos se habrá completado la instalación. El tiempo que tarde dependerá principalmente de su velocidad de descarga de internet. 

Una vez que eso haya finalizado tendremos disponible nuestro Office sin licencia.

# ¿Validación de licencia? ¿Crack de Office?

Es posible validar la licencia mediante un simple script. Esto ocurre gracias al Servicio de Administración de Claves KMS (Key Management Service). Este es un servicio legitimo de Windows y está diseñado para que las organizaciones activen sus productos por volumen. 

Es decir, la organización contrata un montón de licencias que serán utilizadas por toda su empresa, a diferencia del licenciamiento estándar de Microsoft, estas no se anclan a una máquina en especifico, sino a la cuenta de una empresa. Por lo anterior, para este tipo de activación se debe contemplar lo siguiente:

1. La empresa debe montar su propio servidor KMS.
2. Requieren un mínimo de activaciones para funcionar. Es decir, para hacer válidas las activaciones varia el número MÍNIMO de clientes que utilicen la licencia. De otro modo está sería inválida.
3. El office solamente se activa de manera temporal, durante 180 días, y su licencia debe ser renovada antes de que termine el plazo.

Para las organizaciones lo anterior no representa problema alguno, pues suelen cumplir con estos requerimientos. Sin embargo, este mismo modelo de negocio es el que permite se pueda *"engañar"* a Windows para hacerle creer que está bajo un licenciamiento por volumen.

Debido a que cualquier persona puede generar su propio servidor KMS este puede ser modificarlo para que se apruebe cada licencia. Para esto solamente se requiere lo siguiente:

1. Montar tu propio servidor KMS
2. Hacer que tus computadoras consulten al TU SERVIDOR KMS
3. Hacer que cada determinado tiempo se renueve la licencia mediante tu propio servidor KMS

Para esto ya existe un script proporcionado por [https://msguides.com/](https://msguides.com/) el cual se conecta con su propio Servidor KMS.

# ¿Es seguro utilizar activadores KMS?
Como vimos anteriormente el problema no es usar activadores KMS, pues estos son proporcionados por Microsoft a las empresas que pagan licenciamiento por volumen. El verdadero problema es llegar a la pirateria de estos servicios, pues es ahí donde nos podemos encontrar con software malicioso.

Sin embargo, el script activador que proporciona [msguides](https://msguides.com/) parece bastante transpartente. El código con comentarios del activador KMS se encuentra en la sección **Anexo Script con comentarios**.

## ¿Cómo utilizar este script?

Para utilizar este script es necesario descomprimir el archivo `activate.zip`. Este archivo está protegido por contraseña porque de otro modo Windows Defender lo detecta como amenaza al descargarlo. 

+ Asegúrese de que Windows Defender esté desactivado. (Consultar la sección: "*¿Cómo apagar Windows Defender?"*)
+ El password es el siguiente:

##### Password: `activate`

Una vez descomprimido el archivo solamente tenemos que dirigirnos a la carpeta `activate` y *ejecutar como administrador* el archivo `activate.cmd`
1. Click derecho, ejecutar como administrador
1. Nos abrirá una consola 
1. Presionaremos enter una vez. Esto tardará un poco, en caso de ser necesario presionaremos enter de nuevo.
1. Debe aparecernos: `<Product activation successful>`
	+ De no ser así es probable que no haya corrido el script con privilegios de administrador
1. Luego de ello nos preguntará si queremos visitar el blog del autor de este script
	+ responderemos `y` ó `n`
	+ Justo después de elegir nuestra respuesta se cerrará la ventana
1. Y así habremos comprobado que efectivamente el office ha quedado activado

#### Dato curioso: Tu office se transforma a Office 2016 Pro Plus.

OUTPUT de la activación
```
============================================================================
Activating your Office...
============================================================================


The connection to my KMS server failed! Trying to connect to another one...
Please wait...


============================================================================


<Product activation successful>

============================================================================

#My official blog: MSGuides.com

#How it works: bit.ly/kms-server

#Please feel free to contact me at msguides.com@gmail.com if you have any questions or concerns.

#Please consider supporting this project: donate.msguides.com
#Your support is helping me keep my servers running everyday!

============================================================================
Would you like to visit my blog [Y,N]?
```

# Problemas / Soluciones
+ Windows detecta activate como virus
	+ Lo que sucede es que windows detecta el script como un activador de Office y por supuesto lo bloquea. De hecho, en la descripción de Windows Defender menciona.
		+ HackTool:BAT/AutoKMS
		+ This program has potentially unwanted behavior
	+ Y claro, ellos no desean que tú tengas sus productos sin pagar por ellos
	+ Basta con deshabilitar Windows Defender durante la activación.
	+ Si el problema persiste desactiva tu antivirus 
+ Pantalla azul de bloqueo
	+ Al igual que `Windows Defender - Real Time Protection` es necesario desactivar `App & Browser Control - Check apps and files` como se menciona en la sección de `¿Cómo apagar Windows Defender?`
+ ¡No sé la contraseña del zip!
	+ Bro, ese no es un problema. La contraseña es `activate` como se mencionó en el post.

# Anexo Script KMS con comentarios
```cmd
:: @echo off  => define que la terminal no nos devuelva las salidas propias de la terminal
:: Es muy usado en los scripts para evitar la salida de información basura
@echo off

:: title => Crea un título para la ventana
title _ Permanently Activate Office 365 ProPlus for FREE => MSGuides . com

:: & => Es utilizado para concatenar comandos. Usado cuando escribes en una solo línea. 
:: cls => Hace un limpiado de la pantalla para que no muestre lo escritor anteriormente
&cls

:: Pone los titulos que nosotros vemos
&echo ============================================================================
&echo #Project: Activating Microsoft software products for FREE without software
&echo ============================================================================
&echo.
&echo #Supported products: Office 365 ProPlus (x86-x64)
&echo.
&echo.

:: & => Es utilizado para concatenar comandos. Usado cuando escribes en una solo línea. 
:: ( ) => Es usado para agrupar una secuencia de comandos
&
(
    :: Condicion if que checa la existencia de un archivo .vbs (Visual Basic Script)
    :: En caso de que exista entramos a la carpeta 
    if exist "%ProgramFiles%\Microsoft Office\Office16\ospp.vbs" 
        cd /d "%ProgramFiles%\Microsoft Office\Office16"
)
&(  
    :: Condicion if que checa la existencia de un archivo .vbs (Visual Basic Script)
    :: En caso de que exista entramos a la carpeta 
    if exist "%ProgramFiles(x86)%\Microsoft Office\Office16\ospp.vbs" 
        cd /d "%ProgramFiles(x86)%\Microsoft Office\Office16"
)
&(
    for /f %%x in ('dir /b ..\root\Licenses16\proplusvl_kms*.xrm-ms') 
        do cscript ospp.vbs /inslic:"..\root\Licenses16\%%x" >nul
)
&(
    for /f %%x in ('dir /b ..\root\Licenses16\proplusvl_mak*.xrm-ms') 
        do cscript ospp.vbs /inslic:"..\root\Licenses16\%%x" >nul
)

:: Mensajes que nosotros vemos echo. es un salto de linea
&echo.
&echo ============================================================================
&echo Activating your Office...

:: Esta secuenta de comandos settea las claves de los productos y configura varios servidores KMS para corroborar la validez de la clave

&cscript //nologo ospp.vbs /unpkey:WFG99 >nul
&cscript //nologo ospp.vbs /unpkey:DRTFM >nul
&cscript //nologo ospp.vbs /unpkey:BTDRB >nul
&cscript //nologo ospp.vbs /inpkey:XQNVK-8JYDB-WJ9W3-YJ8YR-WFG99 >nul
&set i=1:server
    if %i%==1 set KMS_Sev=kms7.MSGuides.com
    if %i%==2 set KMS_Sev=kms8.MSGuides.com
    if %i%==3 set KMS_Sev=kms9.MSGuides.com
    if %i%==4 goto notsupported
    cscript //nologo ospp.vbs /sethst:%KMS_Sev% >nul

:: Mensajes que nosotros vemos echo. es un salto de linea
&echo ============================================================================
&echo.
&echo.

:: Realiza la activación

cscript //nologo ospp.vbs /act | find /i "successful" 
&

:: Mensajes que nosotros vemos echo. es un salto de linea
& (echo.
&echo ============================================================================
&echo.
&echo #My official blog: MSGuides.com
&echo.
&echo #How it works: bit.ly/kms-server
&echo.
&echo #Please feel free to contact me at msguides.com@gmail.com if you have any questions or concerns.
&echo.
&echo #Please consider supporting this project: donate.msguides.com
&echo #Your support is helping me keep my servers running everyday!
&echo.
&echo ============================================================================

:: Realiza una pregunta para saber si quieres mirar su blog

&choice /n /c YN /m "Would you like to visit my blog [Y,N]?" 
& if errorlevel 2 exit) || (echo The connection to my KMS server failed! Trying to connect to another one... 
:: Mensajes que nosotros vemos echo. es un salto de linea
& echo Please wait... 
& echo. 
& echo. 

& set /a i+=1 
& goto server)
explorer "http://MSGuides.com"
&goto halt

:notsupported

:: Mensajes que nosotros vemos echo. es un salto de linea
echo.
&echo ============================================================================
&echo Sorry! Your version is not supported.
&echo Please try installing the latest version here: bit.ly/odt2k16

:halt
pause >nul
```
# ¿Cómo apagar Windows Defender?

## 1) Abrimos Windows Security 
<img src="./img/1_entrar_wd.png" alt="Paso_1" width="50%"/>

## 2) Dentro del menú Virus & Threat Protection seleccionamos *"Manage settings"*
<img src="./img/2_virus_and_protection_manage_settings.png" alt="Paso_2" width="50%"/>

## 3) Nos aseguramos de dejarlo en modo apagado/off
<img src="./img/3_off_realtime.png" alt="Paso_3" width="50%"/>

## 3) Dentro de App & browser control seleccionamos *"Off"* para "Check apps and files" 
<img src="./img/4_off_app_and_files.png" alt="Paso_4" width="50%" />

## 5) Listo. Podemos realizar la prueba del script para ver que efectivamente funciona.

## 6) Luego de que hayas comprobado el funcionamiento, ¡Activa Windows Defender nuevamente!

# Referencias / Agradecimientos

+ [MSGuides](http://MSGuides.com)
+ [Office Deployment Tool](http://aka.ms/ODT)
+ [Office Deployment Tool configuration options](https://docs.microsoft.com/en-us/deployoffice/office-deployment-tool-configuration-options)
+ [Languages ID Office](https://docs.microsoft.com/en-us/deployoffice/overview-deploying-languages-microsoft-365-apps)
+ [List of Product IDs which are supported by the Office Deployment Tool for Click-to-Run](https://docs.microsoft.com/en-us/office365/troubleshoot/installation/product-ids-supported-office-deployment-click-to-run)
+ [¿Cómo funciona KMS?](https://stackoverflow.com/questions/44243669/need-explanation-on-how-this-windows-cmd-batch-script-accomplishes-the-task-of-a)
+ [Entendiendo KMS](https://docs.microsoft.com/en-us/previous-versions/tn-archive/ff793434(v=technet.10)?redirectedfrom=MSDN)
+ [¿Windows sabe sobre los servicios de activación piratas?](https://www.quora.com/Does-Microsoft-know-that-people-are-using-KMOspico-to-activate-Windows-or-Microsoft-office-Microsoft-Office-Toll-Free-Support-Number-1-800-9824-735)
+ [¿Es segura y válida una activación mediante KMS?](https://superuser.com/questions/1383281/is-kms-digital-online-activation-suite-safe-valid-and-genuine-to-activate-window)

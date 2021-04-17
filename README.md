# ControlGPIO-ESP-Thingsboard
Guía para operar los GPIO del NodeMCU con Thingsboard
# ControlGPIO-ESP-Thingsboard

#Guía para operar los GPIO del NodeMCU con Thingsboard

#### Thingsboard es una plataforma para monitorear y controlar dispositivos, enfocado a IoT y es de código abierto, lo que significa que podemos controlar la cantidad de dispositivos que nosotros deseamos sin la necesidad de pagar por una licencia, lo anterior quiere decir también que se puede usar de manera comercial, aplicado a la industria.

#### Entre las cosas que se pueden hacer con Thingsboard son:
1. Crear dispositivos de provisión y control
2. Recopilar y visualizar datos de dispositivos
3. Analizar datos de los dispositivos y disparar alarmas
4. Entregar datos de los dispositivos a otros sistemas
5. Proporcionar la nube IoT lista para usar o ser la solución en las instalaciones que habilitará la infraestructura del lado del servidor para sus aplicaciones de IoT.

#### ThingsBoard es escalable pues es una plataforma escalable horizontalmente y compilación utilizando tecnologías líderes de código abierto, tolerante a errores  pues  no hay punto único de fallo ya que  cada nodo en el clúster es idéntico,es personalizable pues permite agregar nueva funcionalidad es fácil con widgets personalizables, motor de reglas y sistema de complementos, es s duradero  y es robusto y eficiente  pues  el nodo de servidor único puede manejar decenas o incluso cientos de miles de dispositivos según el caso de uso (un cluster ThingsBoard puede manejar millones de dispositivos). Asimismo también puede conectar dispositivos existentes a la plataforma usando ThingsBoard Gateway .

#### ThingsBoard le permite enviar llamadas de procedimiento remoto (RPC) desde aplicaciones del servidor a dispositivos y viceversa. Básicamente, esta característica le permite enviar comandos a dispositivos y recibir resultados de ejecución de comandos. Similarmente, puede ejecutar la solicitud desde el dispositivo, aplicar algunos cálculos u otra lógica del lado del servidor en el back-end y enviar la respuesta de regreso al dispositivo. Esta guía cubre las capacidades de ThingsBoard RPC. Después de leer esta guía, se familiarizará con los siguientes temas:

- Tipos de llamdas RPC
- Casos de usos de RPC básicos
- La API RPC del lado del cliente y del lado del servidor
- Widgets RPC

## A continuación se hará una aplicación para el control de GPIO del ESP8266 como módulo (NodeMCU) con ayuda de Thingsboard, se verá el control con ayuda de dos Led's conectados a dos pines del ESP.

### Dispositivo RPC API

#### ThingsBoard está diseñado para ejecutarse y utilizarse en la mayoría del hardware, desde Raspberry PI local hasta potentes servidores en la nube. Las formas de configurar un cluster de ThingsBoard soporta los  siguientes sistemas operativos:

- **Windows** : instale el clúster Thingboard en cualquier máquina preexistente que ejecute Windows.
- **Linux (Ubuntu y CentOS)** : instala el clúster Thingboard en cualquier máquina preexistente que ejecute Linux.
- **Raspberry Pi 3 Modelo B (Raspbian Jessie)** : instala el servidor Cassandra y Thingboard en una Raspberry Pi 3 modelo B.
- **Docker (Linux o Mac OS)** : instala un clúster ThingsBoard de un nodo en tu máquina Linux o Mac OS para su desarrollo y prueba.
- **Docker (Windows)** : instala un clúster ThingsBoard de un nodo en tu máquina con Windows para su desarrollo y prueba.
- **Instalación de AWC EC2 utilizando AMI** : instale un clúster ThingsBoard de nodo único con AWI AMI público.

### Se puede usar la versión Demo si la intención es solo hacer pequeñas pruebas, se puede consultar la documentación aquí:
[**Versión Demo Thingsboard**](https://translate.googleusercontent.com/translate_c?depth=2&hl=es&rurl=translate.google.com&sl=en&sp=nmt4&tl=es&u=https://thingsboard.io/docs/user-guide/live-demo&usg=ALkJrhhXPqQaNJiSSHlKJMZg8S-Zfrtszw)

# Control de 2 LED's (ejemplo):

#### En este ejemplo se usará el NodeMCU con el código correspondiente en el IDE de Arduino, se conectará al servidor de Thingsboard a través de MQTT y detectará los comandos RPC.

#### El estado del GPIO y el Widget para el conrol de los GPIO's se visualizarán en el mismo panel personalizable.

#### Identificación de pines de la Raspberry Pi

![]()

### Materiales:

**1. NodeMCU-ESP8266 : se usará el módulo NodeMCU.**

**2. 2 Led's**

**3. 2 Resistencia de 1k**

**4. 2 cables de puente hembra a macho.**

**5. Placa de pruebas (protoboard).

#### La aplicación consiste en un único código en el IDE de Arduino que está bien documentado. Es necesario modificar la constante THINGSBOARD_HOST para que coincida con su dirección IP de instalación del servidor ThingsBoard o nombre de host. Si se utiliza la versión Demo, el HOST será: “demo.thingsboard.io”.

#### La constante ACCESS_TOKEN corresponde al dispositivo que creamos en Thingsboard. Si se usa un servidor de demostración en vivo , obtenga el token de acceso para el “ESP8266 Demo Divice”.

### Código para control de dos GPIO's.

#### El código para el control de dos GPIO's del NodeMCU se encuentra en la carpeta **SRC**, el siguiente hipervínculo nos redirige al código:

[**Código para un LED**](https://github.com/jwilliamsee/ControlGPIO-ESP-Thingsboard/blob/main/SRC/Codigo-ESP-Thingsboard)

#### El diagrama es el siguiente:

![](https://github.com/jwilliamsee/ControlGPIO-ESP-Thingsboard/blob/main/Imagenes/GPIO-Conexion.png?raw=true)

#### Se hicieron las conexiones físicamente en el NodeMCU:

![](https://github)

#### A continuación debemos instalar Nmap, nos ayudará a escanear las ip que tenemos conectados en nuestra red.

**NOTA: El procedimiento que aquí se describe es en Linux, para entrar en Windows, en el video de instalación de Raspbian se describe como.**

##### Información a detalle sobre el proceso que a continuación se muestra, se encuentra en el siguiente vínculo:

[**Escaneo de IP's**](https://itsfoss.com/how-to-find-what-devices-are-connected-to-network-in-ubuntu/)

##### Usando la terminal instaleremos Nmap, nos ayudará a encontrar IP's de los equipos conectados a nuestra red, con el siguiente comando:

	sudo apt install nmap

##### 1. Debemos conocer la IP de nuestra red para poder escanear y llegar hasta la IP de la Raspberry. En el vínculo arriba mencionado se describe como.

##### 2. Se escribe en la terminal el siguiente comando: 

	nmap -sP 192.168.1.* 

##### esa IP que ahí aparece es la de nuestra red, para cada caso será diferente, previamente ya debemos conocerlo y el último número se debe omitir y en su lugar escribir el símbolo de asterísco, para que nos muestre en forma de lista los equipos conectados. Por ejemplo en la IP anterior sería: 192.168.1.1 y el último 1 se sustituyó por un asterísco.

##### Con la IP encontrada de la Raspberry, entraremos a la parte gráfica de nuestra Raspberry.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/ipRaspberry.png?raw=true)

##### 3. Ahora que ya conocemos la IP de nuestra Raspberry podemos entrar a la terminal de la misma, con ayuda del siguiente comando:

	ssh pi@192.168.0.9 -X

##### Y entraremos a nuestra Raspberry, un poco diferente a la forma de entrar en Windows pero prácticamente es lo mismo.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/DentroDeRaspberry.png?raw=true)

##### En la letra A señala la forma de entrar a nuestra terminal de la Raspberry.

##### En la letra B señala un aviso que nos aparece cuando nos conectamos por primera vez la Raspberry y nos pregunta si le damos permiso o si queremos continuar con la conexión, escribimos "yes".

##### En la letra C nos indica el momento donde nos pide la contraseña que usamos en Linux de nuestro equipo, para darle permiso a la conexión.

##### Finalmente en la letra D nos señala que nos hemos conectado y estamos dentro de la Raspberry.

##### Para salir de la terminal de la Raspberry, simplemente escribimos "exit"y será todo.

##### 4. Ya que hemos entrado y después de haber instalado el intérprete Thonny en la Raspberry, abrimos con el comando:

	thonny &

##### Pegamos nuestro código en la interfaz de Thonny haciendo las modificaciones correspondientes del HOST y del TOKEN.

##### El HOST es el servidor al que tenemos acceso de Thingsboard, por ejemplo en la versión de prueba o Demo, el HOST es "demo.thingsboard.io" y el TOKEN dependerá del dispositivo creado, eso se verá a continuación.

##### En caso de haber instalado Thingsboard de manera local, el acceso se dará con los siguientes datos:

	login: tenant@thingsboard.org
	password: tenant

## Visualización de datos en Thingsboard

##### 1. Entramos a Thingsboard. según el caso que usemos (Demo o local).

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/LoginThingsboard.png?raw=true)

##### 2. Ya que nos encontramos dentro de THingsboard, nos dirigimos a dispositivos en el menú al lado izquierdo.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things1.png?raw=true)

##### 3. Nos dirigimos al botón rojo para agregar un nuevo dispositivo, en la esquina inferior derecha.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things2.png?raw=true)

##### 4. Escribimos un nombre y escogemos que tipo de dispositivo estamos creando.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things3.png?raw=true)

##### 5. Buscamos nuestro dispositvo que creamos y accedemos para copiar nuestras credenciales, posteriormente serán usadas.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things4.png?raw=true)


![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things5.png?raw=true)

##### 6. Salimos al menú principal y nos dirigimos a Dashboard, crearemos uno con el mismo nombre de nuestro dispositivo o cualquier otro nombre para poder identificarlo.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things6.png?raw=true)

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things7.png?raw=true)

##### 7. Escribimos los datos correspondientes.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things8.png?raw=true)

##### 8. Salimos al menú principal y nos dirigimos a las librerías de Widgets.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things9.png?raw=true)

##### 9. En las librerías, buscamos una que se llama "GPIO widgets".

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things10.png?raw=true)

##### Lo anterior, para visualizar antes de agregar un nuevo Widget a nuestro Dashboard, cuando hemos identificado que Widget ocupamos, en este caso es el de la Raspberry, vamos al menú principal y nos vamos al Dashboard que creamos antes para agregar el nuevo widget.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things11.png?raw=true)

##### 10. Accedemos y le damos en el botón rojo del signo (+) para agregar un widget, en caso de que tengamos el widget en nuestro equipo de manera local y si no hemos descargado nada, simplemente le damos en el recuadro del centro par aescoger nuestro widget.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things12.png?raw=true)

##### 11. Después de haber seleccionado el recuadro "ADD NEW WIDGET", seleccionamos los datos correspondientes.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things13.png?raw=true)

##### 12. Después de haber seleccionado el Widget corespondiente, escribimos los datos de aacuerdo a nuestro Dashboard y Dispositivo con la intención de no confundirnos en los nombres o evitar errores se escribe el mismo o similar.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things14.png?raw=true)

##### 13. Al crear uno nuevo, llenamos el siguiente recuadro, para finalmente agregar nuestro nuevo panel de control.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things15.png?raw=true)

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things16.png?raw=true)

##### Finalmente tenemos nuestro panel de control agregado y ahí aparece que se encuentra off line, debido a que no tenemos conectado nuestra Raspbeery, cuando se logren conectar ambos, al momento de hacer pruebas, dejará de estar en modo off line.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things17.png?raw=true)

#### Ahora repetimos prácticamente los mismos pasos para agregar el panel de visualización.

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things18.png?raw=true)

##### Finalmente tendremos en nuestro Dashboard los dos paneles agregados, el de visualización y el de control

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things19.png?raw=true)

#### Ahora lo que sigue, es conectar nuestra raspberry adecuadamente, y "correr" el programa para después ir a Thingsboard y en la parte de Dashboard ver como de estar "off line" pasa a estar en modo online pero sin indicarnos, simplemente lo sabemos porque el "off line" desaparece y es ahí cuando podemos hacer uso de los GPIO y ver como se acivan los leds y desactivan, según lo que indicamos en el panel, es necesario actualizar la página en Thingsboard para poder establecer conexión y que desaparezca el "off line".

##### Si desea no instalar Thonny, simplemente como se mencionó antes, escribir en la terminal lo siguiente:

	python GPIO.py


![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things20.png?raw=true)


------------

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/RaspConectada.png?raw=true)


------------

![](https://github.com/jwilliamsee/ControlLedThingsboardRasp/blob/main/imagenes/Things21.png?raw=true)


------------

#### Vínculo de un video donde se ve el funcionamiento:

[**Funcionamiento**](https://youtu.be/3xD2gJ1fan0)

#### En este ejemplo se agregaron más leds pero no todos los GPIO's, sólo algunos, el código sufrirá modificaciones, según lo que desea hacer cada usuario, partiendo de este ejemplo, será fácil entender como funciona.

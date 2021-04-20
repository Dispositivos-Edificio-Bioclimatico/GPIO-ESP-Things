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

**1. ESP-8266 : se usará el módulo NodeMCU.**

**2. 2 Led's**

**3. 2 Resistencia de 1k**

**4. 2 cables de puente hembra a macho.**

**5. Placa de pruebas (protoboard).**

#### La aplicación consiste en un único código en el IDE de Arduino que está bien documentado. Es necesario modificar la constante THINGSBOARD_HOST para que coincida con su dirección IP de instalación del servidor ThingsBoard o nombre de host. Si se utiliza la versión Demo, el HOST será: “demo.thingsboard.io”.

#### La constante ACCESS_TOKEN corresponde al dispositivo que creamos en Thingsboard. Si se usa un servidor de demostración en vivo , obtenga el token de acceso para el “ESP8266 Demo Divice”.

### Código para control de dos GPIO's.

#### El código para el control de dos GPIO's del NodeMCU se encuentra en la carpeta **SRC**, el siguiente hipervínculo nos redirige al código:

[**Código para dos LED's**](https://github.com/jwilliamsee/ControlGPIO-ESP-Thingsboard/blob/main/SRC/Codigo-ESP-Thingsboard)

#### El diagrama es el siguiente:

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/GPIO-Conexion.png?raw=true)

#### Se hicieron las conexiones físicamente en el NodeMCU:

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/EnProto.png?raw=true)

#### Se descarga el IDE de Arduino según el SO que se encuentre usando y se instala.

[**IDE Arduino**](https://www.arduino.cc/en/software)

##### Abrimos el IDE de Arduino instalado en nuestro equipo y "pegamos" nuestro código en el IDE haciendo las modificaciones correspondientes del HOST y del TOKEN.

##### El HOST es el servidor al que tenemos acceso de Thingsboard, por ejemplo en la versión de prueba o Demo, el HOST es "demo.thingsboard.io" y el TOKEN dependerá del dispositivo creado, eso se verá a continuación.

##### En caso de haber instalado Thingsboard de manera local, el acceso se dará con los siguientes datos:

	login: tenant@thingsboard.org
	password: tenant

## Visualización de datos en Thingsboard

##### 1. Entramos a Thingsboard, según el caso que usemos (Demo o local).

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things1.png?raw=true)

##### 2. Ya que nos encontramos dentro de THingsboard, nos dirigimos a dispositivos en el menú al lado izquierdo.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things2.png?raw=true)

##### 3. Nos dirigimos al botón rojo para agregar un nuevo dispositivo, en la esquina inferior derecha.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things3.png?raw=true)

##### 4. Escribimos un nombre y escogemos que tipo de dispositivo estamos creando.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things41.png?raw=true)

##### 5. Buscamos nuestro dispositvo que creamos y accedemos para copiar nuestras credenciales, posteriormente serán usadas.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things5.png?raw=true)

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things7.png?raw=true)

##### 6. Salimos al menú principal y nos dirigimos a Dashboard, crearemos uno con el mismo nombre de nuestro dispositivo o cualquier otro nombre para poder identificarlo.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things6.png?raw=true)

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things8.png?raw=true)

##### 7. Escribimos los datos correspondientes.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/THings9.png?raw=true)

##### 8. Salimos al menú principal y nos dirigimos a las librerías de Widgets.

##### Podemos usar el Widget que ahí viene de ejemplo con más interruptores en el panel, pero para este ejemplo usaremos el de la versión Demo de Thingsboard, cuando entramos en la versión Demo nos dirigimos a la parte de paneles y ahí vienen algunos de prueba y elegimos el del ESP: 

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things10-1.png?raw=true)

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things10-2.png?raw=true)

##### Buscamos el punto rojo en la esquina inferior derecha y le damos en editar el tablero, nos aparecerá opción de descarga de los tableros y le damos a esa opción.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things10-3.png?raw=true)

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things10-4.png?raw=true)

##### La otra opción es de ir directamente a los Widget si se tiene instalado Thingsboard de manera local, de la siguiente forma:

##### 9. En las librerías, buscamos una que se llama "GPIO widgets" y descargamos el panel de visualización y el de control.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things11-1.png?raw=true)

##### Lo anterior, para visualizar antes de agregar un nuevo Widget a nuestro Dashboard, cuando hemos identificado que Widget ocupamos, en este caso es el del ESP, vamos al menú principal y nos vamos al Dashboard que creamos antes para agregar el nuevo widget.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things10.png?raw=true)

##### 10. Accedemos y le damos en el botón rojo del signo (+) para agregar un widget, en caso de que tengamos el widget en nuestro equipo de manera local y si no hemos descargado nada, simplemente le damos en el recuadro del centro para escoger nuestro widget. Para este caso lo hemos descargado y ahora tendremos que importar el que hemos descargado previamente.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things11.png?raw=true)

##### 11. Después de haber seleccionado el recuadro "ADD NEW WIDGET", seleccionamos los datos correspondientes, nos aparecerá un aviso de que no coinciden los tableros con nuestro Dashboard creado.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things12.png?raw=true)

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things14.png?raw=true)

##### Cabe recordar que nosotros importamos los tableros que teníamos en nuestro equipo, para evitar confusión, hay que considerar los detalles en cada paso.

##### 12. Después de haber seleccionado o importado el Widget correspondiente, escribimos los datos de acuerdo a nuestro Dashboard y Dispositivo con la intención de no confundirnos en los nombres o evitar errores se escribe el mismo o similar.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things14-1.png?raw=true)

##### Editamos de acuerdo a nuestro dashboard y dispositivo.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things14-2.png?raw=true)

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things14-3.png?raw=true)

##### Finalmente le damos clic en la flecha y ahora tenemos nuestros paneles agregados y ahí aparece que se encuentra off line, debido a que no tenemos conectado nuestro ESP con el código funcionando, cuando se logren conectar ambos, al momento de hacer pruebas, dejará de estar en modo off line.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Things15.png?raw=true)

### Configurando el IDE de Arduino, Código y el ESP.

#### Después nos dirigimos al IDE de Arduino y en la parte de File--Preferences y pegamos lo siguiente:

	http://arduino.esp8266.com/stable/package_esp8266com_index.json

#### Le damos al OK.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Arduino.png?raw=true)

#### Ahora nos dirigimos a Tools--Boards--Boards Manager y escribimos lo siguiente:

	esp8266

#### Cabe mencionar que la versión es la 2.3.0

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Arduino1.png?raw=true)

#### En Tools--Boards--Esp8266 Modules y elegimos el módulo que estamos usando.

#### Instalamos las siguientes librerías y en esas versiones, para actualizar a las más recientes es necesario ver los cambios en cada versión y adaptarlas a la actual, pero si lo que que se necesita es sólo una prueba no estricta, se instalará las siguientes:

#### Sketch--Include Library--Manage Libraries

	PubSubClient 2.6
	ArduinoJson 5.8.0

#### 

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Arduino2.png?raw=true)

#### Ahora pegamos el código que se encuentra en la carpeta SRC y modificamos lo que se indica en las flechas:

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Arduino3.png?raw=true)

#### El TOKEN es del dispositivo que creamos en Thingsboard al iniciar todo y se refiere a la segunda imagen del paso 5 de esta guía.

#### El thingsboardServer se deja así si se está usando la versión Demo de Thingsboard, si no es así, entonces el servidor cambiará, por ejemplo, para esta prueba se está usando un servidor de Thingsboard instalado de manera local y no la Demo.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Servidor.png?raw=true)

#### Ahora lo que sigue, es conectar nuestro ESP adecuadamente y "correr" el programa para después ir a Thingsboard y en la parte de Dashboard ver como de estar "off line" pasa a estar en modo online pero sin indicarnos, simplemente lo sabemos porque el "off line" desaparece y es ahí cuando podemos hacer uso de los GPIO y ver como se acivan los leds y desactivan, según lo que indicamos en el panel, es necesario actualizar la página en Thingsboard para poder establecer conexión y que desaparezca el "off line".

#### Para cargar el código al ESP es necesario hacer que el ESP se encuentre en modo "flasheo", para eso, justo antes de subir el programa se debe mantener presionado el botón FLASH que tiene el ESP y soltarlo hasta cuando empiece a parpadear el Led del ESP, en ese momento se ha establecido la conexión.

#### Finalmente, sabemos que se estableció la conexión y que modificamos adecuadamente en el código porque el "off line" desaparece y si movemos los interruptores en el panel de visualización se puede ver como cambian, físicamente los Led's se activan y desactivan, según lo que se hace en el panel.

![](https://github.com/jwilliamsee/GPIO-ESP-Things/blob/main/Imagenes/Final.png?raw=true)

------------

#### Vínculo de un video donde se ve el funcionamiento:

[**Pendiente**]()

#### El código sufrirá modificaciones, según lo que desea hacer cada usuario, partiendo de este ejemplo, será fácil entender como funciona.

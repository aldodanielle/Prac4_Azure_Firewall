# Practica 4
## Azure Firewall
### Paso 1:
Entramos a el portal de Azure y creamos una Red Virtual agregándole los datos necesarios que ocupa para que se cree el recurso.

![Imagen 1](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P1.png)
-------------------------------------------------------------------------------------------
### Paso 2:
Una vez agregando los datos Básicos nos pasamos a la pestaña de Direcciones IP y ahí nos aseguramos primero que nuestra direcciones de IPv4 sea 10.0.0.0 con un intervalo de 16, después de ello agregamos 2 sub redes una para nuestro Firewall la cual tiene que llevar el nombre de AzureFirewallSubnet con una dirección de 10.0.1.0 y un intervalo de 26 y la otra sub red le colocamos el nombre que deseemos y el intervalo de 10.0.2.0 y un intervalo de 24 y en esta red se van a encontrar todas nuestras VM y por ultimo solo la revisamos y creamos.

![Imagen 2](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P2.png)
-------------------------------------------------------------------------------------------
### Paso 3:
Creamos una Máquina Virtual con en el mismo grupo de recursos y la misma región, y en este caso en las reglas de entrada no le colocamos que ningún puerto este abierto como se muestra en la segunda imagen.

![Imagen 3](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P3.png)
![Imagen 3.1](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P4.png)
-------------------------------------------------------------------------------------------
### Paso 4:
Una vez llevado los datos básicos de la máquina virtual nos vamos a la pestaña de redes y verificamos que estos estén correctos, es decir, a red virtual que se encontré en el mismo grupo de recursos, en la Subred que se encontré en la segunda subred que creamos esto porque por default la primera subred que creamos Azure la detecta que es para nuestro Firewall y en IP publica lo dejamos que esta no tenga es decir que no pueda acceder a internet la computadora sin antes pasara primero por el firewall esto sea más que nada cuando la máquina virtual va estar en moviéndose dentro de la empresa con información importante. Por último revisamos y creamos la máquina virtual 

![Imagen 4](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P5.png)
-------------------------------------------------------------------------------------------
### Paso 5:
Ahora después de crear nuestra Red Virtual y la Máquina Virtual creamos un firewall en Azure y bastaría con buscarlo con el nombre de Firewalls y crear uno nuevo con los datos que este nos pida y lo agregamos en el mismo grupo de recursos que los dos recursos anteriores (Máquina Virtual y Red Virtual), al igual que le nombre del recuso con el cual se identificara (TEST-FW01) y la misma región de los recursos anteriormente creados. También seleccionamos el tipo de plan en este caso lo dejamos como estándar y la Administración del Firewall como usar las reglas de clásicas y seleccionamos nuestra red virtual creada anteriormente al igual que en la dirección IP publica creamos una nueva (Firewall-IP) esto con el fin de que todo el tráfico de la red pase por el firewall y por último revisamos y creamos el Firewall

![Imagen 5](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P6.png)
![Imagen 5.1](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P7.png)
-------------------------------------------------------------------------------------------
### Paso 6:
Buscamos la IP publica el Firewall recordando que le se le creo uno nuevo con el nombre de firewall-IP, después creamos un enrutamiento para mandar toda la información por el firewall para ello primero buscamos el recurso Tablas de ruta (Rute Table) y le agregamos los datos que nos pida para crear el recurso y al igual que los recursos anteriores lo colocamos en el mismo grupo de recursos y la misma región, por último la revisamos y creamos.
Esta tabla de enrutamiento nos ayudara para crear un camino para las entradas y salidas de firewall y posteriormente pasarlo a la Máquina Virtual.

![Imagen 6](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P8.png)
-------------------------------------------------------------------------------------------
### Paso 7:
Una vez creada nuestra tabla de enrutamiento asociamos nuestra Subred para ellos dentro de el mismo recurso nos dirigimos Configuración/Subredes y una vez aquí no vamos a asociamos nuestra red con nuestra creada desde el principio con nuestra subred para la carga de trabajo y con eso se asocian. 

![Imagen 7](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P9.png)
-------------------------------------------------------------------------------------------
### Paso 8:
En el mismo recurso nos vamos a rutas para agregar una nueva ruta el cual solo conta de ponerle un nombre a la ruta, un destino de prefijo, los intervalos que lleva de destino, el tipo de salto y la próxima dirección del salto en este último lleva nuestra dirección IP privada del Firewall

![Imagen 8](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P10.png)
-------------------------------------------------------------------------------------------
### Paso 9:
Volvemos al Firewall a reglas y vamos a agregar una nueva Recopilación de reglas de aplicación

![Imagen 9](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P11.png)
-------------------------------------------------------------------------------------------
### Paso 10:
Agregamos una nueva regla de aplicación para ello le damos un nombre una prioridad esta prioridad puedes ser del 100 a 65000 teniendo en cuenta que entre más bajo es el número mayor prioridad de ejecución se realizará y entre más grande el número menor prioridad de ejecución tendrá y el tipo de acción a realizar (Permitir y Denegar). Después editamos el FQDN de destino con un nombre de identificación, Source Type, el Souce, es decir, toda la sub red de nuestra carga de trabajo, el protocolo a hacer teniendo en cuenta que para separar cada protocolo ocupamos un coma”,” (http, https) y el destino del mismo agregando desde el triple w (www.google.com), esta regla nos ayuda para permitir y denegra la conexión a varias páginas.

![Imagen 10](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P12.png)
-------------------------------------------------------------------------------------------
### Paso 11:
Ahora estando en la misma venta nos vamos a las reglas de red y agregamos una nueva regla y al igual que la anterior le agregamos un nombre, una prioridad y una acción. Y llenamos todos los campos de la Dirección IP el nombre, el protocolo, el Source type, el Source, el destino del type, las direcciones también separadas por “,” aquí también agregamos las IP de los equipos se pude conectar, y el puerto de destino. 

![Imagen 11](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P13.png)
-------------------------------------------------------------------------------------------
### Paso 12:
Ahora agregamos una regla NAT y para ello se necesita un nombre y una prioridad para que después por regla agreguemos un nombre, protocolo, el Souce type, el Source aquí colocamos un “*” esto para que acepte todas las IP así como las direcciones y aquí colocamos la IP pública del firewall y colocamos el mismo puesto que el anterior y en dirección traducida colocamos la IP privada de la Máquina virtual y por último creamos el puerto el cual es el mismo y la agregamos.

![Imagen 12](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P14.png)
-------------------------------------------------------------------------------------------
### Paso 13:
Nos dirigimos al grupo de recursos u entramos a la interfaz de red y configuramos un servidor DNS personalizado agregamos los mismos DNS que anteriormente había colocado. Y también agregamos una IP de los equipos que se quieran conectar en este caso colocamos la IP de mi computadora para que se conecte.

![Imagen 13](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P15.png)
-------------------------------------------------------------------------------------------
### Paso 14:
Nos conectamos a nuestra Máquina Virtual por RDP y observamos que para poder conectarnos por este protocolo ya tenemos más información esto gracias al que está pasando por el firewall y se está aplicando la configuración que hicimos y nos da toda la información que necesitamos y que debemos cumplir para poder conectarnos.

![Imagen 14](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P16.png)
-------------------------------------------------------------------------------------------
### Paso 15:
Para que la maquina se pueda conectar a internet el primer paso es obtener la IP del firewall esto con el fin de obligar que todo el tráfico de internet forzosamente pase primero por le firewall antes que llega a la máquina. Teniendo ya la IP publica el firewall usamos la aplicación de escritorio remoto de Microsoft y ya solo es cuestión de logearnos y ver las reglas de que se cumplan es decir que solo se pueda conectar a www.google.com y no a otros servidores de internet al menos que nosotros lo permitamos.

![Imagen 15](https://github.com/aldodanielle/Prac4_Azure_Firewall/blob/main/Imgenes/P17.png)
-------------------------------------------------------------------------------------------

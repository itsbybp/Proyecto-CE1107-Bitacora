
# Bitácora — Proyecto 1 - COMPUERTA INTELIGENTE 

**Integrantes:** Isac Marín Siria y Byron Bolaños 

La bitácora se reconstruye al final del proyecto a partir de las evidencias que se conservan durante el desarrollo.

Debido a la carga académica y al tiempo que requiere completar el proyecto, no se lleva un registro formal después de cada sesión. Durante gran parte del proceso se prioriza avanzar con el diseño, el montaje y la corrección de errores.

Por esta razón, se seleccionan nueve fechas representativas del trabajo; fechas que si tienen sentido y concuerdan con mensajes y fotografías.

Los primeros cinco registros corresponden principalmente al diseño y desarrollo de las diferentes partes del sistema, con especial énfasis en los decodificadores, ya que de esta etapa se conserva la mayor cantidad de evidencias como capturas de las pruebas realizadas. Dentro de estos primeros días también se incluyen el desarrollo de la transmisión serial.

No se realizan pruebas unitarias formales. Las simulaciones conservadas corresponden principalmente a los decodificadores.



## 26 de agosto

Se revisan los requerimientos generales del proyecto y se identifican las principales partes que deben desarrollarse.
 
Se plantean las etapas de sensores, transmisión serial, circuito combinacional, visualización, desacople y accionamiento.
 
También se comienza a definir cuáles serán los estados que debe reconocer el sistema una vez recibida la contraseña completa.
 
Desde esta etapa se identifican como importantes los estados asociados a:
 
- Apertura.
- Cierre.
- Carga o espera.
- Error.
 
Se determina que el circuito combinacional debe recibir la información correspondiente a los tres números de la contraseña y producir las señales necesarias para identificar estos estados.
 
En esta etapa todavía no se realiza el montaje físico completo.

<img width="1713" height="1265" alt="image" src="https://github.com/user-attachments/assets/12d5fab4-4a0b-4723-ba86-d52398b65da8" />



---

## 5 de septiembre 

Se comienza a trabajar en la etapa encargada de transmitir cada número de la contraseña de forma serial.
 
La información disponible antes de esta etapa corresponde a tres bits en paralelo, por lo que se plantea utilizar un registro 74HC165 configurado como PISO (*Parallel In - Serial Out*).
 
La función del 74HC165 consiste en recibir los tres bits simultáneamente y, mediante las señales de carga y reloj, desplazarlos uno por uno hacia una única línea de salida serial.
 
También se define que las entradas no utilizadas del registro deben mantenerse en un nivel lógico definido para evitar comportamientos no deseados.
 
En esta etapa se trabaja principalmente en determinar qué entradas del 74HC165 serán utilizadas, cómo se cargarán los tres bits y en qué orden deben salir por la línea serial.

<img width="1206" height="1114" alt="image" src="https://github.com/user-attachments/assets/0a50493a-9e10-450f-9c3c-04ba2de2272c" />


## 10 de septiembre

Se continúa con la etapa de transmisión, trabajando ahora en la recepción y almacenamiento de los datos.
 
Se define el uso de tres registros 74HC164, uno para cada número de la contraseña.
 
La salida serial del 74HC165 se conecta a los tres 74HC164, pero cada uno dispone de su propia señal de reloj.
 
De esta forma, los tres registros reciben la misma línea de datos; sin embargo, únicamente el registro al que se le aplican los pulsos de reloj modifica su contenido.
 
Para cada número se utilizan tres pulsos de reloj, suficientes para desplazar los tres bits correspondientes.
 
Al finalizar el proceso, se toman tres salidas de cada 74HC164, obteniendo un total de nueve bits para representar la contraseña completa.
 
La idea general del funcionamiento queda planteada de la siguiente forma:

<img width="683" height="473" alt="image" src="https://github.com/user-attachments/assets/7af184e9-3c92-4126-ba7e-1a4cb49dd44b" />


Esta etapa permitió dejar definida la forma en que los tres números llegarían posteriormente al circuito combinacional\.



## 13 de septiembre

Se comienza a trabajar con mayor detalle en el circuito combinacional encargado de reconocer las contraseñas.
 
Se utilizan como entradas los nueve bits correspondientes a los tres números almacenados.
 
A partir de estos bits se definen las combinaciones que deben activar las señales `OPEN` y `CLOSE`.
 
Primero se desarrolla la lógica correspondiente al estado de apertura.
 
Se revisa qué bits deben encontrarse en nivel alto y cuáles en nivel bajo para que se active la señal `OPEN`.
 
Posteriormente se realiza el mismo procedimiento para la señal `CLOSE`.
 
También se efectúan ajustes para reducir la cantidad de compuertas necesarias y facilitar posteriormente el montaje físico.
 
Una vez definida la lógica, se comienza a preparar el diseño en el simulador.


<img width="985" height="1098" alt="image" src="https://github.com/user-attachments/assets/b197f136-0803-4393-87ad-1810adebb07e" />

<img width="849" height="887" alt="image" src="https://github.com/user-attachments/assets/3086670c-ff8e-41fe-befb-9ed532f902ed" />


## 18 de septiembre 

Se realizan las simulaciones correspondientes a los decodificadores de apertura y cierre.
 
Se comprueba que la combinación asociada a apertura active únicamente la salida `OPEN` y que la combinación correspondiente a cierre active únicamente la salida `CLOSE`.
 
También se prueban combinaciones distintas para verificar que las salidas permanezcan desactivadas cuando la contraseña no coincide con ninguno de los estados esperados.
 
Además, se revisa la relación de estas señales con los estados que posteriormente serán utilizados por el visualizador de siete segmentos.
 
A partir de los resultados obtenidos en la simulación, se realizan correcciones en las conexiones y en las expresiones lógicas antes de llevar el circuito a protoboard.
 
En esta fecha queda definida la versión de los decodificadores que posteriormente se utiliza durante el montaje físico.

Esta fue la etapa con mayor cantidad de evidencia previa al ensamblaje, ya que se conservaron imágenes del diseño del circuito y capturas de las simulaciones realizadas\.

<img width="1898" height="1611" alt="image" src="https://github.com/user-attachments/assets/be324459-d757-4a6b-8aed-d7dbf0b5efa2" />

<img width="461" height="739" alt="image" src="https://github.com/user-attachments/assets/d9be660d-4138-48be-b622-b025254dd027" />



## 23 de septiembre

Se comienza a unir físicamente las diferentes secciones desarrolladas durante las semanas anteriores.
 
Se conectan las salidas de los registros 74HC164 con el circuito combinacional y se verifica que los nueve bits lleguen correctamente a las entradas de los decodificadores.
 
También se conectan las salidas `OPEN` y `CLOSE`, comprobando su funcionamiento de forma visual mediante LEDs.
 
Durante esta etapa aparecen varios problemas de cableado, principalmente relacionados con el orden de los bits, conexiones desplazadas y señales que no llegan correctamente a los circuitos correspondientes.
 
Se revisan varias conexiones provenientes de los registros y se corrigen errores directamente sobre las protoboards.
 
Asimismo, se comprueba que la información transmitida a través del 74HC165 y almacenada en los 74HC164 llegue al circuito combinacional en el orden esperado.
 
A partir de este momento, el trabajo se concentra principalmente en el acople físico e integración de los diferentes módulos del sistema.

<img width="720" height="1280" alt="image" src="https://github.com/user-attachments/assets/96b8ca7f-dac7-481f-82ad-f96c9eec8315" />
<img width="720" height="1280" alt="image" src="https://github.com/user-attachments/assets/b0622119-f399-438d-82f2-b43e7b372beb" />


---

## 25 de septiembre 

Se continúa con la integración del circuito ya montado.
 
Las salidas de los decodificadores se conectan con el resto del sistema, incluyendo el visualizador de siete segmentos y la etapa de desacople.
 
Se instalan los optoacopladores PC817 correspondientes a las señales `OPEN` y `CLOSE`.
 
Se verifica que las señales generadas por los decodificadores lleguen correctamente a los optoacopladores.
 
Antes de continuar hacia la etapa de accionamiento del motor, las salidas se comprueban visualmente mediante LEDs.
 
También se corrigen conexiones del visualizador y se revisan varios falsos contactos producidos por la gran cantidad de cables presentes en las protoboards.
 
La mayor parte de la sesión se dedica a garantizar que las salidas de los decodificadores continúen respondiendo correctamente después de ser conectadas con las etapas posteriores del sistema.
<img width="856" height="1280" alt="image" src="https://github.com/user-attachments/assets/c88d55fe-0a79-4abb-b1d9-2cd914ad20ab" />
<img width="874" height="1280" alt="image" src="https://github.com/user-attachments/assets/3ffd5bba-47d9-4adb-8c8c-a69df2a2d9e3" />
<img width="848" height="1280" alt="image" src="https://github.com/user-attachments/assets/3982463a-7aa2-4d99-8d38-473bf2954631" />


## 27 de septiembre 

Se agrega la etapa de accionamiento al sistema.
 
Se instalan los reguladores necesarios para la alimentación y se conecta el controlador L293D.
 
Las señales provenientes de los optoacopladores se llevan a las entradas del controlador.
 
Posteriormente, se conecta el motor y se realizan las primeras pruebas de giro.
 
Se comprueba que la señal generada por el decodificador de apertura produzca movimiento en un sentido y que la señal generada por el decodificador de cierre produzca movimiento en el sentido contrario.
 
Es necesario corregir conexiones del motor y revisar en varias ocasiones la alimentación antes de conseguir un comportamiento estable.
 
También se agrega un disipador al regulador asociado al motor debido al calentamiento observado durante las pruebas.
 
Durante esta etapa resulta especialmente importante verificar que los decodificadores continúen entregando correctamente las señales `OPEN` y `CLOSE`, ya que estas pasan a controlar directamente el accionamiento físico del sistema. 

<img width="1152" height="1536" alt="image" src="https://github.com/user-attachments/assets/f786a759-bde6-4347-8061-a7e76004ff9b" />


## 28 y 29 en la madrugada del septiembre

Se realiza la integración final de todos los módulos que conforman el proyecto.
 
Se revisa el funcionamiento completo del sistema, desde el ingreso de los datos hasta el movimiento de la puerta.
 
Se comprueban nuevamente las combinaciones correspondientes a apertura y cierre, verificando que los decodificadores activen correctamente sus respectivas salidas.
 
También se verifica que la transmisión serial permita almacenar los tres números de la contraseña antes de que estos sean procesados por el circuito combinacional.
 
Se revisa además el funcionamiento del visualizador de siete segmentos y la respuesta de la etapa de accionamiento.
 
Se ajusta el mecanismo físico para permitir un recorrido adecuado durante las operaciones de apertura y cierre.
 
La detención final se realiza mediante límites mecánicos, por lo que se efectúan varios ajustes hasta conseguir un desplazamiento estable y consistente.
 
Durante las pruebas aparecen diversos inconvenientes asociados al acople físico del sistema, principalmente cables sueltos, conexiones desplazadas, falsos contactos y errores de interconexión entre módulos provocados por la manipulación constante de las protoboards.
 
Se realizan múltiples pruebas completas repitiendo el proceso de ingreso de la contraseña, transmisión serial, almacenamiento, decodificación, visualización y accionamiento, corrigiendo los problemas detectados en cada iteración.
 
Finalmente, se trabaja en la documentación del proyecto, la selección de evidencias y la reconstrucción de la presente bitácora.

<img width="720" height="1280" alt="image" src="https://github.com/user-attachments/assets/fc381833-67b5-43b0-beb7-1c4c4807218e" /> 

<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/5ed3b769-e6e3-41e3-90b3-b83e6992505f" />

<img width="720" height="1280" alt="image" src="https://github.com/user-attachments/assets/e298e0e3-b346-4cea-aca5-7bb432c4b17a" />


___


perdón que solo hayamos realizado los commits en un solo día pero de verdad que tuvimos que speedrunear el proyecto y palmarla en el intento

salud2

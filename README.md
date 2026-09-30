
# Bitácora — Proyecto 1 - COMPUERTA INTELIGENTE 

**Integrantes:** Isac Marín Siria y Byron Bolaños 

La bitácora fue reconstruida al final del proyecto a partir de las evidencias que se conservaron durante el desarrollo\.

Por carga académica y por el tiempo requerido para completar el proyecto, no se llevó un registro formal después de cada sesión\. Durante gran parte del proceso se priorizó avanzar con el diseño, el montaje y la corrección de errores\.

Por esta razón, se seleccionaron nueve fechas representativas del trabajo realizado\.

Los primeros cinco registros corresponden principalmente al diseño y desarrollo de las diferentes partes del sistema, con especial énfasis en los decodificadores, ya que de esta etapa se conservaron la mayor cantidad de evidencias: imágenes del diseño de las simulaciones y capturas de las simulaciones realizadas\. Dentro de estos primeros días también se incluyen dos jornadas dedicadas al desarrollo de la transmisión serial\.

Los últimos cuatro registros corresponden al acople físico, integración, corrección de conexiones y pruebas del sistema ya montado\.

No se realizaron pruebas unitarias formales\. Las simulaciones conservadas corresponden principalmente a los decodificadores\.

---

## 26 de agosto — Análisis inicial y definición de los estados del sistema

Se revisaron los requerimientos generales del proyecto y se identificaron las principales partes que debían desarrollarse\.

Se plantearon las etapas de sensores, transmisión serial, circuito combinacional, visualización, desacople y accionamiento\.

También se comenzó a definir cuáles serían los estados que debía reconocer el sistema una vez recibida la contraseña completa\.

Desde esta etapa se identificaron como importantes los estados asociados a:

- apertura;
- cierre;
- carga o espera;
- error\.

Se determinó que el circuito combinacional tendría que recibir la información correspondiente a los tres números de la contraseña y producir las señales necesarias para identificar estos estados\.

Todavía no se había realizado el montaje físico completo\.

<img width="1713" height="1265" alt="image" src="https://github.com/user-attachments/assets/12d5fab4-4a0b-4723-ba86-d52398b65da8" />



---

## 5 de septiembre — Diseño inicial del serializador

Se comenzó a trabajar en la etapa encargada de transmitir cada número de la contraseña de forma serial\.

La información disponible antes de esta etapa correspondía a tres bits en paralelo, por lo que se planteó utilizar un registro 74HC165 como PISO\.

La función del 74HC165 consistía en recibir los tres bits simultáneamente y, mediante las señales de carga y reloj, desplazarlos uno por uno hacia una única línea de salida serial\.

También se definió que las entradas no utilizadas del registro debían mantenerse en un nivel lógico definido para evitar comportamientos no deseados\.

En esta etapa se trabajó principalmente en determinar qué entradas del 74HC165 serían utilizadas, cómo se cargarían los tres bits y en qué orden debían salir por la línea serial\.

<img width="1206" height="1114" alt="image" src="https://github.com/user-attachments/assets/0a50493a-9e10-450f-9c3c-04ba2de2272c" />


## 10 de septiembre — Desarrollo de la recepción serial con los 74HC164

Se continuó con la etapa de transmisión, ahora trabajando en la recepción y almacenamiento de los datos\.

Se definió el uso de tres registros 74HC164, uno para cada número de la contraseña\.

La salida serial del 74HC165 se conectaría a los tres 74HC164, pero cada uno tendría su propia señal de reloj\.

De esta forma, los tres registros podían recibir la misma línea de datos, pero solamente el registro al que se le aplicaran los pulsos de reloj modificaría su contenido\.

Para cada número se utilizarían tres pulsos de reloj, suficientes para desplazar los tres bits correspondientes\.

Al finalizar el proceso, se tomarían tres salidas de cada 74HC164, obteniendo un total de nueve bits para representar la contraseña completa\.

La idea general quedó planteada de la siguiente forma:

<img width="683" height="473" alt="image" src="https://github.com/user-attachments/assets/7af184e9-3c92-4126-ba7e-1a4cb49dd44b" />


Esta etapa permitió dejar definida la forma en que los tres números llegarían posteriormente al circuito combinacional\.



## 13 de septiembre — Diseño de los decodificadores OPEN y CLOSE

Se comenzó a trabajar con mayor detalle en el circuito combinacional encargado de reconocer las contraseñas\.

Se utilizaron como entradas los nueve bits correspondientes a los tres números almacenados\.

A partir de estos bits se definieron las combinaciones que debían activar las señales `OPEN` y `CLOSE`\.

Primero se desarrolló la lógica correspondiente al estado de apertura\.

Se revisó qué bits debían encontrarse en nivel alto y cuáles en nivel bajo para que se activara `OPEN`\.

Posteriormente se realizó el mismo procedimiento para `CLOSE`\.

También se hicieron ajustes para reducir la cantidad de compuertas y facilitar posteriormente el montaje físico\.

Una vez definida la lógica, se comenzó a preparar el diseño en el simulador\.

**Evidencia disponible:**

<img width="985" height="1098" alt="image" src="https://github.com/user-attachments/assets/b197f136-0803-4393-87ad-1810adebb07e" />

<img width="849" height="887" alt="image" src="https://github.com/user-attachments/assets/3086670c-ff8e-41fe-befb-9ed532f902ed" />


## 18 de septiembre — Simulación y ajustes finales de los decodificadores

Se realizaron las simulaciones correspondientes a los decodificadores de apertura y cierre\.

Se comprobó que la combinación asociada a apertura activara únicamente la salida `OPEN` y que la combinación correspondiente a cierre activara únicamente `CLOSE`\.

También se probaron combinaciones distintas para comprobar que las salidas permanecieran desactivadas cuando la contraseña no coincidía con ninguno de los estados esperados\.

Además, se revisó la relación de estas señales con los estados que posteriormente serían utilizados por el visualizador de siete segmentos\.

A partir de los resultados de simulación se realizaron correcciones en conexiones y expresiones antes de llevar el circuito a protoboard\.

En esta fecha quedó definida la versión de los decodificadores que posteriormente sería utilizada durante el montaje físico\.

Esta fue la etapa con mayor cantidad de evidencia previa al ensamblaje, ya que se conservaron imágenes del diseño del circuito y capturas de las simulaciones realizadas\.

<img width="1898" height="1611" alt="image" src="https://github.com/user-attachments/assets/be324459-d757-4a6b-8aed-d7dbf0b5efa2" />

<img width="461" height="739" alt="image" src="https://github.com/user-attachments/assets/d9be660d-4138-48be-b622-b025254dd027" />


# Etapa de acople, montaje y pruebas

## 23 de septiembre — Montaje físico de los decodificadores e integración con el sistema

Se comenzó a unir físicamente las diferentes secciones desarrolladas durante las semanas anteriores\.

Se conectaron las salidas de los registros 74HC164 con el circuito combinacional y se revisó que los nueve bits llegaran correctamente a las entradas de los decodificadores\.

También se conectaron las salidas `OPEN` y `CLOSE` y se comprobaron visualmente mediante LEDs\.

Durante esta etapa aparecieron varios problemas de cableado, principalmente relacionados con el orden de bits, conexiones desplazadas y señales que no llegaban correctamente\.

Fue necesario revisar varias conexiones provenientes de los registros y corregir errores directamente sobre las protoboards\.

También se comprobó que la información transmitida a través del 74HC165 y almacenada en los 74HC164 llegara al circuito combinacional en el orden esperado\.

A partir de este momento el trabajo se concentró principalmente en acoplar físicamente los módulos\.
<img width="720" height="1280" alt="image" src="https://github.com/user-attachments/assets/96b8ca7f-dac7-481f-82ad-f96c9eec8315" />
<img width="720" height="1280" alt="image" src="https://github.com/user-attachments/assets/b0622119-f399-438d-82f2-b43e7b372beb" />


---

## 25 de septiembre — Acople de decodificadores, visualizador y desacople

Se continuó con la integración del circuito ya montado\.

Las salidas de los decodificadores se conectaron con el resto del sistema, incluyendo el visualizador de siete segmentos y la etapa de desacople\.

Se instalaron los optoacopladores PC817 correspondientes a `OPEN` y `CLOSE`\.

Se revisó que las señales generadas por los decodificadores llegaran correctamente a los optoacopladores\.

Antes de continuar hacia el motor, las salidas se comprobaron visualmente utilizando LEDs\.

También se corrigieron conexiones del visualizador y se revisaron varios falsos contactos producidos por la cantidad de cables presentes en las protoboards\.

La mayor parte de la sesión se dedicó a conseguir que las salidas de los decodificadores siguieran respondiendo correctamente después de ser conectadas con las siguientes etapas\.
<img width="856" height="1280" alt="image" src="https://github.com/user-attachments/assets/c88d55fe-0a79-4abb-b1d9-2cd914ad20ab" />
<img width="874" height="1280" alt="image" src="https://github.com/user-attachments/assets/3ffd5bba-47d9-4adb-8c8c-a69df2a2d9e3" />
<img width="848" height="1280" alt="image" src="https://github.com/user-attachments/assets/3982463a-7aa2-4d99-8d38-473bf2954631" />


## 27 de septiembre — Acople del L293D y primeras pruebas con el motor

Se agregó la etapa de accionamiento\.

Se instalaron los reguladores necesarios para la alimentación y se conectó el L293D\.

Las señales provenientes de los optoacopladores se llevaron a las entradas del controlador\.

Posteriormente se conectó el motor y se realizaron las primeras pruebas de giro\.

Se comprobó que la señal generada por el decodificador de apertura produjera movimiento en un sentido y que la señal generada por el decodificador de cierre produjera movimiento en el sentido contrario\.

Fue necesario corregir conexiones del motor y revisar varias veces la alimentación antes de conseguir un comportamiento estable\.

También se agregó un disipador al regulador asociado al motor debido al calentamiento observado durante las pruebas\.

Durante esta etapa fue especialmente importante comprobar que los decodificadores continuaran entregando correctamente `OPEN` y `CLOSE`, ya que estas dos señales pasaron a controlar directamente el accionamiento físico\.



## 28 y 29 en la madrugada del septiembre — Acople final y pruebas completas


BÁSICAMENTE LA PALMAMOS ACOCPLANDO 

Se realizó la integración final de todo el proyecto\.

Se revisó el funcionamiento desde la entrada de los datos hasta el movimiento de la puerta\.

Se comprobaron nuevamente las combinaciones correspondientes a apertura y cierre, verificando que los decodificadores activaran correctamente sus respectivas salidas\.

También se revisó que la transmisión serial permitiera almacenar los tres números antes de que estos fueran procesados por el circuito combinacional\.

Se revisó además el visualizador de siete segmentos y la respuesta del accionador\.

Se ajustó el mecanismo físico para permitir el recorrido de apertura y cierre\.

La detención final se realizó mediante límites mecánicos, por lo que se hicieron varios ajustes hasta conseguir un recorrido adecuado\.

Durante las pruebas aparecieron problemas menores de protoboard, principalmente cables sueltos, conexiones desplazadas y falsos contactos provocados por la manipulación constante del circuito\.

Se realizaron varias pruebas completas repitiendo el proceso de ingreso, transmisión serial, almacenamiento, decodificación, visualización y accionamiento\.

Finalmente se trabajó en la documentación, selección de evidencias y reconstrucción de la presente bitácora\.
<img width="720" height="1280" alt="image" src="https://github.com/user-attachments/assets/fc381833-67b5-43b0-beb7-1c4c4807218e" /> 

<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/5ed3b769-e6e3-41e3-90b3-b83e6992505f" />

<img width="720" height="1280" alt="image" src="https://github.com/user-attachments/assets/e298e0e3-b346-4cea-aca5-7bb432c4b17a" />


___


perdón que solo hayamos tenido un solo commit pero de verdad que tuvimos que speedrunear el proyecto 

salud2

# 2doParcialCalculadora
Calculadora con funciones específicas

El proyecto consiste en realizar una calculadora debe ser capaz de ingresar un numero de dos dígitos los cuales se pintan y corren (Desplazan conforme se ingresan) en los displays 7 segmentos. El usuario procede a presionar alguna tecla (#?) para confirmar su entrada

Al confirmar la entrada del primer número, se limpian los displays y el sistema queda listo a la espera de los siguientes dos dígitos. El usuario puede ahora ejecutar una operación entre ambos dígitos presionando teclas dedicadas (A=Suma, B=Resta, C=Multiplicación) con la cual la calculadora procede a procesar la operación y presentar el resultado en los displays de 7 segmentos.

Posteriormente alguna tecla (*?) limpia los displays y la calculadora quedara lista para la siguiente operación

La calculadora también acepta números con solo x1 digito

Opcional: Desde una consola serial extienda las funcionalidades previamente implementadas de su calculadora permitiendo la interacción con el usuario desde la terminal serial en donde se aceptarán dígitos para la operación y el usuario puede elegir mediante un menú que operación ejecutar con estos dos números ingresados.

ESTRATEGIA:
	  PASO 1 PRESIONO UNA TECLA CUALQUIERA,  ESTA SE GUARDA EN LA VARIABLE DIGITO1 QUE PASARA A SER IGUALDAD A LA VARIABLE TEMP1
	  PASO 2 DEBO FORZOSAMENTE PRESIONAR ATERISCO PARA QUE LIMPIE EL DISPLAY Y QUEDE GUADADA EN LA VARIABLE EL NUMERO QUE SE PRESIONO
	  PASO 3 EL PROGRAMA VUELVE A ENTRAR A LOS CICLOS, SE PRESIONA UNA SEGUNDA TECLA QUE SERA GUARDADA EN LA VARIABLE DIGIT2
	  PASO 4 DEBO PRESIONAR FORZOSAMENTE NUMERAL PARA QUE, ENTONCES GUARDE DICHO NUMERO EN LA VARIABLE DIGIT2 QUE SERA IGUALADA A TEMP2
	  PASO 5 SE DEBE APACHAR EL OPERADOR DE SU ELECCCION SEA SUMA RESTA MULTIPLICACION O DIVISION
	  PASO 6 DEPENDIENDO CUAL SE APACHE EJEMPLO: SI ES SUMA QUE CORRESPONDE A LA LETRA "A" ENTRA EN ESE "IF" YA QUE SE CUMPLE LA CONDICION
	         Y AHI MANDA A LLAMAR A LAS VARIABLES QUE TIENEN LOS VALORES GUARDADOS PREVIAMENTE, TAMBIEN TIENE CONDICIONES ANIDADAS
	         ES DECIR QUE DESPLIEGUE "E" DE ERROR CUANDO EL NUMERO SEA MAYOR QUE NUEVE YA QUE EN ESTE CASO SOLO USAMOS UN DISPLAY
	         ASI TAMBIEN, EN EL CASO DE LA DIVISION CUANDO SE DIVIDE ENTRE CERO, Y LA RESTA LE INCLUI QUE DESPLEGARA EL SEGMEN DE
	         EN MEDIO ANTES DEL NUMERO PARA QUE SE INDIQUE SI EL RESULTADO DE LA RESTA ERA NEGATIVO.

DESGLOCE Y EXPLICACION DEL CODIGO
![Captura de Pantalla 2024-05-12 a la(s) 15 14 58](https://github.com/wcaceresc/2doParcialCalculadora/assets/161264041/06eb7d89-8d9c-491f-8a56-aef2ea59d2ae)

Comezando el codigo tenemos la definicion de variables de funciones a utilizar

![Captura de Pantalla 2024-05-12 a la(s) 15 16 37](https://github.com/wcaceresc/2doParcialCalculadora/assets/161264041/23fb3259-9b44-4423-9b76-2893609aa794)

Habilitamos los clocks, puertos y el puerto PA1 que es el de control en este caso un display de catodo comun

![Captura de Pantalla 2024-05-12 a la(s) 15 18 45](https://github.com/wcaceresc/2doParcialCalculadora/assets/161264041/6617844d-7c30-466e-899a-1295a9ff7379)

En esta parte comenzando con la funcion de las filas Ky_filas se establecen como pull up los puertosPc5, Pc6, Pc7 y Pc8
primero tenemos que limpiarlos y luego se setean, para el caso de las columnas unicamente los limpiamos ya que los que 
elegimos para usar con las resistencias pullup son las filas, esto se hace para que la resistencia venza el voltaje con la 
resistencia, se cierra el circuito y va a 0V.

![Captura de Pantalla 2024-05-12 a la(s) 15 22 24](https://github.com/wcaceresc/2doParcialCalculadora/assets/161264041/7999c5b3-86ea-4578-94fc-68678aeffe56)

En esta parte es donde se desarolla lo escencial del proyecto.
empieza a recorrer las columnas, en esta imagen vemos cuando entra a las funcion de columnas, lo primero con que se topa es 
identificar en la columna 1 cual boton fue presionado segun el caso 1-4-7 o * entra en unas condicionales anidadas en este caso 
cuatro ifs de los cuales sea el nuero presionado, hara la logica matematica y guardar en las distintas variables.
para esta imagen suponiendo se elege el digito 1, lo guarda en la variable de digito1 para luego reorrer el codigo y esperar
a otra instruccion que se le de, normalmente presionamos otro boton y se guarda en una segunda variable llamada digit2, posteriromente 
debemos ingresar una operacion a realizar, sea suma, resta, multiplicacion o division (extra).

Como funciona?  
-Presionamos un boton 
-Presonamos asterisco (guarda variable 1)
-Presionamos otro boton
-Presionamos Numeral (gurada variable 2)
-Presionamos A=suma, B=resta, C=multiplicacion o D=division 
-Muestra en el display el resultado de la operacion elegida

Para saber que led debe encender el display aqui muestro el codigo del switch case en donde, recien presionado cualquier boton lo guarda en su variable correspondiente dandole un valor para cada caso y dentro de caada caso, se le dice cuales salidas en los GIOB que fue el asignado debe 
encender, en la sigueinte imagen se despliega el caso cuando es cero, guion medio y dos, si sucecivamente con todos los demas casos

![Captura de Pantalla 2024-05-12 a la(s) 15 35 33](https://github.com/wcaceresc/2doParcialCalculadora/assets/161264041/f387e8e8-7ae2-49ab-b67c-89398786ed37)

Como parte extra añadi varias condiciones:

-Dado que solo era un display de un digito le puse que si era mayor de 9 el resultado mostrara ERROR esto lo hice para la suma y multiplicacion



![Captura de Pantalla 2024-05-12 a la(s) 15 38 03](https://github.com/wcaceresc/2doParcialCalculadora/assets/161264041/65520f63-cc8f-444d-ba1e-ec96f3ecf204)


-En el caso de la dision que muestre ERROR si la division era entre 0

![Captura de Pantalla 2024-05-12 a la(s) 15 39 42](https://github.com/wcaceresc/2doParcialCalculadora/assets/161264041/e437c46b-e67e-4c00-9281-a988dc67a471)


-En el caso de la resta cuando el segundo digito en la operacion es mayor que el primero que nos muestre el guion medio para indicar
 que el resultado es un numero negativo, es decir primero mostrara el guion medio seguido del digito resultado


![Captura de Pantalla 2024-05-12 a la(s) 15 42 05](https://github.com/wcaceresc/2doParcialCalculadora/assets/161264041/248f875c-e26d-49de-acde-58bbc99bf6ed)


De esta manera se logra realizar todos los requerimientos para dicho programa utilizando el menor numero de lineas posibles y cabe mencionar que 
no es necesario presionar ninguna tecla para empezar otra operacion ya ue al desplegar el resultado que funciona como el signo igual 
en una calculadora real, es programa queda listo para una nueva operacion simulando tambien una calculadora real. Y todo esto se logra 
aprovechando el bucle del ciclo que recorre el programa una y otra vez, lo usamos a nuestro favor para repetir las operaciones.

AQUI EL LINK DEL VIDEO MOSTRANDO SU FUNCIONAMIENTO.

(https://www.youtube.com/watch?v=vYO4T14yPbo)
.







          

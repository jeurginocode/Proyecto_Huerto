# Proyecto_Huerto
<center>

**INFORME**
<br>
<br>
<br>
**PROYECTO DE FUNDAMENTOS DE PROGRAMACION**

**JORGE ENRIQUE ARNEDO ARTEAGA,**
**,CARLOS FARITH NUÑEZ CALDERA**
**,CAMILO ERNESTO CALDERIN OGAZA**
<br>

**UNIVERSIDAD PONTIFICIA BOLIVARIANA**
<br>
<br>
**FACULTAD DE INGENIERIA Y ARQUITECTURA**
<br>
<br>
**PROGRAMA DE INGENIA ELECTRONICA**
<br>
<br>
**FUNDAMENTOS DE PROGRAMACION**
<br>
<br>
**MONTERIA**
<br>
**2024**
</center>

# RESUMEN

<div align="justify">
En una sociedad moderna, mantener huertos domésticos resulta complejo, debido a que los jardines se secan por falta de hidratación. Para evitar esto, se plantea diseñar un sistema de riego automático, que combine soluciones de hardware y software libres, para medir la humedad de la tierra porque forman parte del ecosistema del huerto. A esta solución se le añadió un microcontrolador, que actúe como centro de operaciones para asegurar el suministro y la dosificación de agua para mantener hidratada una planta.
</div>

**Palabras claves:** Automatización, recolección de datos, señales de sensores.


# ANALISIS
## Sistema de Riego Automatizado para una Planta
**problema:**: Desarrollar un sistema de riego automatizado que regule el riego de una planta en función de la humedad del suelo y el nivel de agua en un recipiente, además de generar alertas en condiciones críticas.

**Descripción:** : El sistema debe activar una motobomba para regar la planta en este caso una sábila, cuando la humedad del suelo esté por debajo de un umbral predefinido y el nivel de agua en el recipiente sea suficiente. Debe también generar una alerta si el nivel de agua en el recipiente está por debajo de un valor crítico para evitar daños al sistema.

**Componentes:**


*  Sensor de Humedad del Suelo
*  Sensor de Nivel de Agua(Analosgico)
*  Modulo Breadboard Fuente De Poder
*  Motobomba
*  Microcontrolador (Arduino UNO)
*  Tres LEDs Indicadores
*  Zumbador
*  Modulo Reley de un solo canal

**Requerimientos Funcionales:**


1. 	Leer continuamente la humedad del suelo y el nivel de agua en el recipiente.
2.  Activar la motobomba cuando la humedad del suelo esté por debajo de un umbral predefinido y haya suficiente agua en el recipiente.
3. Generar una alerta si el nivel de agua en el recipiente está por debajo de un valor crítico para evitar daños al sistema.
4. Almacenar registros de la humedad y el nivel de agua en un archivo para referencia futura.

**procesos del sistema:**<br>

_1. Entrada:_


*   Lectura constante de la humedad del suelo y el nivel de agua.
*   Seleccionar umbral de humedad del suelo.
*   Seleccionar umbral crítico de nivel de agua.

_2. Procesos:_

*  Comparar los valores leídos con los umbrales predefinidos.
* Activar/desactivar la motobomba según los resultados de la comparación.
* Generar una alerta si el nivel de agua en el recipiente está por debajo del umbral crítico.
* Almacenar registros en un archivo para mantener un historial del sistema.

_3. Resultados:_
* Proporcionar un mensaje que indique si la motobomba ha sido activada para regar la planta
* Genera una alerta si el nivel de agua en el recipiente está por debajo del umbral critico.


**Rericciones:**
* 	Utilizar un microcontrolador compatible con los sensores y actuadores.
*  Implementar el sistema utilizando un lenguaje de programación adecuado para el microcontrolador (por ejemplo, Arduino IDE).
*  Diseñar un circuito seguro y eficiente, evitando cortocircuitos y sobrecargas eléctricas.
*	El costo total del sistema no debe exceder los $200.000 por grupo de máximo 4 personas.

**Otras Variable:**
* Iteración mediante ciclos para la lectura continua de los sensores y actuación del sistema de acuerdo con las condiciones del entorno.

# DISEÑO

¡[insertando imagen](imagenes/DISeÑO.jpg)

# ALGORITMO

1. On    				# Encender el sistema

2. Medir				# Medir el nivel de humedad de la planta y el nivel del agua

3. Guardar 				# Registrar las mediciones (punto 2)

4. Si humedad 	<=	x ---> indicador de humedad

5. Si nivel   	<=	y ---> indicador de nivel del agua 

6. Si humedad 	<= x (x1, x2, x3, x4)

while on:
	while h < x:
		if nivel > y:
			if pump on
			delay i
		else:
			pump off
			sound
		delay i, record
	pump off


#PSEUDOCDIGO
El siguiente psudocodigo es de nuestro codigo ya definitvo:


```
Start

    Declare Constant rele = 2
    Declare Constant sensorHumedad = A0
    Declare Integer lecturaSensor
    Declare Integer humedad
    Declare Constant setpointHumedadBajo = 40
    Declare Constant setpointHumedadAlto = 70
    Constant Integer sensorNivelAguaPin = A1
    Constant Integer verdePin = 3
    Constant Integer amarilloPin = 5
    Constant Integer rojoPin = 6
    Constant Integer buzzerPin = 9

    Module setup()
        Set pinMode(rele, OUTPUT)
        Set digitalWrite(rele, LOW)
        Set pinMode(verdePin, OUTPUT)
        Set pinMode(amarilloPin, OUTPUT)
        Set pinMode(rojoPin, OUTPUT)
        Set pinMode(buzzerPin, OUTPUT)
    End Module

    Module loop()
        Set lectura = analogRead(sensorNivelAguaPin)
        Display "Lectura del sensor de nivel de agua: " + lectura
        Display lecturaSensor
        Set lecturaSensor = analogRead(sensorHumedad)
        Set humedad = map(lecturaSensor, 0, 1023, 100, 0)
        
        If humedad > setpointHumedadBajo Then
            Set digitalWrite(rele, HIGH)
            If lectura < 600 Then
                Set digitalWrite(rele, LOW)
            End If
        Else If humedad < setpointHumedadAlto Then
            Set digitalWrite(rele, LOW)
        End If

        Delay(500)

        If lectura < 600 Then
            Set digitalWrite(verdePin, LOW)
            Set digitalWrite(amarilloPin, LOW)
            Set digitalWrite(rojoPin, HIGH)
            Set tone(buzzerPin, 1000)
        Else If lectura < 660 Then
            Set digitalWrite(verdePin, LOW)
            Set digitalWrite(amarilloPin, HIGH)
            Set digitalWrite(rojoPin, LOW)
            Set noTone(buzzerPin)
        Else
            Set digitalWrite(verdePin, HIGH)
            Set digitalWrite(amarilloPin, LOW)
            Set digitalWrite(rojoPin, LOW)
            Set noTone(buzzerPin)
        End If

        Delay(1000)
    End Module

End
```


# CODIGO
El siguiente codigo es el ya definitivo:

```
int rele = 2;
int sensorHumedad = A0;
int lecturaSensor;
int humedad;
int setpointHumedadBajo = 40;
int setpointHumedadAlto = 70;
const int sensorNivelAguaPin = A1; // Pin analógico al que está conectado el sensor de nivel de agua
const int verdePin = 3; // Pin al que está conectado el LED verde
const int amarilloPin = 5; // Pin al que está conectado el LED amarillo
const int rojoPin = 6; // Pin al que está conectado el LED rojo
const int buzzerPin = 9; // Pin al que está conectado el buzzer
       
void setup() {
  pinMode(rele, OUTPUT);
  digitalWrite(rele, LOW);
  pinMode(verdePin, OUTPUT);
  pinMode(amarilloPin, OUTPUT);
  pinMode(rojoPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
}

void loop() {
  int lectura = analogRead(sensorNivelAguaPin);
  Serial.print("Lectura del sensor de nivel de agua: ");
  Serial.println(lectura);
  Serial.println(lecturaSensor);
  lecturaSensor = analogRead(sensorHumedad);
  humedad = map(lecturaSensor, 0, 1023, 100, 0);
  if (humedad > setpointHumedadBajo){
      digitalWrite(rele, HIGH);
      if (lectura<600)
      digitalWrite(rele, LOW);
  }
  else if (humedad < setpointHumedadAlto){
      digitalWrite(rele, LOW);
  }
  delay(500);

  if (lectura < 600) { // Nivel bajo
    digitalWrite(verdePin, LOW);
    digitalWrite(amarilloPin, LOW);
    digitalWrite(rojoPin, HIGH);
    tone(buzzerPin, 1000); // Hacer sonar el buzzer
    
  } else if (lectura < 660) { // Nivel medio
    digitalWrite(verdePin, LOW);
    digitalWrite(amarilloPin, HIGH);
    digitalWrite(rojoPin, LOW);
    noTone(buzzerPin); // Detener el sonido del buzzer
  } else { // Nivel alto
    digitalWrite(verdePin, HIGH);
    digitalWrite(amarilloPin, LOW);
    digitalWrite(rojoPin, LOW);
    noTone(buzzerPin); // Detener el sonido del buzzer
  }

  delay(1000); // Espera un segundo antes de la próxima lectura
}
```


#PROCESO

##PASO 1

<div align="justify">
Antes de probar ir código fuente primero probamos los componentes sin usar el Arduino para probar que cada funcionara correctamente.
</div>

INSERTA IMAGEN DE DISEÑO

<div align="justify">
En este Protototypo simplemente era los componentes conectados unos con otros en él, aquí no se intervenía ninguno condigo, su funcionamiento era muy sencillo: lo que hacía es cuando el sensor de humedad no detectaba humedad el motor se encendía pero cuando llegaba un cierta humedad, el módulo diferencial se activaba enviaba una señal que después pero tenía sobrepasar pase una cierta resistencia(Que podía cambiar dependiendo de cuanto ajustaba el tornillo),   lo convertía en un señal analógica,  llegaron, al módulo relé activándolo, para que desactiven la bomba.<br>
El único componente que no lo pudimos probar si le Arduino fue le sensor de nivel de agua, debido que la manera mas sencilla de saber si detecta nivel de agua era con monitor serial del IDE de Arduino con el siguiente código y diseño fue el que realizamos

</div>

CODIGO DEL NIVEL DE AGUA

<div align="justify">
El código era muy sencillo simplemente el Arduino analizaba la señal digital que venía del sensor quera del 0 a 1023,(entre más grande es el valor más alto está el nivel de agua, que 0 no detecta agua y 1023 está en lo más alto)  utilizando la función una digitalanalag() y printl, nos muestra la señal que da nuestro senso
</div>

IMAGEN DE SENSOR Y ARDUINO

<div align="justify">
cómo podemos ver aquí simplemente se conecta el  sensor de nivel de agua en los respectivos pines de Arduino UNO de GND(negativo), VCC(positivo) y SEÑ(señal analógica).
</div>

##PASO 2

<div align="justify">
En este paso lo que se  hizo fue los códigos de los dos sistemas que son:

1.	Primer código que dependiendo del nivel de agua se activa la bomba.
2. Segundo código que entre más bajo sea nivel de agua se van de prendiendo y apagando uno tres leds que el ultimo led a su vez suena un buzzer que significa que ya no hay agua el recipiente

</div>

### Primer codigo


INSERTA IMAGEN DE DISEÑO

<div align="justify">
La fuente de alimentación se utiliza para proporcionar energía a la bomba, pero como que esta no tiene que estar funcionando las 24 h la conectamos al relé en modo normalmente abierto marcado como NO (del inglés normally open) esto ara que en el estado normal del relé la bomba está parada y solo se pondrá en marcha una vez demos la señal de cambiar de estado del relé. Él cambió de estado del relé lo vamos a controlar con la señal procedente del pin 7 del Arduino. Dicha señal será enviada cuando la humedad del suelo esté por debajo del setpoint que marquemos (que leeremos en el pin A0). Una vez visto el montaje pasemos a ver el código del Arduino.

</div>

```
int rele = 7;
int sensorHumedad = A0;
int lecturaSensor;
int humedad;
int setpointHumedadBajo = 40;
int setpointHumedadAlto = 70;

void setup() {
  pinMode(rele, OUTPUT);
  digitalWrite(rele, LOW);
}

void loop() {
  lecturaSensor = analogRead(sensorHumedad);
  humedad = map(lecturaSensor, 0, 1023, 100, 0);
  if (humedad < setpointHumedadBajo){
      digitalWrite(rele, HIGH);
  }
  else if (humedad > setpointHumedadAlto){
      digitalWrite(rele, LOW);
  }
  delay(1000);
}
```
<div align="justify">
En la primera parte del código definimos todas las variables que vamos a utilizar en nuestro programa. En la primera línea definimos el pin del Arduino que dará la señal de cambiar de estado del relé. En la siguiente línea definimos el pin en el que leeremos la señal del sensor. Las dos siguientes variables son las que usaremos para almacenar los valores del sensor (en el momento de inicializarlas no hace falta darles ningún valor). Para terminar, tenemos las dos variables que nos definen a partir de que grado de humedad se enciende la bomba (por estar el suelo seco) y en qué punto se vuelve a parar la bomba (una vez el suelo está húmedo), estos valores se pueden modificar para que el grado de humedad en las distintas plantes se mantenga dentro del rango deseado (los valores corresponden a % de humedad en el suelo).

</div>

```
int rele = 7;
int sensorHumedad = A0;
int lecturaSensor;
int humedad;
int setpointHumedadBajo = 40;
int setpointHumedadAlto = 70;
```
Una vez definidas las variables y constantes que vamos a usar, es momento de inicializar el sistema. En este caso indicamos que el pin del relé se tiene que configurar como una salida (enviaremos la señal al relé por este pin). También vamos a inicializar dicho pin en el estado LOW, de esta manera nos aseguramos de que la bomba esté inicialmente parada.

```
void setup() {
  pinMode(rele, OUTPUT);
  digitalWrite(rele, LOW);
}
```
<div align="justify">
Para finalizar, tenemos el cuerpo del programa, la parte que se ejecutara una vez y otra indefinidamente y que controlara que el suelo siempre este dentro de los valores deseados. En primera instancia, leerá la señal procedente del sensor. A continuación convertirá la señal analógica en un valor entre 0-100% (el 0% corresponde a una lectura de 1023 y el 100% a cero). Una vez tenemos la señal convertida a porcentaje de humedad comparamos el valor leído con el setpoint de humedad baja, si la humedad del suelo esta por debajo del valor que nosotros queremos se pondrá en marcha la bomba. Esta permanecerá en funcionamiento hasta que la humedad este por encima del setpoint alto, momento en que se parara. Para no colapsar el sistema vamos a hacer una lectura cada segundo.
</div>

```
void loop() {
  lecturaSensor = analogRead(sensorHumedad);
  humedad = map(lecturaSensor, 0, 1023, 100, 0);
  if (humedad < setpointHumedadBajo){
      digitalWrite(rele, HIGH);
  }
  else if (humedad > setpointHumedadAlto){
      digitalWrite(rele, LOW);
  }
  delay(1000);
}
```

### Segundo Codigo

INSERTA IMAGEN DE DISEÑO GRAFICO

```
const int sensorNivelAguaPin = A1; // Pin analógico al que está conectado el sensor de nivel de agua
const int verdePin = 3; // Pin al que está conectado el LED verde
const int amarilloPin = 5; // Pin al que está conectado el LED amarillo
const int rojoPin = 6; // Pin al que está conectado el LED rojo
const int buzzerPin = 9; // Pin al que está conectado el buzzer

void setup() {
  Serial.begin(9600);
  pinMode(verdePin, OUTPUT);
  pinMode(amarilloPin, OUTPUT);
  pinMode(rojoPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
}

void loop() {
  int lectura = analogRead(sensorNivelAguaPin);
  Serial.print("Lectura del sensor de nivel de agua: ");
  Serial.println(lectura);

  if (lectura < 600) { // Nivel bajo
    digitalWrite(verdePin, LOW);
    digitalWrite(amarilloPin, LOW);
    digitalWrite(rojoPin, HIGH);
    tone(buzzerPin, 1000); // Hacer sonar el buzzer
  } else if (lectura < 660) { // Nivel medio
    digitalWrite(verdePin, LOW);
    digitalWrite(amarilloPin, HIGH);
    digitalWrite(rojoPin, LOW);
    noTone(buzzerPin); // Detener el sonido del buzzer
  } else { // Nivel alto
    digitalWrite(verdePin, HIGH);
    digitalWrite(amarilloPin, LOW);
    digitalWrite(rojoPin, LOW);
    noTone(buzzerPin); // Detener el sonido del buzzer
  }

  delay(1000); // Espera un segundo antes de la próxima lectura
}
```
<div align="justify">
El anterior código Arduino lee continuamente el valor analógico de un sensor de nivel de agua y controla LEDs y un buzzer en función del nivel de agua detectado como también los LEDs y el buzzer se utilizan para indicar visual y auditivamente diferentes niveles de agua (bajo, medio, alto) a su vez la comunicación serial se utiliza para monitorear las lecturas de nivel de agua en el monitor serial.
</div>


_Declaraciones de Variables Globales:_

```
const int sensorNivelAguaPin = A1; // Pin analógico al que está conectado el sensor de nivel de agua
const int verdePin = 3;            // Pin al que está conectado el LED verde
const int amarilloPin = 5;          // Pin al que está conectado el LED amarillo
const int rojoPin = 6;              // Pin al que está conectado el LED rojo
const int buzzerPin = 9;            // Pin al que está conectado el buzzer
```

En esta sección:
* `sensorNivelAguaPin` se define como `A1`, representando el pin analógico al que está conectado el sensor de nivel de agua.
* `verdePin`, `amarilloPin`, `rojoPin` y `buzzerPin` se definen para especificar los pines digitales conectados a los LEDs (verde, amarillo, rojo) y un buzzer, respectivamente.

_Funcion `setup()`:_

```
void setup() {
  Serial.begin(9600);  // Inicia la comunicación serial a 9600 baudios
  pinMode(verdePin, OUTPUT);     // Configura el pin del LED verde como salida
  pinMode(amarilloPin, OUTPUT);  // Configura el pin del LED amarillo como salida
  pinMode(rojoPin, OUTPUT);      // Configura el pin del LED rojo como salida
  pinMode(buzzerPin, OUTPUT);    // Configura el pin del buzzer como salida
}
```
En la fucion `setup()`:
* `Serial.begin(9600);` inicializa la comunicación serial a una velocidad de 9600 baudios.

* `pinMode()` se utiliza para configurar los pines especificados (verdePin, amarilloPin, rojoPin, buzzerPin) como pines de SALIDA.

Funcion`loop()`_
```
void loop() {
  int lectura = analogRead(sensorNivelAguaPin);  // Lee el valor analógico del sensor de nivel de agua
  Serial.print("Lectura del sensor de nivel de agua: ");
  Serial.println(lectura);  // Imprime el valor leído por el sensor

  if (lectura < 600) {  // Si el nivel de agua es bajo
    digitalWrite(verdePin, LOW);    // Apaga el LED verde
    digitalWrite(amarilloPin, LOW); // Apaga el LED amarillo
    digitalWrite(rojoPin, HIGH);   // Enciende el LED rojo
    tone(buzzerPin, 1000);          // Hace sonar el buzzer a 1000 Hz
  } else if (lectura < 660) {  // Si el nivel de agua es medio
    digitalWrite(verdePin, LOW);    // Apaga el LED verde
    digitalWrite(amarilloPin, HIGH); // Enciende el LED amarillo
    digitalWrite(rojoPin, LOW);     // Apaga el LED rojo
    noTone(buzzerPin);               // Detiene el sonido del buzzer
  } else {  // Si el nivel de agua es alto
    digitalWrite(verdePin, HIGH);   // Enciende el LED verde
    digitalWrite(amarilloPin, LOW); // Apaga el LED amarillo
    digitalWrite(rojoPin, LOW);     // Apaga el LED rojo
    noTone(buzzerPin);               // Detiene el sonido del buzzer
  }

  delay(1000);  // Espera un segundo antes de la próxima lectura
}

```
En la funcion`loop()`:
* `analogRead(sensorNivelAguaPin);` lee el valor analógico del sensor de nivel de agua conectado a sensorNivelAguaPin.
* El valor leído se imprime en el monitor serial usando `Serial.print()` y `Serial.println()`.
* Según el nivel de agua (`lectura`), se evalúan diferentes condiciones para controlar el comportamiento de los LEDs (`verdePi`,` amarilloPin`,` rojoPin`) y el buzzer (buzzerPin).
* `delay(1000);` introduce un retardo de 1 segundo antes de la próxima lectura del sensor.




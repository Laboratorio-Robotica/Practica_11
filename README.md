# Practica_11

## Integrantes:  
- Francisco Javier Godinez Lopez
- Pablo Axel Silva Fuentes
- Eduardo David Salas Ayala
- 
## Introducción:  

El objetivo principal de esta práctica es integrar un sensor al robot Epson, empleando un ESP32 para la comunicación serial. El ESP32 será responsable de enviar datos al robot, y según los datos recibidos, el robot deberá realizar diversas acciones, como desplazarse a un punto específico, abrir o cerrar las pinzas, o girar hacia un lado. Esta actividad tiene como finalidad comprender y explorar la aplicación práctica de estos dispositivos en sistemas de control automatizado.

## Instrucciones

El robot debe realizar un movimiento.

1. Seleccionar un sensor o entrada de datos. En este caso, se eligió un potenciómetro por su simplicidad y conveniencia.
2. Configurar la lectura del potenciómetro en el ESP32 para obtener los valores de entrada.
3. Habilitar la función Serial2 en el ESP32 para enviar los datos a través de un pin conectado al módulo RS232.
4. Implementar la lógica en el software Epson RC+ para detectar y procesar los datos recibidos, configurando la lectura desde el puerto serial.
5. Configurar los puntos de destino para el robot en función de los datos recibidos por el puerto serial. En este caso, los datos corresponderán a valores 
   numéricos.
6. Verificar el funcionamiento completo del sistema, asegurando que el control del robot responde correctamente a las entradas proporcionadas.

De tal manera que el codigo desarrollado en el Epson+ quedo de la siguiente manera:



```
Integer dato
Function main
Motor On
Home
Power High
Speed 50
Accel 50, 50

Xqt serial
Do
	
	Select 1
		Case dato = 1
			Go izquierda
		Case dato = 2
			Go derecha
		Case dato = 3
			Go arriba
		Case dato = 4
			Go abajo
		Case dato = 5
			Off 2
		Case dato = 6
			On 2
	Send
	
Loop
Fend

Function serial
	Integer numChars
	OpenCom #1
	Wait 1
	Print "HOLA"
	Do
		Do While numChars = 0
			numChars = ChkCom(1)
		Loop
		ReadBin #1, dato
		Print dato
	Loop
	CloseCom #1
Fend

```


El codigo en ESP32 quedo de la siguiente manera: 

```
// Definir el pin donde está conectado el potenciómetro
const int potPin = 21;
int val;
void setup() {
  // Inicializamos la comunicación serie para ver los datos en el monitor serie
  Serial.begin(9600);
  Serial2.begin(9600, SERIAL_8N1, 16, 17);
  
  // Configurar el pin como entrada (opcional, pero buena práctica)
  pinMode(potPin, INPUT);
  
}

void loop() {
  // Leer el valor analógico del potenciómetro
  int potValue = analogRead(potPin);

  float voltage = potValue * (3.3 / 4095.0);

  Serial.print("pot value: ");
  Serial.print(potValue     );
  Serial.print("   Voltaje: ");
  Serial.println(voltage);
  
    int valor = 4095/9;
  if (potValue <= valor){
    val=1;
    Serial2.write(val);
  }
  if (potValue <= valor*2 && potValue > valor){
    val=2;
    Serial2.write(val);
  }
  if (potValue <= valor*3 && potValue > valor*2){
     val=3;
    Serial2.write(val);
  }
  if (potValue <= valor*4 && potValue > valor*3){
     val=4;
    Serial2.write(val);
  }
  if (potValue <= valor*5 && potValue > valor*4){
     val=5;
    Serial2.write(val);
  }
  if (potValue <= valor*6 && potValue > valor*5){
     val=6;
    Serial2.write(val);
  }

  delay(1000);
}

```

### Debido a fallas en el módulo, no fue posible completar la práctica en su totalidad. Por esta razón, se llevó a cabo una simulación durante la hora de laboratorio, la cual fue aceptada como válida para la entrega. Cabe destacar que, en ese momento, únicamente se lograron capturar fotografías del proceso, ya que no fue posible grabar un video.


![WhatsApp Image 2024-12-12 at 12 23 24 AM](https://github.com/user-attachments/assets/86c04772-d8e7-4eeb-986c-80bf6fdf649c)



![WhatsApp Image 2024-12-12 at 12 23 24 AM (1)](https://github.com/user-attachments/assets/50c6cbac-59b3-43b6-a64e-b9a0adfc92f7)


### El único error mostrado en pantalla se debió a que los puntos almacenados no coincidían entre la versión simulada y la versión real.


## Conclusiones:  

### Francisco Javier Godinez Lopez:

### Pablo Axel Silva Fuentes: 

### Eduardo David Salas Ayala: 



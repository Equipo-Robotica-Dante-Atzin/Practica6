# Práctica 6

## Integrantes

- Dante Mejía Silva
- Atzin Morales Alejandre

## Introducción 

En esta práctica de laboratorio de robótica, se utilizó un motor a pasos controlado mediante un microcontrolador, con el objetivo de realizar movimientos precisos: cuatro vueltas a la izquierda en un segundo y dos vueltas a la derecha en dos segundos. Para llevar a cabo este control, fue fundamental el uso del driver JSSD250M, el cual juega un papel crucial en la correcta operación del motor a pasos.

El driver JSSD250M es un componente esencial porque se encarga de traducir las señales de bajo voltaje y baja corriente generadas por el microcontrolador en señales de mayor potencia necesarias para controlar el motor a pasos. El microcontrolador, al trabajar con niveles de corriente limitados, no puede manejar directamente las demandas de potencia de los motores. El driver actúa como un intermediario, asegurando que el motor reciba los pulsos y la corriente adecuados para funcionar sin dañar los circuitos de control.

Además, el driver JSSD250M garantiza la estabilidad y precisión en el control del motor, permitiendo manejar diferentes configuraciones de velocidad y torque con alta precisión. En esta práctica, su función fue clave para realizar los movimientos especificados, ajustando tanto la frecuencia de los pulsos como la dirección del motor con alta eficiencia. La importancia de este driver radica en su capacidad para manejar la carga del motor y proteger el sistema contra sobrecorrientes o sobrecalentamientos.

## Instrucciones

En primer lugar, se llevó a cabo la identificación de los componentes necesarios para la práctica, destacando el motor a pasos como uno de los elementos clave.

![Imagen de WhatsApp 2024-10-19 a las 15 55 51_cbc7651b](https://github.com/user-attachments/assets/27e80a80-bcf8-42f6-8dd4-20026dce5f4f)

Otro de los componentes esenciales fue el driver, al cual se le asignó un valor específico de pulsos por revolución (6400), determinando así la resolución del control del motor a pasos.

![Imagen de WhatsApp 2024-10-19 a las 15 55 51_5a23a26e](https://github.com/user-attachments/assets/ee4fc3fd-b4c7-4f44-b8b3-253a9d588bbb)

Posteriormente, se procedió a desarrollar el programa en el entorno de desarrollo Arduino IDE, donde se implementaron las instrucciones necesarias para controlar el motor a pasos según los parámetros establecidos.
```
int senal = 11;
bool estado = 0;
int giro = 10;

void setup() {
  estado = 0;
  pinMode(senal,OUTPUT);
  pinMode(giro,OUTPUT);  
}
void loop() {
  digitalWrite(giro,HIGH);
    //f1 = 1.0/(2*pulson_rev*4);
    //T1 = 19.53e-6

    for(long i = 0; i<51200; i++){
      estado = !estado;
      digitalWrite(senal,estado);
    
      delayMicroseconds(20); // delay en microsegundos
    }
  delay(1000);

  digitalWrite(giro,LOW);

  //T2 = 78.125e-6
  for(long i = 0; i<25600; i++){
      estado = !estado;
      digitalWrite(senal,estado);
    
      delayMicroseconds(78); // delay en microsegundos
    }
   delay(1000);
}
```


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

### Variables Globales

1. **int senal = 11;**: Define el pin digital 11 como la señal de salida que enviará los pulsos al driver del motor para controlar su movimiento.
   
3. **bool estado = 0;**: Variable booleana que se alterna entre 0 (LOW) y 1 (HIGH) para generar pulsos que controlan los pasos del motor.
   
5. **int giro = 10;**: Define el pin digital 10 como el que controla la dirección del motor, determinando si gira a la izquierda o a la derecha.

### void setup()

1. **pinMode(senal,OUTPUT);**: Configura el pin 11 como una salida, que se utilizará para enviar señales de pulsos al motor.
   
3. **pinMode(giro,OUTPUT);**: Configura el pin 10 como una salida, para controlar la dirección del giro del motor.

### void loop()

El ciclo principal se ejecuta repetidamente y consta de dos fases: movimiento hacia la izquierda y movimiento hacia la derecha.

1. **Movimiento hacia la izquierda**:

   - **digitalWrite(giro,HIGH);**: Establece la señal en el pin 10 en `HIGH`, lo que indica al motor que gire hacia la izquierda.
     
   - **for(long i = 0; i<51200; i++)**: Un bucle que se ejecuta 51200 veces. Dado que el driver está configurado con 6400 pulsos/revolución, este bucle hará que el motor complete 4 vueltas (6400 * 4 * 2 = 51200).
   - 
   - **estado = !estado;**: Alterna el estado de la señal entre HIGH y LOW, generando los pulsos para el motor.
     
   - **digitalWrite(senal,estado);**: Envía el valor actual de la señal al pin 11.
     
   - **delayMicroseconds(20);**: Establece un retardo de 20 microsegundos entre cada cambio de pulso, controlando la velocidad del motor.
     
   - **delay(1000);**: Pausa de 1 segundo antes de cambiar la dirección del motor.

3. **Movimiento hacia la derecha**:

   - **digitalWrite(giro,LOW);**: Establece la señal en el pin 10 en `LOW`, indicando al motor que gire hacia la derecha.
     
   - **for(long i = 0; i<25600; i++)**: Un bucle que se ejecuta 25600 veces, haciendo que el motor complete 2 vueltas hacia la derecha (6400 * 2 * 2 = 25600).
     
   - **estado = !estado;**: Alterna el estado de la señal nuevamente para generar los pulsos.
     
   - **digitalWrite(senal,estado);**: Envía la señal de pulso al pin 11.
     
   - **delayMicroseconds(78);**: Establece un retardo de 78 microsegundos entre cada cambio de pulso, ajustando la velocidad del motor para el giro hacia la derecha.
     
   - **delay(1000);**: Pausa de 1 segundo antes de reiniciar el ciclo y comenzar nuevamente con el giro hacia la izquierda.

Posteriormente se hizo la conexión de los componentes mediante la ayuda del siguiente esquema:

![Imagen de WhatsApp 2024-10-19 a las 15 55 51_7e57b056](https://github.com/user-attachments/assets/85461b0e-4d55-42a3-a170-3b7198642dc7)

Quedando de manera física de la siguiente manera:

![image](https://github.com/user-attachments/assets/0557a777-b8b2-493c-a831-017199204ac0)

Después simplemente corrimos el código y observamos el correcto funcionamiento del ejercicio.

## Conclusiones

***Atzin Morales Alejandre:*** 



***Dante Mejía Silva:*** 
A través de esta práctica de laboratorio, se adquirieron conocimientos fundamentales sobre el control de motores a pasos utilizando un microcontrolador y el desarrollo de código en Arduino. Se comprendió la importancia de controlar la dirección y el número de vueltas que un motor a pasos puede realizar, lo cual se logra mediante el envío de pulsos desde el microcontrolador. Este proceso implica el uso de señales digitales para activar el motor en la secuencia adecuada, permitiendo que el sistema ejecute movimientos precisos y repetitivos. 

Un aspecto crucial de esta práctica fue la utilización del driver JSSD250M, que actúa como un intermediario entre el microcontrolador y el motor. Se aprendió que este componente es esencial para adaptar las señales de control a los requerimientos de potencia del motor, lo que protege tanto el microcontrolador como el propio motor de posibles daños. Al comprender cómo funcionan estos drivers, se adquirió una visión más profunda sobre la interconexión entre componentes electrónicos en un sistema robótico.

El desarrollo del código nos permitió explorar la generación de pulsos digitales mediante la manipulación de los estados de los pines en el Arduino. Además, se abordó el cambio de dirección del motor programáticamente, lo cual fue logrado al modificar la señal de un pin específico que determina si el motor gira hacia la izquierda o hacia la derecha.

En conclusión, esta práctica no solo proporcionó una base sólida en los conceptos fundamentales de la robótica y el control de motores a pasos, sino que también mejoró nuestra capacidad para programar y gestionar movimientos precisos en sistemas automatizados. Estos aprendizajes son aplicables en diversos proyectos futuros, donde el manejo de motores a pasos es un componente crucial en el diseño de sistemas robóticos y automatizados.

## Referencias Bibliográficas 

[1] 	EpsonCompany, «Especialistas en automatización industrial». 2024, https://www.epson.es/es_ES/robots

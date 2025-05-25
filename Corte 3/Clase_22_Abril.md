# Control de Movimiento Clase 22 de Abril.

Julian Stiven Redondo Chacon & Sebastian Cifuentes Alfonso & David Esteban Vasquez Alarcon

## Índice

[5. Conclusiones](#5-Conclusiones)

[6. Bibliografía](#6-Bibliografía)
  

## 1. Introducción al Control de Movimiento con Quanser y Simulink

El control de movimiento es una disciplina fundamental en la ingeniería de control que se enfoca en regular el comportamiento dinámico de sistemas físicos que requieren movimiento preciso, como motores, robots, vehículos autónomos y actuadores en procesos industriales. En esta etapa del curso, abordaremos los principios y herramientas prácticas para diseñar, simular y validar sistemas de control de movimiento.

Para ello, utilizaremos Quanser, una plataforma educativa y de investigación reconocida por sus sistemas mecatrónicos de alta precisión y sus módulos didácticos orientados al aprendizaje práctico del control. Quanser permite implementar y probar algoritmos de control en tiempo real, brindando una experiencia más cercana al entorno industrial.

La integración con Simulink, un entorno de modelado y simulación basado en bloques de MATLAB, facilita el diseño y prueba de sistemas de control mediante representaciones gráficas y entornos interactivos. Gracias a esta combinación, podemos:

-Modelar sistemas dinámicos complejos.

-Diseñar controladores PID, LQR, adaptativos y más.

-Validar algoritmos en tiempo real con hardware de Quanser.

-Obtener datos experimentales para análisis y mejora del desempeño.

![image](https://github.com/user-attachments/assets/086eeee5-84d3-488e-800f-9871d47978a1)

Figura 1. Quanser. 

## 2. Quanser

Quanser es una plataforma de hardware y software especializada en sistemas de control, que permite a estudiantes e investigadores implementar y validar algoritmos de control en tiempo real. Su integración con MATLAB y Simulink proporciona un entorno poderoso para la simulación, análisis y control físico de plantas reales como péndulos, motores DC, servomecanismos, sistemas de levitación magnética, entre otros.

### 2.1 Arquitectura general de Quanser

Quanser trabaja típicamente con tres componentes clave:

Hardware: Incluye plantas físicas (como el QUBE-Servo 2, Rotary Inverted Pendulum, etc.) y la tarjeta de adquisición de datos Quanser QLabs o QPIDe.

Software:

QUARC: Una extensión de Simulink desarrollada por Quanser para generar código en tiempo real y conectarse con el hardware.

QLabs: Plataforma de simulación basada en realidad virtual para experimentos de control sin necesidad del hardware físico.

Controladores: Se pueden diseñar directamente en Simulink usando bloques prediseñados o personalizados.


| Comando         | Descripción                                                                                         |
| :-------------- | :-------------------------------------------------------------------------------------------------- |
| `QLabs.register`| Abre la página de registro de la [licencia de sitio de MathWorks](link-to-mathworks-page).       |
| `QLabs.setup`   | Instala Quanser Interactive Labs. Descarga, si es necesario.                                        |
| `QLabs.launch`  | Inicia Quanser Interactive Labs. Descarga e instala, si es necesario.                               |
| `QLabs.remove`  | Desinstala Quanser Interactive Labs y elimina los archivos temporales descargados.                  |

Tabla 1. Comandos Quanser

### 2.2 Software

Antes de comenzar a trabajar con los modelos de Quanser, es necesario iniciar el entorno de simulación virtual proporcionado por QLabs. Este software permite interactuar con plantas simuladas en 3D sin necesidad de tener el hardware físico. Para ello, es importante ejecutar primero el comando qlabs_setup, que configura el entorno y las rutas necesarias. Luego, con el comando qlabs_launch, se abre la interfaz principal de QLabs, donde podremos seleccionar el experimento a utilizar. Esta preparación es esencial para que los bloques de Simulink se conecten correctamente con la planta virtual y podamos comenzar el diseño y validación de nuestros controladores.

![image](https://github.com/user-attachments/assets/b6a778d3-de34-44df-aa7f-c3cbc0cfa4e6)

Figura 2. Comando. 

Cuando se ejecuta el comando, aparece una ventana donde el estudiante debe iniciar sesión con su correo institucional. Este paso es necesario para acceder a las plantas virtuales que la universidad tiene habilitadas con su licencia. Una vez se completa el inicio de sesión, ya es posible utilizar los modelos de QLabs y comenzar a trabajar con las simulaciones.

![image](https://github.com/user-attachments/assets/dcf37f54-9cc7-4388-b486-265c87a545bd)

Figura 3. Logueo. 

Una vez se inicia sesión correctamente, QLabs muestra las plantas virtuales disponibles según la licencia de la universidad. En nuestro caso, contamos con tres modelos:

1. **Qube 2 – DC Motor**:  
   Esta planta simula un servomotor de corriente continua. Es ideal para aprender los fundamentos del diseño de sistemas de control clásico, como controladores PID y análisis de respuesta temporal. Se trabaja mucho con control de velocidad y posición.

2. **Aero**:  
   Representa un sistema aeroespacial compuesto por hélices que giran para simular el comportamiento de un sistema dinámico no lineal y acoplado. Es útil para estudiar temas más avanzados como control multivariable, sistemas acoplados y compensadores.

3. **Ball and Beam**:  
   Este modelo simula una bola que se mueve sobre una viga controlada por un motor. Es un experimento clásico en control, ideal para aprender sobre estabilidad, retroalimentación y control de sistemas con dinámica más compleja.

![image](https://github.com/user-attachments/assets/25580f43-0ba6-4697-ba22-2a50fc5d27e8)

Figura 4. Gemelos digitales.

| Modelo                | Sensores principales               | Variables clave                        | Objetivos de control                             |
| --------------------- | ---------------------------------- | -------------------------------------- | ------------------------------------------------ |
| **Qube 2 - DC Motor** | Encoder rotacional                 | Velocidad angular, posición del eje    | Control de posición y velocidad del motor DC     |
| **Aero**              | Encoders en ambos ejes, tacómetros | Ángulo de elevación, ángulo de guiñada | Control de orientación y estabilidad dinámica    |
| **Ball and Beam**     | Sensor de posición lineal          | Posición de la bola sobre la viga      | Mantener la bola estable en una posición deseada |

Tabla 2. Comparacion de gemelos digitales.

## 3 Qube 2 - DC Motor

El QUBE-Servo 2 es una planta didáctica desarrollada por Quanser que permite explorar conceptos de control en sistemas electromecánicos. Está compuesta por:

**Motor DC**: Actúa como actuador principal.

**Cargas intercambiables**: Como el brazo rotatorio y el péndulo invertido.

**Sensores**: Encoders para medir posición y velocidad.

**Interfaz USB**: Para comunicación con el computador mediante QUARC y Simulink.

![image](https://github.com/user-attachments/assets/e4d37ac8-0e78-451d-b4dc-8289e6804c7b)

Figura 5. Qube 2.

### 3.1 Parametros del sistema

A continuación, se presentan algunos parámetros típicos del QUBE-Servo 2:
| Parámetro             | Símbolo | Valor Típico         | Unidad  |
| --------------------- | ------- | -------------------- | ------- |
| Resistencia del motor | $R$     | 8.4                  | Ω       |
| Constante de torque   | $K_t$   | 0.042                | Nm/A    |
| Constante de back-EMF | $K_e$   | 0.042                | V·s/rad |
| Inercia del rotor     | $J$     | $4.0 \times 10^{-6}$ | kg·m²   |
| Inductancia del motor | $L$     | 1.16                 | mH      |

Tabla 3. Parametros de Qube 2.

📚Ejemplo 1:

Queremos que el motor DC del QUBE-Servo 2 siga una velocidad angular deseada de forma rápida y precisa. Para esto, se utilizará un controlador PID clásico en un lazo de retroalimentación.

Usaremos un modelo de primer orden del motor:

$$G(s) = \frac{K}{\tau s + 1}$$

Donde K es 0.8 y 𝜏 es 0.05.

K: Es la ganancia estática, o sea, la velocidad angular en estado estable cuando el motor recibe un voltaje constante para el caso de 1 V, k es 0.8.

τ: Es la constante de tiempo, o sea, cuánto tarda el sistema en llegar al 63% de su valor final después de aplicar el escalón.
En este caso, la curva de respuesta indica que el sistema alcanza el 63% de la velocidad máxima en aproximadamente 0.05 segundos.

Posteriormente se crea un modelo en similunk para ver la respuesta:

![image](https://github.com/user-attachments/assets/f4d25f29-f5b9-49c1-ac5e-c40c62472cf5)

Figura 5. Ejercicio 1 Qube 2.

Donde como respuesta se obtiene:

![image](https://github.com/user-attachments/assets/899be3bf-cd47-421b-b85f-03d7dc345d15)

Figura 6. Ejercicio 1 scope.

Recordar que esta respuesta es sin ninguna perturbacion y sin pendulo, estos y mas aspectos ya en proximos ejercicios se deben de tener en cuenta ya que en un sistema, no todo puede salir perfecto y siempre se van a tener que considerar mas aspectos.

## 4. Simulink

Antes de comenzar a implementar el control sobre el QUBE-Servo 2, es necesario estructurar correctamente el modelo en Simulink para que pueda interactuar con el hardware. Este desarrollo parte de una configuración básica que garantice la comunicación con la planta, la lectura de sensores y el envío de señales de control. A partir de aquí, se incorporan bloques esenciales que permiten construir el lazo de control en tiempo real. 

### 4.1 HIL Initialize

El primer paso es establecer la conexión entre el entorno de Simulink y el QUBE-Servo 2 a través del bloque HIL Initialize, que se encarga de activar la tarjeta de interfaz y preparar el sistema para recibir y enviar datos durante la simulación.

![image](https://github.com/user-attachments/assets/ccab7348-3ee1-4e23-8817-63c2aeb816d3)

Figura 7. HIL Initialize

#### 4.1.1 Configuracion bloque HIL Initialize

![image](https://github.com/user-attachments/assets/ddf522d7-1d07-4f76-b663-6a60fabf678d)

Figura 8. Configuracion HIL Initialize

| Función                            | Descripción                                                                |
| ---------------------------------- | -------------------------------------------------------------------------- |
| Selección del dispositivo          | Permite elegir la tarjeta de adquisición                                   |
| Inicialización de entradas/salidas | Configura los canales analógicos, digitales y PWM                          |
| Reset del hardware                 | Reinicia el hardware cuando se inicia o detiene la simulación              |
| Configuración de reloj             | Define la frecuencia de muestreo y sincronización del hardware             |

Tabla 3. Funciones HIL Initialize

Una primera cosa que se debe tener en cuenta esque vamos a tener en el espacio de Board Identifier dos posibles opciones las cuales colocar, en dado caso que vayamos a usar la planta fisica vamos a dejar ese espacio con un "0" ya que por defecto el saca los datos por el puerto usb, ya si deseamos usar los gemelos digitales tenemos que colocar la siguiente ruta: 

- @tcpip://localhost:18920

Una vez se completan las configuraciones principales del modelo, se procede a ejecutar la simulación. Durante este proceso, es importante verificar que la banda superior de la ventana de Simulink se ilumine en color verde, lo cual indica que la comunicación entre Simulink y el hardware de Quanser se ha establecido correctamente. Este color confirma que el modelo está corriendo en tiempo real y que el sistema está listo para interactuar con la planta física.

> 💡 Nota:
Si la banda aparece en rojo, significa que ocurrió un error crítico y la simulación no ha iniciado. Si aparece en amarillo, suele indicar advertencias relacionadas con la compilación o la conexión con el hardware. En ambos casos, se recomienda revisar los parámetros del bloque HIL Initialize, la selección del dispositivo y los canales activos.

![image](https://github.com/user-attachments/assets/a163f038-d65e-4b6b-8b9b-8ccfe00a5273)

Figura 8. Comunicacion activada

### 4.2 HIL Write Analog

El bloque HIL Write Analog es fundamental dentro del lazo de control, ya que permite enviar señales analógicas desde el modelo de Simulink hacia el hardware del QUBE-Servo 2. Estas señales suelen representar los comandos de control, como una señal PWM para manejar el motor.

Este bloque se conecta comúnmente a la salida del controlador (por ejemplo, un PID) y actúa como la interfaz que traduce la lógica del modelo a una acción física en la planta.

#### 4.2.1 Configuracion bloque Write Analog

| **Función**                        | **Descripción**                                                                |
| ---------------------------------- | ------------------------------------------------------------------------------ |
| Enviar señal de control            | Transmite una señal analógica (como la salida de un PID) hacia el actuador.    |
| Selección de canal                 | Permite especificar el canal analógico a utilizar (ej. canal 0 para el motor). |
| Configuración de voltaje de salida | Define el rango de voltaje permitido (ej. ±5V o ±10V según la planta).         |
| Interfaz hardware-software         | Sirve como puente entre la lógica del modelo y la acción física en el sistema. |
               
Para que el bloque HIL Write Analog funcione correctamente, es fundamental que el nombre del dispositivo coincida exactamente con el utilizado en los demás bloques de hardware (como el HIL Initialize o el HIL Read Encoder). Esta coherencia asegura que todos los bloques estén asociados al mismo hardware y se logre una comunicación efectiva.

Además, se debe configurar el canal analógico correspondiente. En este caso, solo se utiliza un canal, que será el encargado de enviar la señal de voltaje al motor del QUBE-Servo 2. Finalmente, es importante ajustar el tiempo de muestreo (sample time) del bloque, el cual debe estar alineado con el definido para el resto del modelo y con la tasa de simulación deseada.

![image](https://github.com/user-attachments/assets/f5f2ad9b-d420-497d-9db9-62ec21da56f3)

Figura 9. Configuracion HIL Write Analog

![image](https://github.com/rJulian16/APUNTES-CONTROL/blob/ebe98243dbf55546a5c7500b82caaadd5a04d3b7/Corte%203/Imagenes/hola.gif)

Figura 10. Funcionamiento

### 4.3 HIL Read Analog y Read Timebase

#### 4.3.1 HIL Read Analog

El bloque HIL Read Analog permite leer señales analógicas que provienen del hardware hacia el modelo en Simulink. Aunque en el caso del QUBE-Servo 2 este bloque no siempre es necesario , puede ser útil si se trabaja con sensores analógicos como potenciómetros o sensores de fuerza.

Parámetros clave:
Nombre del dispositivo: Debe coincidir con los demás bloques (ej. q8_usb, qube_servo2, etc.).

Canal analógico: Se configura según el canal al que está conectado el sensor.

Sample time: Debe coincidir con el tiempo de muestreo general de la simulación.

>💡 Nota: Si no hay sensores analógicos activos en el sistema, este bloque no es necesario.

#### 4.3.2 HIL Read Timebase

El bloque HIL Read Timebase es esencial cuando se trabaja con lectura de encoders y control en tiempo real. Este bloque permite leer datos a intervalos de tiempo precisos, sincronizados con el hardware.

**¿Para qué se usa?**
Generalmente se utiliza para leer la posición y velocidad angular desde los encoders del QUBE-Servo 2.

**Configuracion**

![image](https://github.com/user-attachments/assets/26d5a735-fc0a-4058-8630-dd1f08f74369)

Figura 11. Configuracion Read Timebase



## 6. Bibliografía

[1] MathWorks, "Simscape Multibody," [En línea]. Disponible: https://la.mathworks.com/products/simscape.html. [Accedido: 06-Mar-2025].

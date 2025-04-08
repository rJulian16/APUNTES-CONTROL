# Control de Movimiento Clase 12 de marzo
Julian Stiven Redondo Chacon & Sebastian Cifuentes Alfonso & David Esteban Vasquez Alarcon
## 1. Simscape
Simscape es una herramienta de MATLAB que se utiliza junto con Simulink para simular sistemas físicos de una manera visual y sencilla. En lugar de escribir ecuaciones manualmente, se pueden construir los modelos usando bloques que representan componentes reales como motores, resistencias o pistones. Una de sus ventajas es que permite conectar estos bloques como si fueran partes de un sistema real, facilitando así la comprensión del comportamiento del sistema completo.
### 1.1 Eslabones
En Simulink, a través del entorno de Simscape Multibody, es posible construir modelos de sistemas mecánicos de manera gráfica y detallada. Uno de los elementos clave en estos sistemas son los eslabones, que funcionan como piezas rígidas encargadas de transmitir movimiento o fuerza dentro de un mecanismo. Estos eslabones forman la estructura básica de mecanismos
Para representar un eslabón, se utiliza comúnmente el bloque Brick Solid, que tiene forma de prisma rectangular y permite personalizar dimensiones, masa, densidad y apariencia visual. Además de este, también se puede emplear el bloque Solid para representar otras formas geométricas. 

💡Ejemplos:

![image](https://github.com/user-attachments/assets/655064ff-0b01-458b-95ab-d37420dcdddb)

Figura 1. Solidos simscape. 

Para representar un eslabón, se utiliza comúnmente el bloque Brick Solid, que tiene forma de prisma rectangular y permite personalizar dimensiones, masa, densidad y apariencia visual. Además de este, también se puede emplear el bloque Solid para representar otras formas geométricas. Los eslabones se conectan entre sí mediante diferentes tipos de uniones o joints, como la Revolute Joint, la Prismatic Joint y la Rigid Transform. Estas conexiones son fundamentales para definir los grados de libertad del sistema y lograr un comportamiento mecánico realista en la simulación.
>🔑 Revolute Joint: Es una unión que permite la rotación relativa entre dos cuerpos alrededor de un solo eje. Es útil para simular movimientos como los de una bisagra o el giro de una rueda. Solo tiene un grado de libertad (rotacional).

>🔑 Prismatic Joint: Esta unión permite el deslizamiento lineal entre dos cuerpos a lo largo de un eje fijo. Se usa para modelar mecanismos que requieren movimiento rectilíneo, como un pistón o un actuador lineal. También tiene un solo grado de libertad, pero lineal.

>🔑Rigid Transform: No es una articulación móvil, sino una conexión rígida que establece una posición y orientación específica entre dos componentes. Sirve para fijar piezas o ajustar la alineación entre bloques en un modelo sin permitir movimiento entre ellos.

💡Ejemplo: Si conectamos los solidos directamente al mundo y generamos la simulacion estos se van a superponerse unos con otros. 

![image](https://github.com/user-attachments/assets/a920c125-b7fa-4968-8601-d74c26678a7a)

Figura 2. Solidos en simulación. 

Para solucionar esto, vamos a usar una de las uniones mencionadas anteriormente, en este caso se va a usar el rigid transform, pero asi como esta, podemos usar cualquiera de las otras conexiones para poder crear nuestros sistemas.

![image](https://github.com/user-attachments/assets/b9ae9fc4-18a9-428c-8d45-d2ece241c45f)

Figura 3. Solidos en simulación conectados con rigid transform. 

### 1.2 Bloque PS Converter (Physical Signal Converter)

En Simscape, el bloque PS Converter, también conocido como Physical Signal Converter, es una herramienta fundamental para la interacción entre los dos tipos de señales que se manejan dentro del entorno: las señales físicas y las señales de Simulink tradicionales.

#### 1.2.1 Función del PS Converter

El PS Converter sirve como un puente entre ambos mundos:

De Simulink a Simscape: Convierte una señal Simulink (por ejemplo, una señal de control o entrada numérica) en una señal física que puede usarse dentro de un modelo Simscape.
De Simscape a Simulink: Cuando se usa en conjunto con el bloque PS-Simulink Converter, permite tomar una magnitud física y convertirla en una señal Simulink para graficarla, procesarla o usarla en un controlador.

#### 1.2.2 Opciones del bloque

Cuando se utiliza el PS Converter, se debe especificar la unidad de la señal física que se desea trabajar.  
Por ejemplo: si se convierte una señal numérica en una velocidad, es necesario indicar que esa señal será en "m/s" (metros por segundo).  
Esto asegura la coherencia de unidades dentro del modelo y evita errores en la simulación.

#### 1.2.3 Relación con otros bloques

El PS Converter generalmente se usa junto con:

Simulink-PS Converter: Para pasar de Simulink a Simscape.
PS-Simulink Converter: Para pasar de Simscape a Simulink.




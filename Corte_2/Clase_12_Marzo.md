# Control de Movimiento Clase 12 de marzo
Julian Stiven Redondo Chacon & Sebastian Cifuentes Alfonso & David Esteban Vasquez Alarcon
# 1. Simscape
Simscape es una herramienta de MATLAB que se utiliza junto con Simulink para simular sistemas físicos de una manera visual y sencilla. En lugar de escribir ecuaciones manualmente, se pueden construir los modelos usando bloques que representan componentes reales como motores, resistencias o pistones. Una de sus ventajas es que permite conectar estos bloques como si fueran partes de un sistema real, facilitando así la comprensión del comportamiento del sistema completo.

# 2. Eslabones
En Simulink, a través del entorno de Simscape Multibody, es posible construir modelos de sistemas mecánicos de manera gráfica y detallada. Uno de los elementos clave en estos sistemas son los eslabones, que funcionan como piezas rígidas encargadas de transmitir movimiento o fuerza dentro de un mecanismo. Estos eslabones forman la estructura básica de mecanismos
Para representar un eslabón, se utiliza comúnmente el bloque Brick Solid, que tiene forma de prisma rectangular y permite personalizar dimensiones, masa, densidad y apariencia visual. Además de este, también se puede emplear el bloque Solid para representar otras formas geométricas. 

💡Ejemplo:

![image](https://github.com/user-attachments/assets/655064ff-0b01-458b-95ab-d37420dcdddb)

Figura 1. Solidos simscape. 

# 3. Uniones y Conexiones en Simscape Multibody

Los eslabones se conectan entre sí mediante diferentes tipos de uniones o joints, como la Revolute Joint, la Prismatic Joint y la Rigid Transform. Estas conexiones son fundamentales para definir los grados de libertad del sistema y lograr un comportamiento mecánico realista en la simulación.
>🔑 Revolute Joint: Es una unión que permite la rotación relativa entre dos cuerpos alrededor de un solo eje. Es útil para simular movimientos como los de una bisagra o el giro de una rueda. Solo tiene un grado de libertad (rotacional).

>🔑 Prismatic Joint: Esta unión permite el deslizamiento lineal entre dos cuerpos a lo largo de un eje fijo. Se usa para modelar mecanismos que requieren movimiento rectilíneo, como un pistón o un actuador lineal. También tiene un solo grado de libertad, pero lineal.

>🔑Rigid Transform: No es una articulación móvil, sino una conexión rígida que establece una posición y orientación específica entre dos componentes. Sirve para fijar piezas o ajustar la alineación entre bloques en un modelo sin permitir movimiento entre ellos.

## 3.1. Rigid Transform

💡Ejemplo: Se crearán varios cuerpos sólidos con diferentes formas y tamaños. A partir de ellos, se aplicarán transformaciones espaciales para ubicarlos en posiciones distintas dentro del modelo, evitando que se sobrepongan entre sí. El objetivo es organizar la distribución de los sólidos utilizando desplazamientos y rotaciones que simulen una estructura mecánica más compleja.

![image](https://github.com/user-attachments/assets/a920c125-b7fa-4968-8601-d74c26678a7a)

Figura 2. Solidos en simulación. 

Para resolver este ejercicio, se utilizará una de las uniones mencionadas anteriormente: el Rigid Transform. Esta herramienta permite aplicar tanto rotaciones como traslaciones a los cuerpos sólidos. En este caso, se trabajará específicamente con el apartado de traslación, con el fin de mover las figuras a lo largo de los ejes X, Y y Z, posicionándolas en distintos puntos del espacio. De esta forma, se evita que los sólidos queden superpuestos y se logra una distribución ordenada dentro del modelo.


![image](https://github.com/user-attachments/assets/b9ae9fc4-18a9-428c-8d45-d2ece241c45f)

Figura 3. Solidos en simulación conectados con rigid transform. 

## 3.2. Revolute Join

💡Ejemplo: Se va a simular un péndulo con forma de barra rectangular, conectado de forma que pueda girar libremente alrededor de un eje fijo. El objetivo es que el sistema permita una rotación completa, similar al movimiento de un péndulo que da vueltas completas sin restricciones.

![image](https://github.com/user-attachments/assets/b98253b6-1776-4aef-89f6-a49134cf6363)

Figura 4. Esquematico ejercicio Revolute Join

El esquemático muestra la presencia de dos sólidos que conforman el sistema. Para organizarlos y definir su comportamiento, se añaden tres bloques adicionales. Primero, se utiliza un Rigid Transform, como en el ejercicio anterior, para posicionar los sólidos de forma que no queden superpuestos, permitiendo una mejor visualización. Luego, se incorpora una Revolute Joint, que será la encargada de permitir el giro del sólido gris. Esta unión se conecta a un costado de la cara trasera del rectángulo, actuando como base del mundo y punto de apoyo para la rotación. Finalmente, se añade una entrada tipo rampa al sistema, con el objetivo de generar un movimiento rotacional continuo, ya que se desea que el sólido gire sin restricciones angulares.

A continuación, se presenta el enlace al modelo desarrollado en Simulink, donde se puede observar el comportamiento del sistema completo en funcionamiento. Este permite visualizar cómo interactúan los sólidos, la rotación generada y el efecto de la entrada aplicada: https://youtu.be/Iz6ljM35qfo

## 3.3. Prismatic Join

💡Ejemplo: En este ejercicio se modelará una esfera que se desplazará a lo largo del eje Z mediante una unión Prismatic Joint. Esta configuración permitirá simular un movimiento lineal vertical controlado, representando así un sistema que puede subir o bajar de forma guiada.

![image](https://github.com/user-attachments/assets/103ceb4c-2c40-4797-896b-5b05a6510921)

Figura 5. Esquematico ejercicio Prismatic Join

Para lograr el movimiento de la esfera en el eje Z, se utiliza una Prismatic Joint, la cual permite el desplazamiento lineal en una sola dirección. En este caso, la unión está alineada con el eje Z para simular un movimiento vertical. A la entrada de esta unión se le conecta una señal tipo seno, lo que provoca que la esfera suba y baje de forma continua y suave, siguiendo el patrón oscilatorio de la onda. Esta configuración permite observar cómo un cuerpo se mueve de manera controlada utilizando señales periódicas como estímulo.

A continuación, se comparte el enlace del modelo de simulación, donde se puede visualizar el desplazamiento de la esfera a lo largo del eje Z. En este se observa cómo la señal seno controla el movimiento ascendente y descendente del sistema en tiempo real.: https://youtu.be/vIKYzzYyOhg

# 4. Bloque PS Converter (Physical Signal Converter)

En Simscape, el bloque PS Converter, también conocido como Physical Signal Converter, es una herramienta fundamental para la interacción entre los dos tipos de señales que se manejan dentro del entorno: las señales físicas y las señales de Simulink tradicionales.

## 4.1. Función del PS Converter

El PS Converter sirve como un puente entre ambos mundos:

De Simulink a Simscape: Convierte una señal Simulink (por ejemplo, una señal de control o entrada numérica) en una señal física que puede usarse dentro de un modelo Simscape.
De Simscape a Simulink: Cuando se usa en conjunto con el bloque PS-Simulink Converter, permite tomar una magnitud física y convertirla en una señal Simulink para graficarla, procesarla o usarla en un controlador.

## 4.2. Opciones del bloque

Cuando se utiliza el PS Converter, se debe especificar la unidad de la señal física que se desea trabajar.  
Por ejemplo: si se convierte una señal numérica en una velocidad, es necesario indicar que esa señal será en "m/s" (metros por segundo).  
Esto asegura la coherencia de unidades dentro del modelo y evita errores en la simulación.

## 4.3. Relación con otros bloques

El PS Converter generalmente se usa junto con:

Simulink-PS Converter: Para pasar de Simulink a Simscape.
PS-Simulink Converter: Para pasar de Simscape a Simulink.

📚Ejercicio: En el siguiente esquematico se ve como las magnitudes fisicas que se generan gracias a los solidos y las distintas uniones que contiene se pueden convertir en una señal simulink, con esto podemos combrobar que nuestro sistema funcione como queremos o que cumpla con los requisitos que se piden. 

![image](https://github.com/user-attachments/assets/45292b2a-e970-4244-a139-d1f69ad8152f)

Figura 6. Solidos en simulación conectados con rigid transform. 

# 5. Ejercicios propuestos en clase:

Durante la sesión se desarrollaron tres ejercicios básicos en Simulink utilizando Simscape Multibody. Cada uno busca representar un tipo diferente de movimiento mecánico, aplicando uniones y bloques específicos para lograrlo. A continuación, se describe brevemente cada ejercicio junto con su solución implementada.

## 📚5.1. Cubo: 

Se modela un cubo que se desplaza a lo largo del eje X, simulando un movimiento lineal horizontal.

![image](https://github.com/user-attachments/assets/e0fce06e-7beb-4cc7-8f03-d2617e17ad83)

Figura 7. Solucion del primer ejercicio. 

Para la solución de este ejercicio, se parte de un esquemático similar al utilizado en el ejercicio del prismatico descrito en el punto 3.3. En este caso, se reemplaza la esfera por un cubo, manteniendo la lógica del movimiento lineal. Dado que el Prismatic Joint está configurado por defecto para operar en el eje Z, se requiere realizar un ajuste para lograr el desplazamiento sobre el eje X. Para ello, se utiliza un bloque Rigid Transform, el cual permite cambiar el sistema de referencia. Se reorienta el sistema de forma que el eje Z se alinee con el eje X, y para asegurar una correcta transformación, también se emparejan los ejes Y con Y, ya que este eje permanece sin cambios. Por último, se conserva la entrada tipo seno, ya que su comportamiento oscilatorio permite visualizar claramente el movimiento del cubo de un lado a otro en el eje deseado.

A continuación, se comparte el enlace al modelo de simulación donde se observa el movimiento del cubo a lo largo del eje X. Gracias a la transformación aplicada y a la señal seno, el cubo oscila horizontalmente, permitiendo visualizar claramente el funcionamiento del sistema y la correcta orientación del desplazamiento: https://youtu.be/f9ET-9DZtIU

## 📚5.2. 3 Eslabones: 

Se modela un sistema compuesto por tres eslabones rectangulares conectados entre sí, formando un marco en forma de “U” invertida. Los dos eslabones laterales se mantienen fijos en sus extremos inferiores y deben girar como péndulos sin restricciones. El eslabón superior (horizontal) debe permanecer conectado a los otros dos, acompañando su movimiento, pero sin rotar, únicamente trasladándose.

![image](https://github.com/user-attachments/assets/7b4a04c7-d034-4146-89db-14a0e780f1e6)

Figura 8. Solucion del segundo ejercicio. 

Para construir este sistema, se utilizan tres sólidos rectangulares. Los eslabones laterales se conectan a la base mediante Revolute Joints, lo que les permite girar libremente como péndulos sin límites angulares. A uno de estos eslabones se le aplica un Rigid Transform para desplazarlo hacia la derecha, evitando que ambos queden alineados en el mismo punto de origen y permitiendo así formar correctamente la estructura en forma de “U”.
El eslabón superior se posiciona entre los extremos superiores de los eslabones laterales y, aunque no rota, acompaña el movimiento mediante una traslación controlada que le permite mantenerse unido a los otros dos. De esta manera, el eslabón horizontal se traslada en sincronía con la oscilación de los laterales, manteniendo la estructura conectada y simulando un marco articulado funcional.

A continuación, se presenta el enlace de la simulación donde se puede observar el comportamiento del sistema articulado. Se aprecia cómo los eslabones laterales oscilan libremente y cómo el eslabón superior se traslada en sincronía, manteniendo la estructura conectada en todo momento: https://youtu.be/z-HsZccP6sc

## 📚5.3. Viela, Manibela, Corredera : 

Se plantea un sistema mecánico compuesto por una biela, una manivela y una corredera. La biela y la manivela están conectadas de forma que pueden rotar entre sí, generando un movimiento continuo. La corredera, por su parte, no rota, sino que se traslada linealmente sobre un eje. El objetivo es representar el funcionamiento típico de este tipo de mecanismo, muy utilizado en sistemas de transmisión mecánica.

![image](https://github.com/user-attachments/assets/f3bad60a-ccca-4c15-9346-a1d68610dc66)

Figura 9. Solucion del tercer ejercicio. 

Para construir este sistema, se modelan tres sólidos rectangulares que representan la manivela, la biela y la corredera. La manivela se conecta a un punto fijo mediante un Revolute Joint, que le permite girar de forma continua. En su otro extremo, se conecta a la biela usando un segundo Revolute Joint, permitiendo que ambas giren de forma sincronizada. Finalmente, la biela se une a la corredera mediante un tercer Revolute Joint, permitiendo que la manivela complete su movimiento rotacional sin afectar la orientación de la corredera.

Para asegurar que todos los componentes estén correctamente alineados en el mismo sistema de coordenadas, se emplean dos bloques Rigid Transform, que ajustan la posición y orientación de los elementos en el espacio. Por último, se utiliza un Prismatic Joint que restringe el movimiento de la corredera únicamente al eje X, permitiendo que esta se desplace linealmente en respuesta a la rotación generada por la manivela. Así, se logra simular con precisión la dinámica del sistema biela-manivela-corredera.

A continuación, se presenta el enlace al modelo del sistema biela-manivela con corredera. En la simulación se observa cómo la rotación de la manivela se transmite a la biela, generando el desplazamiento lineal de la corredera y reproduciendo la dinámica del mecanismo: https://youtu.be/HyWwIMJ60yk

# 6. Conclusiones
- Simscape Multibody permite una representación clara y precisa de sistemas mecánicos complejos, facilitando la visualización y análisis de su comportamiento dinámico mediante la conexión de bloques físicos.
  
- El uso de bloques como Solid, Rigid Transform, Revolute Joint y Prismatic Joint permite diseñar mecanismos articulados y sistemas con grados de libertad específicos, replicando comportamientos reales como rotaciones, traslaciones y restricciones de movimiento.
  
- La correcta implementación de Rigid Transform es fundamental para alinear componentes en el espacio tridimensional y evitar errores en la conexión entre eslabones o sólidos, especialmente cuando se busca representar movimientos en ejes distintos a los predeterminados.
  
- A través de señales de entrada como la onda seno o la rampa, es posible generar movimientos continuos o controlados en los mecanismos, lo que facilita el análisis de respuestas dinámicas y su posible integración con sistemas de control.

# 7. Referencias

[1] MathWorks. (2024). Simscape Multibody Documentation. MATLAB & Simulink. Disponible en: https://www.mathworks.com/help/physmod/sm/

[2] MathWorks. (2024). Modeling Multibody Systems. MATLAB & Simulink Tutorials. Disponible en: https://www.mathworks.com/learn/tutorials/multibody-modeling.html

[3] Palm, W. J. (2013). Modeling, Analysis, and Control of Dynamic Systems (3rd ed.). John Wiley & Sons.

[4] Ogata, K. (2010). Modern Control Engineering (5th ed.). Prentice Hall.

[5] MathWorks. (2024). Simulink Start Page. Disponible en: https://www.mathworks.com/products/simulink.html

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





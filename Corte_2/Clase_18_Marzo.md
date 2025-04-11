# Control de Movimiento Clase 18 de Marzo
Julian Stiven Redondo Chacon & Sebastian Cifuentes Alfonso & David Esteban Vasquez Alarcon

# 1. Perfiles de Movimiento

Los perfiles de movimiento son trayectorias planificadas que definen cómo deben variar las variables de posición, velocidad y aceleración de un sistema mecánico en el tiempo. Estos perfiles son fundamentales en el diseño de sistemas de control de movimiento, ya que permiten que un mecanismo realice desplazamientos suaves, precisos y eficientes, evitando cambios bruscos que podrían causar vibraciones, desgaste prematuro o incluso fallas mecánicas. En el contexto de la simulación con Simulink y Simscape, los perfiles de movimiento se implementan mediante funciones matemáticas o bloques de señal, y se utilizan para alimentar actuadores, servomecanismos u otros componentes dinámicos.

## 1.1. Aplicacion 

Existen dos contextos principales donde se aplican los perfiles de movimiento:

### 1.1.1. Movimiento en un solo eje

Este perfil implica que el sistema solo se mueve en una dirección (por ejemplo, un actuador lineal que se extiende o retrae). Se definen los valores iniciales y finales de posición, y se genera una trayectoria suave que cumpla con condiciones de aceleración y velocidad máximas deseadas.

Los perfiles más comunes son:

**- Trapezoidal:** velocidad constante en el centro del movimiento.

![image](https://github.com/user-attachments/assets/c2830681-f136-4e85-a3b3-4a2812059857)

Figura 1. Ejemplo Perfil trapezoideal.

**-S-curve o polinómico:**: transición más suave entre estados (usado en movimientos delicados).

![image](https://github.com/user-attachments/assets/37514598-c13d-43cf-a613-1892e4248d40)

Figura 2. Ejemplo Perfil S.

Las gráficas típicas en este caso son:

-Posición vs. Tiempo: progresión suave de inicio a fin.

-Velocidad vs. Tiempo: forma trapezoidal o en campana.

-Aceleración vs. Tiempo: picos al inicio y final (acelera y frena).


### 1.1.2. Movimiento multieje

Cuando el sistema debe moverse en más de una dirección al mismo tiempo (por ejemplo, un brazo robótico o un dron), se generan perfiles sincronizados en todos los ejes (X, Y, Z, etc.) para que el movimiento sea coordinado y continuo.

Aquí, los puntos clave del recorrido definen el camino deseado, y los perfiles aseguran que todos los ejes se muevan al ritmo necesario para llegar a cada punto al mismo tiempo, respetando velocidades y aceleraciones máximas.

Las gráficas en cada eje son similares a las del caso de un solo eje, pero se analizan por separado en cada dimensión.

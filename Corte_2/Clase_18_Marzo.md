# Control de Movimiento Clase 18 de Marzo
Julian Stiven Redondo Chacon & Sebastian Cifuentes Alfonso & David Esteban Vasquez Alarcon

# 1. Perfiles de Movimiento

Los perfiles de movimiento son trayectorias planificadas que definen cómo deben variar las variables de posición, velocidad y aceleración de un sistema mecánico en el tiempo. Estos perfiles son fundamentales en el diseño de sistemas de control de movimiento, ya que permiten que un mecanismo realice desplazamientos suaves, precisos y eficientes, evitando cambios bruscos que podrían causar vibraciones, desgaste prematuro o incluso fallas mecánicas. En el contexto de la simulación con Simulink y Simscape, los perfiles de movimiento se implementan mediante funciones matemáticas o bloques de señal, y se utilizan para alimentar actuadores, servomecanismos u otros componentes dinámicos.

## 1.1. Aplicacion 

Existen dos contextos principales donde se aplican los perfiles de movimiento:

### 1.1.1. Movimiento en un solo eje

Este perfil implica que el sistema solo se mueve en una dirección (por ejemplo, un actuador lineal que se extiende o retrae). Se definen los valores iniciales y finales de posición, y se genera una trayectoria suave que cumpla con condiciones de aceleración y velocidad máximas deseadas.

Los perfiles más comunes son:

-Trapezoidal: velocidad constante en el centro del movimiento.

-S-curve o polinómico: transición más suave entre estados (usado en movimientos delicados).

Las gráficas típicas en este caso son:

-Posición vs. Tiempo: progresión suave de inicio a fin.

-Velocidad vs. Tiempo: forma trapezoidal o en campana.

-Aceleración vs. Tiempo: picos al inicio y final (acelera y frena).

📚Ejercicio: Se quiere mover un actuador lineal desde la posición 0 m hasta 2 m en un tiempo total de 3 s. Se desea que el movimiento sea suave, siguiendo un perfil de velocidad tipo trapezoidal.

Parámetros:

-Posición inicial: 0 m

-Posición final: 2 m

-Tiempo total: 3 s

-Aceleración máxima estimada: 2 m/s²

-Velocidad máxima estimada: 1 m/s


### 1.1.2. Movimiento multieje


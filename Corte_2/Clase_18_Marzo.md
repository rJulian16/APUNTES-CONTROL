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

📚Ejercicio 1: Se quiere mover un actuador lineal desde la posición 0 m hasta 2 m en un tiempo total de 3 s. Se desea que el movimiento sea suave, siguiendo un perfil de velocidad tipo trapezoidal.

- Posición inicial: $s_0 = 0$ m  
- Posición final: $s_f = 2$ m  
- Velocidad máxima: $v_{max} = 1$ m/s  
- Aceleración máxima: $a_{max} = 2$ m/s²  

### Cálculos previos:

\[
t_a = \frac{v_{max}}{a_{max}} = \frac{1}{2} = 0.5 \text{ s}
\]  
\[
T = t_a + t_c + t_a = 0.5 + 1.5 + 1 = 3 \text{ s}
\]

---

## Fases del perfil

### Fase 1 – Aceleración constante $(0 \leq t \leq 0.5)$:

\[
a(t) = 2 \quad v(t) = \int a(t)\, dt = 2t \quad s(t) = \int v(t)\, dt = t^2
\]

### Fase 2 – Velocidad constante $(0.5 \leq t \leq 2)$:

\[
a(t) = 0 \quad v(t) = 1 \quad s(t) = 0.25 + 1 \cdot (t - 0.5) = t - 0.25
\]

### Fase 3 – Desaceleración constante $(2 \leq t \leq 3)$:

\[
a(t) = -2 \\
\tau = t - 2 \\
v(\tau) = 1 - 2\tau \\
s(\tau) = 1.75 + \tau - \tau^2 \Rightarrow s(t) = 1.75 + (t - 2) - (t - 2)^2
\]


![image](https://github.com/user-attachments/assets/c5f0342e-8946-44be-8381-3f1607e26a25)

Figura 1.Graficas Ejercicio1

### 1.1.2. Movimiento multieje


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

### Datos iniciales

- Recorrido total: $s_{\text{total}} = 1 \ \text{m}$
- Velocidad máxima: $v_{\text{max}} = 0.5 \ \text{m/s}$
- Aceleración: $a = 1 \ \text{m/s}^2$

### Fases del perfil

#### 1. **Fase de aceleración**

Partimos desde velocidad cero, aplicando aceleración constante.

- Tiempo de aceleración:

$$
t_1 = \frac{v_{\text{max}}}{a} = \frac{0.5}{1} = 0.5 \ \text{s}
$$

- Posición durante esta fase (integrando la velocidad):

$$
s_1(t) = \frac{1}{2} a t^2 = \frac{1}{2}(1)t^2 = 0.5t^2
$$

#### 2. **Fase de velocidad constante**

La velocidad se mantiene constante a $v_{\text{max}}$.

- Posición al final de aceleración:

$$
s(t_1) = s_1(t_1) = 0.5(0.5)^2 = 0.125 \ \text{m}
$$

- Posición durante esta fase (lineal):

$$
s_2(t) = v_{\text{max}} (t - t_1) + s_1(t_1)
$$

Duración de esta fase:

Sabemos que la aceleración y la desaceleración cubren el mismo recorrido, por lo tanto:

$$
s_{\text{constante}} = s_{\text{total}} - 2 \cdot s_1(t_1) = 1 - 2 \cdot 0.125 = 0.75 \ \text{m}
$$

Entonces, la duración de la fase constante es:

$$
t_2 = \frac{0.75}{v_{\text{max}}} = \frac{0.75}{0.5} = 1.5 \ \text{s}
$$

#### 3. **Fase de desaceleración**

Aceleración negativa igual en magnitud a la inicial. Como el movimiento es simétrico:

- Tiempo total:

$$
T = t_1 + t_2 + t_1 = 0.5 + 1.5 + 0.5 = 2.5 \ \text{s}
$$

- Posición durante esta fase (aceleración negativa):

Definimos $\tau = t - (t_1 + t_2)$, que es el tiempo local dentro de esta fase.

$$
s_3(t) = -\frac{1}{2} a \tau^2 + v_{\text{max}} \tau + s_2(t_1 + t_2)
$$

---

### Perfil completo de posición $s(t)$

$$
s(t) =
\begin{cases}
0.5 t^2, & \text{si } 0 \leq t < t_1 \\\\
0.5 (t - t_1) + s_1(t_1), & \text{si } t_1 \leq t < t_1 + t_2 \\\\
-\frac{1}{2} (t - T)^2 + v_{\text{max}} (t - T + t_1) + s(t_1 + t_2), & \text{si } t_1 + t_2 \leq t \leq T
\end{cases}
$$




![image](https://github.com/user-attachments/assets/c5f0342e-8946-44be-8381-3f1607e26a25)

Figura 1.Graficas Ejercicio1

### 1.1.2. Movimiento multieje

Cuando el sistema debe moverse en más de una dirección al mismo tiempo (por ejemplo, un brazo robótico o un dron), se generan perfiles sincronizados en todos los ejes (X, Y, Z, etc.) para que el movimiento sea coordinado y continuo.

Aquí, los puntos clave del recorrido definen el camino deseado, y los perfiles aseguran que todos los ejes se muevan al ritmo necesario para llegar a cada punto al mismo tiempo, respetando velocidades y aceleraciones máximas.

Las gráficas en cada eje son similares a las del caso de un solo eje, pero se analizan por separado en cada dimensión.

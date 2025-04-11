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

- $s_{\text{total}} = 2 \ \text{m}$  
- $T = 3 \ \text{s}$ (tiempo total)  
- Sea $t_1$ el tiempo de aceleración y desaceleración  
- Sea $t_2$ el tiempo de velocidad constante  
- Entonces: $T = 2t_1 + t_2$

La distancia total se reparte así:

- Área bajo la aceleración (triángulo): $s_1 = \frac{1}{2} a t_1^2$
- Área bajo velocidad constante: $s_2 = v_{\text{max}} t_2$
- Pero $v_{\text{max}} = a t_1$

Entonces:

$$
s = 2 \cdot \left( \frac{1}{2} a t_1^2 \right) + a t_1 t_2 = a t_1^2 + a t_1 t_2
$$

Como $t_2 = T - 2t_1$, sustituimos:

$$
2 = a t_1^2 + a t_1 (3 - 2t_1)
$$

Simplificando:

$$
2 = a t_1^2 + 3a t_1 - 2a t_1^2 = -a t_1^2 + 3a t_1
$$

Dividimos ambos lados entre $a$:

$$
\frac{2}{a} = -t_1^2 + 3t_1
$$

Ordenamos:

$$
t_1^2 - 3t_1 + \frac{2}{a} = 0
$$

Ahora elegimos un valor para $t_1$ que haga que la velocidad máxima no sea muy alta y el perfil se vea razonable.

Supongamos que $t_1 = 0.75$ s:

$$
t_2 = 3 - 2 \cdot 0.75 = 1.5 \ \text{s}
$$

Calculamos la aceleración:

$$
s = a \cdot t_1^2 + a \cdot t_1 \cdot t_2 = a (0.75^2 + 0.75 \cdot 1.5) = a (0.5625 + 1.125) = a \cdot 1.6875
$$

Entonces:

$$
2 = a \cdot 1.6875 \Rightarrow a = \frac{2}{1.6875} \approx 1.185 \ \text{m/s}^2
$$

Velocidad máxima:

$$
v_{\text{max}} = a t_1 = 1.185 \cdot 0.75 \approx 0.889 \ \text{m/s}
$$

---

### Perfil de posición $s(t)$

- **Fase 1 (aceleración)**: $0 \leq t < 0.75$

$$
s_1(t) = \frac{1}{2} a t^2 = 0.5925 \cdot t^2
$$

- **Fase 2 (velocidad constante)**: $0.75 \leq t < 2.25$

$$
s_2(t) = v_{\text{max}} (t - 0.75) + s_1(0.75) = 0.889 (t - 0.75) + 0.333
$$

- **Fase 3 (desaceleración)**: $2.25 \leq t \leq 3$

Definimos $\tau = t - 2.25$

$$
s_3(t) = -\frac{1}{2} a \tau^2 + v_{\text{max}} \tau + s_2(2.25)
$$




![image](https://github.com/user-attachments/assets/c5f0342e-8946-44be-8381-3f1607e26a25)

Figura 1.Graficas Ejercicio1

### 1.1.2. Movimiento multieje

Cuando el sistema debe moverse en más de una dirección al mismo tiempo (por ejemplo, un brazo robótico o un dron), se generan perfiles sincronizados en todos los ejes (X, Y, Z, etc.) para que el movimiento sea coordinado y continuo.

Aquí, los puntos clave del recorrido definen el camino deseado, y los perfiles aseguran que todos los ejes se muevan al ritmo necesario para llegar a cada punto al mismo tiempo, respetando velocidades y aceleraciones máximas.

Las gráficas en cada eje son similares a las del caso de un solo eje, pero se analizan por separado en cada dimensión.

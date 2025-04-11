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

- Posición inicial: $s_0 = 0 \ \text{m}$
- Posición final: $s_f = 2 \ \text{m}$
- Tiempo total: $T = 3 \ \text{s}$
- Tiempo de aceleración: $T_{acc} = 1 \ \text{s}$
- Tiempo de velocidad constante (crucero): $T_{cruise} = 1 \ \text{s}$
- Tiempo de desaceleración: $T_{dec} = 1 \ \text{s}$
- Perfil deseado: **Velocidad trapezoidal**
- Tiempo de aceleración y desaceleración: $t_1$
- Tiempo a velocidad constante: $t_2$
  
El perfil trapezoidal tiene **3 fases**:
1. **Aceleración constante**
2. **Velocidad constante**
3. **Desaceleración constante**

La distancia total es el área bajo la curva de velocidad:

$$
s = \int_0^T v(t) \, dt
$$

Separando por fases:

-1. Aceleración ($0 \leq t < t_1$)

$$
v(t) = a \cdot t
$$

$$
s_1(t) = \int_0^{t_1} a \cdot t \, dt = a \cdot \frac{t_1^2}{2}
$$

-2. Velocidad constante ($t_1 \leq t < t_1 + t_2$)

$$
v(t) = v_{\text{max}} = a \cdot t_1
$$

$$
s_2(t) = \int_{t_1}^{t_1 + t_2} a \cdot t_1 \, dt = a \cdot t_1 \cdot t_2
$$

-3. Desaceleración ($t_1 + t_2 \leq t \leq T$)

$$
v(t) = -a(t - T) \quad \text{(bajando desde } v_{\text{max}} \text{ hasta 0)}
$$

$$
s_3(t) = \int_{t_1 + t_2}^{T} -a(t - T) \, dt = a \cdot \frac{t_1^2}{2}
$$

-Distancia total:

$$
s = s_1 + s_2 + s_3 = a \cdot \frac{t_1^2}{2} + a \cdot t_1 \cdot t_2 + a \cdot \frac{t_1^2}{2}
$$

$$
s = a \cdot t_1^2 + a \cdot t_1 \cdot t_2
$$

Reemplazamos $t_2 = T - 2t_1$:

$$
s = a \cdot t_1^2 + a \cdot t_1 (T - 2t_1)
$$

$$
s = a \cdot t_1^2 + a \cdot T \cdot t_1 - 2a \cdot t_1^2 = -a \cdot t_1^2 + a \cdot T \cdot t_1
$$

Factorizamos:

$$
s = a \cdot t_1 (T - t_1)
$$

---

-Sustituimos los valores del enunciado

- $s = 2 \ \text{m}$
- $T = 3 \ \text{s}$

Entonces:

$$
2 = a \cdot t_1 (3 - t_1)
$$

---

-Elegimos $t_1 = 0.75 \ \text{s}$

Entonces:

$$
2 = a \cdot 0.75 (3 - 0.75) = a \cdot 0.75 \cdot 2.25 = a \cdot 1.6875
$$

$$
a = \frac{2}{1.6875} \approx 1.185 \ \text{m/s}^2
$$

Y la velocidad máxima:

$$
v_{\text{max}} = a \cdot t_1 = 1.185 \cdot 0.75 \approx 0.889 \ \text{m/s}
$$

---

-Resumen del perfil

- Aceleración: $a = 1.185 \ \text{m/s}^2$
- Velocidad máxima: $v_{\text{max}} = 0.889 \ \text{m/s}$
- $t_1 = 0.75 \ \text{s}$, $t_2 = 1.5 \ \text{s}$

---

-Posición por tramos

#### 1. $0 \leq t < 0.75$

$$
s(t) = \frac{1}{2} a t^2 = 0.5925 \cdot t^2
$$

-2. $0.75 \leq t < 2.25$

$$
s(t) = v_{\text{max}} (t - 0.75) + s(0.75) = 0.889 (t - 0.75) + 0.333
$$

-3. $2.25 \leq t \leq 3$

Usamos $\tau = t - 2.25$:

$$
s(t) = -\frac{1}{2} a \tau^2 + v_{\text{max}} \cdot \tau + s(2.25) = -0.5925 \cdot \tau^2 + 0.889 \cdot \tau + 1.667
$$


![image](https://github.com/user-attachments/assets/c5f0342e-8946-44be-8381-3f1607e26a25)

Figura 1.Graficas Ejercicio1

### 1.1.2. Movimiento multieje

Cuando el sistema debe moverse en más de una dirección al mismo tiempo (por ejemplo, un brazo robótico o un dron), se generan perfiles sincronizados en todos los ejes (X, Y, Z, etc.) para que el movimiento sea coordinado y continuo.

Aquí, los puntos clave del recorrido definen el camino deseado, y los perfiles aseguran que todos los ejes se muevan al ritmo necesario para llegar a cada punto al mismo tiempo, respetando velocidades y aceleraciones máximas.

Las gráficas en cada eje son similares a las del caso de un solo eje, pero se analizan por separado en cada dimensión.

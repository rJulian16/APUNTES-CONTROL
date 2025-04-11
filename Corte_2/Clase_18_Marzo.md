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

- Posición inicial: $s_0 = 0 \ \text{m}$
- Posición final: $s_f = 2 \ \text{m}$
- Velocidad máxima: $v_{max} = 1 \ \text{m/s}$
- Aceleración máxima: $a_{max} = 2 \ \text{m/s}^2$

---

## Paso 1: Determinar tiempos característicos

### Tiempo de aceleración:

$$
t_a = \frac{v_{max}}{a_{max}} = \frac{1}{2} = 0.5 \ \text{s}
$$

### Distancia recorrida durante aceleración:

Usando la fórmula de movimiento uniformemente acelerado:

$$
s_a = \frac{1}{2} a_{max} t_a^2 = \frac{1}{2} \cdot 2 \cdot (0.5)^2 = 0.25 \ \text{m}
$$

### Longitud del tramo a velocidad constante:

$$
s_c = s_f - 2s_a = 2 - 2 \cdot 0.25 = 1.5 \ \text{m}
$$

### Tiempo a velocidad constante:

$$
t_c = \frac{s_c}{v_{max}} = \frac{1.5}{1} = 1.5 \ \text{s}
$$

### Tiempo total:

$$
T = t_a + t_c + t_a = 0.5 + 1.5 + 0.5 = 2.5 \ \text{s}
$$

---

## Paso 2: Definir el perfil por tramos

### **Fase 1** – Aceleración constante $(0 \leq t \leq 0.5)$

- Aceleración:

$$
a(t) = 2
$$

- Integrando $a(t)$ para obtener $v(t)$:

$$
v(t) = \int a(t) \, dt = \int 2 \, dt = 2t + C_1
$$

Como $v(0) = 0$, entonces $C_1 = 0$:

$$
v(t) = 2t
$$

- Integrando $v(t)$ para obtener $s(t)$:

$$
s(t) = \int 2t \, dt = t^2 + C_2
$$

Como $s(0) = 0$, entonces $C_2 = 0$:

$$
s(t) = t^2
$$

---

### **Fase 2** – Velocidad constante $(0.5 \leq t \leq 2)$

- Aceleración:

$$
a(t) = 0
$$

- Velocidad constante:

$$
v(t) = 1
$$

- Posición:

Como $s(0.5) = (0.5)^2 = 0.25$, entonces:

$$
s(t) = 0.25 + 1 \cdot (t - 0.5) = t - 0.25
$$

---

### **Fase 3** – Desaceleración constante $(2 \leq t \leq 2.5)$

- Aceleración:

$$
a(t) = -2
$$

- Integrando para obtener velocidad:

Sea $\tau = t - 2$:

$$
v(\tau) = \int -2 \, d\tau = -2\tau + C_3
$$

Como $v(0) = 1$, entonces $C_3 = 1$:

$$
v(\tau) = 1 - 2\tau
$$

- Integrando para obtener posición:

$$
s(\tau) = \int (1 - 2\tau) \, d\tau = \tau - \tau^2 + C_4
$$

Como $s(0) = 1.75$ (verificado desde fase 2), entonces $C_4 = 1.75$:

$$
s(\tau) = 1.75 + \tau - \tau^2
$$

Reescribiendo en función de $t$:

$$
s(t) = 1.75 + (t - 2) - (t - 2)^2
$$


![image](https://github.com/user-attachments/assets/c5f0342e-8946-44be-8381-3f1607e26a25)

Figura 1.Graficas Ejercicio1

### 1.1.2. Movimiento multieje


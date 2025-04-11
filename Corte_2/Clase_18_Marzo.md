# Control de Movimiento Clase 18 de Marzo
Julian Stiven Redondo Chacon & Sebastian Cifuentes Alfonso & David Esteban Vasquez Alarcon

# 1. Perfiles de Movimiento

Los perfiles de movimiento son trayectorias planificadas que definen cómo deben variar las variables de posición, velocidad y aceleración de un sistema mecánico en el tiempo. Estos perfiles son fundamentales en el diseño de sistemas de control de movimiento, ya que permiten que un mecanismo realice desplazamientos suaves, precisos y eficientes, evitando cambios bruscos que podrían causar vibraciones, desgaste prematuro o incluso fallas mecánicas. En el contexto de la simulación con Simulink y Simscape, los perfiles de movimiento se implementan mediante funciones matemáticas o bloques de señal, y se utilizan para alimentar actuadores, servomecanismos u otros componentes dinámicos.

💡Ejemplo 1: Movimiento de un actuador lineal en una línea de ensamblaje

Situación:
En una fábrica de ensamblaje de dispositivos electrónicos, un actuador lineal debe mover una pieza desde una estación de trabajo hasta otra ubicada a 2 metros de distancia. El movimiento debe ser rápido pero sin generar vibraciones que puedan dañar componentes delicados.

Solución:
Para lograr un movimiento rápido pero suave, se utiliza un perfil de velocidad trapezoidal. Este perfil permite acelerar progresivamente, mantener una velocidad constante durante la mayor parte del trayecto, y desacelerar suavemente antes de llegar. Así se evita una aceleración o frenado brusco que podría afectar el producto.

![image](https://github.com/user-attachments/assets/d921f6a0-6080-485e-94d9-b19c7d069d16)

Figura 1. Ejemplo 1.

💡Ejemplo 2: Brazo Robotico

Situación:
Un brazo robótico de seis ejes debe tomar un objeto y colocarlo en una caja. El movimiento involucra rotaciones y desplazamientos de varios motores en diferentes ejes, y todos deben llegar a su destino exactamente al mismo tiempo para que el agarre y la liberación sean precisos.

Solución:
En este caso, se utilizan perfiles de movimiento multi-eje sincronizados, como los perfiles tipo S. Estos aseguran que todos los ejes aceleren y desaceleren suavemente, y lo hagan de forma coordinada, manteniendo la trayectoria y evitando esfuerzos desiguales entre motores.

![image](https://github.com/user-attachments/assets/d947daf6-8a0e-4348-942b-77614af6ab2a)

Figura 2. Ejemplo 2.

# 2. Conceptos Basicos

>🔑 Posicion: La posición describe el lugar en el que se encuentra un objeto en el espacio en un instante determinado.
Se representa comúnmente como una función del tiempo: 
$$s(t)$$.
La posición puede estar en una dimensión (línea recta), dos (plano) o tres (espacio). Es el punto de referencia para determinar el movimiento.

>🔑 Velocidad: La velocidad es la rapidez con la que cambia la posición de un objeto respecto al tiempo.
Es la derivada de la posición respecto al tiempo:
$$v(t) = \frac{ds(t)}{dt}$$.
Indica qué tan rápido y en qué dirección se mueve el objeto. Puede ser positiva o negativa dependiendo del sentido del movimiento. Tambien en su expresion integral: $$s(t) = \int v(t) \, dt$$

>🔑 Aceleracion: La aceleración mide la variación de la velocidad en el tiempo. Es la derivada de la velocidad, o la segunda derivada de la posición:
$$a(t) = \frac{dv(t)}{dt} = \frac{d^2s(t)}{dt^2}$$. Representa qué tan rápido cambia la velocidad del objeto. Tambien en su expresion integral: $$v(t) = \int a(t) \, dt$$

# 3. Curvas de Posición, Velocidad y Aceleración

En el análisis del movimiento de un sistema (como un actuador lineal), es fundamental comprender cómo se relacionan las curvas de:

Posición $s(t)$

Velocidad $v(t)$

Aceleración $a(t)$

Estas curvas no solo nos dan información visual del comportamiento del sistema, sino que también nos ayudan a derivar o integrar para obtener los parámetros clave del movimiento.


# 4. Reglas Geometricas

Para el desarrollo y análisis de perfiles de movimiento, es fundamental tener en cuenta ciertos principios que rigen la dinámica de los sistemas. Estas reglas aseguran transiciones suaves, físicas y controlables entre los distintos estados del perfil:

🔹 Relación entre Posición y Velocidad
La posición en un instante de tiempo está determinada por el área bajo la curva de velocidad hasta ese instante.

Esto significa que integrar la velocidad en un intervalo de tiempo nos da el desplazamiento total.

🔹 Relación entre Velocidad y Aceleración
La aceleración corresponde a la pendiente de la curva de velocidad.

Es decir, la derivada de la velocidad con respecto al tiempo nos da la aceleración en cada instante.

De este analisis salen las siguiente ecuaciones: 

  $$v = v_0 + a(t - t_0)$$

  $$s = s_0 + \frac{1}{2}(t - t_0)(v_0 + a(t - t_0))$$
  
# 5. Aplicacion 

Existen dos contextos principales donde se aplican los perfiles de movimiento:

## 5.1. Movimiento en un solo eje

Este perfil implica que el sistema solo se mueve en una dirección (por ejemplo, un actuador lineal que se extiende o retrae). Se definen los valores iniciales y finales de posición, y se genera una trayectoria suave que cumpla con condiciones de aceleración y velocidad máximas deseadas.

Los perfiles más comunes son:

**- Trapezoidal:** velocidad constante en el centro del movimiento.

![image](https://github.com/user-attachments/assets/8dff2912-d1b8-4c78-a4c7-2f3d1f4395a3)

Figura 1. Ejemplo Perfil trapezoideal.

**-S-curve o polinómico:**: transición más suave entre estados (usado en movimientos delicados).

![image](https://github.com/user-attachments/assets/61773fc7-b84e-483c-8e30-284714517549)

Figura 2. Ejemplo Perfil S.

Las gráficas típicas en este caso son:

-Posición vs. Tiempo: progresión suave de inicio a fin.

-Velocidad vs. Tiempo: forma trapezoidal o en campana.

-Aceleración vs. Tiempo: picos al inicio y final (acelera y frena).

| Característica                  | Perfil Trapezoidal                                 | Perfil en S (Sigmoidal)                           |
|-------------------------------|----------------------------------------------------|---------------------------------------------------|
| **Forma de la curva**         | Lineal con tres segmentos: aceleración constante, velocidad constante, y desaceleración constante | Curva suave en forma de "S"                        |
| **Transiciones**              | Bruscas entre segmentos                            | Suaves y continuas                                |
| **Continuidad de la aceleración** | Discontinua                                        | Continua                                           |
| **Uso común**                 | Movimientos simples donde la suavidad no es prioritaria | Sistemas que requieren movimientos suaves (robots, CNC, etc.) |
| **Vibraciones**               | Más propenso a generar vibraciones mecánicas       | Minimiza vibraciones y choques                    |
| **Fácil de implementar**      | Sí, requiere menos cálculos                        | Requiere más cálculos matemáticos o funciones especiales |
| **Precisión de control**      | Menor precisión dinámica en aplicaciones sensibles | Mayor precisión y confort de movimiento           |
| **Derivadas continuas**       | Velocidad continua pero aceleración discontinua    | Derivadas suaves hasta la aceleración             |



📚Ejercicio 1 Perfil Trapezoidal:

**Situación:** Se desea mover un actuador desde la posición $s_0 = 0\,m$ hasta $s = 2\,m$ en $T = 3\,s$, usando un perfil trapezoidal con aceleración constante de $a = 1\,m/s^2$ durante $1\,s$, seguido de velocidad constante y luego frenado.

-Ecuaciones fundamentales:

$$v(t) = \int a(t)\,dt = a \cdot t + v_0$$

$$s(t) = \int v(t)\,dt = \int (a \cdot t + v_0)\,dt = \frac{1}{2} a t^2 + v_0 t + s_0$$

### Parámetros iniciales

- $s_0 = 0\,m$
- $s_f = 2\,m$
- $T = 3\,s$
- Aceleración y desaceleración simétricas
- Tiempo de aceleración: $t_a = 1\,s$
- Tiempo de velocidad constante: $t_c = 1\,s$
- Tiempo de desaceleración: $t_d = 1\,s$

### Ecuaciones del perfil trapezoidal

Fase de aceleración ($0 \leq t < t_a$):

$$a(t) = a = \text{cte}$$

$$v(t) = \int a\,dt = a\,t$$

$$s(t) = \int v(t)\,dt = \int a\,t\,dt = \frac{1}{2}a\,t^2$$

Fase de velocidad constante ($t_a \leq t < t_a + t_c$):

$$v(t) = v_{max} = a\,t_a$$

$$s(t) = s(t_a) + v_{max}(t - t_a)$$

Fase de desaceleración ($t_a + t_c \leq t \leq T$):

$$a(t) = -a$$

$$v(t) = v_{max} - a(t - t_a - t_c)$$

$$s(t) = s(t_a + t_c) + v_{max}(t - t_a - t_c) - \frac{1}{2}a(t - t_a - t_c)^2$$

### Cálculo de aceleración

Se usa la relación de área bajo la curva de velocidad para igualar al desplazamiento total:

$$\text{Área total} = \frac{1}{2}v_{max}t_a + v_{max}t_c + \frac{1}{2}v_{max}t_d = s_f$$

Sabemos que:

$$v_{max} = a\,t_a$$

Entonces:

$$s_f = \frac{1}{2}(a\,t_a)t_a + (a\,t_a)t_c + \frac{1}{2}(a\,t_a)t_d$$

Sustituyendo $t_a = t_c = t_d = 1\,s$, y $s_f = 2\,m$:

$$2 = \frac{1}{2}a + a + \frac{1}{2}a = 2a$$

$$a = 1\,\frac{m}{s^2}$$

Entonces:

$$v_{max} = a\,t_a = 1\,\frac{m}{s}$$

### Resultados

- Aceleración: $a = 1\,m/s^2$
- Velocidad máxima: $v_{max} = 1\,m/s$
- Desplazamiento total: $2\,m$
- Tiempo total: $3\,s$

![image](https://github.com/user-attachments/assets/a97b90f2-5033-4010-9b59-07393d286de2)

Figura 3. Resultados MATLAB .

### 1.1.2. Movimiento multieje

Cuando el sistema debe moverse en más de una dirección al mismo tiempo (por ejemplo, un brazo robótico o un dron), se generan perfiles sincronizados en todos los ejes (X, Y, Z, etc.) para que el movimiento sea coordinado y continuo.

Aquí, los puntos clave del recorrido definen el camino deseado, y los perfiles aseguran que todos los ejes se muevan al ritmo necesario para llegar a cada punto al mismo tiempo, respetando velocidades y aceleraciones máximas.

Las gráficas en cada eje son similares a las del caso de un solo eje, pero se analizan por separado en cada dimensión.

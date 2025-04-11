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

### 3.1. Curva de Aceleración $a(t)$
Es el punto de partida en un perfil de movimiento.

Una aceleración constante se ve como una línea recta horizontal.

Si la aceleración cambia de forma suave, la curva será más compleja (como en un perfil en S).

La pendiente de la velocidad depende directamente de la forma de esta curva.

![image](https://github.com/user-attachments/assets/df78c7ff-38b7-4dfe-b571-cb65743c22e5)

Figura 3. Curva de aceleracion.

### 3.2. Curva de Velocidad $v(t)$

Se obtiene integrando la aceleración:

$$v(t) = \int a(t)dt$$

Si la aceleración es constante, la velocidad será una línea recta inclinada (como en un triángulo).

Si la aceleración varía suavemente, la curva de velocidad toma forma de una “S” suave.

El área bajo esta curva representa el desplazamiento total (posición final).

![image](https://github.com/user-attachments/assets/c949a54f-daaf-49be-8008-207c37e50d07)

Figura 4. Curva de velocidad.

### 3.3. Curva de Posición $s(t)$

Se obtiene integrando la velocidad:

$$s(t) = \int v(t)dt$$

La posición representa cómo cambia el lugar ocupado por el sistema con respecto al tiempo.

Si la velocidad tiene forma de triángulo, la posición tendrá una curva suave de tipo parábola.

En un perfil trapezoidal o en S, la posición muestra un crecimiento continuo con diferentes pendientes (más suave o más rápida).

![image](https://github.com/user-attachments/assets/f6546be5-84b9-45b1-84eb-a43d4d0d1181)

Figura 5. Curva de Posición.

### 3.4. Relación entre las curvas

| **Curva**     | **Se obtiene desde...**                                  | **Qué representa**                          |
|---------------|----------------------------------------------------------|---------------------------------------------|
| Aceleración   | Derivada de la velocidad                                 | Cambio instantáneo de la velocidad          |
| Velocidad     | Derivada de la posición / Integral de la aceleración     | Rapidez de cambio de la posición            |
| Posición      | Integral de la velocidad                                 | Lugar ocupado en el tiempo                  |

📚Ejercicio 1: Se analiza un perfil de movimiento con el objetivo de determinar la posición y la aceleración del sistema en el instante de tiempo t = 5 segundos.

![image](https://github.com/user-attachments/assets/97b5634a-9deb-40dc-a397-2a68ef1d28c3)

Figura 6. Ejercicio 1 planteado en clase.

La clave para encontrar la aceleración está en la gráfica de velocidad, ya que la aceleración es la pendiente de esta curva.

A partir de la gráfica:

- La velocidad varía de 0 in/s a 10 in/s entre t = 0 s y t = 5 s.

La pendiente (aceleración constante) se calcula como:

$$a(t) = \frac{\Delta v}{\Delta t} = \frac{10 - 0}{5 - 0} = 2 \ \text{in/s}^2$$

La posición se obtiene integrando la función de velocidad.  
Si la velocidad sigue una ley lineal (perfil acelerado constante), entonces:

$$v(t) = a t = 2t$$

Integrando para obtener la posición:

$$s(t) = \int v(t) \, dt = \int 2t \, dt = t^2 + C$$

Asumiendo posición inicial $s(0) = 0$ (es decir, $C = 0$):

$$s(t) = t^2$$

Por lo tanto, en $t = 5$ s:

$$s(5) = 5^2 = 25 \ \text{in}$$

-Resultados Finales

- **Aceleración en t = 5 s:**  
  $$a = 2 \ \text{in/s}^2$$

- **Posición en t = 5 s:**  
  $$s = 25 \ \text{in}$$

📚Ejercicio 2 planteado en clase: Un eje esta viajando a una velocidad de 10cm/s. En t=5s empieza a disminuir la velocidad como se ve en el perfil. Cual es la posicion del eje cuando se detiene? Asuma que empieza a desacelerar a 25 cm.

![image](https://github.com/user-attachments/assets/be76edb4-1120-4307-b665-84ce6e163dd7)

Figura 7. Ejercicio 2 planteado en clase.

La pendiente de la velocidad es la aceleración:

$$a = \frac{-10 \ \frac{cm}{s} \cdot \frac{1 \ m}{100 \ cm}}{10s - 5s} = \frac{-0.1 \ \frac{m}{s}}{5s} = -0.01 \ \frac{m}{s^2}$$

El área del perfil de velocidad triangular es la posición alcanzada en t = 15 s:

$$S_0 = \frac{1}{2} \cdot (15s - 5s) \cdot 0.1 \ \frac{m}{s} = 0.5 \ m$$

-Resultado

- **Aceleración:**  
  $$a = -0.01 \ \frac{m}{s^2}$$

- **Posición en t = 15 s:**  
  $$S = 0.5 \ m$$

📚Ejercicio 3 planteado en clase: Un eje(axis) lineal comienza su movimiento desde el reposo en la posicion 0, con una aceleracion de 2m/s. Despues de moverse durante 5 s, cual es la posicion del eje (axis) 

![image](https://github.com/user-attachments/assets/95ee6970-40f9-4483-a75b-7bfa67169128)

Figura 8. Ejercicio 3 planteado en clase.

En la gráfica se representa el comportamiento de la velocidad del eje en función del tiempo, partiendo desde el reposo y aumentando de manera lineal debido a una aceleración constante. Esto se evidencia por la forma recta de la curva, cuya pendiente representa la aceleración aplicada al sistema. Este tipo de análisis permite visualizar de forma clara cómo la aceleración influye directamente en el cambio de velocidad y, por lo tanto, en el desplazamiento total del eje a lo largo del tiempo.

📚Ejercicio 4: Un eje lineal parte desde el reposo y desde la posición $s_0 = 0$ con una aceleración constante de $$a = 1.5\ \text{m/s}^2$$ ¿Cuál será su velocidad después de transcurridos $$t = 5\ \text{s}$$?

- Aceleración: $a = 1.5\ \text{m/s}^2$
- Tiempo: $t = 5\ \text{s}$
- Velocidad inicial: $v_0 = 0\ \text{m/s}$

-**Formulas y Cálculos**

-Velocidad

$$v(t) = a \cdot t$$

Sustituyendo valores:

$$v(5) = 1.5 \cdot 5 = 7.5\ \text{m/s}$$

![image](https://github.com/user-attachments/assets/fbed9178-0705-4a50-a42e-bf10b5bdf0bb)

Figura 9. Ejercicio 4.

En este ejercicio, se observa una gráfica de velocidad que aumenta de manera lineal hasta cierto punto y luego se mantiene constante, lo cual representa un perfil de velocidad tipo trapezoidal. Esta forma indica que el sistema primero acelera, luego mantiene una velocidad constante y eventualmente desacelera (si se continuara la gráfica). Este tipo de perfiles son comunes en sistemas industriales que requieren movimientos suaves pero eficientes. A partir de esta gráfica, se puede determinar tanto la aceleración (analizando la pendiente en la primera fase) como la posición total (calculando el área bajo la curva de velocidad).

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

Figura 10. Ejemplo Perfil trapezoideal.

**-S-curve o polinómico:**: transición más suave entre estados (usado en movimientos delicados).

![image](https://github.com/user-attachments/assets/1e7c0226-80ae-4156-a672-7594c70468b5)

Figura 11. Ejemplo Perfil S.

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

Se desea mover un actuador desde la posición $s_0 = 0\,m$ hasta $s = 2\,m$ en $T = 3\,s$, usando un perfil trapezoidal con aceleración constante de $a = 1\,m/s^2$ durante $1\,s$, seguido de velocidad constante y luego frenado.

### Ecuaciones fundamentales:

$$v(t) = \int a(t)dt = a \cdot t + v_0$$

$$s(t) = \int v(t)dt = \int (a \cdot t + v_0)dt = \frac{1}{2} a t^2 + v_0 t + s_0$$

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

![image](https://github.com/user-attachments/assets/67a50597-cdee-4028-94ac-55a3462eb472)

Figura 12. Resultados MATLAB ejercicio 1 .

📚 Ejercicio 2 Perfil S: 

Se desea mover un actuador lineal desde la posición inicial $s_0 = 0\,m$ hasta $s_f = 2\,m$ en un tiempo total de $T = 3\,s$. A diferencia del perfil trapezoidal, en este caso se utiliza un perfil suavizado tipo "S", donde la aceleración no es constante, sino que cambia suavemente para evitar impactos dinámicos.


### Parámetros iniciales

- $s_0 = 0\,m$
- $s_f = 2\,m$
- $T = 3\,s$
- Perfil suavizado con transición progresiva de aceleración
- Se usará una función sigmoidal tipo seno para suavizar el perfil

### Funciones del perfil tipo S

Utilizamos funciones trigonométricas para suavizar la aceleración y generar curvas suaves de velocidad y posición:

#### Velocidad

$$v(t) = v_{max} \cdot \left( \frac{1 - \cos\left( \frac{\pi t}{T} \right)}{2} \right)$$

#### Posición

$$s(t) = \int v(t) \,dt = \frac{v_{max} T}{2\pi} \left( t - \frac{T}{2\pi} \sin\left( \frac{2\pi t}{T} \right) \right)$$

#### Aceleración

$$a(t) = \frac{dv(t)}{dt} = \frac{\pi v_{max}}{2T} \cdot \sin\left( \frac{\pi t}{T} \right)$$

### Cálculo de $v_{max}$

La posición final $s(T) = 2\,m$ se logra con:

$$s(T) = \int_0^T v(t)\,dt = v_{max} \cdot \left( \frac{T}{2} \right)$$

Entonces:

$$2 = v_{max} \cdot \frac{3}{2}$$

$$v_{max} = \frac{4}{3}\,m/s$$

### Resultados

- Velocidad máxima: $v_{max} = \frac{4}{3}\,m/s$
- Tiempo total: $T = 3\,s$
- Desplazamiento total: $s = 2\,m$
- Movimiento suave y continuo sin saltos en la aceleración

### Ventajas del perfil S

- Evita impactos dinámicos por aceleraciones bruscas
- Ideal para movimientos de precisión o con restricciones mecánicas
- Aumenta la vida útil de componentes al reducir vibraciones

![image](https://github.com/user-attachments/assets/ae6c24a0-bfa1-4fef-ab4e-49a34cce9c59)

Figura 13. Resultados Matlab ejercicio 2.

### 1.1.2. Movimiento multieje

Cuando el sistema debe moverse en más de una dirección al mismo tiempo (por ejemplo, un brazo robótico o un dron), se generan perfiles sincronizados en todos los ejes (X, Y, Z, etc.) para que el movimiento sea coordinado y continuo.

Aquí, los puntos clave del recorrido definen el camino deseado, y los perfiles aseguran que todos los ejes se muevan al ritmo necesario para llegar a cada punto al mismo tiempo, respetando velocidades y aceleraciones máximas.

Las gráficas en cada eje son similares a las del caso de un solo eje, pero se analizan por separado en cada dimensión.

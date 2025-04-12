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

| Variable | Significado |
|----------|-------------|
| tm    | **Tiempo total de movimiento**: tiempo total desde el inicio hasta el final del desplazamiento. |
| ta    | **Tiempo de aceleración**: duración de la fase en la que el sistema acelera desde reposo hasta la velocidad máxima. |
| vm    | **Velocidad máxima**: velocidad constante máxima alcanzada durante el perfil de movimiento. |
| td    | **Tiempo de desaceleración**: duración de la fase donde el sistema frena hasta detenerse. |
| tc    | **Tiempo de velocidad constante**: intervalo en el que el sistema mantiene su velocidad máxima sin acelerar ni frenar. |
| a     | **Aceleración**: cambio de la velocidad respecto al tiempo (positiva o negativa según la fase). |
| s     | **Desplazamiento total**: distancia recorrida durante todo el perfil de movimiento. |

Tabla1. Conceptos de variables basicas.

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

Tabla2.Relacion entre las curvas

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

![image](https://github.com/user-attachments/assets/0bfd5ad9-80fa-458f-9004-4fcad3089441)

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

Tabla3.Comparacion de perfiles trapezoidal y S

📚Ejercicio 5 Perfil Trapezoidal:

Se desea mover un actuador desde la posición $s_0 = 0\,m$ hasta $s = 2\,m$ en $T = 3\,s$, usando un perfil trapezoidal con aceleración constante de $a = 1\,m/s^2$ durante $1\,s$, seguido de velocidad constante y luego frenado.

#### Ecuaciones fundamentales:

$$v(t) = \int a(t)dt = a \cdot t + v_0$$

$$s(t) = \int v(t)dt = \int (a \cdot t + v_0)dt = \frac{1}{2} a t^2 + v_0 t + s_0$$

#### Parámetros iniciales

- $s_0 = 0\,m$
- $s_f = 2\,m$
- $T = 3\,s$
- Aceleración y desaceleración simétricas
- Tiempo de aceleración: $t_a = 1\,s$
- Tiempo de velocidad constante: $t_c = 1\,s$
- Tiempo de desaceleración: $t_d = 1\,s$

#### Ecuaciones del perfil trapezoidal

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

#### Cálculo de aceleración

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

#### Resultados

- Aceleración: $a = 1\,m/s^2$
- Velocidad máxima: $v_{max} = 1\,m/s$
- Desplazamiento total: $2\,m$
- Tiempo total: $3\,s$

![image](https://github.com/user-attachments/assets/67a50597-cdee-4028-94ac-55a3462eb472)

Figura 12. Resultados MATLAB ejercicio 1 .

📚 Ejercicio 6 Perfil S: 

Se desea mover un actuador lineal desde la posición inicial $s_0 = 0\,m$ hasta $s_f = 2\,m$ en un tiempo total de $T = 3\,s$. A diferencia del perfil trapezoidal, en este caso se utiliza un perfil suavizado tipo "S", donde la aceleración no es constante, sino que cambia suavemente para evitar impactos dinámicos.


#### Parámetros iniciales

- $s_0 = 0\,m$
- $s_f = 2\,m$
- $T = 3\,s$
- Perfil suavizado con transición progresiva de aceleración
- Se usará una función sigmoidal tipo seno para suavizar el perfil

#### Funciones del perfil tipo S

Utilizamos funciones trigonométricas para suavizar la aceleración y generar curvas suaves de velocidad y posición:

##### Velocidad

$$v(t) = v_{max} \cdot \left( \frac{1 - \cos\left( \frac{\pi t}{T} \right)}{2} \right)$$

##### Posición

$$s(t) = \int v(t) \,dt = \frac{v_{max} T}{2\pi} \left( t - \frac{T}{2\pi} \sin\left( \frac{2\pi t}{T} \right) \right)$$

##### Aceleración

$$a(t) = \frac{dv(t)}{dt} = \frac{\pi v_{max}}{2T} \cdot \sin\left( \frac{\pi t}{T} \right)$$

#### Cálculo de $v_{max}$

La posición final $s(T) = 2\,m$ se logra con:

$$s(T) = \int_0^T v(t)\,dt = v_{max} \cdot \left( \frac{T}{2} \right)$$

Entonces:

$$2 = v_{max} \cdot \frac{3}{2}$$

$$v_{max} = \frac{4}{3}\,m/s$$

#### Resultados

- Velocidad máxima: $v_{max} = \frac{4}{3}\,m/s$
- Tiempo total: $T = 3\,s$
- Desplazamiento total: $s = 2\,m$
- Movimiento suave y continuo sin saltos en la aceleración

#### Ventajas del perfil S

- Evita impactos dinámicos por aceleraciones bruscas
- Ideal para movimientos de precisión o con restricciones mecánicas
- Aumenta la vida útil de componentes al reducir vibraciones

![image](https://github.com/user-attachments/assets/ae6c24a0-bfa1-4fef-ab4e-49a34cce9c59)

Figura 13. Resultados Matlab ejercicio 2.

### 5.2 Movimiento multieje

Cuando el sistema debe moverse en más de una dirección al mismo tiempo (por ejemplo, un brazo robótico o un dron), se generan perfiles sincronizados en todos los ejes (X, Y, Z, etc.) para que el movimiento sea coordinado y continuo.

Aquí, los puntos clave del recorrido definen el camino deseado, y los perfiles aseguran que todos los ejes se muevan al ritmo necesario para llegar a cada punto al mismo tiempo, respetando velocidades y aceleraciones máximas.

Las gráficas en cada eje son similares a las del caso de un solo eje, pero se analizan por separado en cada dimensión.

📚 Ejercicio 7: Movimiento multieje simple (2 ejes)

#### Enunciado:
Un sistema de 2 ejes (X y Y) debe mover una herramienta desde el punto **(0,0)** hasta el punto **(2,3)** metros, en un tiempo total de **4 segundos**, partiendo desde el reposo y usando perfiles **trapezoidales** independientes en cada eje.

##### Supuestos:
- Movimiento independiente en cada eje.
- Aceleración y desaceleración simétrica.
- Perfil trapezoidal para cada eje.
- Aceleración constante durante cada fase.
- Tiempo total: $T = 4\,s$
- Tiempo de aceleración: $t_a = 1\,s$
- Tiempo de velocidad constante: $t_c = 2\,s$
- Tiempo de desaceleración: $t_d = 1\,s$


#### Ecuaciones usadas:

$$s_f = \frac{1}{2}a\,t_a^2 + v_{max}\,t_c + \frac{1}{2}a\,t_d^2$$

Como $v_{max} = a \cdot t_a$, entonces:

$$s_f = a \left(\frac{1}{2}t_a^2 + t_a t_c + \frac{1}{2}t_d^2\right)$$

#### Cálculos:

##### Eje X:
- Desplazamiento total: $s_{fx} = 2\,m$

$$2 = a_x \cdot \left(0.5 + 2 + 0.5\right) = a_x \cdot 3 \Rightarrow a_x = \frac{2}{3}\,m/s^2$$

$$v_{max\_x} = a_x \cdot t_a = \frac{2}{3} \cdot 1 = 0.667\,m/s$$

##### Eje Y:
- Desplazamiento total: $s_{fy} = 3\,m$

$$3 = a_y \cdot 3 \Rightarrow a_y = 1\,m/s^2$$

$$v_{max\_y} = a_y \cdot t_a = 1 \cdot 1 = 1\,m/s$$


#### Resultados finales:

| Eje | $a$ (m/s²) | $v_{max}$ (m/s) | $s_f$ (m) |
|-----|------------|------------------|-----------|
| X   | 0.667      | 0.667            | 2         |
| Y   | 1          | 1                | 3         |

Tabla4.Resultados Ejercicio 7.

![image](https://github.com/user-attachments/assets/c121d561-ae3c-440d-ad99-c587ddd5aecc)

Figura 14. Matlab ejercicio multieje.

# 6. Ejercicios planteados en clase:

📚 Ejercicio 8: Análisis de trayectoria de un eje con tornillo sin fin

Se desea calcular el tiempo total de movimiento \( t_m \) de un eje accionado por un motor con tornillo sin fin. El movimiento sigue un perfil trapezoidal: aceleración constante, velocidad constante, y luego desaceleración simétrica.

### Parámetros y relaciones iniciales

Las aceleraciones de inicio y frenado son iguales, por lo tanto:

$$t_a = t_d = \frac{v_m}{a}$$

Condiciones iniciales:

$$t_0 = 0, \quad v_0 = 0, \quad s_0 = 0$$

Durante la fase de aceleración (\( 0 < t < t_a \)):

$$s(t) = \int_0^{t_a} a\,dt = \left. \frac{1}{2} a t^2 \right|_0^{t_a} = \frac{1}{2} a t_a^2$$

### Cálculo del recorrido total \( L \)

El desplazamiento total se puede calcular sumando las áreas bajo la curva de velocidad en el perfil trapezoidal:

$$L = \frac{t_a v_m}{2} + t_m v_m + \frac{t_d v_m}{2}$$

Sabiendo que \( t_a = t_d \), simplificamos:

$$L = v_m (t_a + t_m)$$

De ahí, despejamos el tiempo de velocidad constante:

$$t_m = \frac{L}{v_m} - t_a$$

### Fases del movimiento

#### Fase 1: Aceleración \( (0 < t < t_a) \)

Condiciones iniciales:

$$t_0 = 0, \quad v_0 = 0, \quad s_0 = 0$$

Posición:

$$s(t) = \int_0^{t} at \, dt = \frac{1}{2} at^2$$

#### Fase 2: Velocidad constante \( (t_a \leq t < t_a + t_m) \)

$$v(t) = v_m$$

$$s(t) = s(t_a) + v_m (t - t_a)$$

#### Fase 3: Desaceleración \( (t_a + t_m < t < t_{total}) \)

Condiciones iniciales:

$$t_0 = t_a + t_m, \quad v_0 = v_m, \quad s_0 = s(t_a + t_m)$$

Posición:

$$s(t) = s(t_a + t_m) + \int_{t_a + t_m}^{t} \left[ -a(t - (t_a + t_m)) + v_m \right] dt$$

Resolviendo:

$$s(t) = s(t_a + t_m) + \left[ v_m t - \frac{1}{2} a (t - (t_a + t_m))^2 \right]_{t_a + t_m}^{t}$$

📚 Ejercicio 9 planteado en clase: Movimiento de un eje en un robot Gantry

El eje \( x \) de un robot Gantry debe moverse \( 10\,\text{cm} \). La máxima aceleración permitida en este eje es de \( 1\,\text{cm/s}^2 \). Si se desea mover el eje a una velocidad máxima de \( 2\,\text{cm/s} \), ¿cuánto tiempo tomará hacer este movimiento?

### Cálculos

Tiempo de aceleración y desaceleración:

$$t_a = t_d = \frac{v_m}{a} = \frac{2\,\text{cm/s}}{1\,\text{cm/s}^2} = 2\,\text{s}$$

Tiempo de velocidad constante:

$$t_m = \frac{L}{v_m} - t_a = \frac{10\,\text{cm}}{2\,\text{cm/s}} - 2\,\text{s} = 3\,\text{s}$$

Tiempo total de movimiento:

$$t_{total} = t_a + t_m + t_d = 2\,\text{s} + 3\,\text{s} + 2\,\text{s} = 7\,\text{s}$$

### Resultado

El movimiento tomará **7 segundos**.

![image](https://github.com/user-attachments/assets/4aa5d379-cd3a-4aab-a68f-67785494b3d7)

Figura 15. Matlab ejercicio 9.

📚 Ejercicio 10: Cálculo de desplazamientos a partir del perfil de velocidad

Dado el perfil de velocidad de un eje, se desea calcular el desplazamiento en tres intervalos ($S_A$, $S_B$, $S_C$) utilizando reglas geométricas y el método analítico.

### 1. Reglas Geométricas

**$S_A$ (de 0 a 0.5 s):**  
Área de un triángulo:

$$S_A = \frac{1}{2} \cdot \text{base} \cdot \text{altura} = \frac{1}{2} \cdot 0.5\,\text{s} \cdot 2\,\text{cm/s} = 0.5\,\text{cm}$$

**$S_B$ (de 0.5 a 5.5 s):**  
Área de un rectángulo:

$$S_B = \text{base} \cdot \text{altura} = (5.5 - 0.5)\,\text{s} \cdot 2\,\text{cm/s} = 10\,\text{cm}$$

**$S_C$ (de 5.5 a 6 s):**  
Área de un triángulo:

$$S_C = \frac{1}{2} \cdot (6 - 5.5)\,\text{s} \cdot 2\,\text{cm/s} = 0.5\,\text{cm}$$

### 2. Método Analítico

**$S_A$ (de 0 a 0.5 s):**  
La velocidad varía linealmente: \( v(t) = 4t \)

$$S_A = \int_0^{0.5} 4t\,dt = \left[2t^2\right]_0^{0.5} = 0.5\,\text{cm}$$

**$S_B$ (de 0.5 a 5.5 s):**  
Velocidad constante: \( v(t) = 2 \)

$$S_B = \int_{0.5}^{5.5} 2\,dt = \left[2t\right]_{0.5}^{5.5} = 10\,\text{cm}$$

**$S_C$ (de 5.5 a 6 s):**  
Velocidad decreciente: \( v(t) = -4t + 24 \)

$$S_C = \int_{5.5}^{6} (-4t + 24)\,dt = \left[-2t^2 + 24t\right]_{5.5}^{6} = 0.5\,\text{cm}$$

### Resultados

$$S_A = 0.5 \text{ cm}$$
$$S_B = 10 \text{ cm}$$
$$S_C = 0.5 \text{ cm}$$

![image](https://github.com/user-attachments/assets/3e247d13-b955-4600-8e20-f65c9ebfe393)

Figura 16. Matlab ejercicio 10.

# 7. Comparacion entre perfil S y perfil S puro

-**Pefil S puro**

![image](https://github.com/user-attachments/assets/4c507b64-41ca-4ffe-8eb5-eddbf8bf0c6a)

Figura 17. Perfil S puro.

-**Perfil S mixto**

![image](https://github.com/user-attachments/assets/56865f83-1765-47e9-bfad-9ee8a7e94a3c)

Figura 18. Perfil S mixto


| Característica                  | Perfil S Puro                                           | Perfil S Mixto                                          |
|-------------------------------|---------------------------------------------------------|--------------------------------------------------------|
| **Forma de aceleración**       | Continua y suave (jerk constante)                       | Combinación de jerk y aceleración constante            |
| **Discontinuidades**           | Ninguna (jerk es constante en transición)              | Presenta transiciones entre fases con jerk y sin jerk |
| **Aceleración máxima ($a_{max}$)** | Alcanzada de forma suave                                | Alcanzada rápidamente y mantenida en fase constante    |
| **Jerk ($j$)**                 | Constante durante transiciones                          | Discontinuo: fases con y sin jerk                     |
| **Suavidad del movimiento**    | Alta                                                    | Media                                                  |
| **Complejidad matemática**     | Alta (requiere integración continua)                    | Media (mezcla de integración simple y jerk constante) |
| **Tiempo total de movimiento** | Puede ser más largo si se busca suavidad extrema       | Generalmente más corto que el S puro                  |
| **Uso típico**                 | Robótica de precisión, sistemas con mínima vibración   | Aplicaciones industriales estándar                    |

Tabla5. Comparacion entre perfiles S.

# 8. Modelo Matemático del Perfil en S (Velocidad)

En los perfiles de movimiento tipo "S", se busca suavizar los cambios bruscos de aceleración, lo cual se logra modelando la **velocidad** como una función cuadrática del tiempo. Este enfoque permite generar trayectorias suaves y continuas para sistemas mecánicos como motores, actuadores o ejes en CNC.

## Función general de la velocidad

La función de velocidad se define como:

$$v(t) = c_1 t^2 + c_2 t + c_3$$

Donde:

- \( c_1 \), \( c_2 \) y \( c_3 \) son constantes que definen la forma del perfil.
- \( t \) es el tiempo.
- Esta es una parábola (función cuadrática), lo cual garantiza una transición suave entre fases del movimiento.

## Derivadas de la velocidad

A partir de la función de velocidad, se pueden obtener otras magnitudes importantes como la **aceleración** y el **jerk** (variación de la aceleración).

### Aceleración:

La aceleración es la derivada de la velocidad respecto al tiempo:

$$a(t) = \frac{dv(t)}{dt} = 2c_1 t + c_2$$

Esto implica que la aceleración cambia linealmente con el tiempo, lo cual es característico de los perfiles en S.

### Jerk:

El jerk (sacudida) es la derivada de la aceleración respecto al tiempo:

$$j(t) = \frac{da(t)}{dt} = 2c_1$$

En este caso, el jerk es constante, lo cual ayuda a reducir vibraciones o impactos en los sistemas mecánicos.


## Usos y Aplicaciones

Este modelo permite diseñar trayectorias donde la aceleración cambia suavemente, lo cual es esencial para:

- Proteger componentes mecánicos del desgaste.
- Mejorar el confort en aplicaciones como robótica o automatización.
- Optimizar el rendimiento dinámico del sistema.

Este tipo de perfiles se utiliza ampliamente en aplicaciones como:
- Servomecanismos.
- Control de ejes en máquinas CNC.
- Sistemas mecatrónicos donde se requiere precisión y suavidad en el movimiento.

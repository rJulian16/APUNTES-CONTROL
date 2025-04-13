# Control de Movimiento Clase 12 de Marzo
Julian Stiven Redondo Chacon & Sebastian Cifuentes Alfonso & David Esteban Vasquez Alarcon

## 1. Introducción a la Temática

### 1.1 Sistemas de Transmisión

Los sistemas de transmisión son el conjunto de componentes interconectados que permiten la transferencia y modificación del movimiento y la potencia mecánica. Estos sistemas pueden incluir elementos como engranajes, poleas y correas, cadenas, ejes, embragues, frenos y convertidores de torque. La elección del sistema de transmisión adecuado depende de factores como la potencia a transmitir, la relación de velocidad requerida, la distancia entre la fuente y la carga, las condiciones ambientales y los costos. Un sistema de transmisión bien diseñado asegura que la potencia se entregue de manera eficiente y controlada a la carga.

### 1.2 Diseño de Transmisión

El diseño de transmisión es una disciplina fundamental en la ingeniería mecánica que se encarga de la concepción, cálculo y optimización de los elementos encargados de transferir potencia mecánica desde una fuente (como un motor) hacia un actuador o carga. Un buen diseño de transmisión busca maximizar la eficiencia, durabilidad y rendimiento del sistema, cumpliendo con los requerimientos específicos de la aplicación en términos de velocidad, torque y potencia. La correcta selección de los componentes y su configuración es crucial para el funcionamiento óptimo de cualquier máquina o sistema mecánico.

### 1.3 ¿Por qué es importante el diseño de la transmisión?

Cuando se diseña un sistema que tiene que mover algo (una herramienta, una carga, un brazo robótico, etc.), no basta con elegir un motor. Es necesario seleccionar una transmisión adecuada que:

- **Aumente o reduzca velocidad**
- **Multiplique el torque** si se necesita más fuerza
- **Transforme el tipo de movimiento** (rotacional → lineal)
- **Asegure estabilidad y precisión**

> 📌 En resumen: la transmisión conecta el "músculo" (motor) con el "movimiento real" (la carga).

**Problemas comunes si no se diseña bien:**
- El motor no da suficiente torque
- El sistema es lento o impreciso
- Hay vibraciones o resonancia
- Se gasta energía de más

📚Ejercicio 1:

Imaginemos que necesitamos diseñar un sistema de transmisión para reducir la velocidad de un motor eléctrico desde 1750 RPM hasta una velocidad de salida de 350 RPM. El motor tiene una potencia de 5 kW y el sistema debe ser lo más compacto y eficiente posible.

En este caso, uno de los primeros pasos en el diseño sería determinar la **relación de transmisión** requerida:

$$i = \frac{\omega_{entrada}}{\omega_{salida}} = \frac{1750 \ RPM}{350 \ RPM} = 5$$

Esto significa que necesitamos un sistema de transmisión que reduzca la velocidad en un factor de 5. Podríamos lograr esto utilizando diferentes tipos de transmisiones, como:

* **Engranajes:** Un par de engranajes con una relación de número de dientes de 5:1 (por ejemplo, un engranaje conductor con 20 dientes y un engranaje conducido con 100 dientes).
* **Poleas y Correas:** Un sistema de poleas donde el diámetro de la polea conducida sea 5 veces mayor que el diámetro de la polea motriz.
* **Reductores de Velocidad:** Un dispositivo compacto que internamente utiliza engranajes para lograr la reducción de velocidad deseada.

La elección del tipo de transmisión dependerá de otros factores como el espacio disponible, el costo, la eficiencia requerida y la carga a la que se va a conectar el sistema.

### 1.4 Uso de MATLAB en el Diseño de Transmisión:

Para problemas de diseño más complejos, se pueden utilizar herramientas de software como MATLAB. MATLAB permite:

* **Modelado y Simulación:** Crear modelos matemáticos del sistema de transmisión y simular su comportamiento bajo diferentes condiciones de carga y velocidad.
* **Análisis de Fuerzas y Torques:** Calcular las fuerzas y torques que actúan sobre los diferentes componentes del sistema.
* **Optimización:** Optimizar los parámetros de diseño (como el número de dientes de los engranajes, los diámetros de las poleas, etc.) para cumplir con los requerimientos de rendimiento y eficiencia.
* **Análisis Dinámico:** Estudiar la respuesta dinámica del sistema, incluyendo la inercia reflejada y las vibraciones.


## 2. Conceptos Básicos

Antes de profundizar en los detalles del diseño y los sistemas de transmisión, es importante tener claros algunos conceptos fundamentales:

>🔑**Torque (T):** Es una medida de la fuerza que puede hacer que un objeto gire alrededor de un eje. Se mide en Newton-metro (Nm).

>🔑**Velocidad Angular (ω):** Es la tasa de cambio del ángulo de un objeto en rotación. Se mide en radianes por segundo (rad/s) o revoluciones por minuto (RPM).

>🔑**Potencia (P):** Es la tasa a la que se realiza el trabajo o se transfiere energía. En sistemas rotacionales, se relaciona con el torque y la velocidad angular mediante la fórmula:
    $$P = T \cdot \omega$$

>🔑**Inercia (J):** Es la resistencia de un objeto a cambiar su estado de movimiento de rotación. Depende de la masa y la distribución de la masa con respecto al eje de rotación. Se mide en kilogramo-metro cuadrado (kg·m²).

>🔑**Relación de Transmisión (i):** Es la relación entre la velocidad angular de entrada y la velocidad angular de salida de un sistema de transmisión. Puede ser una relación de reducción (velocidad de salida menor que la de entrada) o de aumento (velocidad de salida mayor que la de entrada).
    $$i = \frac{\omega_{entrada}}{\omega_{salida}}$$

>🔑**Eficiencia (η):** Es la relación entre la potencia de salida y la potencia de entrada de un sistema. Siempre es menor o igual a 1 (o 100%) debido a las pérdidas por fricción y otros factores.
    $$\eta = \frac{P_{salida}}{P_{entrada}}$$

## 3. Requerimientos de Diseño

El diseño de un sistema de transmisión debe cumplir con una serie de requerimientos específicos de la aplicación. Algunos de los requerimientos más comunes incluyen:

* **Transmisión de Potencia:** El sistema debe ser capaz de transmitir la potencia requerida desde la fuente hasta la carga sin fallar ni sobrecalentarse.
* **Relación de Velocidad Deseada:** El sistema debe proporcionar la relación de velocidad necesaria para que la carga opere a la velocidad requerida. Esto puede implicar una reducción o un aumento de la velocidad.
* **Eficiencia:** El sistema debe minimizar las pérdidas de energía durante la transmisión para optimizar el consumo y evitar el sobrecalentamiento.
* **Durabilidad y Vida Útil:** Los componentes del sistema deben ser capaces de soportar las cargas y las condiciones de operación durante la vida útil esperada.
* **Costo:** El costo del sistema, incluyendo los materiales, la fabricación y el mantenimiento, debe ser aceptable para la aplicación.
* **Espacio y Peso:** Las dimensiones y el peso del sistema deben ser compatibles con las restricciones de la aplicación.
* **Nivel de Ruido y Vibración:** En muchas aplicaciones, es importante minimizar el ruido y la vibración generados por el sistema de transmisión.
* **Mantenimiento:** El sistema debe ser fácil de mantener y reparar.
* **Seguridad:** El diseño debe garantizar la seguridad de los operarios y del entorno.

Tambien existen diferentes situaciones las cuales pueden surgir en el diseño:

| Tipo | Datos Conocidos                       | Objetivo / Tamaño a Encontrar |
|------|---------------------------------------|------------------------------|
| 1    | Movimiento de carga deseado          | Transmisión y motor          |
| 2    | Motor y transmisión existentes       | Movimiento de carga resultante |
| 3    | Motor existente, movimiento de carga deseado | Transmisión                  |
| 4    | Movimiento de carga deseado, transmisión | Motor                      |

Tabla 1. Problemas a solucionar.

## 4. Inercia y Torque en Sistemas de Transmisión

### 4.1 Inercia Reflejada

Cuando se tiene un sistema de transmisión, la inercia de la carga o de un componente en el lado de salida se "refleja" al lado de entrada (por ejemplo, al eje del motor) modificada por la relación de transmisión. Esto es importante para analizar la respuesta dinámica del sistema.

La inercia reflejada ($J_{ref}$) de una carga con inercia $J_{L}$ a través de una relacion de transmisión (N) se calcula como:

$$J_{r} = J_{L} \cdot N^2$$

Esto significa que si la velocidad se reduce (i > 1), la inercia reflejada en el lado de alta velocidad es menor.

### 4.2 Torque Reflejado (Torque de Carga Reflejado)

De manera similar, el torque de carga ($T_{L}$) que actúa en el lado de salida se refleja al lado de entrada como un torque requerido adicional para mover la carga. El torque de carga reflejado ($T_{ref}$) se calcula como:

$$T_{ref} = \frac{T_{L}}{\eta}$$

Esto permite adaptar el sistema para reducir el esfuerzo del motor o ajustar el comportamiento dinámico.

## 5. Engranajes

Los engranajes son componentes fundamentales en muchos sistemas de transmisión debido a su capacidad para transmitir potencia con una relación de velocidad precisa y alta eficiencia.

### 5.1 Relación de Engranajes

La relación de transmisión ($N$) en un par de engranajes es un parámetro fundamental que determina cómo se modifica la velocidad y el torque entre el engranaje conductor (el que recibe la potencia) y el engranaje conducido (el que entrega la potencia). Matemáticamente, esta relación se define como el cociente entre el número de dientes ($Z$) del engranaje conducido y el número de dientes del engranaje conductor, que también es igual a la relación entre sus diámetros ($D$):

$$N = \frac{Z_{conducido}}{Z_{conductor}} = \frac{\omega_{conducido}}{\omega_{conductor}}$$

Esta relación de transmisión tiene un impacto directo en el comportamiento del sistema. Como se resume en la siguiente tabla:

| Condición de la Relación \( N \) | Comportamiento del Sistema                 |
|----------------------------------|--------------------------------------------|
| \( N > 1 \)                      | Disminuye la velocidad, aumenta el torque  |
| \( N < 1 \)                      | Aumenta la velocidad, disminuye el torque  |
| \( N = 1 \)                      | No hay cambios en velocidad ni torque      |

Tabla 2. Relacion de engranajes. 

En esencia, una relación de transmisión mayor que 1 implica una reducción de velocidad y un aumento proporcional del torque (idealmente, sin pérdidas). Por el contrario, una relación menor que 1 resulta en un aumento de la velocidad y una disminución del torque. Cuando la relación es igual a 1, la velocidad y el torque se transmiten sin modificación entre los engranajes.

📚 Ejercicio 2:

Un motor eléctrico gira a una velocidad de 1200 RPM y está conectado a un sistema de dos engranajes. El engranaje conectado directamente al motor (engranaje conductor) tiene 30 dientes. Este engranaje engrana con un segundo engranaje (engranaje conducido) que tiene 90 dientes.

-**Parámetros Iniciales:**

* Velocidad del motor ($\omega_{motor}$) = 1200 RPM
* Número de dientes del engranaje conductor ($Z_{conductor}$) = 30
* Número de dientes del engranaje conducido ($Z_{conducido}$) = 90

-**Preguntas:**

1.  ¿Cuál es la relación de transmisión del sistema de engranajes?
2.  ¿Cuál es la velocidad de rotación del engranaje conducido?
3.  Si el motor produce un torque de 10 Nm, ¿cuál sería el torque en el engranaje conducido (asumiendo una eficiencia del 100%)?

-**Solución:**

- **Cálculo de la relación de transmisión ($N$):**

    La relación de transmisión se calcula utilizando la fórmula:

    $$N = \frac{Z_{conducido}}{Z_{conductor}}$$

    Sustituyendo los valores:

    $$N = \frac{90 \ dientes}{30 \ dientes} = 3$$

    Por lo tanto, la relación de transmisión del sistema es 3.

- **Cálculo de la velocidad de rotación del engranaje conducido ($\omega_{conducido}$):**

    Sabemos que la relación de transmisión también se puede expresar en términos de las velocidades angulares:

    $$N = \frac{\omega_{conductor}}{\omega_{conducido}}$$

    Donde $\omega_{conductor}$ es la velocidad del motor. Despejando la velocidad del engranaje conducido:

    $$\omega_{conducido} = \frac{\omega_{conductor}}{N}$$

    Sustituyendo los valores:

    $$\omega_{conducido} = \frac{1200 \ RPM}{3} = 400 \ RPM$$

    La velocidad de rotación del engranaje conducido es de 400 RPM.

- **Cálculo del torque en el engranaje conducido ($T_{conducido}$):**

    En un sistema ideal sin pérdidas (eficiencia del 100%), la potencia de entrada es igual a la potencia de salida ($P_{entrada} = P_{salida}$). Como la potencia se relaciona con el torque y la velocidad angular ($P = T \cdot \omega$), podemos escribir:

    $$T_{conductor} \cdot \omega_{conductor} = T_{conducido} \cdot \omega_{conducido}$$

    También sabemos que $\frac{\omega_{conductor}}{\omega_{conducido}} = N$, por lo que $\omega_{conducido} = \frac{\omega_{conductor}}{N}$. Sustituyendo esto en la ecuación de potencia:

    $$T_{conductor} \cdot \omega_{conductor} = T_{conducido} \cdot \frac{\omega_{conductor}}{N}$$

    Despejando el torque en el engranaje conducido:

    $$T_{conducido} = T_{conductor} \cdot N$$

    Sustituyendo los valores:

    $$T_{conducido} = 10 \ Nm \cdot 3 = 30 \ Nm$$

    El torque en el engranaje conducido sería de 30 Nm.

### 5.2 Otros Aspectos Importantes de los Engranajes

* **Tipos de Engranajes:** Existen diferentes tipos de engranajes (rectos, helicoidales, cónicos, sinfín, etc.), cada uno con sus propias características y aplicaciones.
* **Módulo:** Es una medida del tamaño de los dientes del engranaje. Los engranajes que engranan deben tener el mismo módulo.
* **Paso Diametral:** Otra medida del tamaño de los dientes, inversamente proporcional al módulo.
* **Fuerzas en los Engranajes:** La transmisión de potencia a través de los engranajes genera fuerzas de contacto entre los dientes, las cuales deben ser consideradas en el diseño para asegurar la resistencia y durabilidad de los engranajes.
* **Eficiencia de los Engranajes:** Los engranajes bien lubricados tienen una alta eficiencia, generalmente entre el 95% y el 99% por etapa.


# 6. Matlab

## 6.1 Common Gear Constraint

🔑>El bloque Common Gear Constraint en Simscape Multibody simula la conexión de dos engranajes rotatorios. Asegura que sus velocidades de giro estén relacionadas por sus tamaños (radios o dientes), sin necesidad de dibujar los dientes. Para usarlo, debes indicar el tamaño de cada engranaje.

![image](https://github.com/user-attachments/assets/242d3cf4-9ba7-4a34-890c-bd83f3773d5a)

Figura 1. Bloque Gear Matlab.

### 6.2 Funcionamiento y Conexión del Bloque Common Gear Constraint:

El bloque Common Gear Constraint actúa como una unión virtual entre dos cuerpos rígidos rotatorios, representando la interacción de un par de engranajes. Para utilizarlo correctamente, debes seguir estos puntos clave:

-**Conexión a Cuerpos Rígidos:** El bloque tiene dos puertos de conexión, típicamente etiquetados como "Base" y "Follower". Cada uno de estos puertos debe conectarse a un sistema de coordenadas (Coordinate System) que esté fijado a uno de los cuerpos rígidos que representan los engranajes. Estos cuerpos rígidos deben tener al menos un grado de libertad rotacional alrededor del eje de giro de los engranajes.

Configuración de Parámetros: Al hacer doble clic en el bloque Common Gear Constraint, se abre un diálogo donde puedes configurar sus parámetros. Los más importantes son:

-**Constraint Type** (Tipo de Restricción): Puedes definir la relación de transmisión de varias maneras:

-**By base radii** (Por radios base): Especificas el radio base de cada engranaje. La relación de transmisión es la relación inversa de estos radios.

-**By number of teeth** (Por número de dientes): Especificas el número de dientes de cada engranaje. La relación de transmisión es la relación del número de dientes del seguidor (follower) entre el número de dientes de la base (base).

-**By gear ratio** (Por relación de engranajes): Especificas directamente la relación de transmisión entre el seguidor y la base.

-**Base Radius** (Radio Base) / Number of Teeth (Número de Dientes): Dependiendo del tipo de restricción seleccionado, deberás proporcionar los valores 
correspondientes para cada puerto (Base y Follower).

-**Follower to Base Ratio** (Relación Seguidor a Base): Si eliges "By gear ratio", introduces directamente este valor. Un valor mayor que 1 significa que el seguidor gira más rápido que la base.

-**Direction of Rotation** (Dirección de Rotación): Puedes invertir la dirección de rotación relativa entre los engranajes si es necesario, utilizando las opciones "Follower rotates opposite to base" o ajustando los signos en la relación de transmisión.

-**Mecánica Interna:** Internamente, el bloque Common Gear Constraint aplica fuerzas y torques a los cuerpos conectados para asegurar que sus velocidades angulares cumplan con la relación definida por los parámetros. Esto se logra mediante la formulación de ecuaciones de restricción que el solver de Simscape Multibody resuelve durante la simulación.

📚Ejercicio 3 planteado en clase:

Crea un modelo en Simscape Multibody que represente dos engranajes cilíndricos (Engranaje A y Engranaje B) conectados mediante una restricción de engranaje común. Cada engranaje debe poder rotar libremente alrededor de un eje fijo con respecto al marco mundial. Impulsa el Engranaje A con una velocidad angular constante. Observa y analiza la rotación del Engranaje B en relación con el Engranaje A, verificando la relación de transmisión impuesta por la restricción.

![image](https://github.com/user-attachments/assets/4f493900-ee82-4f15-9f7b-99ce291f1cab)

Figura 2. Ejercicio 3 Matlab

Creamos los Bricks Solid que representan físicamente cada engranaje, dándoles forma y masa. Para que puedan girar de manera realista, usamos Revolute Joint, que son como los ejes sobre los que cada engranaje puede dar vueltas; los bloques Rigid Transform nos ayudan a colocar estos ejes donde queremos. La magia de la conexión entre los engranajes la hace el bloque Common Gear Constraint: este bloque es como una "ley física" que le dice al simulador que las rotaciones de los dos engranajes deben estar sincronizadas según sus tamaños, igual que en un mecanismo real. Para poner el sistema en movimiento, usamos una fuente Constant Angular Velocity conectada a uno de los engranajes, actuando como un motor que lo hace girar. Finalmente, para ver cómo se mueve el otro engranaje, colocamos un Angular Velocity Sensor en él y conectamos ese sensor a un Scope, que nos mostrará gráficamente su velocidad a lo largo del tiempo. E

Puedes ver el funcionamiento de este modelo en el siguiente video: https://youtu.be/SZpUC3Usogc

# 7. Eficiencia en Sistemas de Transmisión

Un sistema **eficiente** es aquel que logra el movimiento deseado con el menor consumo posible de energía. La eficiencia de un sistema de transmisión se ve afectada por varios factores relacionados directamente con su diseño y operación:

* Lubricación adecuada: Una lubricación apropiada de los componentes móviles (engranajes, rodamientos, cadenas) reduce la fricción y, por lo tanto, las pérdidas de energía en forma de calor.
* Selección de componentes de alta calidad: Utilizar elementos de transmisión (engranajes, poleas, correas, rodamientos) diseñados para una alta eficiencia minimiza las pérdidas inherentes de cada componente.
* Alineación precisa: Asegurar una correcta alineación entre los diferentes elementos de la transmisión (ejes, engranajes, poleas) reduce la fricción y el desgaste innecesario, mejorando la eficiencia.
* Mantenimiento regular: Un mantenimiento adecuado, que incluye la limpieza, lubricación y ajuste de los componentes, ayuda a mantener la eficiencia del sistema a lo largo del tiempo.
* Condiciones de operación: Evitar operar el sistema bajo cargas o velocidades extremas para las que no fue diseñado puede prevenir pérdidas de eficiencia y prolongar la vida útil de los componentes.

La eficiencia ($\eta$) de un sistema de transmisión se define como la relación entre la potencia de salida ($P_{salida}$) y la potencia de entrada ($P_{entrada}$):

$$\eta = \frac{P_{salida}}{P_{entrada}}$$

Lograr una alta eficiencia en el diseño de la transmisión es fundamental para optimizar el consumo energético y el rendimiento general del sistema mecánico.

# 8. Inercia Total en Sistemas de Transmisión

La **inercia total** ($J_{total}$) que enfrenta el motor es la suma de varias componentes:

$$J_{total} = J_{motor} + J_{transmisión} + J_{carga\_reflejada}$$

Donde:

* $J_{motor}$ es la inercia del rotor del motor.
* $J_{transmisión}$ es la inercia de los elementos de transmisión (engranajes, poleas, etc.) referida al eje del motor.
* $J_{carga\_reflejada}$ es la inercia de la carga reflejada al eje del motor. Si la relación de transmisión es $N = \frac{\omega_{entrada}}{\omega_{salida}}$, entonces:
    $$J_{carga\_reflejada} = \frac{J_{carga}}{N^2}$$
    O, utilizando la notación de la otra imagen donde $N$ podría ser la relación de salida a entrada:
    $$J_{r} = J_{L} \cdot N^2$$
    **Nota:** Asegúrate de usar la definición de $N$ consistente con tus apuntes. Si $N = \frac{\omega_{entrada}}{\omega_{salida}}$, la primera fórmula es la correcta para reflejar la inercia al lado de entrada.

La inercia total influye directamente en la aceleración, la estabilidad del sistema y la elección del motor. Un sistema con alta inercia requerirá más torque para lograr la misma aceleración.

# 9. Relación de Inercia en Sistemas de Transmisión

La **relación de inercia** entre la carga reflejada y el motor es clave para el rendimiento:

$$R_i = \frac{J_{carga\_reflejada}}{J_{motor}}$$

* Una relación baja mejora la respuesta, pero puede requerir motores grandes.
* Una relación alta puede ser útil para movimientos lentos, aunque reduce la eficiencia.

Se busca mantener esta relación dentro de un rango adecuado para lograr un equilibrio entre respuesta y consumo. Generalmente, los fabricantes de motores proporcionan recomendaciones para la relación de inercia óptima según la aplicación.

📚Ejercicio 4 propuesto en clase: Cálculo de la Relación de Inercia

El sistema en la figura usa un engranaje PN023 de Apex Dynamics. Este tiene una relación de 5:1, una inercia reflejada a la entrada de 0.1 Kg - cm² y una eficiencia del 97%. El motor es un Quantum QB02301 NEMA tamaño 23 de Allied Motion Technologies, con una inercia en el rotor de $1.5 \times 10^{-5} \text{ Kg - m}^2$. La inercia de la carga es $10 \times 10^{-4} \text{ Kg - m}^2$. Encuentre la relación de inercia.

-**Solución:**

Primero, necesitamos calcular la inercia de la carga reflejada al eje del motor. La fórmula para la inercia de la carga reflejada ($J_{load \rightarrow M}$) es:

$$J_{load \rightarrow M} = \frac{J_{load}}{\eta N_{GB}^2}$$

Donde:
* $J_{load}$ es la inercia de la carga.
* $\eta$ es la eficiencia del reductor (Gearbox).
* $N_{GB}$ es la relación de transmisión del reductor.

Sustituyendo los valores dados:
* $J_{load} = 10 \times 10^{-4} \text{ Kg - m}^2$
* $\eta = 0.97$
* $N_{GB} = 5$

$$J_{load \rightarrow M} = \frac{10 \times 10^{-4} \text{ Kg - m}^2}{0.97 \cdot 5^2} = \frac{10 \times 10^{-4}}{0.97 \cdot 25} = \frac{10 \times 10^{-4}}{24.25} \approx 4.124 \times 10^{-5} \text{ Kg - m}^2$$

> 📌Nota: La inercia reflejada del reductor a la entrada ($0.1 \text{ Kg - cm}^2$) ya está dada. Necesitamos convertirla a Kg - m²:

$$0.1 \text{ Kg - cm}^2 \times \left( \frac{1 \ m}{100 \ cm} \right)^2 = 0.1 \times 10^{-4} \text{ Kg - m}^2 = 1.0 \times 10^{-5} \text{ Kg - m}^2$$

Ahora, calculamos la inercia total reflejada al motor ($J_R$). La fórmula proporcionada en la imagen parece tener una pequeña variación, sumando la inercia del reductor reflejada a la entrada directamente:

$$J_R = \frac{J_{on \ motor \ shaft} + J_{load \rightarrow M} + J_{GB \rightarrow M}}{J_m}$$

Sin embargo, la inercia reflejada del reductor ya está dada a la entrada, por lo que la fórmula más directa para la relación de inercia sería:

$$R_i = \frac{J_{load \rightarrow M} + J_{GB\_reflejada\_entrada}}{J_{motor}}$$

Usando los valores convertidos y dados:
* $J_{load \rightarrow M} = 4.124 \times 10^{-5} \text{ Kg - m}^2$
* $J_{GB\_reflejada\_entrada} = 1.0 \times 10^{-5} \text{ Kg - m}^2$
* $J_{motor} = 1.5 \times 10^{-5} \text{ Kg - m}^2$

$$R_i = \frac{4.124 \times 10^{-5} + 1.0 \times 10^{-5}}{1.5 \times 10^{-5}} = \frac{5.124 \times 10^{-5}}{1.5 \times 10^{-5}} \approx 3.416$$

El ejemplo calcula la relación de inercia de un sistema compuesto por un motor, un reductor de engranajes y una carga. Primero, se calcula la inercia de la carga reflejada al eje del motor, teniendo en cuenta la relación de transmisión y la eficiencia del reductor. Luego, se suma la inercia reflejada del reductor (ya dada) a la inercia reflejada de la carga para obtener la inercia total vista por el motor (sin incluir la inercia del rotor del motor en el numerador de la relación de inercia como se muestra en la segunda fórmula de la imagen). Finalmente, se divide esta inercia total reflejada por la inercia del rotor del motor para obtener la relación de inercia, que en este caso es aproximadamente 3.416.


## 10. Transmisión Polea-Correa

![image](https://github.com/user-attachments/assets/4e5a5c96-1d3d-49c7-b638-d1819aff9b56)

Figura 3. Polea-correa.

Los sistemas de transmisión por polea y correa son una alternativa común a los engranajes, especialmente cuando se requiere transmitir potencia entre ejes que están relativamente lejos o cuando se busca una transmisión más silenciosa y con cierta capacidad de absorción de choques.

### 10.1 Introducción

Un sistema de transmisión por polea y correa consiste en dos o más poleas montadas en ejes rotatorios y una correa que las conecta. La rotación de la polea motriz se transmite a la polea conducida a través de la fricción entre la correa y las poleas.

### 10.2 Puntos Clave

* **Tipos de Correas:** Existen varios tipos de correas (planas, trapezoidales o en V, dentadas, etc.), cada una adecuada para diferentes aplicaciones en términos de potencia, velocidad y eficiencia.
* **Material de las Poleas y Correas:** Los materiales utilizados deben ser capaces de soportar las cargas y la fricción generada durante la operación.
* **Tensión de la Correa:** Una tensión adecuada en la correa es crucial para asegurar una transmisión eficiente y evitar el deslizamiento.
* **Deslizamiento:** Siempre existe un cierto grado de deslizamiento entre la correa y la polea, lo que puede afectar la precisión de la relación de transmisión y la eficiencia.

### 10.3 Ventajas y Desventajas

| Ventajas                                      | Desventajas                                           |
| :-------------------------------------------- | :---------------------------------------------------- |
| Transmisión silenciosa                        | Mayor espacio requerido en comparación con engranajes |
| Capacidad de absorber choques y vibraciones | Menor eficiencia que los engranajes en general        |
| Costo inicial relativamente bajo             | Mayor mantenimiento debido al desgaste de la correa     |
| Fácil instalación y mantenimiento             | Sensibilidad a la tensión de la correa                 |
| Puede transmitir potencia a largas distancias | Posibilidad de deslizamiento                          |

### 10.4 Relación de Transmisión

La relación de transmisión ($i$) en un sistema de polea y correa se define por la relación entre el diámetro de la polea conducida ($D_{d}$) y el diámetro de la polea motriz ($D_{m}$), o inversamente, por la relación entre la velocidad angular de la polea motriz ($\omega_{m}$) y la velocidad angular de la polea conducida ($\omega_{d}$):

$$i_{polea-correa} = \frac{D_{d}}{D_{m}} = \frac{\omega_{m}}{\omega_{d}}$$

### 10.5 Inercia Reflejada

La inercia de la carga ($J_{carga}$) conectada a la polea conducida se refleja a la polea motriz con una relación similar a la de los engranajes:

$$J_{ref\_polea} = J_{carga} \cdot \left( \frac{D_{m}}{D_{d}} \right)^2 = \frac{J_{carga}}{i^2}$$

### 10.6 Torque de Carga Reflejado

El torque de carga ($T_{carga}$) en la polea conducida se refleja a la polea motriz de la siguiente manera, considerando la eficiencia ($\eta$) de la transmisión:

$$T_{ref\_polea} = T_{carga} \cdot \frac{D_{m}}{D_{d} \cdot \eta} = \frac{T_{carga}}{i\cdot \eta}$$


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

La inercia reflejada ($J_{ref}$) de una carga con inercia $J_{carga}$ a través de una transmisión con relación de transmisión $i$ (donde $i = \frac{\omega_{entrada}}{\omega_{salida}}$) se calcula como:

$$J_{ref} = \frac{J_{carga}}{i^2}$$

Esto significa que si la velocidad se reduce (i > 1), la inercia reflejada en el lado de alta velocidad es menor.

### 4.2 Torque Reflejado (Torque de Carga Reflejado)

De manera similar, el torque de carga ($T_{L}$) que actúa en el lado de salida se refleja al lado de entrada como un torque requerido adicional para mover la carga. El torque de carga reflejado ($T_{ref}$) se calcula como:

$$T_{ref} = \frac{T_{L}}{i \cdot \eta}$$

Donde $\eta$ es la eficiencia de la transmisión. La eficiencia se incluye porque la potencia debe ser conservada (idealmente $P_{entrada} = P_{salida}$). Como $P = T \cdot \omega$, entonces $T_{entrada} \cdot \omega_{entrada} \cdot \eta = T_{salida} \cdot \omega_{salida}$, lo que lleva a la fórmula anterior.

## 5. Engranajes

Los engranajes son componentes fundamentales en muchos sistemas de transmisión debido a su capacidad para transmitir potencia con una relación de velocidad precisa y alta eficiencia.

### 5.1 Relación de Engranajes

La relación de engranajes ($i_{engranajes}$) entre dos engranajes que engranan se define como la relación entre el número de dientes del engranaje conducido ($N_{d}$) y el número de dientes del engranaje conductor ($N_{c}$), o inversamente, como la relación entre la velocidad angular del engranaje conductor ($\omega_{c}$) y la velocidad angular del engranaje conducido ($\omega_{d}$):

$$i_{engranajes} = \frac{N_{d}}{N_{c}} = \frac{\omega_{c}}{\omega_{d}}$$

* Si $N_{d} > N_{c}$ (engranaje conducido más grande), la velocidad se reduce ($i > 1$).
* Si $N_{d} < N_{c}$ (engranaje conducido más pequeño), la velocidad aumenta ($i < 1$).

En un tren de engranajes con múltiples etapas, la relación de transmisión total es el producto de las relaciones de transmisión de cada etapa.

### 5.2 Otros Aspectos Importantes de los Engranajes

* **Tipos de Engranajes:** Existen diferentes tipos de engranajes (rectos, helicoidales, cónicos, sinfín, etc.), cada uno con sus propias características y aplicaciones.
* **Módulo:** Es una medida del tamaño de los dientes del engranaje. Los engranajes que engranan deben tener el mismo módulo.
* **Paso Diametral:** Otra medida del tamaño de los dientes, inversamente proporcional al módulo.
* **Fuerzas en los Engranajes:** La transmisión de potencia a través de los engranajes genera fuerzas de contacto entre los dientes, las cuales deben ser consideradas en el diseño para asegurar la resistencia y durabilidad de los engranajes.
* **Eficiencia de los Engranajes:** Los engranajes bien lubricados tienen una alta eficiencia, generalmente entre el 95% y el 99% por etapa.

## 6. Transmisión Polea-Correa

Los sistemas de transmisión por polea y correa son una alternativa común a los engranajes, especialmente cuando se requiere transmitir potencia entre ejes que están relativamente lejos o cuando se busca una transmisión más silenciosa y con cierta capacidad de absorción de choques.

### 6.1 Introducción

Un sistema de transmisión por polea y correa consiste en dos o más poleas montadas en ejes rotatorios y una correa que las conecta. La rotación de la polea motriz se transmite a la polea conducida a través de la fricción entre la correa y las poleas.

### 6.2 Puntos Clave

* **Tipos de Correas:** Existen varios tipos de correas (planas, trapezoidales o en V, dentadas, etc.), cada una adecuada para diferentes aplicaciones en términos de potencia, velocidad y eficiencia.
* **Material de las Poleas y Correas:** Los materiales utilizados deben ser capaces de soportar las cargas y la fricción generada durante la operación.
* **Tensión de la Correa:** Una tensión adecuada en la correa es crucial para asegurar una transmisión eficiente y evitar el deslizamiento.
* **Deslizamiento:** Siempre existe un cierto grado de deslizamiento entre la correa y la polea, lo que puede afectar la precisión de la relación de transmisión y la eficiencia.

### 6.3 Ventajas y Desventajas

| Ventajas                                      | Desventajas                                           |
| :-------------------------------------------- | :---------------------------------------------------- |
| Transmisión silenciosa                        | Mayor espacio requerido en comparación con engranajes |
| Capacidad de absorber choques y vibraciones | Menor eficiencia que los engranajes en general        |
| Costo inicial relativamente bajo             | Mayor mantenimiento debido al desgaste de la correa     |
| Fácil instalación y mantenimiento             | Sensibilidad a la tensión de la correa                 |
| Puede transmitir potencia a largas distancias | Posibilidad de deslizamiento                          |

### 6.4 Relación de Transmisión

La relación de transmisión ($i_{polea-correa}$) en un sistema de polea y correa se define por la relación entre el diámetro de la polea conducida ($D_{d}$) y el diámetro de la polea motriz ($D_{m}$), o inversamente, por la relación entre la velocidad angular de la polea motriz ($\omega_{m}$) y la velocidad angular de la polea conducida ($\omega_{d}$):

$$i_{polea-correa} = \frac{D_{d}}{D_{m}} = \frac{\omega_{m}}{\omega_{d}}$$

### 6.5 Inercia Reflejada

La inercia de la carga ($J_{carga}$) conectada a la polea conducida se refleja a la polea motriz con una relación similar a la de los engranajes:

$$J_{ref\_polea} = J_{carga} \cdot \left( \frac{D_{m}}{D_{d}} \right)^2 = \frac{J_{carga}}{i_{polea-correa}^2}$$

### 6.6 Torque de Carga Reflejado

El torque de carga ($T_{carga}$) en la polea conducida se refleja a la polea motriz de la siguiente manera, considerando la eficiencia ($\eta_{polea-correa}$) de la transmisión:

$$T_{ref\_polea} = T_{carga} \cdot \frac{D_{m}}{D_{d} \cdot \eta_{polea-correa}} = \frac{T_{carga}}{i_{polea-correa} \cdot \eta_{polea-correa}}$$

---

Espero que estos apuntes te sean de gran utilidad para tu clase. Recuerda que puedes expandir cada sección con más detalles, ejemplos e imágenes según sea necesario. ¡Mucho éxito con tu estudio!

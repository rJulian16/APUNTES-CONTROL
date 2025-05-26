# Control de Movimiento Clase 30 de Abril.

Julian Stiven Redondo Chacon & Sebastian Cifuentes Alfonso & David Esteban Vasquez Alarcon

## Indice

- [1. Introducción](#1-introduccion)
- [2. Tornillo sin fin](#2-tornillo-sin-fin)
  - [2.1 Tipos de Tornillo Guía](#21-tipos-de-tornillo-guía)
    - [2.1.1 Tornillo de rosca trapezoidal](#211-tornillo-de-rosca-trapezoidal)
    - [2.1.2 Tornillo de rosca cuadrada](#212-tornillo-de-rosca-cuadrada)
    - [2.1.3 Tornillo de rosca directa](#213-tornillo-de-rosca-directa)
    - [2.1.4 Tornillo con recirculación de bolas (Ball Screw)](#214-tornillo-con-recirculación-de-bolas-ball-screw)
- [3. Backlash](#3-backlash)
- [4. Relación de transmisión básica](#4-relacion-de-transmision-basica)
  - [4.1 Relación de transmisión cabeceo-paso](#41-relacion-de-transmision-cabeceo-paso)
- [5. Inercia Reflejada](#5-inercia-reflejada)
- [6. Inercia reflejada total y torque de carga](#6-inercia-reflejada-total-y-torque-de-carga)
  - [6.1 Análisis de Inercia Reflejada Total en Sistemas de Tornillo](#61-analisis-de-inercia-reflejada-total-en-sistemas-de-tornillo)
  - [6.2 Análisis de Torque de Carga en Sistemas de Tornillo](#62-analisis-de-torque-de-carga-en-sistemas-de-tornillo)
- [7. Simulink Lead-Screw](#7-simulink-lead-screw)
- [8. Piñón-Cremallera](#8-piñon--cremallera)
  - [8.1 Relación de transmisión piñón-cremallera](#81-relacion-de-transmision-piñon-cremallera)
  - [8.2 Inercia reflejada y torque de carga](#82-inercia-reflejada-y-torque-de-carga)
  - [8.3 Simulink](#83-simulink)
- [9. Banda Transportadora](#9-banda-transportadora)
  - [9.1 Relación de Transmisión y Movimiento](#91-relacion-de-transmision-y-movimiento)
  - [9.2 Inercia reflejada y torque de carga](#92-inercia-reflejada-y-torque-de-carga)
- [10. Conclusiones](#10-conclusiones)
- [11. Referencias](#11-referencias)

## 1. Introduccion 

En el estudio de los sistemas de control de movimiento, los mecanismos de transmisión de potencia y movimiento son fundamentales para transformar la energía generada por un actuador (como un motor) en un desplazamiento útil. A lo largo del semestre, ya hemos explorado diferentes tipos de transmisión, como engranajes, correas y poleas, entendiendo cómo modifican velocidad, fuerza y dirección del movimiento.

Sin embargo, no todos los sistemas de transmisión están diseñados únicamente para rotar. En aplicaciones donde se requiere un desplazamiento lineal preciso, entran en juego otros componentes clave, como el tornillo guía, también conocido como husillo o tornillo de potencia. Estos elementos convierten el movimiento rotacional de un motor en un desplazamiento lineal mediante una tuerca acoplada, lo que resulta esencial en maquinaria CNC, impresoras 3D, actuadores lineales y muchos sistemas mecatrónicos.

## 2. Tornillo sin fin

El tornillo sin fin es un sistema de transmisión de movimiento entre ejes que se cruzan (generalmente en ángulo recto). Está compuesto por dos partes principales:

El tornillo sin fin: una especie de tornillo largo con rosca helicoidal.

La rueda dentada o corona: un engranaje circular cuyos dientes encajan con la rosca del tornillo.

**¿Cómo funciona?**

Cuando el tornillo gira, su rosca empuja los dientes de la rueda dentada, haciendo que esta gire. A diferencia de los engranajes comunes, en este sistema solo el tornillo puede mover la rueda, pero no al revés, lo que lo hace ideal para aplicaciones donde se requiere autobloqueo (es decir, que el movimiento no se devuelva por sí solo).

**Simulink**

![image](https://github.com/user-attachments/assets/285583e6-1bb1-4c06-b375-c81c2de6e831)

Figura 1. Tornillo sin fin Simulink

![image](https://github.com/rJulian16/APUNTES-CONTROL/blob/fa5507616608caa3038b6de0d94c1b95a349c83d/Corte%203/Imagenes/hola3.gif)

Figura 2. Tornillo sin fin

### 2.1. Tipos de Tornillo Guía

En sistemas de transmisión lineal, se utilizan distintos tipos de roscas en los tornillos guía. Los más comunes en aplicaciones mecánicas son:

#### 2.1.1. Tornillo de rosca trapezoidal

**Definición:**
Tiene una rosca con forma de trapecio. Su diseño permite una buena combinación entre eficiencia y resistencia, lo que lo hace adecuado para cargas moderadas y movimientos repetitivos.

**Usos comunes:**

- Husillos de mesas de máquinas-herramienta

- Prensas mecánicas

- Sistemas donde se necesita autobloqueo

![image](https://github.com/user-attachments/assets/a28ed022-25dd-45fc-b21a-e445c3f58fed)

Figura 3. Tornillo sin fin con rosca trapezoidal

#### 2.1.2. Tornillo de rosca cuadrada

**Definición:**
Tiene una rosca con forma rectangular (cuadrada), lo que reduce el rozamiento durante el movimiento. Es más eficiente que el trapezoidal pero más difícil de fabricar.

**Usos comunes:**

- Prensas de alta precisión

- Sistemas que requieren alta eficiencia mecánica

- Aplicaciones donde no se necesita autobloqueo

![image](https://github.com/user-attachments/assets/f236ff3a-7840-4beb-9444-8614ecfdff21)

Figura 4. Tornillo sin fin con rosca cuadrada


| Característica               | Rosca Trapezoidal               | Rosca Cuadrada                       |
| ---------------------------- | ------------------------------- | ------------------------------------ |
| **Forma del perfil**         | Trapecio                        | Cuadrado                             |
| **Eficiencia mecánica**      | Media (\~30–40%)                | Alta (\~50–70%)                      |
| **Autobloqueo**              | Sí (en la mayoría de casos)     | No (tiende a revertir el movimiento) |
| **Facilidad de fabricación** | Alta                            | Baja (requiere más precisión)        |
| **Resistencia al desgaste**  | Buena                           | Regular                              |
| **Costo**                    | Menor                           | Mayor                                |
| **Aplicaciones comunes**     | Equipos de transmisión estándar | Aplicaciones de alta precisión       |

Tabla 1. Comparacion trapezoidal vs cuadrada

#### 2.1.3. Tornillo de rosca directa

**Definición:**

También conocido como tornillo de fricción, es un tornillo guía tradicional en el que la tuerca desliza directamente sobre la rosca del tornillo. El contacto es metal contra metal, sin elementos intermedios.

**Usos comunes:**

- Sistemas simples de posicionamiento

- Ajustes manuales en maquinaria

- Donde se requiere autobloqueo y bajo costo

![image](https://github.com/user-attachments/assets/cbae456c-809f-4a90-959d-275ddc403f80)

Figura 5. Tornillo sin fin con rosca directa

#### 2.1.4. Tornillo con recirculación de bolas (Ball Screw)

**Definición:**

Es un tipo de tornillo guía que utiliza bolas de acero entre el tornillo y la tuerca. Estas bolas circulan dentro de un canal cerrado (recirculación), lo que reduce la fricción y mejora la eficiencia del sistema.

**Usos comunes:**

- Máquinas CNC y robótica

- Impresoras 3D de alta precisión

- Actuadores lineales rápidos y eficientes

![image](https://github.com/user-attachments/assets/92b9a89e-61cf-4f37-a892-37d524bb153e)

Figura 6. Tornillo sin fin con recirculacion de bolas


| Característica             | Rosca Directa (Fricción)    | Recirculación de Bolas         |
| -------------------------- | --------------------------- | ------------------------------ |
| **Eficiencia**             | Baja (\~20–40%)             | Alta (\~85–95%)                |
| **Fricción**               | Alta                        | Muy baja                       |
| **Velocidad de operación** | Baja                        | Alta                           |
| **Precisión**              | Media                       | Alta                           |
| **Autobloqueo**            | Sí                          | No (puede moverse sin control) |
| **Costo**                  | Bajo                        | Alto                           |
| **Mantenimiento**          | Bajo                        | Requiere lubricación y cuidado |
| **Usos comunes**           | Sistemas manuales y simples | CNC, robótica, automatización  |

Tabla 2. Comparacion rosca directa vs recirculacion de bolas

## 3. Backlash

![image](https://github.com/user-attachments/assets/dded1ec3-eeb7-463e-a128-8b413df41879)

Figura 7. Backlash

El backlash, también conocido como juego mecánico o holgura, es el pequeño espacio o movimiento libre entre los dientes de dos elementos engranados, como un tornillo sin fin y una rueda dentada o entre engranajes rectos.

Se debe principalmente a:

- Tolerancias de fabricación
- Necesidad de lubricación entre las superficies  
- Desgaste natural del sistema con el uso  
- Evitar que los dientes se bloqueen por expansión térmica o por sobrecarga

| Efecto                  | Descripción                                                                    |
|-------------------------|-----------------------------------------------------------------------------   |
| Pérdida de precisión | Especialmente crítico en sistemas de control, CNC, robótica o servoactuadores     |
| Juego en reversa     | Cuando se invierte el sentido de giro, hay un "retardo" antes del movimiento real |
| Ruido y vibraciones  | Si es excesivo, puede causar golpeteo entre dientes                               |

Tabla 3. Efectos del backlash

## 4. Relacion de trasmision basica

La relación de transmisión depende del número de hilos (o entradas) del tornillo y del número de dientes de la rueda dentada.

$$i = \frac{Z}{n}$$

**Donde:**

- \( i \): relación de transmisión  
- \( Z \): número de dientes de la rueda dentada 
- \( n \): número de principios o hilos del tornillo (normalmente 1, 2 o más)

📚 Ejercicio 1:

Un motor eléctrico gira a 1500 RPM y está conectado a un sistema tornillo sin fin–rueda dentada.
El tornillo es mono-hilo (1 entrada) y la rueda dentada tiene 45 dientes.
¿Cuál será la velocidad de salida (RPM) de la rueda dentada?

**Paso 1:** Calcular la relación de transmisión:

$$i = \frac{Z}{n} = \frac{45}{1} = 45$$

**Paso 2:** Calcular la velocidad de salida:

$$N_{\text{salida}} = \frac{N_{\text{entrada}}}{i} = \frac{1500}{45} = 33.33 \text{ RPM}$$

La rueda dentada girará a **33.33 RPM**.

📚 Ejercicio 2:

Un sistema tornillo sin fin debe reducir la velocidad de un motor de 1800 RPM a una salida de 60 RPM.  
El tornillo tiene 3 hilos.  
¿Cuántos dientes debe tener la rueda dentada para lograr esa reducción?

Paso 1: Calcular la relación de transmisión requerida:

$$i = \frac{N_{\text{entrada}}}{N_{\text{salida}}} = \frac{1800}{60} = 30$$

Paso 2: Calcular el número de dientes de la rueda:

$$Z = i \cdot n = 30 \cdot 3 = 90 \text{ dientes}$$

La rueda dentada debe tener 90 dientes.

### 4.1. Relacion de trasmision cabeceo-paso

- **Cabeceo(Pitch)**

Es el número de revoluciones que debe dar el tornillo para que la cápsula (o tuerca) se desplace 1 metro (o 1 pulgada en sistema inglés).

- Unidad:
  $$p \ (\text{revoluciones por metro, rev/m})$$

- **Paso(Lead)**

Es la distancia lineal que avanza la cápsula por cada revolución completa del tornillo.

- Relación entre Paso y Cabeceo:

$$\text{Lead} = \frac{1}{p}$$

📚 Ejercicio 3: Relación entre Cabeceo y Paso

Un tornillo tiene un cabeceo de:

$$p = 8 rev / m$$

Calcula:

1. El paso del tornillo en metros por revolución.  
2. ¿Cuánto avanzará la cápsula si el tornillo gira 25 revoluciones?

- Solucion:

Sabemos que:

$$\text{Lead} = \frac{1}{p}$$

Reemplazando:

$$\text{Lead} = \frac{1}{8} = 0.125 \ \text{m/rev}$$

Multiplicamos el paso por el número de revoluciones:

$$\text{Avance} = \text{Lead} \times \text{rev}$$

$$\text{Avance} = 0.125 \ \text{m/rev} \times 25 = 3.125 \ \text{m}$$

- **Paso (Lead):** 0.125 m/rev.
- **Avance en 25 revoluciones:** 3.125 m.


Las ecuaciones describen la relación entre el desplazamiento angular del tornillo y el desplazamiento lineal de la cápsula:

$$\Delta \theta = 2\pi p \Delta x$$

$$\frac{\dot{\Delta \theta}}{\Delta \dot{x}} = 2\pi p$$

Donde:

$$\frac{\Delta \theta}{\Delta t} = \dot{\theta} \quad \text{: Velocidad angular del motor (rad/s o rpm).}$$

$$\frac{\Delta x}{\Delta t} = \dot{x} \quad \text{: Velocidad lineal de la carga (m/s).}$$

- Relación de transmisión:

$$\frac{\dot{\theta}}{\dot{x}} = 2\pi p$$

📚 Ejercicio 4: Relación entre velocidad angular y lineal

Un tornillo guía tiene un cabeceo de $$\( p = 4 \, \text{rev/m} \)$$. 
Si el motor gira a una velocidad angular de $$\( \dot{\theta} = 25.13 \, \text{rad/s} \)$$,  
¿cuál es la velocidad lineal de desplazamiento de la cápsula?


- Datos:

- $$\( p = 4 \, \text{rev/m} \)$$
- $$\( \dot{\theta} = 25.13 \, \text{rad/s} \)$$

Resultado:

$$
\frac{\dot{\theta}}{\dot{x}} = 2\pi p
\Rightarrow 
\dot{x} = \frac{\dot{\theta}}{2\pi p}
$$

$$
\dot{x} = \frac{25.13}{2\pi \cdot 4} = \frac{25.13}{25.13} = 1 \, \text{m/s}
$$


$$
\dot{x} = 1 \text{m/s}
$$

Tuvo una velocidad lineal de $$1 m / s$$

📚 Ejercicio 5: Cálculo del cabeceo del tornillo

Una cápsula se desplaza a una velocidad lineal de  
$$\dot{x} = 0.5 \, \text{m/s}$$ 

cuando el motor gira a una velocidad angular de  
$$\dot{\theta} = 12.57 \, \text{rad/s}$$.  

¿Cuál es el cabeceo del tornillo guía?

- Datos:

- $$\dot{x} = 0.5 \, \text{m/s}$$  
- $$\dot{\theta} = 12.57 \, \text{rad/s}$$

- Solucion:

$$
\frac{\dot{\theta}}{\dot{x}} = 2\pi p
\Rightarrow 
p = \frac{\dot{\theta}}{2\pi \dot{x}}
$$

$$
p = \frac{12.57}{2\pi \cdot 0.5} = \frac{12.57}{3.1416} = 4 \, \text{rev/m}
$$

- Resultado:

El cabeceo del tornillo es de  
$$p = 4 \, \text{rev/m}$$

## 5. Inercia Reflejada

- Energía Cinética de la Carga Lineal
La energía cinética ($KE$) de una carga con masa $m$:

$$KE = \frac{1}{2} m \dot{x}^2$$

- Relación de Transmisión
Para un tornillo sinfín con cabeceo $p$ [rev/m]:

$$\frac{\dot{\theta}}{\dot{x}} = 2\pi p$$

- Energía Cinética en Términos Angulares
Sustituyendo $\dot{x} = \frac{\dot{\theta}}{2\pi p}$:

$$KE = \frac{1}{2} \frac{m}{(2\pi p)^2} \dot{\theta}^2$$

- Inercia Reflejada ($J_{ref}$)
Igualando con $KE = \frac{1}{2} J_{ref} \dot{\theta}^2$:

$$J_{ref} = \frac{m}{(2\pi p)^2}$$

O equivalentemente si $N_S = 2\pi p$:

$$J_{ref} = \frac{m}{N_S^2}$$

- La inercia reflejada representa el efecto de la masa de la carga trasladado al eje del motor, como si ambos estuvieran directamente acoplados.

- Este concepto permite expresar todo el sistema en términos rotacionales, lo que simplifica el análisis dinámico y el diseño de sistemas de control.

- Un tornillo con mayor paso genera una inercia reflejada menor, lo que se traduce en una respuesta más ágil del sistema.

📚 Ejercicio 6:

- Cálculo de Inercia Reflejada y Torque

Un sistema de tornillo sinfín mueve una carga lineal de 15 kg. El tornillo tiene un cabeceo de 3 rev/m.  
Calcular:  
1. La inercia reflejada ($J_{\text{ref}}$) vista por el motor.  
2. Si el motor acelera a 2 rad/s², ¿qué torque se requiere para vencer la inercia de la carga?

Procedimiento:

Partimos de la fórmula de inercia reflejada para un tornillo sinfín:

$$J_{\text{ref}} = \frac{m}{(2\pi p)^2}$$

- Donde:
  - $m = 15\, \text{kg}$ (masa de la carga)
  - $p = 3\, \text{rev/m}$ (cabeceo del tornillo)

$$J_{\text{ref}} = \frac{15}{(2\pi \times 3)^2} = \frac{15}{(6.283 \times 3)^2} = \frac{15}{355.3} \approx 0.042\, \text{kg·m}^2$$

$$\tau = J_{\text{ref}} \cdot \alpha$$

- Donde:
  - $\alpha = 2\, \text{rad/s²}$ (aceleración angular)

Sustituimos $J_{\text{ref}}$:

$$\tau = 0.042 \times 2 = 0.084\, \text{N·m}$$

1. $\boxed{J_{\text{ref}} \approx 0.042\, \text{kg·m}^2}$  
2. $\boxed{\tau = 0.084\, \text{N·m}}$



## 6. Inercia reflejada total y torque de carga

### 6.1. Análisis de Inercia Reflejada Total en Sistemas de Tornillo

-Componentes Clave

- Masas del Sistema
- Carga (Load): $W_L$ [N]
- Carro (Carriage): $W_C$ [N]
- Masa total equivalente:
  $$m = \frac{W_L + W_C}{g}$$
  donde $g = 9.81\, \text{m/s²}$.

- Inercia Reflejada Total ($J_{\text{total}}$)
La inercia total tiene tres componentes principales:

$$J_{\text{total}} = J_{\text{screw}} + J_{\text{load-in}} + J_{\text{carriage-in}}$$

Inercia del tornillo ($J_{\text{screw}}$):
   - Depende de la geometría y material del tornillo.

Inercia de la carga reflejada:
   $$J_{\text{load-in}} = \frac{1}{\eta N_S^2} \left( \frac{W_L}{g} \right)$$

Inercia del carro reflejada:
   $$J_{\text{carriage-in}} = \frac{1}{\eta N_S^2} \left( \frac{W_C}{g} \right)$$

- **Fórmula combinada:**
$$J_{\text{total}} = J_{\text{screw}} + \frac{1}{\eta N_S^2} \left( \frac{W_L + W_C}{g} \right)$$


📚 Ejercicio 7 numerico:

**Datos**:
- Carga $W_L = 500\, \text{N}$
- Peso del carro $W_C = 300\, \text{N}$
- Eficiencia $\eta = 0.8$
- $N_S = 10\, \text{rad/m}$
- $J_{\text{screw}} = 0.05\, \text{kg·m²}$

**Cálculos**:
Masa total:
   $$m = \frac{500 + 300}{9.81} \approx 81.55\, \text{kg}$$

Inercia reflejada de masas:
   $$J_{\text{load+carriage}} = \frac{1}{0.8 \times 10^2} \times 81.55 \approx 1.02\, \text{kg·m²}$$

Inercia total:
   $$J_{\text{total}} = 0.05 + 1.02 = 1.07\, \text{kg·m²}$$

> **Nota**: Para sistemas de alta precisión, considerar también la inercia del acoplamiento motor-tornillo.

### 6.2. Análisis de Torque de Carga en Sistemas de Tornillo

- Componentes de Fuerza Externa

La fuerza externa total ($F_{ext}$) que actúa sobre el sistema se compone de:

$$F_{ext} = F_f + F_g + F_p$$

- Desglose de componentes:

**Fuerza de fricción ($F_f$):**

   $$F_f = \mu (W_L + W_C) \cos \beta$$
   - $\mu$: Coeficiente de fricción
   - $W_L$: Peso de la carga [N]
   - $W_C$: Peso del carro [N]
   - $\beta$: Ángulo de inclinación (0° si horizontal)

**Fuerza gravitacional ($F_g$):**

   $$F_g = (W_L + W_C) \sin \beta$$
   - Si $\beta = 0°$ (horizontal): $F_g = 0$


Fuerza aplicada ($F_p$): Fuerza externa adicional (ej: empuje).


**Fórmula combinada:**

$$F_{ext} = F_p + (W_L + W_C) (\sin \beta + \mu \cos \beta)$$



**Torque Reflejado en el Motor:**

El torque requerido ($T_{\text{load-in}}$) para mover la carga se calcula mediante el trabajo realizado:

   - Relación trabajo-torque:

Trabajo en términos lineales:

   $$\text{Work} = F_{ext} \cdot \Delta x$$
   
   - $\Delta x$: Desplazamiento lineal.

Trabajo en términos rotacionales:

   $$\text{Work} = T_{\text{load-in}} \cdot \Delta \theta$$
   
   - $\Delta \theta$: Desplazamiento angular.

Relación tornillo:

   $$\Delta x = \frac{\Delta \theta}{2\pi p}$$
   
   - $p$: Cabeceo del tornillo [rev/m].

- Torque reflejado:

$$T_{\text{load-in}} = \frac{F_{ext}}{\eta N_S}$$

- $\eta$: Eficiencia del sistema (0.7-0.9).

- $N_S = 2\pi p$: Relación de transmisión.

📚 Ejercicio 8 numerico:

**Datos**:
- $W_L = 500\, \text{N}$, $W_C = 300\, \text{N}$
- $\mu = 0.2$, $\beta = 0°$ (horizontal)
- $p = 5\, \text{rev/m}$, $\eta = 0.85$
- $F_p = 100\, \text{N}$

**Cálculos**:

**Fuerza externa** ($\beta = 0° \Rightarrow \sin \beta = 0$, $\cos \beta = 1$):

   $$F_{ext} = 100 + (500 + 300)(0 + 0.2 \times 1) = 100 + 160 = 260\, \text{N}$$

**Torque reflejado** ($N_S = 2\pi \times 5 = 31.42\, \text{rad/m}$):

   $$T_{\text{load-in}} = \frac{260}{0.85 \times 31.42} \approx 9.74\, \text{N·m}$$

> **Nota**: Para sistemas verticales ($\beta = 90°$), la fuerza gravitacional domina ($F_g = W_L + W_C$).


📚 Ejercicio 9 planteado en clase :

Una carga de 50 Kg debe ser posicionado usando un tornillo esferado de acero con 0,14 Kg/cm³ de densidad, 0,182 cm de diámetro, 36 cm de longitud, 0,75 cm/rev de paso y 90% de eficiencia. El carro pesa 0,23 Kg. Calcule la inercia reflejada por la transmisión hacia su eje de entrada.

La inercia total reflejada en el sistema se compone de:

$$\frac{J_{t}^{\text{trans}}}{\eta t} = J_{\text{screw}} + J_{\text{load-in}} + J_{\text{carriage-in}}$$

Que puede expresarse como:

$$= J_{\text{screw}} + \frac{1}{\eta N_s^2} \left( \frac{W_L + W_C}{g} \right)$$

- Parámetros y Constantes

Aceleración gravitacional:
   - Valor mostrado: 386 in/s² (equivalente a 9.81 m/s² en unidades métricas)

Relación de transmisión:

   - Fórmula:

     $$N_s = 2\pi p$$
     
     $$N_s = 2\pi \times \frac{1}{0.75} \approx 8.38$$
  
La inercia total reflejada ($J_{ref}^{trans}$) se calcula como:

$$J_{ref}^{trans} = J_{screw} + \frac{1}{\eta N_S^2} \left( \frac{W_L + W_C}{g} \right)$$

Para los valores dados:
- $J_{screw} = 5.42 \times 10^{-8}\, \text{kg·m}^2$
- $\eta = 0.9$ (90% de eficiencia)
- $N_S = 8.38$
- $W_L = 50\, \text{kg}$
- $W_C = 0.23\, \text{kg}$
- $g = 9.89\, \text{m/s}^2$

El cálculo resulta:

$$J_{ref}^{trans} = 5.42 \times 10^{-8} + \frac{1}{0.9 \times 8.38^2} \left( \frac{50 + 0.23}{9.89} \right) \approx 8.1\, \text{kg·m}^2$$

- Cálculo de la Inercia del Tornillo ($J_{screw}$)

$$J_{screw} = \frac{\pi L \rho D^4}{32}$$

Sustituyendo en la fórmula:

$$\begin{align*}
I_{screw} &= \frac{\pi \times 0.36 \times 140000 \times (0.00182)^4}{32} \\
&= \frac{\pi \times 0.36 \times 140000 \times 1.1 \times 10^{-11}}{32} \\
&= 5.42 \times 10^{-8}\, \text{kg·m}^2
\end{align*}$$

## 7. Simulink Lead-Screw

Este ejemplo hecho por MathWorks modela un tornillo de avance con fricción. Se mide la fuerza de restricción en el tornillo de avance y se utiliza para calcular el par de fricción dentro del mismo. Se utiliza un modelo de fricción continua de deslizamiento a tirones para determinar el coeficiente de fricción basado en la velocidad de rotación relativa de las dos piezas conectadas por el tornillo de avance.

![image](https://github.com/user-attachments/assets/16d99c99-d84e-4d48-b1de-8c311900f69b)

Figura 8. Tornillo de avance MathWorks

![image](https://github.com/rJulian16/APUNTES-CONTROL/blob/0fca4f3639414e008aed8138e8152530c117a97d/Corte%203/Imagenes/hola4.gif)

Figura 9. Simulink tornillo.

## 8. Piñon- Cremallera

El sistema piñón-cremallera es un mecanismo de transmisión que convierte el movimiento rotacional de un engranaje (piñón) en movimiento lineal a través de una barra dentada (cremallera). Es ampliamente utilizado en sistemas de dirección de vehículos, máquinas CNC y mecanismos de apertura lineal, gracias a su simplicidad, precisión y capacidad para transmitir fuerza en trayectorias rectas.

La relación entre la rotación del piñón y el desplazamiento lineal de la cremallera depende del diámetro primitivo del piñón y del número de dientes, permitiendo un control directo y eficiente del desplazamiento.

### 8.1 Relacion de transmision piñon-cremallera

En un sistema piñón-cremallera, la relación de transmisión ($N$) se define como la razón entre la velocidad angular del piñón (motor) y la velocidad lineal de la cremallera (carga):

$$N = \frac{\omega_{\text{motor}}}{v_{\text{carga}}}$$

Donde:

- $N$: relación de transmisión  
- $\omega_{\text{motor}}$: velocidad angular del piñón (rad/s)  
- $v_{\text{carga}}$: velocidad lineal de la cremallera (m/s)

- Velocidad Lineal de la Cremallera

La velocidad lineal de la cremallera se puede calcular como:

$$v_{\text{rack}} = r_{\text{piñón}} \cdot \omega_{\text{piñón}}$$

Donde:

- $v_{\text{rack}}$: velocidad lineal de la cremallera  
- $r_{\text{piñón}}$: radio primitivo del piñón (m)  
- $\omega_{\text{piñón}}$: velocidad angular del piñón (rad/s)

Otra forma de expresar la relación de transmisión en este sistema es:

$$N_{\text{rp}} = \frac{1}{r_{\text{piñón}}}$$

📚 Ejercicio 10: Un motor mueve un piñón de radio $r = 0.05 \, \text{m}$ (5 cm).  
Si el motor gira a una velocidad angular de $\omega = 20 \, \text{rad/s}$,  
¿cuál es la velocidad lineal de la cremallera?

**Datos:**

- Radio del piñón: $r = 0.05 \, \text{m}$
- Velocidad angular: $\omega = 20 \, \text{rad/s}$

**Procedimiento:**

La velocidad lineal de la cremallera es:

$$v_{\text{rack}} = r_{\text{piñón}} \cdot \omega_{\text{piñón}}$$

$$v_{\text{rack}} = 0.05 \cdot 20 = 1 \, \text{m/s}$$

**Resultado:**

La cremallera se mueve a una velocidad de:

$$v_{\text{rack}} = 1 \, \text{m/s}$$

### 8.2 Inercia reflejada y torque de carga

**La inercia reflejada del sistema:**

$$J_{\text{ref}}^{\text{trans}} = J_{\text{pinion}} + \frac{1}{\eta N_{\text{RP}}^{2}} \left( \frac{W_{L} + W_{C}}{g} \right)$$

Donde:
- $J_{\text{pinion}}$: Inercia del piñón [kg·m²]
- $\eta$: Eficiencia del sistema (ej. 0.9 para 90%)
- $N_{\text{RP}}$: Relación de transmisión [dientes/m o rad/m]
- $W_L$, $W_C$: Pesos de carga y carro [N]
- $g$: Gravedad (9.81 m/s²)

**Torque de Carga Reflejado**

El torque requerido para mover la carga:

$$T_{\text{load} \rightarrow \text{in}} = \frac{F_{\text{ext}}}{\eta N_{\text{RP}}}$$


📚 Ejemplo 11 Numérico:

Datos:
- $W_L = 500\,N$, $W_C = 200\,N$
- $\mu = 0.2$, $\beta = 10°$
- $N_{\text{RP}} = 50\, \text{dientes/m}$
- $\eta = 0.9$

Cálculos:

Fuerza externa:

   $$F_f = 0.2 \times 700 \times \cos 10° ≈ 137.8\,N$$
   $$F_g = 700 \times \sin 10° ≈ 121.5\,N$$
   $$F_{\text{ext}} = 137.8 + 121.5 = 259.3\,N \quad (\text{sin } F_p)$$

Torque reflejado:

   $$T_{\text{load} \rightarrow \text{in}} = \frac{259.3}{0.9 \times 50} ≈ 5.76\,N\cdot m$$


**Observaciones**
- En sistemas horizontales ($\beta = 0°$), $F_g = 0$
- La inercia reflejada decrece cuadráticamente con $N_{\text{RP}}$
- Para altas precisiones, considerar la flexibilidad de la cremallera

### 8.3 Simulink

![image](https://github.com/user-attachments/assets/f628c33d-e459-4540-a295-8abef76edcce)

Figura 10. Simulink diagrama de bloques piñon-cremallera.

![image](https://github.com/rJulian16/APUNTES-CONTROL/blob/bfc72f686054baf3264a0fa6d3248ce5825ed75d/Corte%203/Imagenes/hola5.gif)

Figura 11. Simulacion activa piñon-cremallera.

## 9. Banda Transportadora

Una banda transportadora es un sistema mecánico utilizado para mover materiales o cargas de un punto a otro a lo largo de una trayectoria fija. Está compuesta principalmente por una banda flexible , que se desplaza sobre rodillos o poleas impulsadas por un motor.

Este tipo de mecanismo es ampliamente utilizado en procesos industriales, logísticos y de manufactura, permitiendo un transporte continuo, controlado y eficiente.

**Aplicaciones Comunes:**

- Sistemas de empaque y ensamblaje industrial  
- Clasificación y distribución de productos  
- Líneas de producción en fábricas  
- Transporte de alimentos o materiales pesados

### 9.1. Relación de Transmisión y Movimiento

El movimiento de la banda está relacionado directamente con el giro de un rodillo motriz, y la velocidad lineal de la banda se puede determinar a partir del radio del rodillo y la velocidad angular del motor:

  $$N = \frac{\text{Velocidad motor}}{\text{Velocidad carga}}$$

- Velocidad de la banda (V_belt)

  $$V_{\text{belt}} = r_{\text{ip}} \omega_{\text{ip}}$$
    
  Donde:  
  - $r_{\text{ip}}$: Radio del tambor motriz [m]  
  - $\omega_{\text{ip}}$: Velocidad angular del tambor [rad/s]  

  $$N_{\text{BD}} = \frac{1}{r_{\text{ip}}}$$ 


📚 Ejercicio 12:

Un motor gira a 1750 rpm mueve una banda transportadora mediante un tambor motriz de 15 cm de diámetro. La carga se desplaza a 0.5 m/s. Calcular:  

1. Velocidad angular del tambor ($\omega_{ip}$)  
2. Relación de transmisión ($N$)  
3. Fuerza efectiva en la banda si el torque motor es 25 N·m  

**Datos:**  
- $r_{ip} = 15\,\text{cm}/2 = 0.075\,\text{m}$  
- $V_{\text{belt}} = 0.5\,\text{m/s}$  
- $\tau_{\text{motor}} = 25\,\text{N·m}$  

**Procedimiento:**  

- Velocidad angular del tambor ($\omega_{ip}$):**

   $$\omega_{ip} = \frac{V_{\text{belt}}}{r_{ip}} = \frac{0.5}{0.075} \approx 6.67\,\text{rad/s}$$
  
   Conversión a rpm:
  
   $$6.67\,\text{rad/s} \times \frac{60}{2\pi} \approx 63.7\,\text{rpm}$$

- Relación de transmisión ($N$):

   $$N = \frac{\text{Velocidad motor}}{\text{Velocidad carga}} = \frac{1750}{63.7} \approx 27.5$$

- Fuerza efectiva ($F_{\text{belt}}$):

   - Primero calculamos el torque en el tambor:
  
     $$\tau_{\text{tambor}} = \tau_{\text{motor}} \times \frac{1}{N} = 25 \times \frac{1}{27.5} \approx 0.91\,\text{N·m}$$
     
   - Luego la fuerza:
  
     $$F_{\text{belt}} = \frac{\tau_{\text{tambor}}}{r_{ip}} = \frac{0.91}{0.075} \approx 12.1\,\text{N}$$

**Resultados:**  
$\boxed{\omega_{ip} \approx 6.67\,\text{rad/s}}$  
$\boxed{N \approx 27.5}$  
$\boxed{F_{\text{belt}} \approx 12.1\,\text{N}}$  

### 9.2. Inercia reflejada y torque de carga

- **Inercia reflejada total**:

   $$J_{\text{ref}}^{\text{trans}} = 2J_p + \frac{1}{\eta N_{\text{BD}}^2} \left( \frac{W_L + W_C + W_{\text{belt}}}{g} \right)$$
   
   - $J_p$: Inercia de los piñones (IP y LP) [kg·m²]  
   - $\eta$: Eficiencia del sistema  
   - $N_{\text{BD}}$: Relación de transmisión banda-tambor ($=\frac{1}{r_{ip}}$)  
   - $W_L$, $W_C$, $W_{\text{belt}}$: Pesos de carga, carro y banda [N]  

- **Torque de carga reflejado**:
  
   $$T_{\text{load-in}} = \frac{F_{\text{ext}}}{\eta N_{\text{BD}}}$$
  
   - $F_{\text{ext}} = F_f + F_g + F_p$ (Fuerza externa total)  


📚 Ejercicio 13:

Un sistema de banda transportadora industrial mueve cajas de 80 kg sobre una plataforma que pesa 20 kg. La banda pesa 15 kg y está accionada por dos piñones idénticos (IP y LP) con inercia de 0.05 kg·m² cada uno. El tambor motriz tiene un radio de 0.1 m y el sistema opera con una eficiencia del 85%. Considerando un coeficiente de fricción de 0.3 y una pendiente de 5°, calcule:  

1. La inercia reflejada total en el eje del motor  
2. El torque requerido para mover la carga  


**Datos:**  
- Pesos: $W_L = 80\,kg \times 9.81 = 784.8\,N$, $W_C = 20\,kg \times 9.81 = 196.2\,N$, $W_{\text{belt}} = 15\,kg \times 9.81 = 147.15\,N$  
- $J_p = 0.05\,kg·m²$ (para cada piñón)  
- $r_{ip} = 0.1\,m$ → $N_{\text{BD}} = \frac{1}{0.1} = 10\,m^{-1}$  
- $\eta = 0.85$, $\mu = 0.3$, $\beta = 5°$  

**Procedimiento:**  

- Inercia Reflejada Total
  
   $$J_{\text{ref}}^{\text{trans}} = 2J_p + \frac{1}{\eta N_{\text{BD}}^2} \left( \frac{W_L + W_C + W_{\text{belt}}}{g} \right)$$  

   $$= 2(0.05) + \frac{1}{0.85 \times 10^2} \left( \frac{784.8 + 196.2 + 147.15}{9.81} \right)$$
  
   $$= 0.1 + \frac{1}{85} \times 115 \approx \boxed{1.45\,kg·m²}$$

-Torque de Carga

   - Fuerzas externas:
     
     $$F_f = 0.3 \times 1128.15 \times \cos 5° \approx 337.1\,N$$
      
     $$F_g = 1128.15 \times \sin 5° \approx 98.3\,N$$
      
     $$F_{\text{ext}} = 337.1 + 98.3 = 435.4\,N$$
     
   - Torque reflejado:
       
     $$T_{\text{load-in}} = \frac{435.4}{0.85 \times 10} \approx \boxed{51.2\,N·m}$$

- Potencia del Motor

   - Aceleración angular equivalente ($\alpha$):
     
     $$a = r_{ip} \alpha \Rightarrow \alpha = \frac{0.5}{0.1} = 5\,rad/s²$$  
   - Torque dinámico:
     
     $$\tau_{\text{din}} = J_{\text{ref}}^{\text{trans}} \times \alpha = 1.45 \times 5 = 7.25\,N·m$$
     
   - Torque total:
      
     $$\tau_{\text{total}} = 51.2 + 7.25 = 58.45\,N·m$$


## 10. Conclusiones

- La relación de transmisión en un tornillo sin fin depende del número de hilos del tornillo y del número de dientes de la rueda, permitiendo obtener grandes reducciones en un solo paso, ideal para sistemas de alta carga y baja velocidad.

- El paso (lead) y el cabeceo (pitch) son parámetros clave para comprender el desplazamiento lineal por vuelta del tornillo. Su relación inversa permite transformar movimientos angulares en desplazamientos lineales precisos.

- El husillo de bolas, a diferencia de la rosca directa, reduce la fricción gracias a la recirculación de bolas, mejorando la eficiencia, precisión y vida útil, aunque con mayor costo y complejidad.

- El piñón-cremallera convierte movimiento rotativo en lineal con una relación directa entre la velocidad angular del piñón y la velocidad lineal de la cremallera, siendo ideal para trayectorias largas y repetitivas.

- El concepto de inercia reflejada permite modelar todo el sistema en un único dominio (rotacional o lineal), facilitando el diseño y análisis de controladores en sistemas mecatrónicos.

- En los sistemas con banda transportadora de múltiples rodillos, la velocidad lineal de la banda permanece constante, mientras que las velocidades angulares de los rodillos cambian dependiendo de sus radios, lo que debe considerarse en el diseño y sincronización del sistema.

- A mayor paso de tornillo, menor será la inercia reflejada al eje del motor, lo que puede mejorar la respuesta dinámica del sistema. Sin embargo, esto puede comprometer la precisión en aplicaciones de control fino.


## 11. Referencias

[1] Bolton, W. *Mechatronics: Electronic Control Systems in Mechanical and Electrical Engineering*. Pearson Education, 2015.

[2] Nise, N. S. *Control Systems Engineering*. Wiley, 2019.

[3] Manrique, J. (2024). Apuntes de clase sobre Transmisiones Mecánicas y Dinámica. Universidad XYZ.

[4] De Silva, C. W. *Mechatronics: An Integrated Approach*. CRC Press, 2005.

[5] “Ball Screws vs Lead Screws.” Thomson Linear, [https://www.thomsonlinear.com](https://www.thomsonlinear.com)

[6] Myszka, D. *Machines and Mechanisms: Applied Kinematic Analysis*. Pearson, 2011.

[7] MathWorks. (2023). *Simulink Documentation*. Recuperado de: [https://www.mathworks.com/help/simulink](https://www.mathworks.com/help/simulink)

[8] MathWorks. (2023). *MATLAB Documentation*. Recuperado de: [https://www.mathworks.com/help/matlab](https://www.mathworks.com/help/matlab)



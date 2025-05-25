# Control de Movimiento Clase 30 de Abril.

Julian Stiven Redondo Chacon & Sebastian Cifuentes Alfonso & David Esteban Vasquez Alarcon

## Indice

## 1. Introduccion 

En el estudio de los sistemas de control de movimiento, los mecanismos de transmisión de potencia y movimiento son fundamentales para transformar la energía generada por un actuador (como un motor) en un desplazamiento útil. A lo largo del semestre, ya hemos explorado diferentes tipos de transmisión, como engranajes, correas y poleas, entendiendo cómo modifican velocidad, fuerza y dirección del movimiento.

Sin embargo, no todos los sistemas de transmisión están diseñados únicamente para rotar. En aplicaciones donde se requiere un desplazamiento lineal preciso, entran en juego otros componentes clave, como el tornillo guía, también conocido como husillo o tornillo de potencia. Estos elementos convierten el movimiento rotacional de un motor en un desplazamiento lineal mediante una tuerca acoplada, lo que resulta esencial en maquinaria CNC, impresoras 3D, actuadores lineales y muchos sistemas mecatrónicos.

## 2. Tornillo sin fin

El tornillo sin fin es un sistema de transmisión de movimiento entre ejes que se cruzan (generalmente en ángulo recto). Está compuesto por dos partes principales:

El tornillo sin fin: una especie de tornillo largo con rosca helicoidal.

La rueda dentada o corona: un engranaje circular cuyos dientes encajan con la rosca del tornillo.

**¿Cómo funciona?**

Cuando el tornillo gira, su rosca empuja los dientes de la rueda dentada, haciendo que esta gire. A diferencia de los engranajes comunes, en este sistema solo el tornillo puede mover la rueda, pero no al revés, lo que lo hace ideal para aplicaciones donde se requiere autobloqueo (es decir, que el movimiento no se devuelva por sí solo).

![image](https://github.com/rJulian16/APUNTES-CONTROL/blob/95a886188d245055c909f251f3c0262a91ed5216/Corte%203/Imagenes/tornillo.gif)

Figura 1. Tornillo sin fin

### 2.1 Tipos de Tornillo Guía

En sistemas de transmisión lineal, se utilizan distintos tipos de roscas en los tornillos guía. Los más comunes en aplicaciones mecánicas son:

#### 2.1.1 Tornillo de rosca trapezoidal

**Definición:**
Tiene una rosca con forma de trapecio. Su diseño permite una buena combinación entre eficiencia y resistencia, lo que lo hace adecuado para cargas moderadas y movimientos repetitivos.

**Usos comunes:**

- Husillos de mesas de máquinas-herramienta

- Prensas mecánicas

- Sistemas donde se necesita autobloqueo

![image](https://github.com/user-attachments/assets/a28ed022-25dd-45fc-b21a-e445c3f58fed)

Figura 2. Tornillo sin fin con rosca trapezoidal

#### 2.1.2 Tornillo de rosca cuadrada

**Definición:**
Tiene una rosca con forma rectangular (cuadrada), lo que reduce el rozamiento durante el movimiento. Es más eficiente que el trapezoidal pero más difícil de fabricar.

**Usos comunes:**

- Prensas de alta precisión

- Sistemas que requieren alta eficiencia mecánica

- Aplicaciones donde no se necesita autobloqueo

![image](https://github.com/user-attachments/assets/f236ff3a-7840-4beb-9444-8614ecfdff21)

Figura 3. Tornillo sin fin con rosca cuadrada


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

#### 2.1.3 Tornillo de rosca directa

**Definición:**

También conocido como tornillo de fricción, es un tornillo guía tradicional en el que la tuerca desliza directamente sobre la rosca del tornillo. El contacto es metal contra metal, sin elementos intermedios.

**Usos comunes:**

- Sistemas simples de posicionamiento

- Ajustes manuales en maquinaria

- Donde se requiere autobloqueo y bajo costo

![image](https://github.com/user-attachments/assets/cbae456c-809f-4a90-959d-275ddc403f80)

Figura 4. Tornillo sin fin con rosca directa

#### 2.1.4 Tornillo con recirculación de bolas (Ball Screw)

**Definición:**

Es un tipo de tornillo guía que utiliza bolas de acero entre el tornillo y la tuerca. Estas bolas circulan dentro de un canal cerrado (recirculación), lo que reduce la fricción y mejora la eficiencia del sistema.

**Usos comunes:**

- Máquinas CNC y robótica

- Impresoras 3D de alta precisión

- Actuadores lineales rápidos y eficientes

![image](https://github.com/user-attachments/assets/92b9a89e-61cf-4f37-a892-37d524bb153e)

Figura 5. Tornillo sin fin con recirculacion de bolas


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

Figura 6. Backlash

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

### 4.1 Relacion de trasmision cabeceo-paso

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

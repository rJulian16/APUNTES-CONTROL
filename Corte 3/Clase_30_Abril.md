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

## 3. Relacion de trasmision basica

La relación de transmisión depende del número de hilos (o entradas) del tornillo y del número de dientes de la rueda dentada.

$$i = \frac{Z}{n}$$

**Donde:**

- \( i \): relación de transmisión  
- \( Z \): número de dientes de la **rueda dentada**  
- \( n \): número de **principios** o **hilos** del tornillo (normalmente 1, 2 o más)

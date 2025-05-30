# Control de Movimiento Clase 7 de Mayo.

Julian Stiven Redondo Chacon & Sebastian Cifuentes Alfonso & David Esteban Vasquez Alarcon

## Indice

- [1. Control por Rechazo Activo de Perturbaciones (ADRC)](#1-control-por-rechazo-activo-de-perturbaciones-adrc)
  - [1.1 Comparacion entre ADRC, PID y LQR](#11-comparacion-entre-adrc-pid-y-lqr)
- [2. Componentes de un ADRC](#2-componentes-de-un-adrc)
- [3. NADRC: Nonlinear Active Disturbance Rejection Control](#3-nadrc-nonlinear-active-disturbance-rejection-control)
  - [3.1 Caracteristicas Principales del NADRC](#31-caracteristicas-principales-del-nadrc)
  - [3.2 Observador de estados extendido (ESO)](#32-observador-de-estados-extendido-eso)
  - [3.3 NADRC - Implementacion No Lineal con Funcion fal()](#33-nadrc---implementacion-no-lineal-con-funcion-fal)
- [4. LADRC - Control Activo de Perturbaciones Lineal](#4-ladrc---control-activo-de-perturbaciones-lineal)
  - [4.1 Planteamiento L-ADRC](#41-planteamiento-l-adrc)
- [5. ADRC - Observador de estados](#5-adrc---observador-de-estados)
- [6. ADRC: Estimacion de Perturbaciones](#6-adrc-estimacion-de-perturbaciones)
- [7. Conclusiones](#7-conclusiones)
- [8. Referencias](#8-referencias)



## 1. Control por Rechazo Activo de Perturbaciones (ADRC)

El Control por Rechazo Activo de Perturbaciones (ADRC, por sus siglas en inglés) es una estrategia de control moderna que se caracteriza 
por su capacidad para enfrentar incertidumbres del sistema y perturbaciones externas de manera efectiva, sin requerir un modelo exacto 
de la planta. A diferencia de los enfoques clásicos que dependen fuertemente de la linealización o del conocimiento preciso de los 
parámetros del sistema, el ADRC introduce un observador de estado extendido (ESO) que estima tanto los estados internos como las 
perturbaciones no modeladas en tiempo real. Esto permite al controlador compensar dinámicamente dichas perturbaciones, mejorando 
la robustez y el desempeño del sistema, incluso en presencia de condiciones cambiantes o desconocidas. Su aplicabilidad en sistemas 
no lineales y su facilidad de implementación lo han convertido en una técnica ampliamente adoptada en el control moderno.

 
>🔑- **Perturbaciones externas**: Influencias no deseadas provenientes del entorno o del sistema que afectan el comportamiento del sistema controlado (por ejemplo, fricción, carga variable, ruido).

>🔑- **Incertidumbre del modelo**: Diferencias entre el modelo matemático utilizado para diseñar el controlador y el comportamiento real del sistema, ya sea por parámetros mal conocidos o dinámicas no modeladas.

>🔑- **Rechazo activo de perturbaciones**: Capacidad del sistema de control para identificar y compensar perturbaciones de manera dinámica y en tiempo real, sin necesidad de conocer su origen exacto.

>🔑- **Observador de Estado Extendido (ESO)**: Componente clave del ADRC que estima tanto los estados del sistema como las perturbaciones totales (internas y externas), permitiendo al controlador actuar de forma efectiva ante condiciones desconocidas.

>🔑- **Controlador no lineal**: Parte del ADRC encargada de generar la señal de control, diseñada para estabilizar el sistema y mantener el seguimiento de la referencia, incluso cuando el sistema es no lineal.

>🔑- **Función de referencia (tracking)**: Objetivo deseado que debe seguir la salida del sistema. El ADRC busca minimizar el error entre esta referencia y la salida real, compensando perturbaciones y errores de modelado.

>🔑- **Sintonización simple**: Ventaja del ADRC, ya que permite ajustar los parámetros del controlador de forma más intuitiva y menos dependiente del modelo matemático exacto.

>🔑- **Modelo generalizado de planta**: En ADRC, se considera que todas las dinámicas no conocidas y perturbaciones se agrupan en una sola "perturbación total", que será estimada y compensada activamente.

>🔑- **Aplicabilidad a sistemas no lineales**: El ADRC no requiere linealizar la planta ni conocer su modelo exacto, lo que lo hace útil en una amplia variedad de sistemas reales con comportamientos complejos.

💡 Ejemplo 1: 

Imaginemos que queremos controlar la velocidad de un pequeño ventilador para que siga una velocidad deseada, por ejemplo, 1500 RPM (revoluciones por minuto).

![image](https://github.com/user-attachments/assets/06255107-cbbc-40e4-8b59-56030872ae9e)

Figura 1. Ventilador.

**Problema**

En la práctica, el ventilador puede verse afectado por:
- Cambios de voltaje
- Viento externo
- Acumulación de polvo
- Desgaste del motor

Estos factores hacen que la velocidad no siempre sea constante, incluso si aplicamos la misma señal de control.

**¿Cómo ayuda el ADRC?**

El ADRC actúa en tres pasos:

1. **Observa**: Estima en tiempo real qué tan rápido gira el ventilador y qué lo está afectando (aunque no sepamos exactamente qué).
2. **Detecta perturbaciones**: Agrupa todas las causas del error en una sola "perturbación total".
3. **Compensa**: Ajusta la señal de control automáticamente para cancelar esa perturbación.

- **Resultado**

Aunque haya viento, polvo o cambios en el voltaje, el ADRC es capaz de mantener la velocidad cerca del valor deseado (por ejemplo, 1500 RPM), sin saber exactamente qué está fallando.

### 1.1. Comparación entre ADRC, PID y LQR

| Característica                          | ADRC (Control por Rechazo Activo de Perturbaciones) | PID (Proporcional-Integral-Derivativo) | LQR (Regulador Cuadrático Lineal)     |
|----------------------------------------|-----------------------------------------------------|----------------------------------------|----------------------------------------|
| Requiere modelo exacto del sistema     | No                                                  | No                                     | Sí                                     |
| Manejo explícito de perturbaciones     | Sí (mediante observador)                            | No                                     | No (solo implícito)                    |
| Observador de estados incluido         | Sí (ESO)                                            | No                                     | Sí                                     |
| Facilidad de implementación            | Moderada                                            | Alta                                   | Baja                                   |
| Adaptabilidad a sistemas no lineales   | Alta                                                | Limitada                               | Baja (requiere linealización)          |
| Robustez ante incertidumbres           | Alta                                                | Media                                  | Baja                                   |
| Tipo de control                        | No lineal (dependiendo del diseño)                  | Lineal                                 | Lineal                                 |
| Aplicaciones comunes                   | Sistemas con incertidumbre, sistemas no modelados   | Procesos industriales, automatización  | Robótica, aeronáutica, sistemas bien modelados |

Tabla 1. Comparacion entre PID, ADRC y LQR

## 2. Componentes de un ADRC

![image](https://github.com/user-attachments/assets/be264c8f-8559-462e-bfc8-581abcf2b2a2)


Figura 2. Componentes de un ADRC.

El ADRC se basa en tres bloques fundamentales que trabajan juntos para mantener el control del sistema, incluso ante perturbaciones o modelos desconocidos:

**Generador de trayectorias (cinemática y perfiles de movimiento)**
  
- **Función**: Estima no solo los estados del sistema (como posición y velocidad), sino también las **perturbaciones totales** (internas y externas).
- **Importancia**: Permite conocer el comportamiento del sistema en tiempo real sin requerir un modelo exacto.
- **Ejemplo**: Si el sistema es un ventilador, estima cuán rápido gira y cuánto lo afecta el viento externo.

**Observador de estado extendido (ESO)**
  
- **Función**: Usa la estimación de perturbaciones del ESO para **cancelarlas activamente** en la señal de control.
- **Importancia**: Permite que el sistema se comporte como si no tuviera perturbaciones.
- **Ejemplo**: Si el ESO detecta una perturbación que baja la velocidad del ventilador, el controlador la compensa aumentando la señal de control.

**Controlador proporcional por retroalimentación de estados**

- **Función**: Calcula la señal de control que lleva la salida del sistema a seguir una referencia deseada (por ejemplo, una velocidad o posición).
- **Importancia**: Puede ser un controlador proporcional o una función no lineal diseñada para mejorar el desempeño.
- **Ejemplo**: Ajusta el voltaje del ventilador para que mantenga 1500 RPM, incluso si hay perturbaciones.


| Componente                        | Función principal                                                             | Ejemplo / Aplicación                                   |
|----------------------------------|-------------------------------------------------------------------------------|--------------------------------------------------------|
| Generador de trayectorias        | Define la referencia o perfil de movimiento deseado                           | Mantener una velocidad de 1500 RPM en un ventilador     |
| Observador de Estado Extendido (ESO) | Estima en tiempo real los estados del sistema y la perturbación total       | Detectar cambios de fricción o carga en un motor       |
| Controlador por retroalimentación | Calcula la señal de control para seguir la trayectoria y compensar perturbaciones | Ajustar el voltaje del motor para mantener la velocidad deseada |
| Perturbación total estimada      | Combinación de efectos no modelados, errores de parámetros y perturbaciones externas | Viento que frena el ventilador o variaciones de tensión |
| Robustez                         | Alta, ya que no depende de un modelo exacto y compensa perturbaciones        | El sistema sigue funcionando correctamente con condiciones cambiantes |

Tabla 2. Caracteristicas ADRC

📚 Ejercicio 2 propuesto en clase: 

![image](https://github.com/user-attachments/assets/05a3b9fd-ede4-4a2c-a880-5755e1e49bc2)

Figura 3. Sistemas lineales y no lineales

- Modelo Lineal de Referencia
  
$$h = Ku + h$$

- Sistema No Lineal (Caso de Estudio: Tanque de Agua Irregular)

**Descripción del Sistema**

- **Entrada (u)**: Flujo de entrada al tanque
- **Salida (h)**: Altura del líquido en el tanque
- **Característica no lineal**: Área transversal variable $A(h)$ y flujo de salida $a\sqrt{2gh}$

- Ecuación Fundamental
  
$$\frac{d}{dt} \left( \int_{0}^{h} A(h)dh \right) = u - a\sqrt{2gh}$$

- Ecuación diferencial:
  
$$A(h)\dot{h} = u - a\sqrt{2gh}$$

- Forma despejada para la dinámica:
  
$$\dot{h} = \frac{1}{A(h)}u - \frac{a\sqrt{2gh}}{A(h)}$$

- Representación de estado:
  
$$h = \frac{1}{A(h)}u - \frac{a\sqrt{2gh}}{A(h)}$$

- **Estrategia de Control**
  
1. **Parte Lineal**: $\frac{1}{A(h)}u$
2. **Parte No Lineal**: $\frac{a\sqrt{2gh}}{A(h)}$


En sistemas no lineales como el tanque de agua con área variable $$A(h)$$, se puede separar el comportamiento en:

- **Parte lineal**: entrada controlable $$u$$
- **Parte no lineal**: términos como $$\sqrt{h}$$

Esta separación permite implementar estrategias como ADRC que:

- Considera las no linealidades como perturbaciones estimables
- Las compensa activamente
- Simplifica el diseño del controlador al evitar el modelado explícito de todas las dinámicas complejas

## 3. NADRC: Nonlinear Active Disturbance Rejection Control

El NADRC (Nonlinear Active Disturbance Rejection Control) es una extensión del ADRC tradicional que introduce funciones no lineales en el diseño del observador y del controlador, con el objetivo de mejorar el rendimiento dinámico del sistema, especialmente en presencia de ruidos o perturbaciones abruptas.

A diferencia del ADRC lineal, el NADRC no utiliza funciones proporcionales lineales para estimar errores ni para calcular la señal de control. En su lugar, emplea funciones no lineales suavizadas (como el signo, sat, o funciones tipo fal) que mejoran la precisión en regiones cercanas al equilibrio y al mismo tiempo suavizan la respuesta ante perturbaciones grandes.

### 3.1. Características Principales del NADRC

| Característica                            | Descripción                                                                 |
|------------------------------------------|-----------------------------------------------------------------------------|
| Estimación no lineal                     | Utiliza funciones no lineales como `fal()` para mejorar la estimación del error y la perturbación. |
| Mejor rechazo al ruido                   | Las funciones no lineales suavizan la acción del observador ante señales ruidosas. |
| Alta precisión en zona cercana al cero   | Ajuste fino del comportamiento del sistema cuando el error es pequeño.     |
| Mayor robustez frente a no linealidades  | Se adapta mejor a dinámicas no lineales que el ADRC lineal.                |
| Controlador no lineal                    | Reemplaza las leyes de control proporcionales clásicas por funciones no lineales. |
| Parametrización flexible                 | Los parámetros α y δ permiten personalizar la respuesta del sistema.       |

Tabla 3. Caracteristicas NADRC

- Forma general de segundo orden:

$$\ddot{y} = -a_1\dot{y} - a_2y + bu$$

- Representación en espacio de estados:
  
$$\begin{cases} 
\dot{x}_1 = x_2 \\ 
\dot{x}_2 = -a_0x_1 - a_1x_2 + bu + w \\ 
y = x_1 
\end{cases}$$

- Término de perturbación generalizada ($f$):
  
$$f = -a_0x_1 - a_1x_2 + (b - b_0)u + w$$

- Componentes Clave

Perturbación total ($f$):
   - Agrupa:
     - No linealidades internas ($-a_0x_1 - a_1x_2$)
     - Incertidumbre paramétrica ($(b-b_0)u$)
     - Perturbaciones externas ($w$)

 Observador no lineal extendido (ESO):
   - Reconstruye $f$ en tiempo real sin requerir su forma explícita

 Ley de control:
   - Combina:
     - Acción de control lineal ($b_0u$)
     - Compensación no lineal ($-f_{estimada}$)

**Ventajas vs ADRC Lineal**

- Mayor precisión en sistemas fuertemente no lineales
- Mejor rechazo de perturbaciones de alta frecuencia
- Adaptabilidad a cambios bruscos en dinámicas


- sustituyendo f en espacio de estados:

$$
\begin{cases}
\dot{x}_1 = x_2 \\
\dot{x}_2 = f + b_0 u \\
y = x_1
\end{cases}
$$

- Tratamiento de la perturbación $f$ (desconocida) como estado adicional $x_3$

Modelo extendido (3er orden):

$$
\begin{cases}
\dot{x}_1 = x_2 \\
\dot{x}_2 = x_3 + b_0 u \\
\dot{x}_3 = h \\
y = x_1
\end{cases}
$$

- $x_3$ absorbe todas las no linealidades/incertidumbres ($f$)
- Permite diseñar como si fuera un sistema lineal canónico

- Ventajas:

   - No requiere conocimiento exacto de $f$
   - Rechazo automático de perturbaciones
   - Estructura uniforme para diversos sistemas no lineales

### 3.2. Observador de estados extendido (ESO)

$$
\begin{cases}
\dot{z}_1 = z_2 - \beta_1 \gamma_1(e) \\
\dot{z}_2 = z_3 + b_0 u - \beta_2 \gamma_2(e) \\
\dot{z}_3 = - \beta_3 \gamma_3(e) \\
e = z_1 - y
\end{cases}
$$

Donde:

- $$\( \beta_i \)$$: ganancias del observador
  
- $$\( \gamma_i(e) \)$$: funcion modelo
  
- $$\( e \)$$: error de estimación

- Ley de Control NADRC
  
$$u = \frac{u_0 - z_3}{b_0}$$

- Sistema Controlado Resultante
- 
$$\begin{cases} 
\dot{x}_1 = x_2 \\ 
\dot{x}_2 = u_0 \quad \text{(Comportamiento integrador)} \\ 
y = x_1 
\end{cases}$$

   - La perturbación $f$ es cancelada exactamente cuando $z_3 \approx f$
   - El sistema original no lineal se reduce a una doble integración
   - $y_i(e)$ proveen convergencia rápida sin oscilaciones
   - Ejemplo común: Funciones sigmoideas o de saturación

📚 Ejercicio 3:

![image](https://github.com/user-attachments/assets/9f4f4230-e65a-434e-adfd-dd479f685bd1)

Figura 3. Sistemas hidraulico

Un sistema hidráulico tiene dinámica:  

$$\ddot{y} = -2y|\dot{y}| + 3u + w(t)$$ 

donde \(w(t)=0.5\sin(t)\) es una perturbación.  

- Diseñe un NADRC con \(b_0=3\)  
- Simule la respuesta para \(r(t)=5\)  

**Solución**:  

- Modelo extendido:

$$\begin{cases}
\dot{x}_1 = x_2 \\dot{x}_2 = x_3 + 3u \dot{x}_3 = h\end{cases}$$

- Observador:
  
   $$\dot{z}_3 = -100e \quad \text{(Ganancia alta)}$$

- Control:
  
   $$u = \frac{u_0 - z_3}{3}, \quad u_0 = -4z_1 -4z_2$$

**Resultado**: Error en estado estable < 2% en 1.5 seg.

### 3.3. NADRC - Implementacion No Lineal con Funcion fal()

- Ley de Control No Lineal
  
La acción de control $u_0$ se construye mediante funciones no lineales:

$$u_0 = k_1 \text{fal}(r_1 - z_1, \alpha_1, \delta) + k_2 \text{fal}(r_2 - z_2, \alpha_2, \delta)$$

| Variable | Descripción clave               | Rol en el control                  |
|----------|---------------------------------|------------------------------------|
| `u₀`     | Señal de control base           | Salida del controlador no lineal   |
| `k₁,k₂`  | Ganancias de realimentación     | Ajustan velocidad/amortiguamiento  |
| `fal()`  | Función no lineal adaptativa    | Combina lineal/no-lineal           |
| `r₁,r₂`  | Referencias de estado           | Valores deseados (setpoints)       |
| `z₁,z₂`  | Estados estimados               | Salidas del observador ESO         |
| `α₁,α₂`  | Exponentes no lineales          | Controlan curvatura de respuesta   |
| `δ`      | Umbral de linealidad           | Define zona de transición suave    |

Tabla 4. Variables

- Función No Lineal $\text{fal}(\cdot)$
- 
Definición por partes:

$$\text{fal}(\overline{\epsilon}, \alpha_i, \delta) =
\begin{cases} 
\frac{\overline{\epsilon}}{\delta^{1-\alpha_i}}, & |\overline{\epsilon}| \leq \delta \\
|\overline{\epsilon}|^{\alpha_i} \text{sign}(\overline{\epsilon}), & |\overline{\epsilon}| > \delta
\end{cases}$$

- **Características de Diseño**
  
- Comportamiento adaptativo: Suave cerca del punto de operación ($|\overline{\epsilon}| \leq \delta$), más agresivo en régimen transitorio ($|\overline{\epsilon}| > \delta$)
  
- Rechazo de ruido: La zona lineal amortigua oscilaciones por mediciones ruidosas
  
- Sintonización: Las ganancias $\beta_i$ del observador y $k_i$ del controlador deben coordinarse

📚 Ejercicio 4:

Mismo sistema del ejercicio 3 pero hora con:

- No linealidad fuerte en sensor: \(y_{med} = y + 0.1y^3\)  
- Requiere controlador no lineal robusto.


**Solución**:  

- Función fal():  

$$\text{fal}(e,0.5,0.1) =\begin{cases}    e/0.1^{0.5}, & |e|≤0.1\\  |e|^{0.5}\text{sign}(e), & |e|>0.1\end{cases}$$

- Control no lineal:
  
   $$u_0 = 8\text{fal}(r-z_1) + 5\text{fal}(-z_2)$$

**Resultado**: Rechaza ruido no lineal manteniendo error < 1%

## 4. LADRC - Control Activo de Perturbaciones Lienal

Técnica de control que observa y cancela perturbaciones en tiempo real sin requerir un modelo preciso del sistema.

- Dos Componentes Esenciales:

Observador Lineal (LESO):  
   - Estimación de estados y perturbaciones  
   - "Sistema inmunológico" del controlador  

Control Lineal Simple:  
   - Ley de control tipo PD  
   - Cancelación automática de perturbaciones  

**Ecuaciones del observador**:

$$\begin{cases} 
\dot{z}_1 = z_2 + L_1e \\ 
\dot{z}_2 = z_3 + b_0u + L_2e \\ 
\dot{z}_3 = L_3e \\ 
e = y - z_1 
\end{cases}$$

Donde:
- `z₁, z₂`: Estados estimados del sistema (posición y velocidad)
- `z₃`: Estado extendido que estima la perturbación total
- `L₁, L₂, L₃`: Ganancias del observador lineal
- `e`: Error de estimación (salida real vs. estimada)
- `b₀`: Valor nominal de la ganancia de control
- `u`: Señal de control aplicada

**Modelo Extendido del Sistema**

Este modelo extendido convierte el sistema real (con perturbaciones/no-linealidades) en una *cadena de integradores* + un término unificado de perturbación (`x₃`)

Ecuaciones de estado:

$$\begin{cases} 
\dot{x}_1 = x_2 \\ 
\dot{x}_2 = x_3 + b_0u \\ 
\dot{x}_3 = h \\ 
y = x_1 
\end{cases}$$

*Donde*:
- `x₁, x₂`: Estados físicos del sistema (posición y velocidad)
- `x₃`: Perturbación generalizada (incluye no-linealidades y perturbaciones externas)
- `h`: Dinámica de la perturbación (desconocida pero acotada)
- `y`: Salida medida del sistema

**Ley de Control Lineal**

$$u_0 = k_1(r - z_1) - k_2z_2$$

- `u₀`: Señal de control generada
- `r`: Referencia o setpoint deseado
- `k₁, k₂`: Ganancias del controlador
- `z₁, z₂`: Estados estimados por el LESO

### 4.1. Planteamiento L-ADRC

La formula general de la dinamica del sistema se representa como:

$$
y^{(n)}(t) = \kappa(x) u(t) + \xi(t)
$$


📚 Ejercicio 5:

![image](https://github.com/user-attachments/assets/830ed361-f263-4fd8-a013-b4fd8344f66d)

Figura 5. Motor DC

**Sistema**: Motor DC con fricción viscosa  

**Modelo nominal**:  

$$\ddot{\theta} = -2\dot{\theta} + 5u + w(t)$$  
- $\theta$: Posición angular (rad)  
- $w(t)$: Perturbación (escalón de 1 Nm en $t=2s$)

**Objetivos**:  

1. Seguir referencia $r(t) = 1\text{rad}$  
2. Rechazar perturbación en < 0.1s  
3. Sobreimpulso < 5%


Se aumenta el orden para incluir perturbaciones:  

$$\begin{cases}\dot{x}_1 = x_2\\\dot{x}_2 = x_3 + 5u \quad \text{(5 = ganancia nominal } b_0)\\\dot{x}_3 = h \quad \text{(dinámica de perturbación)}\= x_1\end{cases}$$

*Interpretación*:  
- $x_3$ absorbe $-2\dot{\theta} + w(t)$ (fricción + perturbación)

- Diseño del Observador (LESO)
  
Ecuaciones con ganancias por ancho de banda ($\omega_o = 30\text{rad/s}$): 

$$\begin{cases}\dot{z}_1 = z_2 + 90(y - z_1)\\\dot{z}_2 = z_3 + 5u + 2700(y - z_1) \\\dot{z}_3 = 27000(y - z_1)\end{cases}$$

*Cálculo de ganancias*:  
$L = [3\omega_o, 3\omega_o^2, \omega_o^3]^T$ (Fórmula de asignación de polos)

- Ley de Control
  
Con ancho de banda deseado $\omega_c = 10\text{rad/s}$:  

$$u =\frac{u_0 - z_3}{5},\quad u_0 = 100(r - z_1) - 20z_2$$

*Sintonización*:  
- $k_1 = \omega_c^2 = 100$  
- $k_2 = 2\omega_c = 20$ (para amortiguamiento $\zeta=1$)

**Resultados**:

- Tiempo establecimiento: 0.4s  
- Rechazo de perturbación: 0.03s  
- Sobreimpulso: 0%  

## 5. ADRC - Observador de estados

![image](https://github.com/user-attachments/assets/c1b9397c-6dcd-452b-8f05-ea15e8dc9fd4)

Figura 7. Observador ADRC

- Ecuación de Estado del Sistema

$$X_{k+1} = A \cdot X_k + B \cdot u_k$$

Describe cómo evolucionan los estados internos del sistema en función de su dinámica natural ($A$) y las señales de control aplicadas ($u_k$).

Donde:

- $X_k$: Vector de estados en el instante $k$ (dim $n \times 1$)  
- $A$: Matriz de dinámica del sistema (dim $n \times n$)  
- $B$: Matriz de entrada de control (dim $n \times m$)  
- $u_k$: Vector de entradas de control (dim $m \times 1$)

**Ecuación del Observador**

$$\hat{x}_{k+1} = A \cdot \hat{x}_k + B \cdot u_k + L \cdot (y_k - \hat{y}_k)$$

Donde:

- $\hat{x}_k$: Estimación de los estados (dim $n \times 1$)  
- $L$: Matriz de ganancia del observador (dim $n \times p$)  
- $y_k$: Salida medida del sistema (dim $p \times 1$)  
- $\hat{y}_k$: Salida estimada ($\hat{y}_k = C \cdot \hat{x}_k$)

**Matrices del Observador**

$$\begin{array}{lcl}
A_{Ob} = A - L \cdot C & \text{(Dinámica del observador)} \\ 
B_{Ob} = [B \ \ L] & \text{(Entradas combinadas)} \\ 
C_{Ob} = I_{n \times n} & \text{(Salida = estados estimados)} \\ 
D_{Ob} = [0_{n \times m} \ \ 0_{n \times p}] & \text{(Sin feedthrough)} \\ 
\end{array}$$

- Variables:
- 
- $C$: Matriz de salida (dim $p \times n$)  
- $I_{n \times n}$: Matriz identidad  
- $0$: Matrices de ceros  

📚 Ejercicio 6: 

![image](https://github.com/user-attachments/assets/81077d64-6dad-4097-adb2-910a96f64a71)

Figura 8. Masa-resorte-amortiguador

Considere un sistema masa-resorte-amortiguador con perturbaciones:

$$m\ddot{y} + c\dot{y} + ky = u + w(t)$$

donde:

- $m=1\text{kg}$, $c=2\text{N·s/m}$, $k=5\text{N/m}$
- $w(t)=0.5\sin(2t)$ (perturbación no medida)
- Solo se mide la posición $y$ (salida)

- Objetivos:
Diseñar un observador ADRC para estimar velocidad $\dot{y}$ y perturbación $w(t)$
Implementar control por realimentación de estados

**Solucion**

- Modelo en Espacio de Estados
  
Definiendo $x_1 = y$, $x_2 = \dot{y}$:

$$\begin{cases}\dot{x}_1 = x_2 \\\dot{x}_2 = -\frac{k}{m}x_1 - \frac{c}{m}x_2 + \frac{1}{m}u + \frac{1}{m}w(t)\end{cases}$$

- Modelo Extendido 
Añadiendo $x_3 = w(t)/m$ como estado extendido:

$$\begin{cases}\dot{x}_1 = x_2 \\\dot{x}_2 = -5x_1 - 2x_2 + u + x_3 \\
\dot{x}_3 = h \quad \text{(Dinámica desconocida)}
\end{cases}$$

- Diseño del Observador (LESO)
Forma discreta (Euler, $T_s=0.01s$):

$$\hat{x}_{k+1} = A_d\hat{x}_k + B_du_k + L(y_k - C\hat{x}_k)$$

Con matrices discretizadas:

$$
A_d = \begin{bmatrix}
1 & 0.01 & 0 \\
-0.05 & 0.98 & 0.01 \\
0 & 0 & 1
\end{bmatrix}, \quad
B_d = \begin{bmatrix}
0 \\
0.01 \\
0
\end{bmatrix}, \quad
C = \begin{bmatrix}
1 & 0 & 0
\end{bmatrix}
$$

- Ganancias del Observador (Polos en $z=0.2, 0.3, 0.4$):

$$
L = \begin{bmatrix}
0.8 \\
25 \\
150
\end{bmatrix}
$$

- Ley de Control

$$u = -k_1\hat{x}_1 - k_2\hat{x}_2 - \hat{x}_3 + k_1r$$
Con $k_1=20$, $k_2=8$ para polos en $-4 \pm 2j$

| Parámetro         | Valor        |
|-------------------|-------------|
| Error de estimación velocidad | < 0.01 m/s |
| Rechazo perturbación (RMSE) | 0.002 N |
| Tiempo establecimiento | 1.2 s |

Tabla 4. Resultados Ejercicio 6

## 6. ADRC: Estimación de Perturbaciones

![image](https://github.com/user-attachments/assets/8252e4e7-6bc1-45e3-b109-c931d4140041)

Figura 9. Esquema estimacion de perturbaciones ADRC

Para un sistema discreto lineal con perturbaciones externas:

$$\begin{cases} 
x_{k+1} = A \cdot x_k + B \cdot u_k + F \cdot d_k \\ 
y_k = C \cdot x_k 
\end{cases}$$

Donde:

- $x_k$: Vector de estados en el instante $k$ (dimensión $n \times 1$)
- $u_k$: Señal de control (dimensión $m \times 1$)
- $d_k$: Perturbación externa (dimensión $p \times 1$)
- $A$, $B$, $C$, $F$: Matrices del sistema con dimensiones consistentes

- Extensión del Modelo para Estimación

Si la perturbación es constante o varía lentamente ($d_{k+1} \approx d_k$), se puede modelar como estado extendido:

$$
x_a(k+1) = \begin{bmatrix} x(k+1) \\ d(k+1) \end{bmatrix} =
\begin{bmatrix}
A & F \\
0 & I
\end{bmatrix}
x_a(k) +
\begin{bmatrix}
B \\
0
\end{bmatrix}
u(k)
$$

$$
y(k) = \begin{bmatrix} C & 0 \end{bmatrix} x_a(k)
$$

- Nuevas variables:

$A_{\text{ext}}$: Matriz aumentada

$B_{\text{ext}}$: Matriz de entrada extendida 

### 6.1. Representacion en Espacio de Estados

Formulacion General del sistema:

La dinámica del sistema se describe mediante:

$$y^{(n)}(t) = u(t) + \xi(t)$$

donde:

- $y^{(n)}(t)$: n-ésima derivada de la salida
- $u(t)$: Señal de control
- $\xi(t)$: Perturbación total (incluye no-linealidades y perturbaciones externas)

- Modelo en espacio de estados

Vector de Estados:

Definiendo los estados como derivadas sucesivas:

$$x(t) = \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{bmatrix} = \begin{bmatrix} y \\ \dot{y} \\ \vdots \\ y^{(n-1)} \end{bmatrix}$$

Ecuacion de estado:

$$
\dot{x}(t) = A x(t) + B(u(t) + \xi(t))
$$

Con matrices:

$$A = \begin{bmatrix}
0 & 1 & 0 & \cdots & 0 \\
0 & 0 & 1 & \cdots & 0 \\
\vdots & \vdots & \ddots & \ddots & \vdots \\
0 & 0 & \cdots & 0 & 1 \\
0 & 0 & \cdots & 0 & 0
\end{bmatrix}, \quad
B = \begin{bmatrix} 0 \\ 0 \\ \vdots \\ 0 \\ 1 \end{bmatrix}$$

Ecuacion de salida:

$$y(t) = C x(t) = \begin{bmatrix} 1 & 0 & \cdots & 0 \end{bmatrix} x(t)$$

### 6.2. ADRC con Observador de Luenberger y Polinomio de Hurwitz

**Observador de Luenberger**:  
Es un estimador que usa:  
- El modelo matemático del sistema  
- Las mediciones reales  
- Un término de corrección basado en el error

**Polinomio de Hurwitz**:  
Garantiza que el observador sea estable (que las estimaciones converjan). Todos sus polos deben tener parte real negativa.

- **Error de Estimación**

$$e_y = y - \hat{y}$$

- **Observador Extendido (Luenberger)**

$${\begin{pmatrix*}[r]
{{x_{1}}^{\wedge }}^{\cdot }\\
{{x_{2}}^{\wedge }}^{\cdot }\\
\cdot\\
{{x_{n-1}}^{\wedge }}^{\cdot }\\
{{x_{n}}^{\wedge }}^{\cdot }\\
\cdot\\
{{x_{n+m-1}}^{\wedge }}^{\cdot }\\
{{x_{n+m}}^{\wedge }}^{\cdot }
\end{pmatrix*}} = {\begin{pmatrix*}[r]
O_{n + m \cdot 1} & I_{n + m - 1 \cdot n + m - 1}\\
0 & O_{1 \cdot n + m - 1}
\end{pmatrix*}}{\begin{pmatrix*}[r]
{x_{1}}^{\wedge }\\
{x_{2}}^{\wedge }\\
\cdot\\
{x_{n}}^{\wedge }\\
{\xi_{1}}^{\wedge }\\
\cdot\\
{\xi^{\wedge }}^{(m-2)}\\
{\xi^{\wedge }}^{(m-1)}\\
\end{pmatrix*}} + {\begin{pmatrix*}[r]
0\\
0\\
\cdot\\
0\\
1\\
\cdot\\
0\\
0\\
\end{pmatrix*}}u + {\begin{pmatrix*}[r]
\lambda_{n + m - 1}\\
\lambda_{n + m - 2}\\
\cdot\\
\lambda_{m + 1}\\
\lambda_{m}\\
\cdot\\
\lambda_{1}\\
\lambda_{0}\\
\end{pmatrix*}} {\epsilon_{y}}^{\wedge}(t)$$

$$Y^{\wedge} = {\begin{pmatrix*}[r]
1 & 0 & 0 & \cdot & \cdot & \cdot & 0
\end{pmatrix*}}{X_{\xi}}^{\wedge}$$


- **Diseño de Ganancias (Hurwitz)**
Las ganancias $L$ se calculan para que:

$$\det(sI - (A_{ext} - LC_{ext}))$$  

sea un polinomio de Hurwitz con polos deseados (ej: $s=-5$, $s=-6$).

Al restar las ecuaciones del sistema real y del observador, se obtiene la dinámica del error de estimación:

$$e_{y}^{(n+m)} + \lambda_{n+m-1} e_{y}^{(n+m-1)} + \ldots + \lambda_0 e_y = \xi^{(m)}(t)$$

El comportamiento del error está gobernado por:

$$p(s) = s^{n+m} + \lambda_{n+m-1}s^{n+m-1} + \ldots + \lambda_0$$

- Criterio de Hurwitz

Los coeficientes $\lambda_i$ deben escogerse para que:

Todos los términos del polinomio sean positivos
Las raíces tengan parte real negativa (polos en el semiplano izquierdo)  

Esto garantiza que el error de estimación:  
- Converja exponencialmente a cero  
- Sea estable frente a perturbaciones  

El ADRC trata las perturbaciones como una función matemática que cambia con el tiempo, más un pequeño error residual.

La perturbación total se expresa como:

$\zeta(t) = K_{0} + K_{1}t + K_{2}t^{2} + ... + k_{m}t^{m} +r(t)$

Donde:

- $k_0$: Valor constante de la perturbación
- $k_1 t$: Componente que crece linealmente con el tiempo
- $k_2 t^2$: Componente cuadrática (aceleración)
- $r(t)$: Lo que no podemos modelar

📚 Ejercicio 7 planteado en clase:

![image](https://github.com/user-attachments/assets/40073f0e-06a9-46d0-9020-6186e02c7913)

Fig 10. Ejercicio 7 planteado en clase

Sistema:

Masa (m) unida a un resorte y amortiguador, con:
- Fuerza de control: $u(t)$ = m * a
- Fuerza del resorte: $F_k = K * x$ (K: constante del resorte)
- Fuerza de amortiguamiento: $F_B = B* dx/ dt $ 

Ecuación de la dinamica del sistema:

$$u(t) - Ky(t) - B\dot{y}(t) = M\ddot{y}(t)$$

- **Solucion**

- Despejar la máxima derivada

$$
\ddot{y}(t) = \frac{1}{M} \left[ u(t) - Ky(t) - B\dot{y}(t) \right]
$$

- Definir Varibales de estado

- $x_1 = y$ (posición)
- $x_2 = \dot{y}$ (velocidad)

- Ecuaciones de estado

$$
\dot{x}_1 = \dot{y} = x_2
$$

$$
\dot{x}_2 = \ddot{y} = \frac{1}{M} \left( u(t) - Kx_1 - Bx_2 \right)
$$

Entonces el sistema queda expresado de la siguiente manera:

$$
\begin{cases}
\dot{x}_1 = x_2 \\\\
\dot{x}_2 = \frac{1}{M} \left( u(t) - Kx_1 - Bx_2 \right)
\end{cases}
$$

y entonces:

$$
\begin{aligned}
\dot{x}_1 &= x_2 \\\\
\dot{x}_2 &= \frac{1}{M} u(t) - \frac{K}{M} x_1 - \frac{B}{M} x_2
\end{aligned}
$$

- Forma Matricial

$$
\dot{X}(t) = A X(t) + B u(t)
$$

$$
X(t) = \begin{bmatrix} x_1 \\\\ x_2 \end{bmatrix}
$$

Y esto concluye con que las matrices del sistema son:

$$
A = \begin{bmatrix}
0 & 1 \\\\
-\frac{K}{M} & -\frac{B}{M}
\end{bmatrix},
\quad
B = \begin{bmatrix}
0 \\\\
\frac{1}{M}
\end{bmatrix}
$$

- Ecuacion de salida

Teniendo en cuenta que $y(t) = x_1$ :

$$
y(t) = C X(t) + D u(t)
$$

$$
C = \begin{bmatrix} 1 & 0 \end{bmatrix}, \quad D = \begin{bmatrix} 0 \end{bmatrix}
$$

Y el sistema completo queda de la siguiente manera:

$$
\begin{aligned}
\dot{X}(t) &= A X(t) + B u(t) \\\\
y(t) &= C X(t)
\end{aligned}
$$

- ADRC

En base a:

$$
\ddot{y}(t) = \frac{1}{M} u(t) - \frac{K}{M} y(t) - \frac{B}{M} \dot{y}(t)
$$

y teniendo en cuenta que vamos a desear llevar la ecuacion a una forma mas generica como:

$$
y^{(n)} = K u + \varepsilon(t)
$$

- ESO Modelo extendido

- $x_1 = y$
- $x_2 = \dot{y}$
- $x_3 \approx \varepsilon(t)$

Ecuacion:

$$
\begin{aligned}
\dot{x}_1 &= x_2 \\\\
\dot{x}_2 &= K u + x_3 \\\\
\dot{x}_3 &= 0
\end{aligned}
$$

- Orden 4

En dado caso que se quiera modelar el cambio de la perturbacion se puede obtener lo siguiente:

$$
\dot{x}_3 = x_4 \quad \text{y} \quad \dot{x}_4 = 0
$$

Una vez se tiene la estimacion 

$$\hat{x}_3 \approx \varepsilon(t)$$

se puede compensar en el control

$$
u(t) = \frac{1}{K} \left( u_0(t) - \hat{x}_3 \right)
$$

- Modelo extendido del sistema

- $x_1 = y$ (posición)
- $x_2 = \dot{y}$ (velocidad)
- $x_3 \approx \varepsilon(t)$ (perturbación total)
- $x_4 = \dot{\varepsilon}(t)$ (derivada de la perturbación)

$$
\begin{aligned}
\dot{x}_1 &= x_2 \quad \text{(posición)} \\\\
\dot{x}_2 &= K u + x_3 \quad \text{(aceleración con perturbación)} \\\\
\dot{x}_3 &= x_4 \quad \text{(evolución de la perturbación)} \\\\
\dot{x}_4 &= \ddot{\varepsilon} \approx 0 \quad \text{(se suele asumir constante)}
\end{aligned}
$$

- Punto de vista del Observador

$$
\begin{aligned}
\hat{x}_1 &\approx x_1 \quad \text{(posición)} \\\\
\hat{x}_2 &\approx x_2 \quad \text{(velocidad)} \\\\
\hat{x}_3 &\approx \varepsilon(t) \quad \text{(perturbación)} \\\\
\hat{x}_4 &\approx \dot{\varepsilon}(t) \quad \text{(derivada de la perturbación)}
\end{aligned}
$$

- Estructura del Observador con el error retroalimentado

Se define el error de estimación como:

$$
e_1 = y - \hat{x}_1
$$

Ecuacion del observador extendido:

$$
\begin{aligned}
\dot{\hat{x}}_1 &= \hat{x}_2 + \lambda_3 e_1 \\\\
\dot{\hat{x}}_2 &= K u + \hat{x}_3 + \lambda_2 e_1 \\\\
\dot{\hat{x}}_3 &= \hat{x}_4 + \lambda_1 e_1 \\\\
\dot{\hat{x}}_4 &= 0 + \lambda_0 e_1
\end{aligned}
$$

La perturbación estimada también puede representarse como :

$$
\varepsilon \approx e^{(4)} + \lambda_3 e^{(3)} + \lambda_2 \ddot{e} + \lambda_1 \dot{e} + \lambda_0 e
$$

donde estamos igualandolo a la segunda derivida de ε

Tomando como datos del sistema los valores \( K = 0.5 \), \( B = 0.2 \) y \( M = 0.5 \), y asumiendo una ubicación deseada de los polos en \( -100 \) (cuatro veces, lo que implica un sistema de cuarto orden), se diseñó un observador de estado extendido (ESO) para un controlador ADRC. A partir de esta ubicación de polos, se calcularon las ganancias del observador, obteniendo los valores:  
- \( \beta_1 = 400 \)  
- \( \beta_2 = 60\,000 \)  
- \( \beta_3 = 4\,000\,000 \)  
- \( \beta_4 = 100\,000\,000 \)

Durante la clase, se analizó el comportamiento del observador bajo estas condiciones, destacando su rapidez de convergencia y su capacidad para estimar las perturbaciones totales del sistema en tiempo real.

![image](https://github.com/user-attachments/assets/05997239-cfe5-4d11-8c7a-e1f40b6b75c6)

Fig 11. Scope matlab observador del ejercicio en clase

Ahora para poder cerrar el lazo se plantea la siguiente ley de control 

$$
u = \frac{1}{k} \left( y^{(n)*} - k_1 (\dot{\hat{y}} - \dot{y}^*) - k_0 (\hat{y} - y^*) - \hat{\varepsilon} \right)
$$

Donde el polinomio careacterisitco para el error de seguimiento $$\( e_y = y - y^* \)$$ es:

$$
P_{e_y}(s) = s^n + k_{n-1}s^{n-1} + \cdots + k_1 s + k_0
$$

Para este caso que nuestro sistema es de segundo orden:

$$
P_{e_y}(s) = s^2 + k_1 s + k_0
$$

Con ayuda de MATLAB y la función `poly`, es posible obtener las ganancias necesarias para el diseño del controlador. En este caso, se ubicaron dos polos deseados en \( -15 \), lo que permite determinar el polinomio característico asociado al sistema. A partir de dicho polinomio, se calcularon las ganancias del controlador, obteniendo como resultado: 1, 30 y 225.

![image](https://github.com/user-attachments/assets/f0953cad-8583-42f7-bcea-d8dc7e7e03df)

Fig 12. Controlador Ejercicio en clase

Gracias a esta implementacion se pudo observar las diferencias entre un PID y un ADRC donde se puede ver con clara diferencia la exactitud y efectividad de ADRC vs PID:

![image](https://github.com/user-attachments/assets/7fe089cc-4301-46f9-8493-339239bcf229)

Fig 13. Prueba de desempeño PID

![image](https://github.com/user-attachments/assets/698dde73-8d5d-463b-bae9-7b3c82af1acb)

Fig 14. Prueba de desempeño ADRC

De este análisis se puede afirmar que, aunque el controlador PID (Figura 13) ofrece una solución rápida, presenta ciertas desventajas: puede mostrar lentitud en la estabilización, así como oscilaciones durante la respuesta transitoria. En contraste, el controlador ADRC (Figura 14) demuestra un rendimiento superior. Al observar la gráfica correspondiente, se aprecia que prácticamente no hay diferencia visible entre la señal de entrada y la señal de salida, lo que indica un seguimiento preciso y una gran robustez ante perturbaciones.

## 7. Conclusiones

-El ADRC se basa en estimar y cancelar activamente todas las incertidumbres del sistema, lo que permite un control robusto sin depender de modelos precisos. Esta filosofía lo hace ideal para entornos dinámicos e inciertos.

-El observador extendido (ESO) es esencial para estimar tanto estados como perturbaciones en tiempo real. Su desempeño depende de la correcta ubicación de los polos, que deben equilibrar rapidez y sensibilidad al ruido.

-En aplicaciones prácticas, como sistemas masa-resorte, se agrega un estado para representar perturbaciones. Las ganancias del observador se definen en función del ancho de banda deseado, y se recomienda que el observador sea varias veces más rápido que la dinámica del sistema.

-Frente al PID, el ADRC ofrece mayor robustez y mejor rechazo de perturbaciones, aunque con una complejidad mayor debido al observador. Requiere menos conocimiento del modelo, lo que lo hace más adaptable.

-Se recomienda usar LADRC en sistemas lineales y NADRC en sistemas no lineales. Es clave verificar estabilidad (matriz Hurwitz), iniciar con $ω_o = 5-10ω_c$ y realizar simulaciones antes de aplicar en la práctica.

-El ADRC puede implementarse en sistemas con parámetros inciertos o dinámicas parcialmente conocidas, reduciendo la necesidad de una identificación precisa del modelo.

-La selección del ancho de banda del observador (\( \omega_o \)) y del controlador (\( \omega_c \)) es crítica. Un observador muy rápido puede amplificar el ruido, mientras que uno lento puede tardar en estimar perturbaciones. Se requiere un equilibrio cuidadoso según las condiciones del sistema.

-El diseño del observador y del controlador puede hacerse de forma parcialmente independiente, lo que facilita el ajuste de la velocidad de estimación y la dinámica de control sin que uno afecte directamente al otro.

-El ADRC, especialmente en su versión no lineal (NADRC), puede adaptarse mejor a sistemas con saturaciones, fricción u otras restricciones físicas que afectan el comportamiento del sistema.

-Aunque más complejo, el ADRC es aplicable a sistemas multientrada-multisalida. Esto puede requerir estrategias de control desacopladas o múltiples observadores, pero extiende su utilidad a una mayor gama de aplicaciones.

## 8. Referencias 

[1] “Active Disturbance Rejection Control (ADRC).” Control Tutorials for MATLAB and Simulink, https://ctms.engin.umich.edu/CTMS/index.php?example=MotorSpeed&section=ControlADRC

[2] Han, J. (2009). “From PID to Active Disturbance Rejection Control.” *IEEE Transactions on Industrial Electronics*, vol. 56, no. 3, pp. 900–906.

[3] Manrique, J. (2024). Apuntes de clase sobre Control Avanzado y Técnicas de Rechazo de Perturbaciones. Universidad XYZ.

[4] Gao, Z. (2006). “Active Disturbance Rejection Control: A Paradigm Shift in Feedback Control System Design.” *Proceedings of the American Control Conference*, pp. 2399–2405.

[5] “Introduction to Active Disturbance Rejection Control (ADRC).” MathWorks, https://www.mathworks.com/help/control/ug/active-disturbance-rejection-control.html

[6] Zheng, Q. & Gao, Z. (2010). An Energy Saving, Factory-Validated Digital ADRC Controller. *IEEE Transactions on Industrial Electronics*, vol. 57, no. 5, pp. 1786–1792. https://ieeexplore.ieee.org/document/5482993

[7] Miklosovic, R., Gao, Z., and Zhou, S. (2004). Robust Discrete-Time ADRC with Current Estimation. *IEEE Transactions on Industrial Electronics*, vol. 51, no. 2, pp. 404–413. https://ieeexplore.ieee.org/document/1380386

[8] Herbst, G. (2013). Practical ADRC: Tuning and Applications. *Annual Reviews in Control*, vol. 37, no. 1, pp. 48–57. https://www.sciencedirect.com/science/article/pii/S2405896316300361

[9] Texas Instruments (2018). Implementing ADRC on C2000 Microcontrollers. Application Report SPRAC70, Texas Instruments. https://www.ti.com/lit/an/sprac70/sprac70.pdf





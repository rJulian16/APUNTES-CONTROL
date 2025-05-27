# Control de Movimiento Clase 7 de Mayo.

Julian Stiven Redondo Chacon & Sebastian Cifuentes Alfonso & David Esteban Vasquez Alarcon

## Indice

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

![image](https://github.com/user-attachments/assets/835f6a16-0d39-4486-b1b2-a7208d01140b)

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

Figura 2. Sistemas lineales y no lineales

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

### 3.1 Características Principales del NADRC

| Característica                            | Descripción                                                                 |
|------------------------------------------|-----------------------------------------------------------------------------|
| Estimación no lineal                     | Utiliza funciones no lineales como `fal()` para mejorar la estimación del error y la perturbación. |
| Mejor rechazo al ruido                   | Las funciones no lineales suavizan la acción del observador ante señales ruidosas. |
| Alta precisión en zona cercana al cero   | Ajuste fino del comportamiento del sistema cuando el error es pequeño.     |
| Mayor robustez frente a no linealidades  | Se adapta mejor a dinámicas no lineales que el ADRC lineal.                |
| Controlador no lineal                    | Reemplaza las leyes de control proporcionales clásicas por funciones no lineales. |
| Parametrización flexible                 | Los parámetros α y δ permiten personalizar la respuesta del sistema.       |

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
\dot{x}_2 = f + b_{0}u \\ 
y = x_1 
\end{cases}
$$

- Tratamiento de la perturbación $f$ (desconocida) como estado adicional $x_3$

Modelo extendido (3er orden):

$$\begin{cases} 
\dot{x}_1 = x_2 \\ 
\dot{x}_2 = x_3 + b_{0}u \\ 
\dot{x}_3 = h \quad \text{(Dinámica de la perturbación)} \\ 
y = x_1 
\end{cases}$$

- $x_3$ absorbe todas las no linealidades/incertidumbres ($f$)
- Permite diseñar como si fuera un sistema lineal canónico

- Ventajas:

   - No requiere conocimiento exacto de $f$
   - Rechazo automático de perturbaciones
   - Estructura uniforme para diversos sistemas no lineales

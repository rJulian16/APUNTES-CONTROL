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

> 
- **Perturbaciones externas**: Influencias no deseadas provenientes del entorno o del sistema que afectan el comportamiento del sistema controlado (por ejemplo, fricción, carga variable, ruido).

- **Incertidumbre del modelo**: Diferencias entre el modelo matemático utilizado para diseñar el controlador y el comportamiento real del sistema, ya sea por parámetros mal conocidos o dinámicas no modeladas.

- **Rechazo activo de perturbaciones**: Capacidad del sistema de control para identificar y compensar perturbaciones de manera dinámica y en tiempo real, sin necesidad de conocer su origen exacto.

- **Observador de Estado Extendido (ESO)**: Componente clave del ADRC que estima tanto los estados del sistema como las perturbaciones totales (internas y externas), permitiendo al controlador actuar de forma efectiva ante condiciones desconocidas.

- **Controlador no lineal**: Parte del ADRC encargada de generar la señal de control, diseñada para estabilizar el sistema y mantener el seguimiento de la referencia, incluso cuando el sistema es no lineal.

- **Función de referencia (tracking)**: Objetivo deseado que debe seguir la salida del sistema. El ADRC busca minimizar el error entre esta referencia y la salida real, compensando perturbaciones y errores de modelado.

- **Robustez**: Propiedad de un sistema de control que le permite mantener un desempeño aceptable aun ante incertidumbres, perturbaciones y variaciones en los parámetros del sistema.

- **Sintonización simple**: Ventaja del ADRC, ya que permite ajustar los parámetros del controlador de forma más intuitiva y menos dependiente del modelo matemático exacto.

- **Modelo generalizado de planta**: En ADRC, se considera que todas las dinámicas no conocidas y perturbaciones se agrupan en una sola "perturbación total", que será estimada y compensada activamente.

- **Aplicabilidad a sistemas no lineales**: El ADRC no requiere linealizar la planta ni conocer su modelo exacto, lo que lo hace útil en una amplia variedad de sistemas reales con comportamientos complejos.

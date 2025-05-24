# Control de Movimiento Clase 22 de Abril.

Julian Stiven Redondo Chacon & Sebastian Cifuentes Alfonso & David Esteban Vasquez Alarcon

## Índice

[5. Conclusiones](#5-Conclusiones)

[6. Bibliografía](#6-Bibliografía)
  

## 1. Introducción al Control de Movimiento con Quanser y Simulink

El control de movimiento es una disciplina fundamental en la ingeniería de control que se enfoca en regular el comportamiento dinámico de sistemas físicos que requieren movimiento preciso, como motores, robots, vehículos autónomos y actuadores en procesos industriales. En esta etapa del curso, abordaremos los principios y herramientas prácticas para diseñar, simular y validar sistemas de control de movimiento.

Para ello, utilizaremos Quanser, una plataforma educativa y de investigación reconocida por sus sistemas mecatrónicos de alta precisión y sus módulos didácticos orientados al aprendizaje práctico del control. Quanser permite implementar y probar algoritmos de control en tiempo real, brindando una experiencia más cercana al entorno industrial.

La integración con Simulink, un entorno de modelado y simulación basado en bloques de MATLAB, facilita el diseño y prueba de sistemas de control mediante representaciones gráficas y entornos interactivos. Gracias a esta combinación, podemos:

-Modelar sistemas dinámicos complejos.

-Diseñar controladores PID, LQR, adaptativos y más.

-Validar algoritmos en tiempo real con hardware de Quanser.

-Obtener datos experimentales para análisis y mejora del desempeño.

![image](https://github.com/user-attachments/assets/086eeee5-84d3-488e-800f-9871d47978a1)

Figura 1. Quanser. 

## 2. Quanser

Quanser es una plataforma de hardware y software especializada en sistemas de control, que permite a estudiantes e investigadores implementar y validar algoritmos de control en tiempo real. Su integración con MATLAB y Simulink proporciona un entorno poderoso para la simulación, análisis y control físico de plantas reales como péndulos, motores DC, servomecanismos, sistemas de levitación magnética, entre otros.

### 2.1 Arquitectura general de Quanser

Quanser trabaja típicamente con tres componentes clave:

Hardware: Incluye plantas físicas (como el QUBE-Servo 2, Rotary Inverted Pendulum, etc.) y la tarjeta de adquisición de datos Quanser QLabs o QPIDe.

Software:

QUARC: Una extensión de Simulink desarrollada por Quanser para generar código en tiempo real y conectarse con el hardware.

QLabs: Plataforma de simulación basada en realidad virtual para experimentos de control sin necesidad del hardware físico.

Controladores: Se pueden diseñar directamente en Simulink usando bloques prediseñados o personalizados.


| Comando         | Descripción                                                                                         |
| :-------------- | :-------------------------------------------------------------------------------------------------- |
| `QLabs.register`| Abre la página de registro de la [licencia de sitio de MathWorks](link-to-mathworks-page).       |
| `QLabs.setup`   | Instala Quanser Interactive Labs. Descarga, si es necesario.                                        |
| `QLabs.launch`  | Inicia Quanser Interactive Labs. Descarga e instala, si es necesario.                               |
| `QLabs.remove`  | Desinstala Quanser Interactive Labs y elimina los archivos temporales descargados.                  |

Tabla 1. Comandos Quanser

### 2.2 Software

Antes de comenzar a trabajar con los modelos de Quanser, es necesario iniciar el entorno de simulación virtual proporcionado por QLabs. Este software permite interactuar con plantas simuladas en 3D sin necesidad de tener el hardware físico. Para ello, es importante ejecutar primero el comando qlabs_setup, que configura el entorno y las rutas necesarias. Luego, con el comando qlabs_launch, se abre la interfaz principal de QLabs, donde podremos seleccionar el experimento a utilizar. Esta preparación es esencial para que los bloques de Simulink se conecten correctamente con la planta virtual y podamos comenzar el diseño y validación de nuestros controladores.

![image](https://github.com/user-attachments/assets/b6a778d3-de34-44df-aa7f-c3cbc0cfa4e6)

Figura 2. Comando. 

## 6. Bibliografía

[1] MathWorks, "Simscape Multibody," [En línea]. Disponible: https://la.mathworks.com/products/simscape.html. [Accedido: 06-Mar-2025].

# Control de Movimiento Clase 12 de Marzo
Julian Stiven Redondo Chacon & Sebastian Cifuentes Alfonso & David Esteban Vasquez Alarcon

## 1. Introducción: ¿Por qué es importante el diseño de la transmisión?

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

![image](https://github.com/user-attachments/assets/c4171fce-6565-4243-bb62-b24bb3239d40)

Fig: Engranajes Simulink

---

## 2. Fundamentos de Transmisión Mecánica

### 2.1. ¿Qué es una transmisión?

Es el conjunto de elementos que transfiere energía mecánica desde un actuador a la carga. La transmisión puede:

- Cambiar la velocidad del eje
- Cambiar el torque (fuerza de giro)
- Convertir tipos de movimiento

### 2.2. Requisitos de diseño

1. **Torque suficiente** a la máxima velocidad
2. **Relación de inercia aceptable** (ni muy alta, ni muy baja)
3. **Criterios adicionales**: costo, precisión, tiempos de ciclo

![image](https://github.com/user-attachments/assets/66847fde-a993-4257-818e-0835c4edaba5)
Fig.2. Ilustracion findtop
| Escenario                                                    | Estrategia de Diseño                                 |
|--------------------------------------------------------------|------------------------------------------------------|
| Se tiene una transmisión establecida y se busca un movimiento concreto | Selección del motor más adecuado                     |
| Se dispone de un motor y se desea alcanzar un movimiento específico | Cálculo y diseño de la transmisión necesaria         |
| Se cuenta con un motor y transmisión ya definidos            | Análisis del movimiento resultante                   |
| Se conoce el perfil de movimiento deseado                    | Dimensionamiento del motor y selección de transmisión|

---

## 3. Inercia y Torque Reflejado

### 3.1. ¿Qué es la inercia?

Es la resistencia de un cuerpo a cambiar su velocidad de rotación.

$$ \sum T = J \cdot \alpha $$

En sistemas mecatrónicos se usa el concepto de *inercia reflejada*, que es cómo "se siente" la inercia de la carga desde el motor, teniendo en cuenta la transmisión.

### 3.2. Torque reflejado

Es el torque que debe entregar el motor, ajustado por la eficiencia y relación de la transmisión.

$$ T_m = \frac{T_l}{\eta N} $$


![image](https://github.com/user-attachments/assets/a4d3a72b-de89-46a0-b3f4-329e14cacb1a)

Fig.3. Engranajes
---

## 4. Tipos de Transmisión Mecánica

### 4.1. Engranajes

Sistema más común cuando se necesita precisión y rigidez.
## Engranajes: Modificación de Torque y Velocidad

Los **engranajes** son componentes fundamentales en sistemas mecánicos, utilizados para **modificar el torque** y la **velocidad** de rotación.

### Relación de Transmisión

La relación de transmisión \( N \) se define como:

```math
N = \frac{Z_{conducido}}{Z_{conductor}} = \frac{D_{conducido}}{D_{conductor}}
```
| Condición de la Relación \( N \) | Comportamiento del Sistema                 |
|----------------------------------|--------------------------------------------|
| \( N > 1 \)                      | Disminuye la velocidad, aumenta el torque  |
| \( N < 1 \)                      | Aumenta la velocidad, disminuye el torque  |
| \( N = 1 \)                      | No hay cambios en velocidad ni torque      |


📘 **Ejemplo:**
Sistema con engranaje de 5:1 y eficiencia del 97%. Carga requiere 2 Nm.

```python
T_motor = 2 / (0.97 * 5) = 0.412 Nm
```
rpm_carga = 1000 * (10 / 40) = 250 rpm
J_ref = 20 / ((2 * pi * 0.005)^2 * 0.9) ≈ 22.5 kg·m²
v_lineal = 0.025 * 100 = 2.5 m/s
v_banda = 0.04 * 200 = 8 m/s

---
## 5. Eficiencia

Un sistema mecánico eficiente es aquel que logra el movimiento deseado utilizando la menor cantidad de energía posible. La eficiencia está directamente relacionada con la capacidad del sistema para transformar energía de entrada en trabajo útil, y se puede expresar mediante la siguiente fórmula:

```math
\eta = \frac{E_{\text{útil}}}{E_{\text{entrada}}} \times 100\%
```

## 6. Simulación en Simscape Multibody

Simscape Multibody es una herramienta de MATLAB/Simulink que permite modelar sistemas mecánicos complejos, incluyendo enlaces, articulaciones y contactos.

### 6.1. Pasos para simular una transmisión

1. **Crear los sólidos (Solid Blocks):** motor, poleas, engranajes, etc.
2. **Definir parámetros físicos:** masa, dimensiones, inercia.
3. **Conectar con uniones (Joints):** revolute, prismatic, etc.
4. **Establecer condiciones iniciales:** velocidad, torque, posición.
5. **Ejecutar la simulación** y observar la respuesta (posición, velocidad, torque).

![image](https://github.com/user-attachments/assets/aad58276-3ee6-40ec-93c4-8bb3ab4ef0b9)
Fig.4. Motor, Tranmisión, carga

### 6.2. Consejos para modelar

- Si el movimiento es rotacional, usar `Revolute Joint`
- Si es lineal, usar `Prismatic Joint`
- Para engranajes, se puede usar el bloque `Gear Constraint`
- Las bandas pueden modelarse con `Pulley Constraint` y una masa rotacional

---
## 7. Relación de Inercia

La **relación de inercia** entre la carga reflejada y el motor es un parámetro fundamental para lograr un buen rendimiento dinámico en sistemas de control de movimiento. Esta relación se expresa como:

```math
Ri = \frac{J_{\text{carga reflejada}}}{J_{\text{motor}}}
```
## 8. Poleas y Correas

El sistema de **poleas y correas** es ampliamente utilizado debido a su **simplicidad**, **bajo costo** y capacidad para transmitir movimiento entre **ejes distantes**.

![image](https://github.com/user-attachments/assets/0b94ae07-0a55-47b1-bb19-c3cc69dd6b91)

Fig.5. Polea

### Relación de Transmisión

La relación de transmisión entre dos poleas se calcula mediante:

```math
N = \frac{D_{\text{conducida}}}{D_{\text{conductor}}}
```

| Condición         | Características del sistema                      |
|------------------|--------------------------------------------------|
| Ventajas         | Bajo nivel de ruido, tolera desalineaciones, amortigua vibraciones |
| Desventajas      | Pérdidas por deslizamiento, requiere mantenimiento, menor eficiencia que engranajes |


## 9. Ejemplos Resueltos

### 📘 Ejemplo 1: Engranaje con carga

Motor con $J_m = 0.01$ kg·m² mueve una carga de $0.5$ kg·m² mediante un reductor 10:1 ($\eta = 92\%$).

**Solución:**

```python
J_ref = 0.5 / (0.92 * 10**2) = 0.00543 kg·m²
J_total = 0.01 + 0.00543 = 0.01543 kg·m²
J_R = J_total / J_m = 1.543

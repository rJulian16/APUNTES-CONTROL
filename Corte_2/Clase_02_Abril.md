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
Fuente: Docente

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
Fuente: Findtop

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

Fuente: Docente
---

## 4. Tipos de Transmisión Mecánica

### 4.1. Engranajes

Sistema más común cuando se necesita precisión y rigidez.


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

## 6. Simulación en Simscape Multibody

Simscape Multibody es una herramienta de MATLAB/Simulink que permite modelar sistemas mecánicos complejos, incluyendo enlaces, articulaciones y contactos.

### 6.1. Pasos para simular una transmisión

1. **Crear los sólidos (Solid Blocks):** motor, poleas, engranajes, etc.
2. **Definir parámetros físicos:** masa, dimensiones, inercia.
3. **Conectar con uniones (Joints):** revolute, prismatic, etc.
4. **Establecer condiciones iniciales:** velocidad, torque, posición.
5. **Ejecutar la simulación** y observar la respuesta (posición, velocidad, torque).

![image](https://github.com/user-attachments/assets/aad58276-3ee6-40ec-93c4-8bb3ab4ef0b9)
Fuente: Docente

### 6.2. Consejos para modelar

- Si el movimiento es rotacional, usar `Revolute Joint`
- Si es lineal, usar `Prismatic Joint`
- Para engranajes, se puede usar el bloque `Gear Constraint`
- Las bandas pueden modelarse con `Pulley Constraint` y una masa rotacional

---

## 7. Ejemplos Resueltos

### 📘 Ejemplo 1: Engranaje con carga

Motor con $J_m = 0.01$ kg·m² mueve una carga de $0.5$ kg·m² mediante un reductor 10:1 ($\eta = 92\%$).

**Solución:**

```python
J_ref = 0.5 / (0.92 * 10**2) = 0.00543 kg·m²
J_total = 0.01 + 0.00543 = 0.01543 kg·m²
J_R = J_total / J_m = 1.543

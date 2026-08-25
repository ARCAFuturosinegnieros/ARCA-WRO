# WRO Future Engineers 2026 — Informe Técnico de Ingeniería

## 1. Información del equipo

- **Nombre del equipo:** [ARCA]
- **País:** Costa Rica
- **Institución:** [Colegio Científico del Atlántico]
- **Integrantes:** [Amanda Guzmán Pérez], [Aaron Brenes López]
- **Tutor:** [Elkira Francis Hernández]

## 2. Nuestro robot

El robot autónomo desarrollado para WRO Futuros ingenieros 2026 está construido utilizando la plataforma metálica modular **TETRIX MAX** y controlado por la tarjeta de control robótico **TETRIX Pulse**. Utiliza un esquema de movilidad de cuatro ruedas con tracción trasera accionado por un motor de corriente continua  y un sistema de dirección servocontrolada en el eje delantero. Cuenta con una batería de 6VOLT integrada del Kit de **TETRIX MAX**, Una cámara ESP-32CAM, Sensor ultrasonico original del kit. 

### Características principales:

- **Controlador:** TETRIX PULSE Robotics Controller (ATmega328P @ 16 MHz).
- **Motores:** 
  - Tracción: TETRIX PRIME DC Motor 6V.
  - Dirección: TETRIX Standard-Scale Servo Motor
- **Sensores:** 
  - Sensor ultrasónico frontal de medición continua de distancia.
  - Cámara ESP-32 CAM integrado con un Microprocesador ESP32-S, con un modulo de cámara OV2640.

## 3. Gestión de movilidad

### Diseño mecánico
El chasis está construido a partir de vigas metálicas extruidos en forma de "T" de **TETRIX MAX**, formando una estructura rectangular rígida.

### Sistema de tracción
El movimiento del vehículo se realiza mediante tracción en las dos ruedas traseras (RWD). El motor TETRIX PRIME DC Motor transmite su rotación directamente a un engranaje central montado sobre el eje posterior continuo de acero. La retroalimentación en el motor permite implementar un control de velocidad en bucle, permitiendo aceleración y frenados con precisión.

### Sistema de dirección
El giro se ejecuta mediante un mecanismo de viraje articulado delantero impulsado por un servomotor montado en posición vertical superior. El brazo del servo ajusta mediante una barra de acoplamiento el ángulo de orientación de las manguetas de las ruedas delanteras.

### Decisiones de diseño
- **Perfiles de aluminio TETRIX MAX:** Proveen alta resistencia a deformaciones e impactos accidentales contra los límites de la pista.
- **Batería en posición trasera:** Incrementa la masa sobre el eje motriz, maximizando la fricción y tracción de las ruedas traseras de goma.
- **Servomotor en nivel superior:** Protege la electrónica del mecanismo de dirección contra colisiones frontales.

### Evolución
1. **Prototipo V1:** Chasis inicial de tracción diferencial; descartado por falta de precisión en trayectoria rectilínea a alta velocidad.
2. **Prototipo V2:** Chasis de aluminio con dirección de servomotor y ruedas delgadas; presentaba holgura en el pivote frontal.
3. **Versión Final V3:** Chasis reforzado con perfiles TETRIX MAX, adición de rodamientos de precisión en el eje de tracción y montaje centrado del motor TorqueNADO.

## 4. Gestión de energía y sensores

### Sistema de alimentación
El vehículo cuenta con una fuente de alimentación única de **12V NiMH (3000 mAh)**. La tarjeta **TETRIX PRIZM** regula la tensión a 5V para el microcontrolador, los puertos de sensores y el servomotor de dirección. El puente H interno suministra energía modulada por ancho de pulso (PWM) al motor TorqueNADO de tracción.

### Sensores

| Sensor | Ubicación | Información Obtiene | Uso en el Robot |
| :--- | :--- | :--- | :--- |
| **Sensor Ultrasónico** | Frontal inferior | Distancia en cm al objeto o pared | Detección de paredes de esquina, esquiva de bloques y estacionamiento. |
| **Encoder Óptico** | Integrado en motor TorqueNADO | Pulsos de rotación del motor | Medición de odometría, distancia recorrida y cálculo de velocidad. |

### Calibración
- **Ultrasonido:** Se aplican rutinas de muestreo continuo tomando la mediana de 5 lecturas consecutivas para descartar picos de ruido causados por reflexiones no deseadas.
- **Encoder:** Reseteo a cero (`prizm.resetEncoders()`) al inicio de cada tramo para medir progresiones angulares exactas.

## 5. Gestión de obstáculos

### Detección de obstáculos
El sensor ultrasónico realiza barridos frontales continuos. Cuando la distancia medida cae por debajo de 25 cm, el procesador interpreta la presencia de un elemento o muro frontal.

### Algoritmo
Al detectar un obstáculo:
1. El software reduce la potencia del motor principal para estabilizar la suspensión.
2. El servomotor de dirección gira al ángulo de compensación predeterminado (por ejemplo, ±30°).
3. Tras recorrer la distancia medida por el encoder para superar el objeto, el servo regresa a su centro (90°).

### Navegación
Mantiene una trayectoria recta centrada ajustando el ángulo del servo de dirección en pequeños incrementos a través de las constantes de corrección odométrica del encoder.

## 6. Software

### Arquitectura del programa
Desarrollado en C++ mediante el entorno Arduino IDE y la librería oficial `TETRIX_PRIZM.h`. Se organiza en una **Máquina de Estados Finitos (FSM)**:
- `STATE_WAIT`: Espera el pulso del botón verde de inicio.
- `STATE_RUN`: Control de avance en pista con lecturas de sensores.
- `STATE_AVOID`: Corrección de rumbo por esquiva.
- `STATE_PARK`: Secuencia final de parqueo.

### Estacionamiento
Al cumplir el conteo total de distancia en pulsos de encoder correspondientes a las tres vueltas reglamentarias, el robot reduce su potencia al 20%, orienta la dirección hacia la zona de parqueo y se detiene cuando el ultrasonido detecta la pared posterior a menos de 10 cm.

## 7. Proceso de ingeniería

### Problemas encontrados y soluciones
- **Holgura en la dirección:** Se reemplazaron los empalmes plásticos por herrajes metálicos de alta rigidez TETRIX MAX.
- **Ruido en ultrasonido:** Se integró un capacitor de filtrado y un filtro por medión en el firmware.
- **Pérdida de tracción:** Se programó un arranque progresivo (*Soft-Start*) de PWM en el motor trasero.

## 8. Cómo compilar y cargar el programa

1. Instalar **Arduino IDE** (v1.8.19 o superior).
2. Descargar e instalar la biblioteca **TETRIX PRIZM** desde el gestor de librerías.
3. Seleccionar como placa: `Arduino Uno` (procesador ATmega328P).
4. Conectar el puerto USB del PRIZM, seleccionar el COM activo y pulsar **Subir**.

## 9. Estructura del repositorio

```text
├── cad/          # Archivos de impresión 3D (soportes)
├── doc/          # Documentación técnica PDF
├── images/       # Fotografías oficiales del robot
├── src/          # Código fuente en Arduino IDE (.ino)
└── README.md     # Documentación principal
- **Batería:** Pack de batería NiMH TETRIX MAX de 12V DC / 3000 mAh.
- **Sistema de dirección:** Dirección pivotante accionado por servomotor superior conectado a barra articulada en las manguetas delanteras.
- **Sistema de tracción:** Tracción trasera (RWD) con transmisión por engranaje cilíndrico central hacia el eje de acero posterior.

## 3. Gestión de movilidad

### Diseño mecánico
El chasis está construido a partir de perfiles metálicos extruidos en "U" de **TETRIX MAX**, formando una estructura rectangular rígida de dos pisos:
- **Nivel inferior:** Aloja el tren motriz trasero con eje rígido sobre rodamientos, el motor TorqueNADO central y las manguetas articuladas delanteras.
- **Nivel superior:** Soporta la tarjeta de control **TETRIX PRIZM**, el paquete de batería NiMH de 12V asegurado en un compartimento trasero y la interfaz de botones de control.

### Sistema de tracción
El movimiento del vehículo se realiza mediante tracción en las dos ruedas traseras (RWD). El motor TorqueNADO transmite su rotación directamente a un engranaje central montado sobre el eje posterior continuo de acero. La retroalimentación del encoder integrado en el motor permite implementar un control de velocidad PID en bucle cerrado, permitiendo rampas de aceleración y frenados de precisión.

### Sistema de dirección
El giro se ejecuta mediante un mecanismo de viraje articulado delantero impulsado por un servomotor montado en posición vertical superior. El brazo del servo ajusta mediante una barra de acoplamiento el ángulo de orientación de las manguetas de las ruedas delanteras.

### Decisiones de diseño
- **Perfiles de aluminio TETRIX MAX:** Proveen alta resistencia a deformaciones e impactos accidentales contra los límites de la pista.
- **Batería en posición trasera:** Incrementa la masa sobre el eje motriz, maximizando la fricción y tracción de las ruedas traseras de goma.
- **Servomotor en nivel superior:** Protege la electrónica del mecanismo de dirección contra colisiones frontales.

### Evolución
1. **Prototipo V1:** Chasis inicial de tracción diferencial; descartado por falta de precisión en trayectoria rectilínea a alta velocidad.
2. **Prototipo V2:** Chasis de aluminio con dirección de servomotor y ruedas delgadas; presentaba holgura en el pivote frontal.
3. **Versión Final V3:** Chasis reforzado con perfiles TETRIX MAX, adición de rodamientos de precisión en el eje de tracción y montaje centrado del motor TorqueNADO.

## 4. Gestión de energía y sensores

### Sistema de alimentación
El vehículo cuenta con una fuente de alimentación única de **12V NiMH (3000 mAh)**. La tarjeta **TETRIX PRIZM** regula la tensión a 5V para el microcontrolador, los puertos de sensores y el servomotor de dirección. El puente H interno suministra energía modulada por ancho de pulso (PWM) al motor TorqueNADO de tracción.

### Sensores

| Sensor | Ubicación | Información Obtiene | Uso en el Robot |
| :--- | :--- | :--- | :--- |
| **Sensor Ultrasónico** | Frontal inferior | Distancia en cm al objeto o pared | Detección de paredes de esquina, esquiva de bloques y estacionamiento. |
| **Encoder Óptico** | Integrado en motor TorqueNADO | Pulsos de rotación del motor | Medición de odometría, distancia recorrida y cálculo de velocidad. |

### Calibración
- **Ultrasonido:** Se aplican rutinas de muestreo continuo tomando la mediana de 5 lecturas consecutivas para descartar picos de ruido causados por reflexiones no deseadas.
- **Encoder:** Reseteo a cero (`prizm.resetEncoders()`) al inicio de cada tramo para medir progresiones angulares exactas.

## 5. Gestión de obstáculos

### Detección de obstáculos
El sensor ultrasónico realiza barridos frontales continuos. Cuando la distancia medida cae por debajo de 25 cm, el procesador interpreta la presencia de un elemento o muro frontal.

### Algoritmo
Al detectar un obstáculo:
1. El software reduce la potencia del motor principal para estabilizar la suspensión.
2. El servomotor de dirección gira al ángulo de compensación predeterminado (por ejemplo, ±30°).
3. Tras recorrer la distancia medida por el encoder para superar el objeto, el servo regresa a su centro (90°).

### Navegación
Mantiene una trayectoria recta centrada ajustando el ángulo del servo de dirección en pequeños incrementos a través de las constantes de corrección odométrica del encoder.

## 6. Software

### Arquitectura del programa
Desarrollado en C++ mediante el entorno Arduino IDE y la librería oficial `TETRIX_PRIZM.h`. Se organiza en una **Máquina de Estados Finitos (FSM)**:
- `STATE_WAIT`: Espera el pulso del botón verde de inicio.
- `STATE_RUN`: Control de avance en pista con lecturas de sensores.
- `STATE_AVOID`: Corrección de rumbo por esquiva.
- `STATE_PARK`: Secuencia final de parqueo.

### Estacionamiento
Al cumplir el conteo total de distancia en pulsos de encoder correspondientes a las tres vueltas reglamentarias, el robot reduce su potencia al 20%, orienta la dirección hacia la zona de parqueo y se detiene cuando el ultrasonido detecta la pared posterior a menos de 10 cm.

## 7. Proceso de ingeniería

### Problemas encontrados y soluciones
- **Holgura en la dirección:** Se reemplazaron los empalmes plásticos por herrajes metálicos de alta rigidez TETRIX MAX.
- **Ruido en ultrasonido:** Se integró un capacitor de filtrado y un filtro por medión en el firmware.
- **Pérdida de tracción:** Se programó un arranque progresivo (*Soft-Start*) de PWM en el motor trasero.

## 8. Cómo compilar y cargar el programa

1. Instalar **Arduino IDE** (v1.8.19 o superior).
2. Descargar e instalar la biblioteca **TETRIX PRIZM** desde el gestor de librerías.
3. Seleccionar como placa: `Arduino Uno` (procesador ATmega328P).
4. Conectar el puerto USB del PRIZM, seleccionar el COM activo y pulsar **Subir**.

## 9. Estructura del repositorio

```text
├── cad/          # Archivos de impresión 3D (soportes)
├── doc/          # Documentación técnica PDF
├── images/       # Fotografías oficiales del robot
├── src/          # Código fuente en Arduino IDE (.ino)
└── README.md     # Documentación principal

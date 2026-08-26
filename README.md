![image alt](https://github.com/ARCAFuturosinegnieros/ARCA-WRO/blob/9b341d565939584d5ee5446afa225ad2bcc4d892/fotos/image.png)

<br>

---
<br>
<p align="center">
 
</p>

# WRO Futuros Ingenieros - [ARCA]⚙️

Este es el repositorio oficial de [Futuros Ingenieros](https://github.com/open-robosports) de [ARCA](https://github.com/gisoddolfato99-jpg/Robosports).

## Nuestro Equipo
* **Categoría de Edad:** Senior
##  **Integrantes:**
  
* **Amanda Guzmán Pérez**
  <br>
  
  <div align="left">
  <img src="https://github.com/ARCAFuturosinegnieros/ARCA-WRO/blob/668f44cd1caf4b8b99bff547426b2795b14e3182/image.png" width="300" />
</div>

<br>

* **Aaron Brenes López**
  <br>

    <div align="left">
  <img src="https://github.com/ARCAFuturosinegnieros/ARCA-WRO/blob/af7423c7f9fd3f6694f7f12f0a4a840a8add86d7/fotos/image.png" width="300" />
</div>

<br>

  
* **Tutora: Elkira Francis Hernández**
  <br>
  
  <div align="left">
  <img src="https://github.com/ARCAFuturosinegnieros/ARCA-WRO/blob/390537ad35ead2b94e3dd51417955df57b91acca/fotos/image.png" width="300" height="400" />
</div>


---

## Descripción del Robot 🤖
El robot desarrollado para la categoría WRO Futuros Ingenieros 2026  es un vehículo autónomo basado en la plataforma de construcción robótica de aluminio extruido **TETRIX MAX**. Implementa un sistema de navegación inteligente y control en tiempo real mediante el controlador robótico programable TETRIX PULSE. El diseño incorpora un sistema de dirección servocontrolada montado directamente sobre el eje delantero, transmisión directa de tracción en las ruedas traseras, controlador de distancia ultrasónico de alta precisión en el frontal y retroalimentación óptico integrado para la medición precisa.


> [!IMPORTANT]
>**Controlador:** TETRIX PULSE (ATmega328P @ 16 MHz).
- **Motores:** 
  - Tracción: TETRIX PRIME DC MOTOR 6V
  - Dirección: 
- **Sensores:** 
  - Sensor ultrasónico frontal de medición continua de distancia.
  - Cámara ESP-32S CAM para la detección de señales 
- **Batería:** Batería NiMH TETRIX MAX de 12V DC / 3000 mAh.
- **Sistema de dirección:** Dirección pivotante accionado por servomotor superior conectado a barra articulada en las manguetas delanteras.
- **Sistema de tracción:** Tracción trasera (RWD) con transmisión por engranaje cilíndrico central hacia el eje de acero posterior.
-
<br>

--- 
## 3. Gestión de movilidad

### Diseño mecánico
El chasis está construido a partir de vigas metálicas en forma de "T" de **TETRIX MAX**, formando una estructura rectangular rígida 

### Sistema de tracción
El movimiento del vehículo se realiza mediante tracción en las dos ruedas traseras. El motor DC de TETRIX PRIME transmite su rotación directamente a un engranaje central montado sobre el eje posterior continuo de acero. La retroalimentación integrado en el motor permite implementar un control de velocidad en bucle cerrado, permitiendo la aceleración y frenados de precisión.

### Sistema de dirección
El giro se ejecuta mediante un mecanismo de viraje articulado delantero impulsado por un servomotor montado en posición vertical superior. El brazo del servo ajusta mediante una barra de acoplamiento el ángulo de orientación de las ruedas delanteras.

### Decisiones de diseño
- **Vigas de metal TETRIX MAX:** Proveen alta resistencia a deformaciones e impactos accidentales contra los límites de la pista.
- **Batería en posición inferios:** Ayuda a la hora de colocar los demás sensores para que no obstruya el espacio.
- **Servomotor en nivel superior:** Protege la electrónica del mecanismo de dirección contra colisiones frontales.


### Sistema de alimentación
El vehículo cuenta con una fuente de alimentación única de **12V NiMH (3000 mAh)**. La tarjeta **TETRIX PULSE** regula la tensión a 5V para el microcontrolador, los puertos de sensores y el servomotor de dirección. El puente H interno suministra energía modulada por ancho de pulso (PWM) al motor TorqueNADO de tracción.

### Calibración
- **Sensor Ultrasonico**: Se aplican rutinas de muestreo continuo tomando la mediana de 5 lecturas consecutivas para descartar picos de ruido causados por reflexiones no deseadas.
- **Cámara ESP-32S CAM:** Probar la detección de colores para realizar una acción.


### Detección de obstáculos
El sensor ultrasónico realiza muestreos frontales continuos. Cuando la distancia medida cae por debajo de 25 cm, el procesador interpreta la presencia de un elemento o muro.

### Algoritmo
Al detectar un obstáculo con la cámara ESP-32S CAM:
1. El software reduce la potencia del motor principal para estabilizar la suspensión.
2. El servomotor de dirección gira al ángulo de compensación predeterminado.
3. Tras recorrer la distancia medida por el sensor ultrasonico para superar el objeto, el servo regresa a su centro.

### Navegación
Mantiene una trayectoria recta centrada ajustando el ángulo del servo de dirección en pequeños incrementos a través de las constantes de correcciones del sensor.
## 6. Software

### Arquitectura del programa
Desarrollado en C++ mediante el entorno Arduino IDE y la librería oficial `TETRIX_PULSE.h`. Se organiza de manera que:
- `STATE_WAIT`: Espera el pulso del botón verde de inicio.
- `STATE_RUN`: Control de avance en pista con lecturas de sensores.
- `STATE_AVOID`: Corrección de rumbo por esquiva.
- `STATE_PARK`: Secuencia final de parqueo.

### Estacionamiento
Al cumplir el conteo total de distancia correspondientes a las tres vueltas reglamentarias, el robot reduce su potencia al 20%, orienta la dirección hacia la zona de parqueo y se detiene cuando el sensor ultrasónico detecta la pared posterior a menos de 10 cm.

## 7. Proceso de ingeniería

### Problemas encontrados y soluciones
- **Posición de la bateria:** Se cambio el lugar de colocación que teníamos originalmente ya que obstruía el paso de el cable conector del la placa a la computadora.
- **Ruido en sensor ultrasónico:** Se integró un capacitor de filtrado y un filtro en el firmware.
- **Uso de llantas** Se cambio el diseño de llantas elegidas originalmente ya que no eran compatibles con el diseño que fabricamos ya que le daba más peso y no se podían colocar, en cambio integramos un diseño de llantas originales de **TETRIX MAX** ya que eran 100% compatibles en todos los aspectos.

###  Galería de Fotos

<br>

<div align="center"><table><tr>Vista superior</tr><tr><td>
<img src="https://github.com/ARCAFuturosinegnieros/ARCA-WRO/blob/2c364574de68fa2e31664add8f51146796cb31ef/fotos/image.png"/></td><td>
<img src="https://github.com/ARCAFuturosinegnieros/ARCA-WRO/blob/888fe7e2e05cbb53ec6cf26e7ded6f8d583ed459/fotos/image.png"/></td></tr></table></div>

<br>

<div align="center"><table><tr>Vista delantera y trasera</tr><tr><td>
<img src="https://github.com/ARCAFuturosinegnieros/ARCA-WRO/blob/c9bd1f16435fac034dbdf43c7c610ea48e0f43a6/fotos/image.png"/></td><td>
<img src="https://github.com/ARCAFuturosinegnieros/ARCA-WRO/blob/33b9ee4ff25c50ddb34202f55c837d1c2d8be736/fotos/image.png"/></td></tr></table></div>



---
<br>

> [!IMPORTANT]
> **Rol en la ronda**
>El robot según la salida comienza su recurrido según donde determine la ronda, con la cámara podrá leer los colores de las señales donde según lo leído decidira de forma autónoma que camino seguir, luego de completar estas realizara el estacionamiento donde con sus sensores ultrasónicos decidirá como aparcar bien.
> 


> [!NOTE]
> El robot frena su recorrido y redirecciona si detecta un muro. 
> **Está programado en c++**

---

 **🚀 Instalación y Uso**

**Requisitos Previos**
-Descargar Arduino IDE y las librerías de TETRIX MAX PULSE
- Kit de TETRIX MAX PRIME
- Tener computadora





---

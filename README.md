![image alt](https://github.com/ARCAFuturosinegnieros/ARCA-WRO/blob/9b341d565939584d5ee5446afa225ad2bcc4d892/fotos/image.png)

<br>

---
<br>


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
  <img src="https://github.com/ARCAFuturosinegnieros/ARCA-WRO/blob/c7d249c432e7ef262d8b77408beb4f68d91cb8b5/image.png" width="300" />
</div>

<br>

  
* **Tutora: Elkira Francis Hernández**
  <br>
  
  <div align="left">
  <img src="https://github.com/gisoddolfato99-jpg/Robosports/blob/7e591b46830c22a55a88fd3e2ce2d9de683d906f/feature/WhatsApp%20Image%202026-08-24%20at%204.52.05%20PM.jpeg" width="300" height="400" />
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
<img src="https://github.com/ARCAFuturosinegnieros/ARCA-WRO/tree/4e1e04dc913c21f20132559b2cde1057c76feffe/fotos"/></td></tr></table></div>

<br>

<div align="center"><table><tr>Robot de la rampa</tr><tr><td>
<img src="https://github.com/gisoddolfato99-jpg/Robosports/blob/5d15b8e690788a2a1fb1196902a3e4971874338b/feature/prototipo/1/WhatsApp%20Image%202026-08-24%20at%203.55.55%20PM.jpeg"/></td><td>
<img src="https://github.com/gisoddolfato99-jpg/Robosports/blob/5d15b8e690788a2a1fb1196902a3e4971874338b/feature/prototipo/1/WhatsApp%20Image%202026-08-24%20at%203.55.59%20PM.jpeg"/></td></tr></table></div>



---
<br>

> [!IMPORTANT]
> ### 🕹️ Rol es en la Cancha
> * **Robot 1 (Robot del muro):** Tira las bolas mediante los choques.
> 
> * **Robot 2 (Robot de la rampa):** Tira las bolas cuando detecta un colór en específico.

### 💻 Arquitectura del Código

**El robot de la rampa se divide en estas fases:**

1. **Avance:** El robot avanza hasta que la cámara detecta el color de la rampa.
2. **Tiro:** Cuando el robot está en el color adecuado tira la pelota.
3. **Bucle:** Luego de tirarla, el robot gira y choca contra el muro para crear un ciclo donde queda dando vueltas y tirando las pelotas.

<br>

**El robot del muro se divide en estas fases:**

1. **Avance:** El robot avanza hasta chocar el muro y tira las bolas.
2. **Bucle:** Cuando choca, retrocede y gira. Después de hacer este patrón 4 veces, vuelve a tirar la pelota.

<br>

> [!NOTE]
> El robot frena su recorrido si detecta la bola rosa (en los dos prototipos).
>
> **Está programado en python/bloques**

---

## 🚀 Instalación y Uso

### Requisitos Previos
* Tener Chrome o cualquier navegador compatible con Lego Spike Prime
* Kit de [Lego Spike](https://github.com/LEGO/spike-prime-docs)
* Tener computadora

### Códigos de los robots
> [!NOTE]
> * https://github.com/gisoddolfato99-jpg/Robosports/blob/7b36257d28c1a814bc8b996cd1c6eea39508d2ac/c%C3%B3digos/Romuro.md
> 
> * https://github.com/gisoddolfato99-jpg/Robosports/blob/faf9b45a7bf8a074c2df498f72b86c060638c646/c%C3%B3digos/bich.png



---

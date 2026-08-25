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
> **Hardware y Componentes**
> * **Controlador Principal:** [LEGO SPIKE Prime](https://github.com/LEGO/spike-prime-docs)
> * **Actuadores:** 2x Motores grandes para tracción, 1x Motor mediano para el mecanismo de golpeo
> * **Sensores:** 1x Giroscopio interno, 2x Sensores de color para detección de bola rosa, 1x sensor de fuerza para los golpes

<br>

--- 

###  Galería de Fotos

<br>

<div align="center"><table><tr>Robot del muro</tr><tr><td>
<img src="https://github.com/gisoddolfato99-jpg/Robosports/blob/fb2c760a20bfd880a7ba884b4ba6023ceec8b445/feature/prototipo/1/WhatsApp%20Image%202026-08-24%20at%203.55.47%20PM.jpeg"/></td><td>
<img src="https://github.com/gisoddolfato99-jpg/Robosports/blob/fb2c760a20bfd880a7ba884b4ba6023ceec8b445/feature/prototipo/1/1a.jpeg"/></td></tr></table></div>

<br>

<div align="center"><table><tr>Robot de la rampa</tr><tr><td>
<img src="https://github.com/gisoddolfato99-jpg/Robosports/blob/5d15b8e690788a2a1fb1196902a3e4971874338b/feature/prototipo/1/WhatsApp%20Image%202026-08-24%20at%203.55.55%20PM.jpeg"/></td><td>
<img src="https://github.com/gisoddolfato99-jpg/Robosports/blob/5d15b8e690788a2a1fb1196902a3e4971874338b/feature/prototipo/1/WhatsApp%20Image%202026-08-24%20at%203.55.59%20PM.jpeg"/></td></tr></table></div>



---
<br>

> [!IMPORTANT]
> ### 🕹️ Roles en la Cancha
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

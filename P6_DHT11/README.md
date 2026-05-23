# P6 - Monitoreo de Temperatura y Humedad con LCD (Raspberry Pi)

Este repositorio contiene la sexta práctica de sistemas embebidos, donde se implementa la lectura de un sensor ambiental y la visualización de los datos en tiempo real sobre una pantalla LCD a través del bus I2C.

## Descripción

Este proyecto permite interactuar con sensores externos y protocolos de comunicación. A través de scripts modulares en Python, la Raspberry Pi extrae la temperatura y humedad local mediante un sensor DHT11 y proyecta estos valores en un display LCD de 16x2. El código está separado en módulos para facilitar su lectura y mantenimiento.

## Objetivos

* Leer datos ambientales mediante los pines GPIO.
* Configurar y utilizar el protocolo de comunicación I2C.
* Implementar programación modular separando la lógica del sensor, la pantalla y el flujo principal.
* Manejar de forma segura las excepciones para evitar caídas del sistema ante fallos de lectura.

## Requisitos de Hardware

| Cantidad | Componente | Notas |
| :--- | :--- | :--- |
| 1 | Raspberry Pi | Modelos 3 o 4 |
| 1 | Sensor DHT11 | Módulo de temperatura y humedad |
| 1 | Pantalla LCD 16x2 | Debe incluir el módulo adaptador I2C |
| 1 | Resistencia 10kΩ | Pull-up para el pin de datos del DHT11 |
| Varios | Jumpers y Protoboard | Para realizar las conexiones físicas |

## Esquema de Conexión

* **Sensor DHT11:** * Señal (Datos) ➔ Pin GPIO 17 (Pin físico 11).
  * Alimentación ➔ 5V o 3.3V.
  * Tierra ➔ GND.
* **Pantalla LCD (I2C):** * SDA (Datos I2C) ➔ Pin GPIO 2 (Pin físico 3).
  * SCL (Reloj I2C) ➔ Pin GPIO 3 (Pin físico 5).
  * Alimentación ➔ 5V.
  * Tierra ➔ GND.

## Instalación y Uso

**1. Habilitar la comunicación I2C**
Desde la terminal, abre la configuración de la Raspberry Pi y activa el puerto:
```bash
sudo raspi-config
```
*(Ruta: Interfacing Options -> I2C -> Enable)*

**2. Preparar el entorno e instalar dependencias**
Es necesario contar con las utilidades del sistema para I2C y las librerías de Python para controlar los componentes:
```bash
sudo apt update
sudo apt install python3-pip python3-smbus i2c-tools -y
pip3 install adafruit-circuitpython-dht RPLCD adafruit-blinka
```

**3. Ejecución del proyecto**
Asegúrate de clonar o descargar los archivos de este repositorio en una misma carpeta (`main.py`, `sensor.py`, `display.py`, `utils.py`). Luego, otorga permisos y ejecuta el programa principal:
```bash
chmod +x main.py
python3 main.py
```

**Nota:** Para detener el programa de forma segura y liberar los recursos, presiona `Ctrl + C` en la terminal.

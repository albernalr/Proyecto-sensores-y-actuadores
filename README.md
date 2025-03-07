# Control de Servomotor XINJE DS2-20P7 via Python/MATLAB 🚀

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8+-yellow.svg)](https://www.python.org/)
[![MATLAB R2021a+](https://img.shields.io/badge/MATLAB-R2021a+-orange.svg)](https://www.mathworks.com)

Repositorio académico para el control de servomotores XINJE DS2-20P7 mediante comunicación serial RS232/RS485, desarrollado en el Laboratorio de Control de la Universidad Nacional de Colombia.



## Características principales ✨
- 🔌 Configuración detallada del servo drive Xinje DS2-20P7-AS
- 📡 Protocolos de comunicación Modbus RTU y comandos directos
- 🐍 Ejemplos en Python para control básico y avanzado
- 📊 Scripts MATLAB para análisis de movimiento y adquisición de datos
- 📄 Documentación técnica completa (esquemas + manual de laboratorio)
- 🛠️ Configuraciones listas para entornos académicos/laboratorio

## Requisitos de instalación ⚙️

### Prerrequisitos
- Python 3.8+ con paquetes:
  ```bash
  pip install pyserial minimalmodbus numpy matplotlib

  # Proceso para Enviar Comandos por Comunicación Serial

## 1. Configuración Inicial del Puerto Serial
Establezca los parámetros de comunicación según su dispositivo:

| Parámetro       | Valor Típico       | Descripción                |
|-----------------|--------------------|----------------------------|
| Baud Rate       | 9600, 115200       | Velocidad de transmisión   |
| Parity          | NONE, EVEN, ODD    | Control de errores         |
| Data Bits       | 8                  | Bits por carácter          |
| Stop Bits       | 1                  | Fin de trama               |
| Flow Control    | None               | Control de flujo           |
| Timeout         | 1 segundo          | Tiempo de espera respuesta |

## 2. Estructura Básica de un Comando Modbus RTU
Para dispositivos que usan protocolo Modbus:

```python
[ Dirección ] [ Función ] [ Datos ] [ CRC ]

import serial
import time

# Configurar puerto
ser = serial.Serial(
    port='COM2',
    baudrate=115200,
    parity=serial.PARITY_EVEN,
    stopbits=serial.STOPBITS_ONE,
    bytesize=serial.EIGHTBITS,
    timeout=1
)

# Comando para habilitar motor (Ejemplo HEX: 01 06 00 64 00 01 49 C9)
command = bytes.fromhex("01 06 00 64 00 01 49 C9")

try:
    ser.write(command)
    time.sleep(0.1)  # Esperar respuesta
    response = ser.read(ser.in_waiting)
    print(f"Respuesta: {response.hex().upper()}")
    
except Exception as e:
    print(f"Error: {str(e)}")
    
finally:
    ser.close()
```
% Crear objeto serial
```
s = serialport("COM2", 115200);
configureTerminator(s, "CR");
s.Parity = "even";
s.Timeout = 1;

% Comando de lectura de posición (HEX: 01 03 20 00 00 02 76 29)
command = uint8([1 3 32 0 0 2 118 41]);

try
    write(s, command, "uint8");
    pause(0.1);
    response = read(s, 9, "uint8");
    disp(response);
catch e
    disp(getReport(e));
end

clear
```
6. Pasos Clave
Inicializar conexión con parámetros correctos

Convertir comando a bytes/HEX según protocolo

Enviar trama completa incluyendo CRC

Esperar respuesta con timeout adecuado

Interpretar datos según documentación del dispositivo

Cerrar conexión después de cada operación

7. Solución de Problemas Básica
🔍 Verificar conexión física del cable

🔢 Confirmar parámetros de comunicación

📟 Chequear dirección Modbus del dispositivo

🛑 Asegurar que el CRC sea calculado correctamente

⏱️ Aumentar timeout si hay retardos en la respuesta

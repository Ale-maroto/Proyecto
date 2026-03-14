# Controlador de Movimiento Coordinado para Brazo Robótico 4-DOF (FPGA + ESP32 IoT)

Este proyecto implementa un sistema de control híbrido para un brazo robótico de 4 grados de libertad. Utiliza una **FPGA** para la generación precisa de señales PWM y el control de trayectoria en tiempo real, y un **ESP32** como puente de comunicación inalámbrica para control remoto vía Wi-Fi/Bluetooth.

## 🎯 Objetivos

### Objetivo General
Desarrollar un sistema embebido de alto rendimiento que permita el control coordinado y remoto de un brazo robótico 4-DOF, integrando lógica de hardware dedicada y conectividad IoT.

### Objetivos Específicos
* **Control de Hardware:** Diseñar módulos PWM en HDL con resolución de microsegundos para evitar vibraciones en los servos.
* **Comunicación Híbrida:** Implementar un protocolo de comunicación UART entre el ESP32 y la FPGA para el envío de coordenadas.
* **Interfaz Inalámbrica:** Crear un servidor web o interfaz móvil en el ESP32 para manipular el brazo a distancia.
* **Sincronización:** Asegurar que los 4 ejes se muevan de forma coordinada para realizar trayectorias suaves.

##Lista de Materiales
###Hardware
FPGA: Intel Cyclone IV / Xilinx Artix-7.
MCU: ESP32 DevKit V1.
Actuadores: 4 Servomotores (2x MG996R, 2x SG90).
Estructura: Kit de Brazo Robótico 4-DOF (Acrílico o Aluminio).
Alimentación: Fuente externa 5V @ 4A (Tierra común con FPGA y ESP32).
Otros: Convertidor de niveles lógicos (si la FPGA no es tolerante a 3.3V), cables jumper y protoboard.

###Software
FPGA: Quartus Prime / Vivado (HDL: VHDL/Verilog).
ESP32: Arduino IDE / PlatformIO (C++).
Simulación: ModelSim para la lógica digital.

---

## 🏗️ Arquitectura del Sistema

El sistema utiliza una estructura de control jerárquica:



1.  **Capa de Aplicación (ESP32):** Recibe comandos vía Wi-Fi y los traduce a tramas seriales.
2.  **Capa de Control (FPGA):** Procesa las tramas, calcula la interpolación y genera los pulsos PWM físicos.

### Diagrama a Bloques Interno
```ascii
 [ Smartphone ] --(Wi-Fi)--> [ ESP32 ] --(UART)--> [ FPGA (Control Unit) ]
                                                        |
                                       ---------------------------------
                                      |         |         |         |
                                   [Servo 1] [Servo 2] [Servo 3] [Servo 4]
                                    (Base)   (Hombro)   (Codo)    (Pinza)


## Cronograma y Metas del Proyecto

| Fase | Tarea / Meta | Responsable | Entregable |
| :--- | :--- | :--- | :--- |
| **Fase 1** | **Configuración e Infraestructura:** Creación del repositorio, estructura de carpetas y módulo PWM base en HDL. | Todo el equipo | Repositorio organizado y señales PWM vistas en osciloscopio/simulación. |
| **Fase 2** | **Comunicación Serial (UART):** Implementación del receptor UART en FPGA y el transmisor en ESP32. Definición del protocolo de datos. | Arquitecto RTL & Dev Firmware | Comunicación exitosa: El ESP32 envía un dato y la FPGA lo interpreta. |
| **Fase 3** | **Control Inalámbrico e Interfaz:** Creación del Servidor Web en ESP32 y lógica de control de posición en la FPGA. | Dev Firmware & Ing. Control | Interfaz móvil funcional que mueve al menos un motor de forma remota. |
| **Fase 4** | **Integración y Coordinación:** Calibración de los 4 grados de libertad y pruebas de movimiento coordinado (trayectorias). | Integrador & QA | Brazo robótico realizando una tarea completa (ej. pick and place). |
| **Fase 5** | **Optimización y Documentación:** Limpieza de código, reporte final y video demostrativo. | Todo el equipo | Documentación técnica completa y repositorio finalizado. |

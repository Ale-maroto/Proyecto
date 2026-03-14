# Controlador de Movimiento Coordinado para Brazo Robótico 4-DOF en FPGA

Este proyecto consiste en el diseño y desarrollo de un sistema de control digital implementado en hardware (FPGA) para gestionar el movimiento sincronizado de un brazo robótico de 4 grados de libertad (4-DOF). El enfoque principal es lograr trayectorias fluidas mediante la generación precisa de señales PWM y lógica de control coordinada.

##  Objetivos

### Objetivo General
Diseñar e implementar un controlador robusto en lenguaje de descripción de hardware (HDL) que permita la manipulación precisa de un brazo robótico 4-DOF, garantizando la coordinación de sus articulaciones en tiempo real.

### Objetivos Específicos
* **Generación de Señales:** Desarrollar módulos PWM con alta resolución para el control de posición de servomotores.
* **Control de Trayectorias:** Implementar una Máquina de Estados Finitos (FSM) que gestione secuencias de movimiento complejas.
* **Optimización de Recursos:** Minimizar el uso de celdas lógicas y registros dentro de la FPGA.
* **Interfaz de Usuario:** Integrar un sistema de control externo (switches o comunicación serial) para la manipulación del brazo.

---

##  Arquitectura del Sistema (Diagrama a Bloques)

El diseño se basa en una arquitectura modular para facilitar el mantenimiento y la escalabilidad:

```ascii
       _________________________________________________________
      |                     FPGA                                |
      |   __________        _______________________             |
      |  |          |      |                       |    ______  |
CLK --|->| Prescaler|----->|  Controlador Central  |-->|      | |--> PWM 1 (Base)
      |  |__________|      |         (FSM)         |   | PWM  | |--> PWM 2 (Hombro)
      |                    |_______________________|   | GEN  | |--> PWM 3 (Codo)
      |   __________                   ^               | UNIT | |--> PWM 4 (Pinza)
SWs --|->| Debounce |------------------|               |______| |
      |  |__________|                                           |
      |_________________________________________________________|

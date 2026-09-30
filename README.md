# AVR Smart Home Automation System

A microcontroller-based Smart Home Automation System implemented using a **Master–Slave AVR architecture**. The system provides secure user authentication, room and device control, temperature monitoring, automatic air-conditioning control, and communication between the Master and Slave controllers through **SPI**.

## Project Overview

The system is divided into two main controllers:

* **Master Controller:** Handles the user interface, authentication, EEPROM storage, device commands, and system control.
* **Slave Controller:** Handles sensor acquisition, device control, temperature monitoring, and automatic AC control.

The Master communicates with the Slave using **SPI**, while the user interacts with the system through an **LCD and keypad**.

## System Architecture

```text
                    +----------------------+
                    |    User Interface    |
                    |    LCD + Keypad      |
                    +----------+-----------+
                               |
                               v
                    +----------------------+
                    |   Master Controller  |
                    |                      |
                    | - Authentication     |
                    | - EEPROM             |
                    | - Menu System        |
                    | - Device Control     |
                    | - Status Requests    |
                    +----------+-----------+
                               |
                              SPI
                               |
                               v
                    +----------------------+
                    |   Slave Controller   |
                    |                      |
                    | - ADC / Temperature  |
                    | - Device Control     |
                    | - AC Automation      |
                    | - Status Handling    |
                    +----------+-----------+
                               |
              +----------------+----------------+
              |                |                |
             AC               TV          Room Devices
```

## Main Features

### User Authentication

* Admin and Guest user modes.
* Password-based authentication.
* Password storage using **EEPROM**.
* Protection against repeated incorrect login attempts.
* Persistent login-block status using EEPROM.

### Smart Home Control

The Master controller provides control of:

* Room 1
* Room 2
* Room 3
* Room 4
* TV
* Air Conditioner

Users can send ON/OFF commands and request the current device status.

### Temperature Monitoring

The Slave controller uses an **ADC** to acquire temperature information and periodically updates the measured temperature.

### Automatic AC Control

The system supports automatic AC operation based on the required temperature.

A hysteresis mechanism is used to reduce unnecessary switching:

* If the measured temperature is sufficiently above the required temperature → AC ON.
* If the measured temperature is sufficiently below the required temperature → AC OFF.
* Around the target temperature → maintain the previous AC state.

### Session Management

* Timer-based session timeout.
* Automatic session expiration after inactivity.
* Return to the authentication interface when the session expires.

## Communication

The Master and Slave controllers communicate through **SPI**.

The Master sends commands for:

* Device ON/OFF control
* Device status requests
* Temperature-related operations

The Slave processes the received commands and controls the corresponding devices.

## Software Architecture

The project follows a modular driver-based structure.

### Master

```text
Master
├── DIO
├── EEPROM
├── LCD
├── LED
├── Keypad
├── SPI
├── Timer
├── Menu
└── Main Application
```

### Slave

```text
Slave
├── DIO
├── ADC
├── LED
├── SPI
├── Timer
└── Main Application
```

This structure separates hardware drivers from application-level logic and makes the system easier to maintain and extend.

## Project Structure

```text
AVR-Smart-Home-Automation/
│
├── Master code/
│   └── Master code/
│       └── Master code/
│           ├── DIO.c
│           ├── DIO.h
│           ├── EEPROM.c
│           ├── EEPROM.h
│           ├── LCD.c
│           ├── LCD.h
│           ├── LED.c
│           ├── LED.h
│           ├── SPI.c
│           ├── SPI.h
│           ├── keypad_driver.c
│           ├── keypad_driver.h
│           ├── menu.c
│           ├── menu.h
│           ├── timer_driver.c
│           ├── timer_driver.h
│           ├── main.c
│           └── ...
│
└── Slave code/
    └── Slave code/
        └── Slave code/
            ├── ADC_driver.c
            ├── ADC_driver.h
            ├── DIO.c
            ├── DIO.h
            ├── LED.c
            ├── LED.h
            ├── SPI.c
            ├── SPI.h
            ├── timer_driver.c
            ├── timer_driver.h
            ├── main.c
            └── ...
```

## Technologies & Concepts

* Embedded C
* AVR Microcontrollers
* Master–Slave Architecture
* SPI Communication
* ADC
* EEPROM
* Timers
* GPIO / DIO
* LCD Interface
* Keypad Interface
* Modular Driver Architecture
* Embedded Security / Authentication
* Temperature-Based Automation

## Roadmap

* [x] Implement Master–Slave AVR architecture
* [x] Implement SPI communication between Master and Slave
* [x] Add LCD and keypad-based user interface
* [x] Implement Admin and Guest authentication
* [x] Store passwords and security status in EEPROM
* [x] Implement room and device control
* [x] Implement device status monitoring
* [x] Implement temperature monitoring using ADC
* [x] Implement automatic AC control with temperature hysteresis
* [x] Add session timeout and login protection
* [ ] Improve communication error handling
* [ ] Add more sensors and smart-home devices
* [ ] Improve system diagnostics and fault reporting
* [ ] Extend the system with additional automation scenarios

## My Role

**Embedded Systems Developer**

* Designed and implemented embedded software modules for the Master and Slave controllers.
* Developed and integrated peripheral drivers including SPI, ADC, EEPROM, Timer, LCD, Keypad, DIO, and LED drivers.
* Implemented the authentication and menu-management logic.
* Developed Master–Slave communication and device-control functionality.
* Implemented temperature-based automatic AC control using ADC measurements and hysteresis.
* Structured the project using modular and reusable embedded software components.

## Author

**Bahgat Mahmoud Bahgat**

Communications and Electronics Engineer
Embedded Systems | Edge Computing | AI-Enabled Embedded Systems

LinkedIn: [Bahgat Mahmoud](https://www.linkedin.com/in/bahgat-mahmoud-2508b320a/)

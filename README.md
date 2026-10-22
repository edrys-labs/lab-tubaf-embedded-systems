# Lab - TUBAF: Embedded Systems

Remote laboratories for the "Embedded Systems" course at TU Bergakademie Freiberg.
Reuse these labs for your own courses or self-study.

Import the configuration files into a newly created lab on https://edrys-labs.github.io or use the Deploy-Lab buttons below.

## Station Setup

To run a station, use the [pyxtermjs](https://github.com/edrys-labs/module-pyxtermjs) terminal server in a secure Docker environment:

```bash
docker run -it -p 127.0.0.1:5000:5000 --device=/dev/ttyACM0:/dev/ttyACM0 edryslabs/module-pyxtermjs:latest
```

Binding the port to `127.0.0.1` keeps the terminal server reachable only from the station's own computer.

The tasks expect their boards at fixed ports: tasks 1 and 3 at `/dev/ttyACM0`, task 2 at `/dev/ttyACM1`. If one
computer runs the stations of tasks 1 and 2, pass both boards to the container:

```bash
docker run -it -p 127.0.0.1:5000:5000 --device=/dev/ttyACM0:/dev/ttyACM0 --device=/dev/ttyACM1:/dev/ttyACM1 edryslabs/module-pyxtermjs:latest
```

The port can also be changed in the settings of the terminal module (`port`).

Alternatively, set up your own Docker environment or use the terminal server directly with Python.
See: https://github.com/edrys-labs/module-pyxtermjs

Each task has simulator rooms next to the station: students prepare the station task in an
[AVR8js simulator](https://github.com/edrys-labs/module-avr8js) of the Arduino Uno, with simulated parts and
charts of pins, interrupts and the ADC. The simulator needs no station.

## Task 1: Ultrasonic Distance Measurement

Students implement ultrasonic sensor control with two difficulty tracks:

- **Track A (Fundamentals)**: Low-level sensor control, GPIO timing, pulse measurement, distance calculation
- **Track B (Library Integration)**: NewPing library, user configuration, LCD menus, unit conversion

**Simulator**:
- Room 2 (Track A): measuring how long a button is pressed, then a simulated ultrasonic sensor on the station's
  pins with a distance slider and a chart of the trigger and echo pulses.
- Room 3 (Track B): the LCD with a simulated ultrasonic sensor, for building the configuration menu.

**Hardware**: Arduino Uno, SRF04 ultrasonic sensor (Trigger pin 12, Echo pin 11), 16×2 LCD display (I2C)

**Learning**: Sensor communication, timing signals, datasheet analysis, display interfaces

[<img src="https://img.shields.io/badge/%F0%9F%9A%80%20-%20Deploy%20Lab%20-%20light?style=plastic" height="25" />](https://edrys-labs.github.io/?/deploy/https://raw.githubusercontent.com/edrys-labs/lab-tubaf-embedded-systems/main/laboratory/de/task-1.yaml)

https://raw.githubusercontent.com/edrys-labs/lab-tubaf-embedded-systems/main/laboratory/de/task-1.yaml

![Task 1](media/task-1.png)

## Task 2: ADC-Based Distance Scanner

Students build a 180° rotating infrared scanner by replacing `analogRead()` with direct ADC register manipulation.

**Tasks**:
- Refactor code into reusable functions
- Configure ADC registers (`ADMUX`, `ADCSRA`) directly
- Transform voltage readings to distance (cm) using sensor datasheet
- Visualize measurements on radar-style plot

**Simulator** (Room 2): fixing a faulty ADC configuration (reference voltage, prescaler, channel selection,
conversion flag), with a chart of the voltage at A0 and of every conversion.

**Hardware**: Arduino Uno, Sharp GP2Y0A02 infrared sensor, servo motor

**Learning**: Register-level ADC programming, sensor calibration, code refactoring

[<img src="https://img.shields.io/badge/%F0%9F%9A%80%20-%20Deploy%20Lab%20-%20light?style=plastic" height="25" />](https://edrys-labs.github.io/?/deploy/https://raw.githubusercontent.com/edrys-labs/lab-tubaf-embedded-systems/main/laboratory/de/task-2.yaml)

https://raw.githubusercontent.com/edrys-labs/lab-tubaf-embedded-systems/main/laboratory/de/task-2.yaml

![Task 2](media/task-2.png)

## Task 3: Interrupt-Driven Motor Control

Students replace polling with interrupt-based programming to synchronize stepper motor position with LED visualization.

**Tasks**:
- Implement ISR for Hall sensor (falling edge trigger)
- Use `volatile` for shared variables between main code and ISR
- Map motor position (2048 steps) to LED ring (24 LEDs)
- Remove polling logic, rely on interrupt-driven position reset

**Simulator**:
- Room 2: fixing a faulty interrupt setup for a button and an LED, with a chart of the pin, the interrupt flag
  and the interrupt service routines.
- Room 3: a small copy of the station with a stepper motor (200 steps per turn), the LED ring and a button in
  place of the Hall sensor.

**Hardware**: Arduino Uno, 28BYJ-48 stepper motor, ULN2003 driver, Hall sensor, Adafruit NeoPixel LED ring (24 LEDs)

**Learning**: Interrupt configuration, ISR programming, motor control, visual feedback synchronization

[<img src="https://img.shields.io/badge/%F0%9F%9A%80%20-%20Deploy%20Lab%20-%20light?style=plastic" height="25" />](https://edrys-labs.github.io/?/deploy/https://raw.githubusercontent.com/edrys-labs/lab-tubaf-embedded-systems/main/laboratory/de/task-3.yaml)

https://raw.githubusercontent.com/edrys-labs/lab-tubaf-embedded-systems/main/laboratory/de/task-3.yaml

![Task 3](media/task-3.png)

## More Information

For detailed explanations of each lab, see the blog posts:
- [Ultrasonic Distance Measurement Lab](https://edrys-labs.github.io/blog/posts/021_remote-lab-distance-measurement/)
- [ADC Distance Scanner Lab](https://edrys-labs.github.io/blog/posts/022_remote-lab-adc-scanner/)
- [Interrupt Motor Control Lab](https://edrys-labs.github.io/blog/posts/023_remote-lab-interrupts-motor/)

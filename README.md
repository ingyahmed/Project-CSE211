# NUCLEO-F401RE Digital Clock & Analog Voltage Display

## Project Overview

This project implements a digital clock combined with an analog voltage display on a 4-digit 7-segment display using the NUCLEO-F401RE development board paired with an Arduino Multifunction Shield. It showcases real-time data monitoring by displaying either the elapsed time since reset or the current analog voltage read from a potentiometer.

The 7-segment display is driven via a shift register controlled through digital pins on the NUCLEO board. Users can toggle between the time and voltage display modes using onboard buttons, making this project a practical example of embedded real-time data handling with MBED OS.

https://github.com/user-attachments/assets/9e0e4534-b90c-4504-8ee2-65e7095bd422

---

## Features

- **Time Display:** Shows elapsed time in MM:SS format, counting minutes and seconds since reset.
- **Voltage Display:** Reads and displays the analog voltage from a potentiometer with 2 decimal places.
- **User Input:**
  - Button S1 resets the clock to 00:00.
  - Button S3 toggles the display to show voltage readings.
- **Hardware Control:** Utilizes a shift register to drive a multiplexed 4-digit 7-segment display.
- **Real-time Updates:** Uses MBED OS timers and interrupt service routines for precise timekeeping.

---

## Hardware Requirements

- **NUCLEO-F401RE Development Board**
- **Arduino Multifunction Shield** (includes 4-digit 7-segment display, potentiometer, and switches)

### Pin Connections

| Signal     | NUCLEO Pin |
|------------|------------|
| Latch (ST_CP) | D4       |
| Clock (SH_CP) | D7       |
| Data (DS)     | D8       |
| Potentiometer (Analog Input) | A0 |
| Button S1 (Reset) | A1    |
| Button S3 (Display Voltage) | A3 |

---

## Software Requirements

- MBED Studio IDE

---

## System Design

### Startup and Initialization

- **Vector Table:** Located at address 0x0, sets up initial stack pointer and reset handler.
- **Reset Handler:** Calls `SystemInit` for clock setup, then jumps to `main()`.
- **Default Exception Handlers:** Loop infinitely if unexpected interrupts occur.

### Code Structure

- **Pin Configuration:** DigitalOut for shift register pins and DigitalIn for buttons.
- **Analog Input:** Reads potentiometer voltage via on-chip ADC.
- **Timekeeping:** Uses a `Ticker` to increment seconds and minutes every 1 second via ISR.
- **Shift Register Functions:**
  - `shiftOutMSBFirst()` sends bits MSB first to the shift register.
  - `writeToShiftRegister()` sends segment and digit data.
- **Display Logic:** Multiplexes 4 digits to show time or voltage with optional decimal points.

---

## Usage

1. **Reset Clock:** Press **Button S1** to reset timer to 00:00.
2. **Display Voltage:** Hold **Button S3** to display the current potentiometer voltage.
3. **Display Time:** When Button S3 is not pressed, the display shows elapsed time in MMSS format.
4. The display refreshes continuously to maintain stable output.

---

## Results

- Real-time voltage changes are shown instantly when **Button S3** is pressed.
- Timer increments every second and resets correctly when **Button S1** is pressed.
- Seamless switching between time and voltage display modes.

---

## Conclusion

This project successfully demonstrates integration of the NUCLEO-F401RE with an Arduino multifunction shield to display real-time clock and analog voltage measurements on a 4-digit 7-segment display. By leveraging MBED OS features such as timers and interrupts, it provides an accurate, user-friendly embedded system application.

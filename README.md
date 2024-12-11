# TIMER_HW_IP Driver

Advanced driver implementation for a hardware timer module in embedded systems.

## Project Overview

The TIMER_HW_IP driver is a versatile solution for managing hardware timers in embedded systems, offering precision timing and efficient integration with FPGA-based platforms like Altera/Intel FPGAs. It includes macros for starting, stopping, resetting, and reading timer values to ensure seamless performance in real-time applications.

## Features

- **Hardware Control**:
  - Reset, start, and stop the timer with simple macros.
  - High-resolution timer readings for precise interval measurements.
- **Scalability**:
  - Compatible with Altera/Intel FPGA systems using Nios II processors.
- **Real-Time Capabilities**:
  - Ideal for applications requiring precise delays and timing.

## Functions

1. **TIMER_RESET**: Resets the timer to its initial state.
2. **TIMER_START**: Starts the timer and initiates measurement.
3. **TIMER_STOP**: Stops the timer without resetting the current value.
4. **TIMER_READ**: Retrieves the current timer value for interval analysis.

## File Structure

- **src/**: Contains source files including driver macros and configurations.
- **doc/**: Includes the detailed driver manual and usage examples.
- **examples/**: Ready-to-use examples demonstrating timer functionality in C.

## Usage Instructions

### Setup
1. Include `altera_avalon_timer_regs.h` in the `HAL/inc` folder of your BSP project.
2. Configure the timer component in your Nios II environment.
3. Add the macros provided in the driver documentation to your project.

### Example Usage

```c
#include <stdio.h>
#include <io.h>
#include "altera_avalon_timer_regs.h"

int main() {
    int seconds = 0, minutes = 0;

    TIMER_RESET;
    TIMER_START;

    while (1) {
        while (TIMER_READ < 50000000); // Wait for 1 second (50 MHz timer)
        TIMER_RESET;
        TIMER_START;
        if (seconds < 59) {
            seconds++;
            printf("Second = %d\n", seconds);
        } else {
            minutes++;
            seconds = 0;
            printf("Minutes = %d\n", minutes);
        }
    }
    return 0;
}

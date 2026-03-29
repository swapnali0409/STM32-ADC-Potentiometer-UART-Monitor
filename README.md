# STM32-ADC-Potentiometer-UART-Monitor
A simple STM32 project that reads analog input from a potentiometer using ADC and sends real-time values to a serial terminal via UART.
#  STM32 ADC Potentiometer Monitor

##  About this project

This is a simple and practical STM32 project where I read an analog value using a potentiometer and display it on my PC using UART.

Instead of using fixed values, I used a potentiometer (POT) to generate a variable voltage. The STM32 reads this voltage using ADC and sends the corresponding digital value to the serial terminal.

This helped me understand how real-world analog signals are handled in embedded systems.

---

##  What this project does

* Reads analog voltage using ADC
* Converts it into digital value (0–4095)
* Sends data to PC using UART
* Displays values continuously in serial terminal (PuTTY)

---

##  How it works (simple)

1. Potentiometer provides variable voltage (0–3.3V)
2. ADC reads this voltage
3. STM32 converts it into digital value
4. Value is sent through UART
5. You see output on your PC

 Simple flow:

Potentiometer → ADC → Digital Value → UART → PC Terminal

---

##  Output

In PuTTY or any serial monitor, you will see:

```
0
512
1023
2048
3000
4095
```

As you rotate the potentiometer, the values change smoothly.

---

##  Hardware Required

* STM32 board (e.g., Nucleo / Discovery)
* Potentiometer (10k recommended)
* Jumper wires
* USB cable

---

##  Pin Configuration

### 🎛️ Potentiometer Connection

| POT Pin    | Connection          |
| ---------- | ------------------- |
| Left pin   | GND                 |
| Right pin  | 3.3V                |
| Middle pin | PA0 (ADC Channel 0) |

---

###  UART Configuration

| Signal    | Pin    |
| --------- | ------ |
| TX        | PA2    |
| RX        | PA3    |
| Baud Rate | 115200 |

---

##  ADC Configuration

* ADC Instance: ADC1
* Channel: Channel 0 (PA0)
* Resolution: 12-bit
* Conversion Mode: Continuous
* Data Range: 0 to 4095

---

##  Important Code Part

```c
HAL_ADC_Start(&hadc1);
HAL_ADC_PollForConversion(&hadc1, HAL_MAX_DELAY);
readValue = HAL_ADC_GetValue(&hadc1);

sprintf(tx_buffer, "%d\r\n", readValue);

HAL_UART_Transmit(&huart2, (uint8_t*)tx_buffer, strlen(tx_buffer), HAL_MAX_DELAY);
```

---

##  Why this project is useful

This is a basic but very important project to understand:

* ADC working in STM32
* Analog to digital conversion
* UART communication
* Real-time data monitoring

This is the foundation for many real-world systems.

---

##  Limitations

* Uses blocking functions (HAL_MAX_DELAY)
* No filtering of noisy signals
* Continuous polling (not interrupt-based)

---

##  Future Improvements

* Convert ADC value to voltage (in volts)
* Use interrupt or DMA for ADC
* Add LCD display
* Apply averaging/filtering for stable readings

---

##  Final Note

This project helped me understand how STM32 reads real-world analog signals.

Once you understand this, you can build:

* Sensor-based systems
* Data logging projects
* IoT applications
* Control systems

---

 Simple project, but very powerful concept!

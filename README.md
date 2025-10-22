# Pressure-Sensor-with-#ESP32-and-The-16-Bit-ADC-ADS1115
-- Hey, all. We will go over how to interface the Pressure Transmitter sensor with ESP32 and the 16-bit ADC ADS1115 --

**The top highlight we should know: Pressure sensor measured through Analog Signal as an input.** Analog signal is a type of signal that is used to read real-world conditions, one of which is pressure.

We need these materials to set up the pressure sensor on the pipe. 
<img width="960" height="428" alt="Pressure transmitter sensor2" src="https://github.com/user-attachments/assets/954d23f0-4dd9-4125-8a46-327614a28276" />

The 16-bit ADC ADS1115 is used as an external ADC for the ESP32 because the ADC read from the ESP32 is non-linear, which affects the system's output. At least try calibrating first to solve the ESP32 linearity issue using [this repository](https://github.com/e-tinkers/esp32-adc-calibrate). However, if the calibration does not significantly improve the output readings, which remain non-linear or fluctuating, applying mathematical methods such as linear or polynomial regression could be considered. 

Using an external ADC like ADS1115 could be another option if need multiple analog inputs from the sensors nor need higher precision reading and small signals to be measured with high resolution. It is recommended to read the [ADS115 library](https://github.com/adafruit/Adafruit_ADS1X15/blob/master/examples/continuous/continuous.ino).

## The Scheme
According to the ADS1115 datasheet, >the resistor and capacitor are needed. When the ADS1115 are converting data, they draw current in short spikes. The 0.1μF bypass capacitor supplies the momentary bursts of extra current needed from the supply. 
<img width="1010" height="706" alt="Resistor" src="https://github.com/user-attachments/assets/d871eb17-2667-47ec-9cb5-4247438ddba9" />






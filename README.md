# Pressure-Sensor-with-#ESP32-and-The-16-Bit-ADC-ADS1115
-- Hey, all. We will go over how to interface the Pressure Transmitter sensor with ESP32 and the 16-bit ADC ADS1115 --

**The top highlight we should know: Pressure sensor measured through Analog Signal as an input.** Analog signal is a type of signal that is used to read real-world conditions, one of which is pressure.

We need these materials to set up the pressure sensor on the pipe. 
<img width="960" height="428" alt="Pressure transmitter sensor2" src="https://github.com/user-attachments/assets/954d23f0-4dd9-4125-8a46-327614a28276" />

The 16-bit ADC ADS1115 is used as an external ADC for the ESP32 because the ADC read from the ESP32 is non-linear, which affects the system's output. At least try calibrating first to solve the ESP32 linearity issue using [this repository](https://github.com/e-tinkers/esp32-adc-calibrate). However, if the calibration does not significantly improve the output readings, which remain non-linear or fluctuating, applying mathematical methods such as linear or polynomial regression could be considered. 

Here is an example comparison between before and after raw reading from the ESP32 ADC against the calibrated reading with LUT.
<img width="1883" height="528" alt="Untitled design (12)" src="https://github.com/user-attachments/assets/65e47807-6681-48f2-89a8-58d9cffbaae1" />

Using an external ADC like ADS1115 could be another option if need multiple analog inputs from the sensors nor need higher precision reading and small signals to be measured with high resolution. It is recommended to read the [ADS1115 library](https://github.com/adafruit/Adafruit_ADS1X15/blob/master/examples/continuous/continuous.ino).



## The Scheme
According to the ADS1115 datasheet, 
> The resistor and capacitor are needed. When the ADS1115 is converting data, it draws current in short spikes. The 0.1μF bypass capacitor supplies the momentary bursts of extra current needed from the supply. On the I2C interface, the bus wires are pulled high by pull-up resistors.
<img width="1010" height="706" alt="Resistor" src="https://github.com/user-attachments/assets/d871eb17-2667-47ec-9cb5-4247438ddba9" />

The addition of multiple analog inputs necessitates accurate calculation of **the system’s power (voltage and current) requirements**, as the system typically depends on the external power supply.
<img width="992" height="438" alt="Resistor (1)" src="https://github.com/user-attachments/assets/5b866782-01cc-40b7-aaf2-fa6e378e5d6b" />

## The Code & Calibration
It is crucial to ensure the initialization of the ADS1115 functions is correct. The while loop () is used to execute a block of code repeatedly until a certain condition is met. If there is an error, it will get stuck on the looping process and cannot continue to the following code nor iterate.
```
if (!ads.begin())
{
Serial.println("Failed to initialize ADS.");
while (1);
yield();
}
```
The pressure sensor has a working voltage from ±0.5V to 5V. If there is no any load, the voltage will remain at ±0.5V. 
Make sure that the jumper wires connecting the sensors and modules are in good condition to minimize resistance and electrical noise in the input readings.

The ADC input range (or gain) can be adjusted using the following functions; however, caution must be exercised, as improper gain settings may damage the components or cause the ADS1115 to malfunction. Based on the reference image below, at the default gain 1 bit corresponds to 0.1875mV.

![17](https://github.com/user-attachments/assets/de7bbf02-ca70-4ffa-88f0-18b2008fe035)







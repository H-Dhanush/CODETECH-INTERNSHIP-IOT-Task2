# CODETECH-INTERNSHIP-IOT-Task2

**Name:** Dhanush H <br>
**Company:** CODETECH IT SOLUTIONS <br>
**ID:** CT08DS1824 <br>
**Domain:** Internet of Things <br>
**Duration:** June to July 2024 <br>
**Mentor:** Mohammed Muzammil Ahmed <br>


## Overview of the Project

### Project: Home Automation using ESP32 with Light Bulb and RemoteXY

### Objective

The objective of this project is to create a WiFi-based control system for a light bulb using the RemoteXY platform. The system allows users to control the light bulb's state (ON/OFF) via a graphical user interface on a connected device.

### Key Activities

**Setup WiFi Connection:**
      - Configure the microcontroller as a WiFi access point with a predefined SSID and password. This setup allows devices to connect to the network and access the control interface.

**Configure RemoteXY Interface:**
      - Define and initialize the RemoteXY interface with a simple GUI that includes a switch to control the light bulb. This involves setting up the necessary input and output variables.

**Control Light Bulb:**
      - Implement the logic to change the light bulb's state based on user input from the RemoteXY interface. The state change is reflected in real-time by writing to the appropriate GPIO pin.

**Serial Communication:**
      - Use serial communication to debug and monitor the state changes of the light bulb. Print messages to the serial monitor indicating whether the light bulb is ON or OFF, which aids in troubleshooting.

**State Change Detection:**
      - Detect changes in the light bulb's state and update the serial monitor only when a change occurs. This reduces unnecessary serial output and helps identify the exact moment of state transitions.

**RemoteXY Handling:**
      - Continuously handle RemoteXY events and update the control interface. Ensure that the system remains responsive to user inputs and maintains a stable connection.

### Technologies Used

**WiFi Library:**
      - Utilizes the WiFi library to establish the microcontroller as a WiFi access point, enabling wireless communication. This library handles network setup, connection management, and data transmission.

**RemoteXY Library:**
      - Employs the RemoteXY library to create a user-friendly graphical interface for remote control. This library simplifies the creation of GUIs and handles the communication between the control interface and the microcontroller.

**Serial Communication:**
      - Uses the Serial library for debugging and monitoring purposes. This technology provides a simple way to output messages to the serial monitor, helping developers track the system's behavior.

**Microcontroller (e.g., ESP32):**
      - The core hardware component that runs the control system, manages WiFi connections, interfaces with the RemoteXY library, and controls the light bulb via GPIO pins.

**GPIO (General Purpose Input/Output):**
      - Utilizes GPIO pins on the microcontroller to physically control the light bulb. The digitalWrite function sets the pin high or low, turning the light bulb on or off based on the RemoteXY input.

### Hardware and Software Required

● ESP32 <br>
● Light Bulb <br>
● Realy <br>
● Breadboard <br>
● Jumper wires and normal copper wire <br>
● Wire Plug <br>
● Bulb Holder <br>
● USB cable for Programming(ESP32) <br>
● Arduino IDE <br>
● RemoteXY <br>

### Steps to do this project:

1. **Ensure Latest Arduino IDE:**<br>
        ● Before starting, make sure you have the latest version of the Arduino IDE installed. If not, uninstall the current version and install the latest one to ensure compatibility.

2. **Add ESP32 to Arduino IDE:**<br>
       ● Open Arduino IDE.<br>
       ● Go to **File > Preferences**.<br>
       ● In the "Additional Board Manager URLs" field, enter the following URLs: <br>
         https://dl.espressif.com/dl/package_esp32_index.json, http://arduino.esp8266.com/stable/package_esp8266com_index.json <br>
       ● Click **OK**.

3. **Install ESP32 Board:** <br>
       ● Open the Boards Manager by navigating to **Tools > Board > Boards Manager**.<br>
       ● Search for **ESP32**.<br>
       ● Click the **Install** button for **ESP32 by Espressif Systems**.

4. **Install Required Libraries:**<br>
       ● Open the Library Manager by going to **Tools > Manage Libraries**.<br>
       ● Search for **RemoteXY** and install it.<br>
       ● Search for **WiFi** and ensure it is installed.

5. **Set Up WiFi Connection:**<br>
       ● Define the WiFi settings in your code:<br>
         #define REMOTEXY_MODE__WIFI_POINT <br>
         #define REMOTEXY_WIFI_SSID "RemoteXY" <br>
         #define REMOTEXY_WIFI_PASSWORD "12345678" <br>
         #define REMOTEXY_SERVER_PORT 6377<br>
       ● Include the necessary libraries:<br>
         #include <WiFi.h> <br>
         #include <RemoteXY.h> <br>
         

6. **Configure RemoteXY Interface:** <br>
       ● Define the GUI configuration: <br>
         uint8_t RemoteXY_CONF[] = { 255,1,0,0,0,29,0,17,0,0,0,164,1,106,200,1,1,1,0,2,31,80,44,22,1,36,26,31,31,79,70,70,0,79,78,0 };
         <br>
       ● Define the RemoteXY structure:<br>
         struct {<br>
           uint8_t Light_Bulb; // =1 if switch ON and =0 if OFF<br>
           uint8_t connect_flag;  // =1 if wire connected, else =0<br>
         } RemoteXY;<br>

7. **Initialize RemoteXY and Set Up GPIO:** <br> 
       ● In the **setup()** function, initialize RemoteXY and set the pin mode: <br>
         
         void setup() {  <br>
           RemoteXY_Init(); <br>
           pinMode(PIN_LIGHT_BULB, OUTPUT); <br>
           Serial.begin(115200); <br>
         }
         

8. **Control Light Bulb:** <br>
       ● In the **loop()** function, handle RemoteXY events and control the light bulb: <br>
         void loop() {  <br>
           RemoteXY_Handler();  <br>
           digitalWrite(PIN_LIGHT_BULB, (RemoteXY.Light_Bulb == 0) ? LOW : HIGH);  <br>
         } <br>

9. **Monitor State Changes:** <br>
       ● Add logic to monitor and print state changes to the Serial monitor: <br>
         bool lastState = LOW; <br>

         void loop() { <br>
           RemoteXY_Handler(); <br>
           bool currentState = (RemoteXY.Light_Bulb == 0) ? LOW : HIGH; <br>
           if (currentState != lastState) { <br>
             if (currentState == HIGH) { <br>
               Serial.println("Light Bulb is OFF"); <br>
             } else { <br>
               Serial.println("Light Bulb is On"); <br>
             } <br>
             lastState = currentState; <br>
           } <br>
         } <br>

10. **Final Touches:** <br>
       ● Avoid using **delay()** in the loop; use **RemoteXY_delay()** if needed. <br>
       ● Ensure the setup and loop functions are correctly defined and free of blocking code. <br>

11. **Upload and Test:** <br>
       ● Connect your ESP32 board to the computer. <br>
       ● Select the correct board and port from the **Tools > Board** and **Tools > Port** menus. <br>
       ● Upload the code to your ESP32. <br>
       ● Connect to the "RemoteXY" WiFi network using the password "12345678". <br>
       ● Open the RemoteXY app on your device, connect to the ESP32, and control the light bulb.
  
### Circuit Diagram

![image](https://github.com/H-Dhanush/CODETECH-INTERNSHIP-IOT-Task2/assets/167459628/093401d8-2d15-4e00-b515-2e5cad7874aa)

### Output in Serail Monitor

![image](https://github.com/H-Dhanush/CODETECH-INTERNSHIP-IOT-Task2/assets/167459628/c23008c7-2123-4d58-8f1d-e6866dbcf20c)

### Graphical Interface in RemoteXY

![image](https://github.com/H-Dhanush/CODETECH-INTERNSHIP-IOT-Task2/assets/167459628/7c2a3b60-9663-4e75-b815-7ea3ee258cae)

### Output when Light Bulb is OFF

![image](https://github.com/H-Dhanush/CODETECH-INTERNSHIP-IOT-Task2/assets/167459628/1d7914e6-4330-4318-b735-1192ef3038a8)

### Output when Light Bulb is ON

![image](https://github.com/H-Dhanush/CODETECH-INTERNSHIP-IOT-Task2/assets/167459628/2b089455-8bfb-4c07-b6e3-41947b1a0cc0)

### Conclusion
This project not only demonstrates the basics of remote device control but also lays the groundwork for more advanced IoT applications. Anyone can further expand this project by integrating additional sensors, actuators, or incorporating cloud-based services for data logging and analysis.With this foundational knowledge, you are well-equipped to explore and innovate in the realm of IoT and home automation. Happy tinkering!





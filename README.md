## ESP32 Encoder OSC Send (Eos Channel) 
### *With AP Config and Double Reset Detector*

----------
*This project uses an ESP32 board to send OSC messages to Eos and control channels with an encoder.*

----------


###  Example:
Chnage intensity of a channel in Eos wirelessly with a turn of the encoder.


Use case could be follow spot ops have dynamic control of their intensity.

https://user-images.githubusercontent.com/70780576/211750836-6df9e416-fb22-4ce9-8b21-e421121dd19d.mov

- When the encoder is turned it will send a custom OSC message `/eos/user=7/chan/300` (specified in the AP config) to a computer with an IP `10.101.100.105` on the local network running QLab on port `8000`. Internally the code will append a `"+%` or `"-%"` to the osc address dependent of the rotation of the encoder. This syntax adjusts the intensity up or down for channel 300 in Eos. (USB is only used for power)

----------

### Hardware:
This demo used a FREENOVE ESP32-WROVER-DEV controller with a breadboard and a button on pin 13.

<img width="350" alt="Screen Shot 2021-11-21 at 4 17 23 PM" src="https://user-images.githubusercontent.com/70780576/211749180-fe8243b4-5d29-47b6-8f9b-474f2bcb79a2.jpg">

----

### Setup:

- After uploading to the device it will enter config mode and broadcast an AP. 
  - *On your computer/device you should see a wifi called "esp32_osc".* 
  
  <img width="107" alt="Screenshot 2023-01-10 at 11 42 25 PM" src="https://user-images.githubusercontent.com/70780576/211749751-785e2253-0027-4965-ac81-95733d8a9924.png">


- Once connected, a WiFiManager window will open > Configure WiFi

<img width="354" alt="Screenshot 2023-01-10 at 11 43 12 PM" src="https://user-images.githubusercontent.com/70780576/211749811-9815d346-39fe-4d93-a8d2-504619aad1ff.png">


- Enter SSID, Password, OSC IP (Eos device you're sending osc to), OSC Port, OSC Address, OSC Argument (optional), DT Pin (GPIO), and CLK Pin (GPIO).
   - If you leave the Static IP, Gateway and Subnet empty then the device will use DHCP to get an IP and connect.

<img width="251" alt="Screenshot 2023-01-10 at 11 44 01 PM" src="https://user-images.githubusercontent.com/70780576/211749879-2e751571-6dbf-4514-8a44-4e8d40d11797.png">

<img width="259" alt="Screenshot 2023-01-10 at 11 44 18 PM" src="https://user-images.githubusercontent.com/70780576/211749904-5ab5d3cf-58b2-492b-9c50-04d7a307786b.png">


- When finished click "Save" and the ESP32 will store the configuration and reset. On boot it will automatically connect to the stored SSID WiFi. The onboard Blue LED will flash when connecting and stay on if connected. 

- In Eos go to `Setup > Show Control > OSC` Enable OSC RX
  - Port should match AP config `8000`

------

### Troubleshooting & Resetting:
- If after you click Save and the WiFi doesn't connect, because of a invalid password possibly, then you can get back to the config screen by going to `192.168.4.1` in your browser.
- If the onboard reset button is pressed twice (not too fast), then the ESP32 will reset to enter config mode (No blue LED) and broadcast an AP to change settings.

----



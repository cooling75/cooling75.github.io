# Arduino-cli and VSCode

With the second try I was successful to get arduino-cli and VSCode to work together. 

In the past I was working and testing in the Arduino IDE and copying the code manually to VSCode to sync it via git. To be able to work directly in VSCode would save some time so I invested some time into it.

Loosely covered my steps and pain points were:

1. Install arduino-cli and configure VSCode to use it in the Arduino extension settings

2. I added the board urls also to the list in the settings.json in VSCode (Arduino extension settings)

```json
"arduino.additionalUrls": [
        "https://arduino.esp8266.com/stable/package_esp8266com_index.json",
        "https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json"
    ],
``` 

3. For esp32/esp8266 programming add the boards to arduino-cli:

```bash
arduino-cli config init --additional-urls \
https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json,\
https://arduino.esp8266.com/stable/package_esp8266com_index.json

arduino-cli core update-index
```

4. Every sketch must be in a separate folder named exactly like the __.ino__ file of the sketch itself.

5. Press "F1" type in "Select sketch" and select the sketch you want to verfiy. A hidden subfolder __.vscode__ with a file __arduino.json__ will be created. Add (name the folder as you like):

```json
"output": "../build"
```
# efm8-arduino-programmer
Program EFM8 devices using an arduino

Thanks to jaromir-sukuba and racerxdl for working on firmware to implement C2 protocol via arduino GPIO.  This work largely pulls from them.

# Setting up

C2 is a 2-pin protocol.  Any arduino should work to implement the protocol via GPIO.  Just need to make sure that the correct pins are mapped for your Arduino.  Check the [firmware file](https://github.com/conorpp/efm8-arduino-programmer/blob/master/prog/prog.ino#L11) and change the pins to map to your device if needed.  Currently, it is for Arduino Mega and maps C2D and C2CK to digital pins 2 and 3, respectively.

Program the firmware to the arduino and connect C2D, C2CK, and GND to your target device.

### Software

You need to have Python installed.  Then, install some required python modules.

```
pip install -r requirements.txt
```

# Running

It is set up in a client/server model to be able to easily support programming multiple targets at the same time.

First you must run the server that will handle communication to the arduino.

```
python prog_server.py <serial-port> [<serial-port2> ...]
```

Supply a list of serial ports (you can use more than one arduino at a time) to handle programming.  E.g /dev/USB1 or COM1.

Then you can finally program something using the client script.

```
python prog_client.py <firmware.hex> <port>
```

This will connect to the server and tell it to download specified firmware via specified arduino.  

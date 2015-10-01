# Earthquake Detector

Description here...

This earthquake detector requires the following components from the Grove Starter Kit Plus:

1. Intel Edison with Arduino breakout board
2. Grove Accelerometer
3. RGB LCD Display

## How It Works

This earthquake detector will listen for vibrations using the accelerometer.

When it thinks it detects an earthquake, it will attempt to verify with the USGS API that an earthquake occurred

It will then use the LCD Display to either warn of the quake, or let you know it was  a false alarm.

## How To Setup

To begin, clone the Intel IoT Examples with git on your computer:

    $ git clone https://github.com/hybridgroup/intel-iot-examples.git

Not sure how to do that? [Here is an excellent guide from Github on how to get started](https://help.github.com/desktop/guides/getting-started/).

### Adding The Code To Eclipse IoT

Eclipse initial setup instructions go here...

### Connecting The Grove Sensors

![](./../../../images/earthquake-detector.jpg)

You will need to have the Grove Shield connected to the Arduino-compatible breakout board, in order to plug in all the various Grove devices into the Grove shield. Make sure you have the tiny VCC switch on the Grove Shield set to the "5V" position.

Plug one end of a Grove cable into the "Accelerometer", then connect the other end to any of the "I2C" ports on the Grove Shield.

Plug one end of a Grove cable into the "RGB LCD", then connect the other end into any of the "I2C" ports on the Grove Shield.

### Intel Edison Setup

This example uses the `restclient-cpp` library to perform REST calls to the server. The code for `restclient-cpp` can be found in the `lib` directory. The `restclient-cpp` library requires the `libcurl` package, which is already installed on the Intel Edison by default.

### Running The Code On Edison

When you're ready to run the example, you can click on the "Run" icon located in the menubar at the top of the Eclipse editor.
This will compile the program using the Cross G++ Compiler, link it using the Cross G++ Linker, transfer the binary to the Edison, and then execute it on the Edison itself.

## Data Store Server Setup

You can optionally store the data generated by this example program in a backend database deployed using Node.js, and the Redis datastore. You use your own account on a hosted service such as Microsoft Azure or IBM Bluemix.

For information on how to setup your own cloud data server, go to:

https://github.com/hybridgroup/intel-iot-examples-datastore

### Running The Example With The Cloud Server

To run the example with the optional backend datastore you need to set the `SERVER` and `AUTH_TOKEN` environment variables. You can do this in Eclipse by:

1. Select the "Run" menu and choose "Run Configurations". The "Run Configurations" dialog will be displayed.
2. Click on "doorbell" under "C/C++ Remote Application". This will display the information for your application.
3. Add the environment variables to the field for "Commands to execute before application" so it ends up looking like this, except using the server and auth token that correspond to your own setup:

```
chmod 755 /tmp/earthquake-detector
export SERVER="http://intel-examples.azurewebsites.net/counter/earthquake-detector/inc"
export AUTH_TOKEN="YOURTOKEN"
```

4. Click on the "Apply" button to save your new environment variables.

Now when you run your program using the "Run" button, it should be able to call your server to save the data right from the Edison.

## Determining The Intel Edison IP Address

You can determine what IP address the Intel Edison is connected to by running:

    ip addr show | grep wlan

You will see output similar to:

    3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast qlen 1000
        inet 192.168.1.13/24 brd 192.168.1.255 scope global wlan0

The IP address is shown next to `inet`. In the example above, the IP address is `192.168.1.13`

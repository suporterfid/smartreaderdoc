# Smartreader R700

The Smartreader R700 is an custom application (CAP) reference design that configures and manages an Impinj R700 RAIN RFID Reader interfacing with the Impinj IoT Interface with additional options to publish data directly from the reader to defined outputs like:
- Local HTTP streams on the reader;
- MQTT broker;
- HTTP POST;
- TCP/IP socket;
- UDP socket;
- Serial port over USB;
- USB Flash Drive;

The easy-to-use graphical user interface makes it easy to configure the device to quickly read tag data such as EPC, TID and User Memory and record other relevant information such as the last timestamp and antenna port number and antenna zone name.

Smartreader provides a simple reader configuration user interface for deploying your RAIN RFID infrastructure.

This software is not intended to be a complete end-to-end inventory management solution.

## Characteristics
- Easy-to-use graphical user interface for single reader deployments
used to identify RAIN RFID tags
- Tag data read (EPC, user memory and TID)
- Defines basic reader settings for reading RAIN RFID tags and saving the configuration directly in the reader's memory
- Sending RAIN RFID data via MQTT, HTTP POST, Socket TCP/IP Server, UDP Server, USB flash drive or serial port over USB
(when available on the reader)

## Supported Impinj Hardware and Firmware Versions
Smartreader embedded software applications support the following readers:
- IPJ-R700-241 - all settings (including Antenna Hub)
- IPJ-R700-341 - all settings (including Antenna Hub)

All firmware versions after 8.1.0.240 (included) are supported

## Installing Smartreader on your Impinj reader
Install Smartreader software via the Impinj readers web interface
1. First, download the Smartreader software.
2. Enter the Impinj Reader Web Interface. 
3. Select the .upgx file by either clicking on the select link or by dragging the file into the boxed region. 
4. Once the upload finishes, the firmware verification and installation will start automatically. When the install is complete, the new cap will not be active until the reader is rebooted.
5. Click the Reboot button to reboot the reader. The connection to the reader will be disrupted and the Reboot button will pulse until it comes back.

It may take the reader up to three minutes to unzip and install all the necessary files. Let the reader complete the installation and then proceed with restarting the reader.

To access the Smartreader configuration screen, open a web browser by providing the following address for the connection `https://reader_ip_address:8443/` where *reader_ip_address* represents the IP address or hostname of your Impinj reader. The default username and password to access the configuration screen are: “admin” and “admin”.

To obtain a license for your reader, contact your Smartreader vendor.
After obtaining a valid license, copy/paste it into the License field and click **"Apply Settings"**.

## Features

### Keepalive
In this section you can configure a time in seconds for Smartreader to send notifications indicating that the reader and the software are active. 

### Reader Settings
In this section, you will configure the reader operating mode, transmit power, and GPIO settings.

#### RAIN RFID Settings
Here you can configure RAIN RFID related parameters such as RF operation mode, inventory mode, target sessions, tag population estimation and transmit power for each antenna individually, it is also possible to define a name of a reading zone for each antenna.

*Important! Smartreader will automatically identify the reader model and the total number of antennas. For example, if you have an R700 with 2 Antenna Hubs, there will be 18 ports available for configuration on this screen.*

#### Advanced GPO
Here you can configure how reader GPOs will behave.
The following conditions can trigger a GPO change based on the following statuses
- Normal
- Reader Inventory Status
- Reader Inventory Tag Status
- Success on Rule Validation
- Error on Rule Validation

When activating the GPO in NORMAL mode it is possible to activate or deactivate a GPO port by HTTP GET request:
Enable port 1: 
`https://reader_ip_address:8443/api/gpo/1/status/ON`
Disable port 1: 
`https://reader_ip_address:8443/api/gpo/1/status/OFF`

Enable port 2: 
`https://reader_ip_address:8443/api/gpo/2/status/ON`
Disable port 2: 
`https://reader_ip_address:8443/api/gpo/2/status/OFF`

Enable port 3: 
`https://reader_ip_address:8443/api/gpo/3/status/ON`
Disable port 3: 
`https://reader_ip_address:8443/api/gpo/3/status/OFF`

#### Triggers
This is where you can configure GPI triggers to start/stop inventory based on external sensors.

### Data Format
Here you configure how the collected information will be formatted.

#### Fields to include
The Smartreader can include basic information such as EPC data, antenna port information, antenna reading zone name, timestamp, RSSI, TID, phase, frequency, status of GPI ports, GS1 tag data standard parsed values, custom fields.

Optionally, Smartreader can convert SGTIN-96 encoded data into GTIN formats automatically. Please choose the desired formatting, along with the delimiters that will be used to separate each field.

#### Format
Smartreader will format the data with delimiters and line terminators (in place of Plain Text) and will also assign a name to the reader.

#### Filters
Smartreader can also apply software and hardware filters to reduce network traffic and prevent unwanted tag reads.

### Data Output Options
 Smartreader can send the automatically collected information to one or more destinations through different protocols and methods configured in this section.

#### Local HTTP streams
To connect to the reader, form an HTTP request and consume the resulting stream for as long as is practical.  
The reader will hold the connection open indefinitely, barring reader error, excessive client-side lag,  
network hiccups, reader maintenance or duplicate logins. In the event there is no new data to stream for  an extended period of time, a keep-alive CR-LF character pair will be sent. 

The method to form an HTTP request and parse the response will be different for every language or  framework, so consult the documentation for the HTTP library you are using.

#### Local socket server
When selecting this option, the Smartreader will send the tag information to a local socket server available inside the reader, in order to access the tag reading data just access the reader's IP address through the TELNET protocol on the port informed in the configuration (ex: 14150).

#### Local UDP server
When selecting this option, the Smartreader will send the tag information to a local UDP server available inside the reader, in order to access the tag reading data just access the reader's IP address through the UDP protocol on the port informed in the configuration (ex: 11000).

#### MQTT 
If you want to send the read data directly to a MQTT broker, you can configure MQTT information for your service here.

#### HTTP POST 
If you want to send the read data directly to a web server, you can configure HTTP post information for your service here. It is possible to inform the URL of the server, the interval in seconds to perform the POST and choose an authentication type.

#### Serial Port
Smartreader will display the collected information on the USB port, using a virtual serial port. This feature also allows the Smartreader to send data over a special cable behaving like a keyboard if you select this option.
You should choose a baudrate for this operation.

#### USB flash drive
The Smartreader will record the collected information on a USB stick connected to the reader's USB port, if you select this option.

## Using the Smartreader

Once you configure the desired settings, click on the **Apply Settings** button, an alert must be displayed otherwise it will mean that the settings have not been applied.

Go to the ***Actions*** tab, click on the **Reload Application** button.

The new settings will be used by the application once it's reloaded.
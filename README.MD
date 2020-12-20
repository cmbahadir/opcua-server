# Simple but efficient OPC UA Server

This is a more user friendly form of opc ua server based on the project https://github.com/cmbahadir/opcua-esp32. It consist of a configurator tool called ServerConfigurator and firmware running on ESP32.

### Prerequisites

- Hardware : Development is based on [ESP32-EVB](https://www.olimex.com/Products/IoT/ESP32/ESP32-EVB/open-source-hardware) but any ESP32 board consisting ethernet is expected to work. ESP32-EVB has also nice looking enclosure. 

<p align="center">
  <img src="doc/esp32_evb.png?raw=true" alt="ESP32-EVB" style="border-radius: 8px;"/>
</p>

- ESP-IDF : It is required to have esp-idf cloned with submodules.
- Python : For server configurator with the packages in /ServerConfigurator/req.txt.

## Getting Started
A more detailed information can be found here: https://selftronics.com/2020/06/23/cheapest-embedded-opc-ua-server/

ESP32:

    git clone --recursive https://github.com/espressif/esp-idf.git <your-esp-idf-root-path>
    export IDF_PATH=<your-esp-idf-root-path>
    export PATH=$PATH:<xtensa-toolchain-path>
    cd <your-esp-idf-root-path>/examples/
    git clone https://github.com/cmbahadir/opcua-server
    cd opcua-esp32
    idf.py build
   
ServerConfigrator (You can also do it inside a virtualenv):
    
    cd ServerConfigurator
    pip install -r req.txt
    python ServerConfigurator.py
   
After you flash the build to ESP32, it will be available as Wi-Fi AP with name "PROV_*". "*" part depends on the MAC address of your board. It won't require any configuration to connect.

After you are successfully connected with the AP you should run the "ServerConfigurator", set the Security to "AES-CTR" and enter the password as "abcd1234" (this can be changed statically).

<p align="center">
  <img src="doc/server_configurator.png?raw=true" alt="Server Configurator"/>
</p>

You can set the connection type as "Wi-Fi" or "Ethernet", currently static ip address is only supported for ethernet connection. After you are done with the changes click to download, after a successful download, download button will turn into green.

<p align="center">
  <img src="server_configurator_connected.png?raw=true" alt="Server Configurator Download"/>
</p>

## License

This project is licensed under the Mozilla Public License Version 2.0 which is inherited from Open62541 project - see the [LICENSE.md](LICENSE.md) file for details.

## Caution

It is the users responsibility to use this project in production, it is not suggested to use for critical applications. Only suggested for PoC's and diy projects.

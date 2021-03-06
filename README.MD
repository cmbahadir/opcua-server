# A small OPC UA Server

This is a more user friendly form of opc ua server based on the project https://github.com/cmbahadir/opcua-esp32. It consist of a configurator tool called ServerConfigurator and firmware running on ESP32.

### Prerequisites

- Hardware : Development is based on [ESP32-EVB](https://www.olimex.com/Products/IoT/ESP32/ESP32-EVB/open-source-hardware) but any ESP32 board consisting ethernet is expected to work. ESP32-EVB has also nice looking enclosure. 

<p align="center">
  <img src="doc/esp32_evb.png?raw=true" alt="ESP32-EVB" style="border-radius: 8px;"/>
</p>

- If you want to build and flash to the board then it is required to have esp-idf cloned in your local with submodules.
- Python is required for "serverConfigurator" with the [packages](/ServerConfigurator/requirements.txt) installed.

## Usage
Blog post about general usage: https://selftronics.com/2020/12/20/small-simple-but-efficient-open-source-opc-ua-server/

### Flashing firmware to ESP32:
Released packages contain firmware binaries to be flashed. You can directly download and flash to your development board, unfortunately flasher tool of Espressif systems only supports Windows. You can download the flasher tool from Espressif's tools page here;

https://www.espressif.com/sites/default/files/tools/flash_download_tool_v3.8.5.zip

### Provisioning with ServerConfigrator:

ServerConfigurator tool can be downloaded as zip file from [releases](https://github.com/cmbahadir/opcua-server/releases/tag/v0.1). There are two executables depending on your operating system, download the corresponding zip according to your OS.


After you are successfully connected with the AP you should run the "ServerConfigurator", set the Security to "AES-CTR" and enter the password as "abcd1234" (this can be changed statically).

<p align="center">
  <img src="doc/server_configurator.png?raw=true" alt="Server Configurator" style="border-radius: 8px;"/>
</p>

You can set the connection type as "Wi-Fi" or "Ethernet", settings a static ip address is only supported for ethernet connection for now, click download to set the configuration in the server. After a successful download, download button will turn into green and its text will change as "success".

<p align="center">
  <img src="doc/server_configurator_connected.png?raw=true" alt="Server Configurator Download" style="border-radius: 8px;"/>
</p>

## Building from source

### Building firmware from Source:
If you would like to build the firmware from source you have to follow the steps here, ignore here if you have successfully flashed the released binaries.

    git clone --recursive https://github.com/espressif/esp-idf.git <your-esp-idf-root-path>
    export IDF_PATH=<your-esp-idf-root-path>
    export PATH=$PATH:<xtensa-toolchain-path>
    cd <your-esp-idf-root-path>/examples/
    git clone https://github.com/cmbahadir/opcua-server
    cd opcua-esp32
    idf.py build
  
After you flash the build to ESP32, it will be available as Wi-Fi AP with name "PROV_xxx". "xxx" depends on the MAC address of your board. It won't require any configuration to connect.


#### Building Serverconfigurator from source:
If you want to build the Serverconfigurator from source then you got to follow these steps.

    cd ServerConfigurator
    pip install -r requirements.txt
    python ServerConfigurator.py

## License

This project is licensed under the Mozilla Public License Version 2.0 which is inherited from Open62541 project - see the [LICENSE.md](LICENSE.md) file for details.

## Caution

It is the users responsibility to use this project in production, it is not suggested to use for critical applications. Only suggested for PoC's and diy projects.
